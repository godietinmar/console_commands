# Comandos Neo4j (Cypher)

Este archivo contiene una lista de comandos para Neo4j usando Cypher Query Language y herramientas de línea de comandos, organizados por categoría.

## Herramientas de Línea de Comandos

### cypher-shell

**Descripción:**  
Cliente de línea de comandos para Neo4j que permite ejecutar consultas Cypher.

**Sintaxis:**
```bash
cypher-shell [opciones]
```

**Opciones comunes:**
- `-a`: Dirección del servidor (por defecto bolt://localhost:7687)
- `-u`: Usuario (por defecto neo4j)
- `-p`: Contraseña
- `-d`: Base de datos (Neo4j 4.0+)
- `--format`: Formato de salida (auto, verbose, plain)
- `--debug`: Modo debug
- `--non-interactive`: Modo no interactivo
- `--file`: Ejecutar archivo de consultas
- `--param`: Parámetros para consultas

**Ejemplos:**
```bash
# Conectar con valores por defecto
cypher-shell

# Conectar con autenticación
cypher-shell -u neo4j -p contraseña

# Conectar a servidor remoto
cypher-shell -a bolt://servidor:7687 -u neo4j -p contraseña

# Ejecutar archivo de consultas
cypher-shell -u neo4j -p contraseña --file consultas.cypher

# Modo no interactivo con consulta
echo "MATCH (n) RETURN count(n);" | cypher-shell -u neo4j -p contraseña --non-interactive

# Con parámetros
cypher-shell -u neo4j -p contraseña --param "name=>'Juan'"
```

### neo4j-admin

**Descripción:**  
Herramienta de administración para Neo4j.

**Ejemplos:**
```bash
# Importar datos desde CSV
neo4j-admin import \
  --database=neo4j \
  --nodes=import/nodes.csv \
  --relationships=import/relationships.csv

# Backup de base de datos
neo4j-admin backup --database=neo4j --to=/backups/

# Restore de base de datos
neo4j-admin restore --database=neo4j --from=/backups/neo4j

# Verificar consistencia
neo4j-admin check-consistency --database=neo4j

# Información de almacenamiento
neo4j-admin memrec --database=neo4j
```

### neo4j

**Descripción:**  
Comando para controlar el servidor Neo4j.

**Ejemplos:**
```bash
# Iniciar servidor
neo4j start

# Detener servidor
neo4j stop

# Reiniciar servidor
neo4j restart

# Estado del servidor
neo4j status

# Modo consola (primer plano)
neo4j console
```

## Cypher Query Language Básico

### Información del Sistema

```cypher
// Versión de Neo4j
CALL dbms.components();

// Información de la instancia
CALL dbms.queryJmx("org.neo4j:instance=kernel#0,name=Configuration");

// Estadísticas de la base de datos
CALL db.stats.retrieve();

// Procedimientos disponibles
CALL dbms.procedures();

// Funciones disponibles
CALL dbms.functions();

// Información de índices
CALL db.indexes();

// Información de constraints
CALL db.constraints();

// Bases de datos (Neo4j 4.0+)
SHOW DATABASES;

// Usuarios
SHOW USERS;

// Roles
SHOW ROLES;
```

### Nodos (Nodes)

#### Crear Nodos

```cypher
// Crear nodo simple
CREATE (n);

// Crear nodo con etiqueta
CREATE (p:Persona);

// Crear nodo con etiqueta y propiedades
CREATE (p:Persona {nombre: 'Juan Pérez', edad: 30, email: 'juan@example.com'});

// Crear múltiples nodos
CREATE 
  (p1:Persona {nombre: 'Ana García', edad: 25}),
  (p2:Persona {nombre: 'Luis Rodríguez', edad: 35}),
  (e:Empresa {nombre: 'TechCorp', fundada: 2010});

// Crear nodo con múltiples etiquetas
CREATE (p:Persona:Empleado {nombre: 'María López', edad: 28, cargo: 'Desarrolladora'});

// Crear y retornar nodo
CREATE (p:Persona {nombre: 'Carlos Martín', edad: 32})
RETURN p;
```

#### Consultar Nodos

```cypher
// Obtener todos los nodos
MATCH (n) RETURN n;

// Obtener nodos con etiqueta específica
MATCH (p:Persona) RETURN p;

// Obtener nodos con propiedades específicas
MATCH (p:Persona {nombre: 'Juan Pérez'}) RETURN p;

// Filtrar por propiedades
MATCH (p:Persona)
WHERE p.edad > 25
RETURN p.nombre, p.edad;

// Múltiples condiciones
MATCH (p:Persona)
WHERE p.edad >= 25 AND p.edad <= 35
RETURN p;

// Usar CONTAINS para texto
MATCH (p:Persona)
WHERE p.nombre CONTAINS 'Juan'
RETURN p;

// Usar expresiones regulares
MATCH (p:Persona)
WHERE p.email =~ '.*@gmail\\.com'
RETURN p;

// Ordenar resultados
MATCH (p:Persona)
RETURN p.nombre, p.edad
ORDER BY p.edad DESC;

// Limitar resultados
MATCH (p:Persona)
RETURN p.nombre
LIMIT 10;

// Saltar resultados (paginación)
MATCH (p:Persona)
RETURN p.nombre
ORDER BY p.nombre
SKIP 10 LIMIT 5;
```

#### Actualizar Nodos

```cypher
// Actualizar propiedades
MATCH (p:Persona {nombre: 'Juan Pérez'})
SET p.edad = 31, p.telefono = '123-456-7890'
RETURN p;

// Agregar etiqueta
MATCH (p:Persona {nombre: 'Juan Pérez'})
SET p:Empleado
RETURN p;

// Quitar etiqueta
MATCH (p:Persona:Empleado {nombre: 'Juan Pérez'})
REMOVE p:Empleado
RETURN p;

// Quitar propiedad
MATCH (p:Persona {nombre: 'Juan Pérez'})
REMOVE p.telefono
RETURN p;

// Actualizar usando expresiones
MATCH (p:Persona)
WHERE p.edad IS NOT NULL
SET p.categoria = CASE 
  WHEN p.edad < 30 THEN 'Joven'
  WHEN p.edad >= 30 AND p.edad < 60 THEN 'Adulto'
  ELSE 'Senior'
END;
```

#### Eliminar Nodos

```cypher
// Eliminar nodo sin relaciones
MATCH (p:Persona {nombre: 'Juan Pérez'})
DELETE p;

// Eliminar nodo y sus relaciones
MATCH (p:Persona {nombre: 'Juan Pérez'})
DETACH DELETE p;

// Eliminar todos los nodos de una etiqueta
MATCH (p:Persona)
DETACH DELETE p;

// Eliminar nodos con condición
MATCH (p:Persona)
WHERE p.edad < 18
DETACH DELETE p;
```

### Relaciones (Relationships)

#### Crear Relaciones

```cypher
// Crear relación entre nodos existentes
MATCH (p1:Persona {nombre: 'Juan Pérez'}), (p2:Persona {nombre: 'Ana García'})
CREATE (p1)-[:CONOCE]->(p2);

// Crear relación con propiedades
MATCH (p:Persona {nombre: 'Juan Pérez'}), (e:Empresa {nombre: 'TechCorp'})
CREATE (p)-[:TRABAJA_EN {desde: date('2020-01-01'), cargo: 'Desarrollador'}]->(e);

// Crear nodos y relación en una sola consulta
CREATE (p1:Persona {nombre: 'Pedro Sánchez', edad: 29}),
       (p2:Persona {nombre: 'Laura Jiménez', edad: 26}),
       (p1)-[:CONOCE {desde: date('2023-01-01')}]->(p2);

// Relación bidireccional
MATCH (p1:Persona {nombre: 'Juan Pérez'}), (p2:Persona {nombre: 'Ana García'})
CREATE (p1)-[:AMIGO]->(p2), (p2)-[:AMIGO]->(p1);
```

#### Consultar Relaciones

```cypher
// Obtener todas las relaciones
MATCH ()-[r]->() RETURN r;

// Obtener relaciones específicas
MATCH (p:Persona)-[r:CONOCE]->(p2:Persona)
RETURN p.nombre, p2.nombre, r;

// Patrón de relación sin dirección
MATCH (p1:Persona)-[r:CONOCE]-(p2:Persona)
WHERE p1.nombre = 'Juan Pérez'
RETURN p2.nombre;

// Múltiples tipos de relación
MATCH (p:Persona)-[r:CONOCE|AMIGO]->(p2:Persona)
RETURN p.nombre, type(r), p2.nombre;

// Relaciones con propiedades
MATCH (p:Persona)-[r:TRABAJA_EN]->(e:Empresa)
WHERE r.desde >= date('2020-01-01')
RETURN p.nombre, e.nombre, r.cargo;

// Caminos de longitud específica
MATCH (p1:Persona)-[:CONOCE*2]->(p2:Persona)
WHERE p1.nombre = 'Juan Pérez'
RETURN p2.nombre;

// Caminos de longitud variable
MATCH (p1:Persona)-[:CONOCE*1..3]->(p2:Persona)
WHERE p1.nombre = 'Juan Pérez'
RETURN DISTINCT p2.nombre;

// Camino más corto
MATCH (p1:Persona {nombre: 'Juan Pérez'}), (p2:Persona {nombre: 'Laura Jiménez'})
MATCH path = shortestPath((p1)-[:CONOCE*]-(p2))
RETURN path;
```

#### Actualizar Relaciones

```cypher
// Actualizar propiedades de relación
MATCH (p:Persona {nombre: 'Juan Pérez'})-[r:TRABAJA_EN]->(e:Empresa)
SET r.cargo = 'Senior Developer', r.salario = 75000
RETURN r;

// Quitar propiedad de relación
MATCH (p:Persona)-[r:TRABAJA_EN]->(e:Empresa)
WHERE p.nombre = 'Juan Pérez'
REMOVE r.salario;
```

#### Eliminar Relaciones

```cypher
// Eliminar relación específica
MATCH (p1:Persona {nombre: 'Juan Pérez'})-[r:CONOCE]->(p2:Persona {nombre: 'Ana García'})
DELETE r;

// Eliminar todas las relaciones de un tipo
MATCH ()-[r:CONOCE]->()
DELETE r;

// Eliminar relaciones con condición
MATCH (p:Persona)-[r:TRABAJA_EN]->(e:Empresa)
WHERE r.desde < date('2015-01-01')
DELETE r;
```

## Consultas Avanzadas

### Agregaciones

```cypher
// Contar nodos
MATCH (p:Persona) RETURN count(p);

// Contar relaciones
MATCH ()-[r:CONOCE]->() RETURN count(r);

// Agrupar y contar
MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa)
RETURN e.nombre, count(p) as empleados
ORDER BY empleados DESC;

// Estadísticas numéricas
MATCH (p:Persona)
RETURN 
  count(p) as total,
  avg(p.edad) as edad_promedio,
  min(p.edad) as edad_minima,
  max(p.edad) as edad_maxima,
  sum(p.edad) as suma_edades;

// Recopilar valores
MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa)
RETURN e.nombre, collect(p.nombre) as empleados;

// Recopilar con DISTINCT
MATCH (p:Persona)-[:CONOCE]->(amigo:Persona)
RETURN p.nombre, collect(DISTINCT amigo.nombre) as amigos;
```

### Subconsultas y UNION

```cypher
// UNION para combinar resultados
MATCH (p:Persona) RETURN p.nombre as nombre, 'Persona' as tipo
UNION
MATCH (e:Empresa) RETURN e.nombre as nombre, 'Empresa' as tipo;

// UNION ALL (incluye duplicados)
MATCH (p:Persona) WHERE p.edad < 30 RETURN p.nombre
UNION ALL
MATCH (p:Persona) WHERE p.edad > 25 RETURN p.nombre;

// Subconsulta con EXISTS
MATCH (p:Persona)
WHERE EXISTS {
  MATCH (p)-[:TRABAJA_EN]->(:Empresa)
}
RETURN p.nombre;

// Subconsulta con COUNT
MATCH (p:Persona)
WHERE size((p)-[:CONOCE]->()) > 2
RETURN p.nombre, size((p)-[:CONOCE]->()) as num_conocidos;
```

### Condicionales y Casos

```cypher
// CASE simple
MATCH (p:Persona)
RETURN p.nombre,
  CASE p.edad
    WHEN 25 THEN 'Veinticinco'
    WHEN 30 THEN 'Treinta'
    ELSE toString(p.edad)
  END as edad_texto;

// CASE con condiciones
MATCH (p:Persona)
RETURN p.nombre,
  CASE 
    WHEN p.edad < 30 THEN 'Joven'
    WHEN p.edad >= 30 AND p.edad < 60 THEN 'Adulto'
    ELSE 'Senior'
  END as categoria;

// COALESCE para valores nulos
MATCH (p:Persona)
RETURN p.nombre, coalesce(p.telefono, 'Sin teléfono') as telefono;
```

### Funciones de Texto y Fecha

```cypher
// Funciones de texto
MATCH (p:Persona)
RETURN 
  p.nombre,
  upper(p.nombre) as nombre_mayuscula,
  lower(p.nombre) as nombre_minuscula,
  size(p.nombre) as longitud_nombre,
  split(p.nombre, ' ') as partes_nombre;

// Funciones de fecha
RETURN 
  date() as fecha_hoy,
  datetime() as fecha_hora_actual,
  date('2024-01-01') as fecha_especifica,
  datetime('2024-01-01T10:00:00') as fecha_hora_especifica;

// Operaciones con fechas
MATCH (p:Persona)-[r:TRABAJA_EN]->(e:Empresa)
WHERE r.desde IS NOT NULL
RETURN 
  p.nombre,
  r.desde,
  duration.between(r.desde, date()) as tiempo_trabajando;
```

## Índices y Constraints

### Índices

```cypher
// Crear índice simple
CREATE INDEX persona_nombre FOR (p:Persona) ON (p.nombre);

// Crear índice compuesto
CREATE INDEX persona_nombre_edad FOR (p:Persona) ON (p.nombre, p.edad);

// Crear índice de texto completo
CREATE FULLTEXT INDEX persona_texto FOR (p:Persona) ON EACH [p.nombre, p.email];

// Listar índices
SHOW INDEXES;

// Eliminar índice
DROP INDEX persona_nombre;

// Usar índice de texto completo
CALL db.index.fulltext.queryNodes("persona_texto", "Juan García");
```

### Constraints

```cypher
// Constraint de unicidad
CREATE CONSTRAINT persona_email_unique FOR (p:Persona) REQUIRE p.email IS UNIQUE;

// Constraint de existencia
CREATE CONSTRAINT persona_nombre_exists FOR (p:Persona) REQUIRE p.nombre IS NOT NULL;

// Constraint de clave (Neo4j 4.0+)
CREATE CONSTRAINT persona_id FOR (p:Persona) REQUIRE p.id IS NODE KEY;

// Listar constraints
SHOW CONSTRAINTS;

// Eliminar constraint
DROP CONSTRAINT persona_email_unique;
```

## Procedimientos Almacenados (APOC)

### Instalación APOC

```cypher
// Verificar si APOC está instalado
CALL dbms.procedures() YIELD name
WHERE name STARTS WITH 'apoc'
RETURN count(name) as apoc_procedures;
```

### Procedimientos APOC Comunes

```cypher
// Cargar datos desde JSON
CALL apoc.load.json('file:///data.json')
YIELD value
CREATE (p:Persona)
SET p = value;

// Cargar desde CSV
CALL apoc.load.csv('file:///personas.csv')
YIELD map
CREATE (p:Persona)
SET p = map;

// Exportar a CSV
CALL apoc.export.csv.all('export.csv', {});

// Exportar consulta a JSON
CALL apoc.export.json.query('MATCH (p:Persona) RETURN p', 'personas.json', {});

// Ejecutar Cypher periódicamente
CALL apoc.periodic.iterate(
  'MATCH (p:Persona) RETURN p',
  'SET p.procesado = true',
  {batchSize: 100}
);

// Algoritmos de grafos
CALL apoc.algo.pageRank(['Persona'], ['CONOCE'], {iterations: 20});

// Detectar comunidades
CALL apoc.algo.community(['Persona'], ['CONOCE'], 'WRITE', {property: 'community'});
```

## Administración y Monitoreo

### Gestión de Usuarios y Seguridad

```cypher
// Crear usuario (Neo4j 4.0+)
CREATE USER juan SET PASSWORD 'contraseña123';

// Cambiar contraseña
ALTER USER juan SET PASSWORD 'nueva_contraseña';

// Crear rol
CREATE ROLE desarrollador;

// Asignar rol a usuario
GRANT ROLE desarrollador TO juan;

// Otorgar permisos
GRANT READ {*} ON GRAPH neo4j TO desarrollador;
GRANT WRITE ON GRAPH neo4j TO desarrollador;

// Ver usuarios
SHOW USERS;

// Ver roles
SHOW ROLES;

// Eliminar usuario
DROP USER juan;
```

### Monitoreo y Estadísticas

```cypher
// Transacciones activas
CALL dbms.listTransactions();

// Consultas en ejecución
CALL dbms.listQueries();

// Terminar consulta
CALL dbms.killQuery('query-id');

// Estadísticas de la base de datos
CALL db.stats.retrieve();

// Información de memoria
CALL dbms.queryJmx("java.lang:type=Memory");

// Pool de conexiones
CALL dbms.pool.status();
```

## Scripts de Utilidad

### Script de Backup

```bash
#!/bin/bash
# backup_neo4j.sh

NEO4J_HOME="/var/lib/neo4j"
BACKUP_DIR="/backups/neo4j"
DATE=$(date +%Y%m%d_%H%M%S)
DATABASE="neo4j"

mkdir -p $BACKUP_DIR

# Detener Neo4j (si es necesario)
# neo4j stop

# Backup usando neo4j-admin
neo4j-admin backup \
  --database=$DATABASE \
  --to=$BACKUP_DIR/backup_$DATE

# Comprimir backup
tar -czf $BACKUP_DIR/neo4j_backup_${DATE}.tar.gz $BACKUP_DIR/backup_$DATE

# Limpiar backup sin comprimir
rm -rf $BACKUP_DIR/backup_$DATE

# Reiniciar Neo4j (si se detuvo)
# neo4j start

echo "Backup completado: neo4j_backup_${DATE}.tar.gz"
```

### Script de Monitoreo

```cypher
-- monitoreo.cypher
// Información general
CALL dbms.components() YIELD name, versions, edition
RETURN name, versions[0] as version, edition;

// Estadísticas de nodos y relaciones
MATCH (n) RETURN labels(n) as etiqueta, count(n) as cantidad
UNION
MATCH ()-[r]->() RETURN type(r) as tipo_relacion, count(r) as cantidad;

// Índices y constraints
SHOW INDEXES YIELD name, state, type
RETURN name, state, type;

SHOW CONSTRAINTS YIELD name, type
RETURN name, type;

// Consultas lentas (si están habilitadas)
CALL dbms.listQueries() 
YIELD queryId, query, elapsedTimeMillis, status
WHERE elapsedTimeMillis > 1000
RETURN queryId, substring(query, 0, 100) as query_snippet, elapsedTimeMillis, status;
```

### Script de Limpieza

```cypher
-- limpieza.cypher
// Eliminar nodos huérfanos (sin relaciones)
MATCH (n)
WHERE NOT (n)--()
DELETE n;

// Eliminar duplicados por propiedad
MATCH (p:Persona)
WITH p.email as email, collect(p) as personas
WHERE size(personas) > 1
UNWIND personas[1..] as duplicado
DETACH DELETE duplicado;

// Limpiar propiedades nulas
MATCH (n)
WHERE any(key in keys(n) WHERE n[key] IS NULL)
WITH n, [key in keys(n) WHERE n[key] IS NULL] as null_keys
FOREACH (key in null_keys | REMOVE n[key]);
```

## Ejemplos de Uso Común

### Red Social

```cypher
// Crear usuarios
CREATE (juan:Usuario {nombre: 'Juan Pérez', email: 'juan@example.com', fecha_registro: date()}),
       (ana:Usuario {nombre: 'Ana García', email: 'ana@example.com', fecha_registro: date()}),
       (luis:Usuario {nombre: 'Luis Rodríguez', email: 'luis@example.com', fecha_registro: date()});

// Crear relaciones de amistad
MATCH (juan:Usuario {nombre: 'Juan Pérez'}), (ana:Usuario {nombre: 'Ana García'})
CREATE (juan)-[:AMIGO {desde: date()}]->(ana),
       (ana)-[:AMIGO {desde: date()}]->(juan);

// Crear posts
MATCH (juan:Usuario {nombre: 'Juan Pérez'})
CREATE (juan)-[:PUBLICO]->(post:Post {
  contenido: 'Mi primer post en Neo4j!',
  fecha: datetime(),
  likes: 0
});

// Dar like a post
MATCH (ana:Usuario {nombre: 'Ana García'}), (post:Post)
WHERE (post)<-[:PUBLICO]-(:Usuario {nombre: 'Juan Pérez'})
CREATE (ana)-[:LIKE {fecha: datetime()}]->(post)
SET post.likes = post.likes + 1;

// Encontrar amigos de amigos
MATCH (juan:Usuario {nombre: 'Juan Pérez'})-[:AMIGO]->()-[:AMIGO]->(sugerencia:Usuario)
WHERE NOT (juan)-[:AMIGO]-(sugerencia) AND juan <> sugerencia
RETURN DISTINCT sugerencia.nombre;

// Posts más populares
MATCH (post:Post)
RETURN post.contenido, post.likes
ORDER BY post.likes DESC
LIMIT 10;
```

### Sistema de Recomendaciones

```cypher
// Crear productos y categorías
CREATE (electronica:Categoria {nombre: 'Electrónica'}),
       (libros:Categoria {nombre: 'Libros'}),
       (laptop:Producto {nombre: 'Laptop Gaming', precio: 1299.99}),
       (libro:Producto {nombre: 'Aprende Neo4j', precio: 29.99});

CREATE (laptop)-[:PERTENECE_A]->(electronica),
       (libro)-[:PERTENECE_A]->(libros);

// Crear usuarios y compras
CREATE (cliente:Cliente {nombre: 'María López', edad: 28});

MATCH (cliente:Cliente {nombre: 'María López'}), (laptop:Producto {nombre: 'Laptop Gaming'})
CREATE (cliente)-[:COMPRO {fecha: date(), rating: 5}]->(laptop);

// Usuarios que compraron productos similares
MATCH (cliente:Cliente {nombre: 'María López'})-[:COMPRO]->(producto:Producto)-[:PERTENECE_A]->(categoria:Categoria)
MATCH (categoria)<-[:PERTENECE_A]-(otros_productos:Producto)
WHERE NOT (cliente)-[:COMPRO]->(otros_productos)
RETURN otros_productos.nombre, categoria.nombre
LIMIT 5;

// Recomendaciones basadas en clientes similares
MATCH (cliente:Cliente {nombre: 'María López'})-[:COMPRO]->(producto:Producto)<-[:COMPRO]-(otros_clientes:Cliente)
MATCH (otros_clientes)-[:COMPRO]->(recomendaciones:Producto)
WHERE NOT (cliente)-[:COMPRO]->(recomendaciones)
RETURN recomendaciones.nombre, count(*) as frecuencia
ORDER BY frecuencia DESC
LIMIT 5;
```

### Gestión de Empleados y Organigrama

```cypher
// Crear empresa y departamentos
CREATE (empresa:Empresa {nombre: 'TechCorp', fundada: 2010}),
       (it:Departamento {nombre: 'IT'}),
       (ventas:Departamento {nombre: 'Ventas'}),
       (rrhh:Departamento {nombre: 'RRHH'});

CREATE (it)-[:PERTENECE_A]->(empresa),
       (ventas)-[:PERTENECE_A]->(empresa),
       (rrhh)-[:PERTENECE_A]->(empresa);

// Crear empleados
CREATE (ceo:Empleado {nombre: 'Carlos CEO', cargo: 'CEO', salario: 150000}),
       (cto:Empleado {nombre: 'Ana CTO', cargo: 'CTO', salario: 120000}),
       (dev1:Empleado {nombre: 'Juan Developer', cargo: 'Senior Developer', salario: 75000}),
       (dev2:Empleado {nombre: 'María Developer', cargo: 'Junior Developer', salario: 45000});

// Asignar a departamentos
MATCH (cto:Empleado {cargo: 'CTO'}), (it:Departamento {nombre: 'IT'})
CREATE (cto)-[:TRABAJA_EN]->(it);

MATCH (dev:Empleado) WHERE dev.cargo CONTAINS 'Developer'
MATCH (it:Departamento {nombre: 'IT'})
CREATE (dev)-[:TRABAJA_EN]->(it);

// Jerarquía organizacional
MATCH (ceo:Empleado {cargo: 'CEO'}), (cto:Empleado {cargo: 'CTO'})
CREATE (cto)-[:REPORTA_A]->(ceo);

MATCH (dev:Empleado), (cto:Empleado {cargo: 'CTO'})
WHERE dev.cargo CONTAINS 'Developer'
CREATE (dev)-[:REPORTA_A]->(cto);

// Consultar organigrama
MATCH (jefe:Empleado)<-[:REPORTA_A*]-(subordinados:Empleado)
WHERE jefe.cargo = 'CEO'
RETURN jefe.nombre as jefe, collect(subordinados.nombre) as equipo;

// Empleados por departamento con salarios
MATCH (emp:Empleado)-[:TRABAJA_EN]->(dept:Departamento)
RETURN dept.nombre, 
       collect(emp.nombre) as empleados,
       avg(emp.salario) as salario_promedio,
       sum(emp.salario) as costo_total
ORDER BY costo_total DESC;
```

### Sistema de Transporte y Rutas

```cypher
// Crear ciudades
CREATE (madrid:Ciudad {nombre: 'Madrid', poblacion: 3200000}),
       (barcelona:Ciudad {nombre: 'Barcelona', poblacion: 1600000}),
       (valencia:Ciudad {nombre: 'Valencia', poblacion: 800000}),
       (sevilla:Ciudad {nombre: 'Sevilla', poblacion: 700000});

// Crear conexiones de transporte
CREATE (madrid)-[:CONECTA_CON {distancia: 620, tiempo: 380, medio: 'tren'}]->(barcelona),
       (madrid)-[:CONECTA_CON {distancia: 355, tiempo: 210, medio: 'tren'}]->(valencia),
       (madrid)-[:CONECTA_CON {distancia: 530, tiempo: 320, medio: 'tren'}]->(sevilla),
       (barcelona)-[:CONECTA_CON {distancia: 350, tiempo: 180, medio: 'tren'}]->(valencia);

// Encontrar ruta más corta por distancia
MATCH (origen:Ciudad {nombre: 'Madrid'}), (destino:Ciudad {nombre: 'Barcelona'})
MATCH path = shortestPath((origen)-[:CONECTA_CON*]-(destino))
RETURN path, reduce(distancia = 0, rel in relationships(path) | distancia + rel.distancia) as distancia_total;

// Encontrar ruta más rápida
MATCH (origen:Ciudad {nombre: 'Madrid'}), (destino:Ciudad {nombre: 'Valencia'})
MATCH path = allShortestPaths((origen)-[:CONECTA_CON*]-(destino))
RETURN path, reduce(tiempo = 0, rel in relationships(path) | tiempo + rel.tiempo) as tiempo_total
ORDER BY tiempo_total
LIMIT 1;

// Ciudades accesibles desde una ciudad
MATCH (madrid:Ciudad {nombre: 'Madrid'})-[:CONECTA_CON*1..2]-(accesible:Ciudad)
RETURN DISTINCT accesible.nombre, accesible.poblacion
ORDER BY accesible.poblacion DESC;
```
