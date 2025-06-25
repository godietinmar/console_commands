# Comandos Cassandra (CQL)

Este archivo contiene una lista de comandos para Apache Cassandra usando CQL (Cassandra Query Language) y herramientas de línea de comandos, organizados por categoría.

## Herramientas de Línea de Comandos

### cqlsh (CQL Shell)

**Descripción:**  
Shell interactivo para ejecutar comandos CQL en Cassandra.

**Sintaxis:**
```bash
cqlsh [opciones] [host [port]]
```

**Opciones comunes:**
- `-u`: Usuario
- `-p`: Contraseña
- `-k`: Keyspace inicial
- `-f`: Ejecutar archivo CQL
- `-e`: Ejecutar comando y salir
- `--ssl`: Usar conexión SSL
- `--cqlversion`: Versión de CQL
- `--protocol-version`: Versión del protocolo
- `--connect-timeout`: Timeout de conexión
- `--request-timeout`: Timeout de request
- `--no-color`: Deshabilitar colores
- `--debug`: Modo debug

**Ejemplos:**
```bash
# Conectar a servidor local
cqlsh

# Conectar a servidor remoto
cqlsh servidor.example.com 9042

# Conectar con autenticación
cqlsh -u cassandra -p cassandra

# Conectar con keyspace específico
cqlsh -k mi_keyspace

# Ejecutar archivo CQL
cqlsh -f script.cql

# Ejecutar comando específico
cqlsh -e "SELECT * FROM system.local;"

# Conectar con SSL
cqlsh --ssl servidor.example.com

# Conectar con timeout personalizado
cqlsh --connect-timeout=10 --request-timeout=30 servidor.example.com
```

### nodetool

**Descripción:**  
Herramienta de administración para Cassandra.

**Ejemplos:**
```bash
# Estado del cluster
nodetool status

# Información del nodo
nodetool info

# Estadísticas del cluster
nodetool ring

# Compactación
nodetool compact
nodetool compact mi_keyspace mi_tabla

# Limpieza (tombstones)
nodetool cleanup

# Reparación
nodetool repair
nodetool repair mi_keyspace

# Flush de memtables
nodetool flush
nodetool flush mi_keyspace mi_tabla

# Snapshots
nodetool snapshot
nodetool snapshot mi_keyspace

# Estadísticas de CF
nodetool cfstats
nodetool cfstats mi_keyspace.mi_tabla
```

### cassandra-stress

**Descripción:**  
Herramienta de pruebas de rendimiento.

**Ejemplos:**
```bash
# Test de escritura básico
cassandra-stress write n=100000

# Test de lectura
cassandra-stress read n=50000

# Test mixto
cassandra-stress mixed ratio\(write=1,read=3\) n=100000

# Con configuración específica
cassandra-stress write n=100000 -node servidor1,servidor2
```

## Comandos CQL Básicos

### Información del Sistema

```cql
-- Información del cluster
SELECT * FROM system.local;

-- Información de peers
SELECT * FROM system.peers;

-- Keyspaces disponibles
SELECT * FROM system_schema.keyspaces;

-- Tablas en keyspace
SELECT * FROM system_schema.tables WHERE keyspace_name = 'mi_keyspace';

-- Columnas de tabla
SELECT * FROM system_schema.columns 
WHERE keyspace_name = 'mi_keyspace' AND table_name = 'mi_tabla';

-- Índices
SELECT * FROM system_schema.indexes 
WHERE keyspace_name = 'mi_keyspace';

-- Versión de Cassandra
SELECT cluster_name, cql_version, native_protocol_version, release_version 
FROM system.local;
```

### Gestión de Keyspaces

