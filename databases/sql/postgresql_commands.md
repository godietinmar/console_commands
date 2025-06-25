# Comandos SQL (PostgreSQL)

Este archivo contiene una lista de comandos SQL comunes para PostgreSQL, organizados por categoría.

## Conexión y Administración Básica

### psql (Cliente de línea de comandos)

**Descripción:**  
Cliente interactivo de PostgreSQL para ejecutar consultas y comandos administrativos.

**Sintaxis:**
```bash
psql [opciones] [base_datos] [usuario]
```

**Opciones comunes:**
- `-h`, `--host`: Host del servidor PostgreSQL
- `-p`, `--port`: Puerto del servidor (por defecto 5432)
- `-U`, `--username`: Nombre de usuario
- `-d`, `--dbname`: Base de datos a conectar
- `-W`, `--password`: Forzar solicitud de contraseña
- `-c`, `--command`: Ejecutar un comando y salir
- `-f`, `--file`: Ejecutar comandos desde archivo
- `-l`, `--list`: Listar bases de datos disponibles

**Ejemplos:**
```bash
# Conectar al servidor local como usuario postgres
psql -U postgres

# Conectar a servidor remoto con base de datos específica
psql -h 192.168.1.10 -U usuario -d mi_base_datos

# Conectar con puerto personalizado
psql -h localhost -p 5433 -U usuario -d mi_base_datos

# Ejecutar comando específico
psql -U postgres -c "SELECT version();"

# Ejecutar script SQL
psql -U postgres -d mi_base_datos -f script.sql

# Listar todas las bases de datos
psql -U postgres -l
```

## Comandos Meta de psql

### Comandos de Información

**\l** - Listar bases de datos
```sql
\l
\l+  -- Con información adicional
```

**\dt** - Listar tablas
```sql
\dt           -- Tablas en esquema actual
\dt *.*       -- Todas las tablas
\dt+ tabla    -- Información detallada de tabla
```

**\d** - Describir objetos
```sql
\d tabla             -- Estructura de tabla
\d+ tabla            -- Información detallada
\di                  -- Listar índices
\dv                  -- Listar vistas
\df                  -- Listar funciones
\dn                  -- Listar esquemas
\du                  -- Listar usuarios/roles
```

**\ds** - Listar secuencias
```sql
\ds
```

**\dp** - Listar permisos
```sql
\dp tabla
\z tabla    -- Equivalente a \dp
```

### Comandos de Conexión

**\c** - Cambiar conexión
```sql
\c base_datos           -- Cambiar base de datos
\c base_datos usuario   -- Cambiar BD y usuario
\c - usuario            -- Cambiar solo usuario
```

**\conninfo** - Información de conexión actual
```sql
\conninfo
```

### Comandos de Salida y Formato

**\o** - Redirigir salida
```sql
\o archivo.txt    -- Redirigir a archivo
\o               -- Volver a salida estándar
```

**\a** - Alternar formato alineado
```sql
\a
```

**\t** - Alternar encabezados de columna
```sql
\t
```

**\x** - Alternar salida expandida
```sql
\x
```

**\timing** - Mostrar tiempo de ejecución
```sql
\timing on
\timing off
```

### Comandos de Archivos

**\i** - Ejecutar archivo SQL
```sql
\i archivo.sql
```

**\e** - Editar consulta en editor
```sql
\e
```

**\g** - Ejecutar última consulta
```sql
\g
```

**\s** - Mostrar historial de comandos
```sql
\s
\s archivo.txt    -- Guardar historial en archivo
```

## Herramientas de Administración

### pg_dump

**Descripción:**  
Herramienta para crear copias de seguridad de bases de datos PostgreSQL.

**Sintaxis:**
```bash
pg_dump [opciones] [base_datos]
```

**Opciones comunes:**
- `-h`, `--host`: Host del servidor
- `-p`, `--port`: Puerto del servidor
- `-U`, `--username`: Usuario
- `-W`, `--password`: Solicitar contraseña
- `-f`, `--file`: Archivo de salida
- `-v`, `--verbose`: Modo verbose
- `-c`, `--clean`: Incluir comandos DROP
- `-C`, `--create`: Incluir comando CREATE DATABASE
- `-a`, `--data-only`: Solo datos
- `-s`, `--schema-only`: Solo esquema
- `-t`, `--table`: Tabla específica

**Ejemplos:**
```bash
# Backup completo de base de datos
pg_dump -U postgres -h localhost mi_base_datos > backup.sql

# Backup con formato custom
pg_dump -U postgres -Fc mi_base_datos -f backup.dump

# Backup solo de esquema
pg_dump -U postgres -s mi_base_datos > esquema.sql

# Backup de tabla específica
pg_dump -U postgres -t mi_tabla mi_base_datos > tabla.sql

# Backup con comandos de limpieza
pg_dump -U postgres -c -C mi_base_datos > backup_completo.sql
```

### pg_restore

**Descripción:**  
Restaurar base de datos desde backup creado con pg_dump.

**Sintaxis:**
```bash
pg_restore [opciones] [archivo]
```

**Ejemplos:**
```bash
# Restaurar desde archivo custom
pg_restore -U postgres -d nueva_base_datos backup.dump

# Restaurar con limpieza previa
pg_restore -U postgres -c -d mi_base_datos backup.dump

# Restaurar tabla específica
pg_restore -U postgres -t mi_tabla -d mi_base_datos backup.dump
```