```cql
-- Crear keyspace
CREATE KEYSPACE mi_keyspace 
WITH REPLICATION = {
  'class': 'SimpleStrategy',
  'replication_factor': 3
};

-- Crear keyspace con NetworkTopologyStrategy
CREATE KEYSPACE mi_keyspace_prod 
WITH REPLICATION = {
  'class': 'NetworkTopologyStrategy',
  'datacenter1': 3,
  'datacenter2': 2
};

-- Usar keyspace
USE mi_keyspace;

-- Alterar keyspace
ALTER KEYSPACE mi_keyspace 
WITH REPLICATION = {
  'class': 'SimpleStrategy',
  'replication_factor': 5
};

-- Eliminar keyspace
DROP KEYSPACE mi_keyspace;

-- Describir keyspace
DESCRIBE KEYSPACE mi_keyspace;
```

### Gestión de Tablas

```cql
-- Crear tabla básica
CREATE TABLE usuarios (
  id UUID PRIMARY KEY,
  nombre TEXT,
  email TEXT,
  fecha_creacion TIMESTAMP,
  activo BOOLEAN
);

-- Crear tabla con clave compuesta
CREATE TABLE posts (
  usuario_id UUID,
  fecha_creacion TIMESTAMP,
  id UUID,
  titulo TEXT,
  contenido TEXT,
  tags SET<TEXT>,
  PRIMARY KEY (usuario_id, fecha_creacion, id)
) WITH CLUSTERING ORDER BY (fecha_creacion DESC, id ASC);

-- Crear tabla con TTL por defecto
CREATE TABLE sesiones (
  session_id TEXT PRIMARY KEY,
  usuario_id UUID,
  datos TEXT,
  fecha_creacion TIMESTAMP
) WITH default_time_to_live = 3600;

-- Crear tabla con opciones de compactación
CREATE TABLE logs (
  fecha DATE,
  hora TIMESTAMP,
  nivel TEXT,
  mensaje TEXT,
  PRIMARY KEY (fecha, hora)
) WITH compaction = {
  'class': 'TimeWindowCompactionStrategy',
  'compaction_window_size': 1,
  'compaction_window_unit': 'DAYS'
};

-- Alterar tabla
ALTER TABLE usuarios ADD telefono TEXT;
ALTER TABLE usuarios DROP telefono;
ALTER TABLE usuarios WITH gc_grace_seconds = 864000;

-- Eliminar tabla
DROP TABLE usuarios;

-- Describir tabla
DESCRIBE TABLE usuarios;
```

### Tipos de Datos

```cql
-- Tipos básicos
CREATE TABLE ejemplo_tipos (
  id UUID PRIMARY KEY,
  
  -- Tipos numéricos
  entero INT,
  entero_largo BIGINT,
  decimal_val DECIMAL,
  flotante FLOAT,
  doble DOUBLE,
  contador COUNTER,
  
  -- Tipos de texto
  texto TEXT,
  cadena VARCHAR,
  ascii_val ASCII,
  
  -- Tipos de fecha y hora
  timestamp_val TIMESTAMP,
  fecha DATE,
  hora TIME,
  
  -- Tipos booleanos
  activo BOOLEAN,
  
  -- Tipos de red
  direccion_ip INET,
  
  -- Tipos de colección
  lista_numeros LIST<INT>,
  conjunto_tags SET<TEXT>,
  mapa_propiedades MAP<TEXT, TEXT>,
  
  -- Tipos especiales
  id_tiempo TIMEUUID,
  datos_binarios BLOB
);
```

## Operaciones CRUD

### Insertar Datos

```cql
-- Insertar registro básico
INSERT INTO usuarios (id, nombre, email, fecha_creacion, activo)
VALUES (uuid(), 'Juan Pérez', 'juan@example.com', toTimestamp(now()), true);

-- Insertar con TTL
INSERT INTO sesiones (session_id, usuario_id, datos)
VALUES ('sess_123', uuid(), '{"last_login": "2024-01-01"}')
USING TTL 3600;

-- Insertar con timestamp específico
INSERT INTO posts (usuario_id, fecha_creacion, id, titulo, contenido)
VALUES (uuid(), '2024-01-01 10:00:00', uuid(), 'Mi Post', 'Contenido del post')
USING TIMESTAMP 1609459200000000;

-- Insertar en colecciones
INSERT INTO productos (id, nombre, tags, propiedades)
VALUES (uuid(), 'Laptop', {'electrónica', 'computadora'}, 
        {'marca': 'Dell', 'modelo': 'XPS13'});

-- Insertar con IF NOT EXISTS
INSERT INTO usuarios (id, nombre, email)
VALUES (uuid(), 'Ana García', 'ana@example.com')
IF NOT EXISTS;
```

### Actualizar Datos

```cql
-- Actualizar campos
UPDATE usuarios 
SET nombre = 'Juan Carlos Pérez', activo = false
WHERE id = a1b2c3d4-e5f6-7890-abcd-ef1234567890;

-- Actualizar con TTL
UPDATE sesiones 
SET datos = '{"updated": true}'
WHERE session_id = 'sess_123'
USING TTL 1800;

-- Actualizar colecciones
UPDATE productos 
SET tags = tags + {'nuevo', 'oferta'}
WHERE id = a1b2c3d4-e5f6-7890-abcd-ef1234567890;

UPDATE productos 
SET propiedades['color'] = 'negro'
WHERE id = a1b2c3d4-e5f6-7890-abcd-ef1234567890;

-- Actualizar con condición
UPDATE usuarios 
SET nombre = 'Nuevo Nombre'
WHERE id = a1b2c3d4-e5f6-7890-abcd-ef1234567890
IF activo = true;

-- Incrementar contador
UPDATE estadisticas 
SET visitas = visitas + 1
WHERE pagina = 'home';
```

### Consultar Datos

```cql
-- Seleccionar todos los campos
SELECT * FROM usuarios;

-- Seleccionar campos específicos
SELECT id, nombre, email FROM usuarios;

-- Filtrar por clave de partición
SELECT * FROM posts WHERE usuario_id = a1b2c3d4-e5f6-7890-abcd-ef1234567890;

-- Filtrar por clave de partición y clustering
SELECT * FROM posts 
WHERE usuario_id = a1b2c3d4-e5f6-7890-abcd-ef1234567890 
  AND fecha_creacion >= '2024-01-01';

-- Ordenar resultados (solo por clustering columns)
SELECT * FROM posts 
WHERE usuario_id = a1b2c3d4-e5f6-7890-abcd-ef1234567890 
ORDER BY fecha_creacion DESC;

-- Limitar resultados
SELECT * FROM usuarios LIMIT 10;

-- Usar ALLOW FILTERING (cuidado con rendimiento)
SELECT * FROM usuarios WHERE activo = true ALLOW FILTERING;

-- Consultar con IN
SELECT * FROM usuarios WHERE id IN (uuid1, uuid2, uuid3);

-- Consultar colecciones
SELECT * FROM productos WHERE tags CONTAINS 'electrónica';
SELECT * FROM productos WHERE propiedades CONTAINS KEY 'marca';

-- Consultar con token
SELECT * FROM usuarios WHERE token(id) > token(a1b2c3d4-e5f6-7890-abcd-ef1234567890);
```

### Eliminar Datos

```cql
-- Eliminar registro completo
DELETE FROM usuarios WHERE id = a1b2c3d4-e5f6-7890-abcd-ef1234567890;

-- Eliminar campos específicos
DELETE email, telefono FROM usuarios 
WHERE id = a1b2c3d4-e5f6-7890-abcd-ef1234567890;

-- Eliminar con condición
DELETE FROM usuarios 
WHERE id = a1b2c3d4-e5f6-7890-abcd-ef1234567890
IF activo = false;

-- Eliminar elementos de colección
DELETE tags['electrónica'] FROM productos 
WHERE id = a1b2c3d4-e5f6-7890-abcd-ef1234567890;

-- Eliminar con timestamp
DELETE FROM posts 
WHERE usuario_id = a1b2c3d4-e5f6-7890-abcd-ef1234567890 
  AND fecha_creacion = '2024-01-01 10:00:00'
USING TIMESTAMP 1609459300000000;
```