### pg_dumpall

**Descripción:**  
Crear backup de todo el clúster PostgreSQL.

**Ejemplos:**
```bash
# Backup completo del clúster
pg_dumpall -U postgres > cluster_backup.sql

# Backup solo de roles y tablespaces
pg_dumpall -U postgres -r > roles.sql
```

### createdb / dropdb

**Descripción:**  
Crear y eliminar bases de datos desde línea de comandos.

**Ejemplos:**
```bash
# Crear base de datos
createdb -U postgres mi_nueva_base_datos

# Crear con template específico
createdb -U postgres -T template0 mi_base_datos

# Eliminar base de datos
dropdb -U postgres mi_base_datos
```

### createuser / dropuser

**Descripción:**  
Crear y eliminar usuarios/roles desde línea de comandos.

**Ejemplos:**
```bash
# Crear usuario
createuser -U postgres nuevo_usuario

# Crear usuario con privilegios
createuser -U postgres -s -P admin_usuario

# Eliminar usuario
dropuser -U postgres usuario_a_eliminar
```

## Comandos SQL Específicos de PostgreSQL

### Gestión de Esquemas

```sql
-- Crear esquema
CREATE SCHEMA mi_esquema;

-- Cambiar esquema por defecto
SET search_path TO mi_esquema, public;

-- Ver esquema actual
SELECT current_schema();

-- Ver path de búsqueda
SHOW search_path;
```

### Gestión de Roles y Permisos

```sql
-- Crear rol
CREATE ROLE nuevo_rol LOGIN PASSWORD 'contraseña';

-- Crear usuario (equivalente a rol con LOGIN)
CREATE USER nuevo_usuario PASSWORD 'contraseña';

-- Otorgar privilegios
GRANT SELECT, INSERT ON tabla TO usuario;
GRANT ALL PRIVILEGES ON DATABASE mi_base_datos TO usuario;

-- Revocar privilegios
REVOKE INSERT ON tabla FROM usuario;

-- Ver roles
SELECT rolname FROM pg_roles;
```

### Gestión de Tablespaces

```sql
-- Crear tablespace
CREATE TABLESPACE mi_tablespace LOCATION '/ruta/del/tablespace';

-- Crear tabla en tablespace específico
CREATE TABLE mi_tabla (id INT) TABLESPACE mi_tablespace;

-- Ver tablespaces
SELECT spcname FROM pg_tablespace;
```

### Información del Sistema

```sql
-- Versión de PostgreSQL
SELECT version();

-- Información de conexiones activas
SELECT * FROM pg_stat_activity;

-- Tamaño de bases de datos
SELECT datname, pg_size_pretty(pg_database_size(datname)) 
FROM pg_database;

-- Tamaño de tablas
SELECT schemaname, tablename, 
       pg_size_pretty(pg_total_relation_size(schemaname||'.'||tablename))
FROM pg_tables;

-- Estadísticas de tabla
SELECT * FROM pg_stat_user_tables WHERE relname = 'mi_tabla';
```

### Mantenimiento

```sql
-- Vacuum básico
VACUUM mi_tabla;

-- Vacuum completo
VACUUM FULL mi_tabla;

-- Vacuum con análisis
VACUUM ANALYZE mi_tabla;

-- Reindex
REINDEX TABLE mi_tabla;
REINDEX DATABASE mi_base_datos;

-- Estadísticas
ANALYZE mi_tabla;
```

## Variables de Entorno

- `PGHOST`: Host del servidor PostgreSQL
- `PGPORT`: Puerto del servidor
- `PGUSER`: Usuario por defecto
- `PGPASSWORD`: Contraseña (no recomendado)
- `PGDATABASE`: Base de datos por defecto
- `PSQL_EDITOR`: Editor para comando \e

## Archivos de Configuración

- `.pgpass`: Archivo de contraseñas (`~/.pgpass`)
- `pg_service.conf`: Configuración de servicios
- `postgresql.conf`: Configuración principal del servidor
- `pg_hba.conf`: Configuración de autenticación

## Ejemplos de Uso Común

### Backup y Restauración Completa

```bash
# Backup
pg_dump -U postgres -h localhost -Fc mi_base_datos > backup_$(date +%Y%m%d).dump

# Restauración
createdb -U postgres nueva_base_datos
pg_restore -U postgres -d nueva_base_datos backup_20241221.dump
```

### Migración entre Servidores

```bash
# Método 1: Via archivo
pg_dump -U postgres -h servidor1 base_datos | psql -U postgres -h servidor2 base_datos

# Método 2: Con formato custom
pg_dump -U postgres -h servidor1 -Fc base_datos -f backup.dump
pg_restore -U postgres -h servidor2 -d base_datos backup.dump
```

### Monitoreo Básico

```sql
-- Conexiones activas
SELECT count(*) FROM pg_stat_activity;

-- Consultas lentas
SELECT query, query_start, state 
FROM pg_stat_activity 
WHERE state = 'active' AND query_start < now() - interval '5 minutes';

-- Locks
SELECT * FROM pg_locks WHERE NOT granted;
```