## Índices

### Índices Secundarios

```cql
-- Crear índice secundario
CREATE INDEX idx_usuario_email ON usuarios (email);
CREATE INDEX idx_usuario_activo ON usuarios (activo);

-- Índice en colección
CREATE INDEX idx_producto_tags ON productos (tags);
CREATE INDEX idx_producto_propiedades_keys ON productos (KEYS(propiedades));
CREATE INDEX idx_producto_propiedades_values ON productos (VALUES(propiedades));

-- Índice en campo anidado (para UDT)
CREATE INDEX idx_direccion_ciudad ON usuarios (direccion.ciudad);

-- Listar índices
SELECT * FROM system_schema.indexes WHERE keyspace_name = 'mi_keyspace';

-- Eliminar índice
DROP INDEX idx_usuario_email;
```

### Índices Materializados (Materialized Views)

```cql
-- Crear vista materializada
CREATE MATERIALIZED VIEW usuarios_por_email AS
SELECT id, nombre, email, fecha_creacion
FROM usuarios
WHERE email IS NOT NULL
PRIMARY KEY (email, id);

-- Vista materializada más compleja
CREATE MATERIALIZED VIEW posts_por_fecha AS
SELECT usuario_id, fecha_creacion, id, titulo
FROM posts
WHERE usuario_id IS NOT NULL 
  AND fecha_creacion IS NOT NULL
  AND id IS NOT NULL
PRIMARY KEY (fecha_creacion, usuario_id, id)
WITH CLUSTERING ORDER BY (usuario_id ASC, id ASC);

-- Consultar vista materializada
SELECT * FROM usuarios_por_email WHERE email = 'juan@example.com';

-- Eliminar vista materializada
DROP MATERIALIZED VIEW usuarios_por_email;
```

## Tipos de Datos Definidos por Usuario (UDT)

```cql
-- Crear tipo de dato personalizado
CREATE TYPE direccion (
  calle TEXT,
  ciudad TEXT,
  codigo_postal TEXT,
  pais TEXT
);

-- Usar UDT en tabla
CREATE TABLE usuarios_completos (
  id UUID PRIMARY KEY,
  nombre TEXT,
  email TEXT,
  direccion FROZEN<direccion>,
  direcciones LIST<FROZEN<direccion>>
);

-- Insertar con UDT
INSERT INTO usuarios_completos (id, nombre, email, direccion)
VALUES (uuid(), 'Juan Pérez', 'juan@example.com', 
        {calle: 'Calle Mayor 123', ciudad: 'Madrid', codigo_postal: '28001', pais: 'España'});

-- Actualizar campo de UDT
UPDATE usuarios_completos 
SET direccion.ciudad = 'Barcelona'
WHERE id = a1b2c3d4-e5f6-7890-abcd-ef1234567890;

-- Eliminar UDT
DROP TYPE direccion;
```

## Funciones y Agregados

### Funciones Incorporadas

```cql
-- Funciones de fecha y hora
SELECT id, nombre, toTimestamp(now()) as timestamp_actual,
       dateOf(id) as fecha_from_timeuuid
FROM usuarios;

-- Funciones de UUID
SELECT uuid(), now(), minTimeuuid('2024-01-01'), maxTimeuuid('2024-12-31');

-- Funciones de token
SELECT token(id), id FROM usuarios;

-- Funciones de conversión
SELECT id, nombre, ttl(email) as email_ttl, writetime(nombre) as nombre_writetime
FROM usuarios;

-- Funciones de colección
SELECT id, nombre, 
       tags + {'nuevo_tag'} as tags_con_nuevo,
       propiedades['marca'] as marca
FROM productos;
```

### Funciones Agregadas

```cql
-- Contar registros
SELECT COUNT(*) FROM usuarios;

-- Contar con filtro
SELECT COUNT(*) FROM usuarios WHERE activo = true ALLOW FILTERING;

-- Agregados en grupos (limitado en Cassandra)
SELECT usuario_id, COUNT(*) as total_posts
FROM posts
GROUP BY usuario_id;

-- Agregados con funciones
SELECT MAX(fecha_creacion), MIN(fecha_creacion), COUNT(*)
FROM posts
WHERE usuario_id = a1b2c3d4-e5f6-7890-abcd-ef1234567890;
```

## Batch Operations

```cql
-- Batch básico
BEGIN BATCH
  INSERT INTO usuarios (id, nombre, email) VALUES (uuid(), 'Usuario 1', 'user1@example.com');
  INSERT INTO usuarios (id, nombre, email) VALUES (uuid(), 'Usuario 2', 'user2@example.com');
  UPDATE usuarios SET activo = true WHERE id = a1b2c3d4-e5f6-7890-abcd-ef1234567890;
APPLY BATCH;

-- Batch con timestamp
BEGIN BATCH USING TIMESTAMP 1609459200000000
  INSERT INTO posts (usuario_id, fecha_creacion, id, titulo) 
  VALUES (uuid(), '2024-01-01 10:00:00', uuid(), 'Post 1');
  INSERT INTO posts (usuario_id, fecha_creacion, id, titulo) 
  VALUES (uuid(), '2024-01-01 10:01:00', uuid(), 'Post 2');
APPLY BATCH;

-- Batch unlogged (mejor rendimiento, menos consistencia)
BEGIN UNLOGGED BATCH
  INSERT INTO logs (fecha, hora, nivel, mensaje) 
  VALUES ('2024-01-01', now(), 'INFO', 'Log 1');
  INSERT INTO logs (fecha, hora, nivel, mensaje) 
  VALUES ('2024-01-01', now(), 'INFO', 'Log 2');
APPLY BATCH;
```

## Administración y Monitoreo

### Comandos de Mantenimiento

```cql
-- Información de tabla
SELECT * FROM system_schema.tables WHERE keyspace_name = 'mi_keyspace';

-- Estadísticas de tabla (usar nodetool)
-- nodetool tablestats mi_keyspace.mi_tabla

-- Compactación manual
-- nodetool compact mi_keyspace mi_tabla

-- Limpieza de tombstones
-- nodetool cleanup mi_keyspace

-- Información de nodos
SELECT * FROM system.peers;
SELECT * FROM system.local;
```

### Trazas y Debugging

```cql
-- Habilitar trazas
TRACING ON;

-- Ejecutar consulta con trazas
SELECT * FROM usuarios WHERE id = a1b2c3d4-e5f6-7890-abcd-ef1234567890;

-- Ver trazas
-- Las trazas se muestran automáticamente

-- Deshabilitar trazas
TRACING OFF;

-- Expandir resultados
EXPAND ON;
SELECT * FROM usuarios LIMIT 1;
EXPAND OFF;
```

## Configuración de Consistencia

```cql
-- Configurar nivel de consistencia para la sesión
CONSISTENCY LOCAL_QUORUM;

-- Niveles de consistencia disponibles:
-- ANY, ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, SERIAL, LOCAL_SERIAL

-- Verificar consistencia actual
CONSISTENCY;

-- Ejemplo de operación con consistencia específica
CONSISTENCY QUORUM;
SELECT * FROM usuarios_criticos WHERE id = a1b2c3d4-e5f6-7890-abcd-ef1234567890;

CONSISTENCY ONE;
SELECT * FROM logs WHERE fecha = '2024-01-01';
```

## Scripts de Utilidad

### Script de Backup

```bash
#!/bin/bash
# backup_cassandra.sh

KEYSPACE="mi_keyspace"
BACKUP_DIR="/backups/cassandra"
DATE=$(date +%Y%m%d_%H%M%S)

mkdir -p $BACKUP_DIR

# Crear snapshot
nodetool snapshot $KEYSPACE -t backup_$DATE

# Copiar snapshots
for node_dir in /var/lib/cassandra/data/$KEYSPACE/*/snapshots/backup_$DATE; do
    if [ -d "$node_dir" ]; then
        table_name=$(basename $(dirname $(dirname $node_dir)))
        cp -r $node_dir $BACKUP_DIR/${table_name}_$DATE
    fi
done

# Comprimir backup
tar -czf $BACKUP_DIR/cassandra_${KEYSPACE}_${DATE}.tar.gz $BACKUP_DIR/*_$DATE

# Limpiar directorios temporales
rm -rf $BACKUP_DIR/*_$DATE

# Limpiar snapshot
nodetool clearsnapshot $KEYSPACE -t backup_$DATE

echo "Backup completado: cassandra_${KEYSPACE}_${DATE}.tar.gz"
```

### Script de Monitoreo

```cql
-- monitoreo.cql
-- Script para monitorear estado de Cassandra

-- Información del cluster
SELECT cluster_name, cql_version, release_version FROM system.local;

-- Información de nodos
SELECT peer, host_id, rack, release_version FROM system.peers;

-- Keyspaces
SELECT keyspace_name, replication FROM system_schema.keyspaces;

-- Tablas por keyspace
SELECT keyspace_name, table_name FROM system_schema.tables 
WHERE keyspace_name = 'mi_keyspace';

-- Índices
SELECT keyspace_name, table_name, index_name FROM system_schema.indexes 
WHERE keyspace_name = 'mi_keyspace';
```

### Script de Limpieza

```bash
#!/bin/bash
# cleanup_cassandra.sh

KEYSPACE="mi_keyspace"

echo "Iniciando limpieza de Cassandra..."

# Compactación mayor
nodetool compact $KEYSPACE

# Limpieza de datos no necesarios
nodetool cleanup $KEYSPACE

# Limpiar snapshots antiguos
nodetool clearsnapshot

# Reparación incremental
nodetool repair $KEYSPACE

echo "Limpieza completada."
```

## Ejemplos de Uso Común

### Sistema de Logging

```cql
-- Tabla para logs
CREATE TABLE logs (
  fecha DATE,
  hora TIMESTAMP,
  nivel TEXT,
  aplicacion TEXT,
  mensaje TEXT,
  metadata MAP<TEXT, TEXT>,
  PRIMARY KEY (fecha, hora, nivel, aplicacion)
) WITH CLUSTERING ORDER BY (hora DESC, nivel ASC, aplicacion ASC)
  AND compaction = {'class': 'TimeWindowCompactionStrategy'}
  AND default_time_to_live = 2592000;  -- 30 días

-- Insertar logs
INSERT INTO logs (fecha, hora, nivel, aplicacion, mensaje, metadata)
VALUES ('2024-01-01', now(), 'ERROR', 'api-gateway', 'Connection timeout',
        {'user_id': '1001', 'endpoint': '/api/users'});

-- Consultar logs del día
SELECT * FROM logs WHERE fecha = '2024-01-01';

-- Consultar logs por nivel
SELECT * FROM logs WHERE fecha = '2024-01-01' AND nivel = 'ERROR';
```

### Sistema de Métricas

```cql
-- Tabla para métricas por minuto
CREATE TABLE metricas_minuto (
  metrica TEXT,
  fecha DATE,
  hora TIMESTAMP,
  valor DOUBLE,
  tags MAP<TEXT, TEXT>,
  PRIMARY KEY ((metrica, fecha), hora)
) WITH CLUSTERING ORDER BY (hora DESC);

-- Insertar métrica
INSERT INTO metricas_minuto (metrica, fecha, hora, valor, tags)
VALUES ('cpu_usage', '2024-01-01', now(), 85.5, {'host': 'server1', 'datacenter': 'us-east'});

-- Consultar métricas del día
SELECT * FROM metricas_minuto 
WHERE metrica = 'cpu_usage' AND fecha = '2024-01-01';

-- Tabla para contadores
CREATE TABLE contadores (
  nombre TEXT,
  fecha DATE,
  valor COUNTER,
  PRIMARY KEY (nombre, fecha)
);

-- Incrementar contador
UPDATE contadores SET valor = valor + 1 
WHERE nombre = 'page_views' AND fecha = '2024-01-01';
```

### Sistema de Eventos

```cql
-- Tabla para eventos por usuario
CREATE TABLE eventos_usuario (
  usuario_id UUID,
  timestamp TIMESTAMP,
  evento_id TIMEUUID,
  tipo TEXT,
  datos MAP<TEXT, TEXT>,
  PRIMARY KEY (usuario_id, timestamp, evento_id)
) WITH CLUSTERING ORDER BY (timestamp DESC, evento_id DESC);

-- Insertar evento
INSERT INTO eventos_usuario (usuario_id, timestamp, evento_id, tipo, datos)
VALUES (a1b2c3d4-e5f6-7890-abcd-ef1234567890, now(), now(), 'login',
        {'ip': '192.168.1.100', 'user_agent': 'Mozilla/5.0'});

-- Consultar eventos recientes del usuario
SELECT * FROM eventos_usuario 
WHERE usuario_id = a1b2c3d4-e5f6-7890-abcd-ef1234567890
LIMIT 10;

-- Vista materializada para eventos por tipo
CREATE MATERIALIZED VIEW eventos_por_tipo AS
SELECT tipo, timestamp, usuario_id, evento_id, datos
FROM eventos_usuario
WHERE tipo IS NOT NULL AND usuario_id IS NOT NULL 
  AND timestamp IS NOT NULL AND evento_id IS NOT NULL
PRIMARY KEY (tipo, timestamp, usuario_id, evento_id)
WITH CLUSTERING ORDER BY (timestamp DESC, usuario_id ASC, evento_id DESC);
```

### Sistema de Inventario

```cql
-- Tabla para productos
CREATE TABLE productos (
  categoria TEXT,
  producto_id UUID,
  nombre TEXT,
  precio DECIMAL,
  stock INT,
  especificaciones MAP<TEXT, TEXT>,
  tags SET<TEXT>,
  fecha_creacion TIMESTAMP,
  PRIMARY KEY (categoria, producto_id)
);

-- Tabla para movimientos de stock
CREATE TABLE movimientos_stock (
  producto_id UUID,
  fecha DATE,
  timestamp TIMESTAMP,
  tipo TEXT,  -- 'entrada', 'salida', 'ajuste'
  cantidad INT,
  motivo TEXT,
  usuario TEXT,
  PRIMARY KEY (producto_id, fecha, timestamp)
) WITH CLUSTERING ORDER BY (fecha DESC, timestamp DESC);

-- Insertar producto
INSERT INTO productos (categoria, producto_id, nombre, precio, stock, especificaciones, tags, fecha_creacion)
VALUES ('electronica', uuid(), 'Laptop Gaming', 1299.99, 10, 
        {'marca': 'Dell', 'modelo': 'G5', 'ram': '16GB'}, 
        {'gaming', 'laptop', 'dell'}, now());

-- Actualizar stock
UPDATE productos SET stock = stock - 1 
WHERE categoria = 'electronica' AND producto_id = a1b2c3d4-e5f6-7890-abcd-ef1234567890;

-- Registrar movimiento
INSERT INTO movimientos_stock (producto_id, fecha, timestamp, tipo, cantidad, motivo, usuario)
VALUES (a1b2c3d4-e5f6-7890-abcd-ef1234567890, '2024-01-01', now(), 'salida', 1, 'venta', 'vendedor1');

-- Consultar productos por categoría
SELECT * FROM productos WHERE categoria = 'electronica';

-- Consultar movimientos de producto
SELECT * FROM movimientos_stock 
WHERE producto_id = a1b2c3d4-e5f6-7890-abcd-ef1234567890 
  AND fecha >= '2024-01-01';
```
