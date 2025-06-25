# Comandos MongoDB

Este archivo contiene una lista de comandos MongoDB para línea de comandos y shell de MongoDB, organizados por categoría.

## Herramientas de Línea de Comandos

### mongosh (MongoDB Shell moderno)

**Descripción:**  
Shell interactivo moderno para MongoDB (reemplaza al mongo shell legacy).

**Sintaxis:**
```bash
mongosh [opciones] [conexión]
```

**Opciones comunes:**
- `--host`: Host del servidor MongoDB
- `--port`: Puerto del servidor (por defecto 27017)
- `--username`: Nombre de usuario
- `--password`: Contraseña
- `--authenticationDatabase`: Base de datos de autenticación
- `--ssl`: Usar conexión SSL
- `--eval`: Evaluar código JavaScript
- `--file`: Ejecutar archivo JavaScript
- `--quiet`: Modo silencioso
- `--norc`: No cargar archivo .mongorc.js

**Ejemplos:**
```bash
# Conectar a servidor local
mongosh

# Conectar a servidor remoto
mongosh --host servidor.example.com --port 27017

# Conectar con autenticación
mongosh --username admin --password --authenticationDatabase admin

# Conectar con URI de conexión
mongosh "mongodb://usuario:contraseña@servidor:27017/basedatos"

# Ejecutar comando específico
mongosh --eval "db.version()"

# Ejecutar script JavaScript
mongosh --file script.js

# Conectar con SSL
mongosh --ssl --host servidor.example.com
```

### mongo (Legacy Shell)

**Descripción:**  
Shell legacy de MongoDB (deprecado, usar mongosh).

**Ejemplos:**
```bash
# Conectar a servidor local
mongo

# Conectar con base de datos específica
mongo mi_base_datos

# Conectar con autenticación
mongo -u admin -p --authenticationDatabase admin
```

## Comandos del Shell MongoDB

### Comandos de Base de Datos

**show dbs** - Listar bases de datos
```javascript
show dbs
```

**use** - Cambiar/crear base de datos
```javascript
use mi_base_datos
```

**db** - Mostrar base de datos actual
```javascript
db
```

**db.dropDatabase()** - Eliminar base de datos
```javascript
db.dropDatabase()
```

**db.stats()** - Estadísticas de base de datos
```javascript
db.stats()
```

### Comandos de Colecciones

**show collections** - Listar colecciones
```javascript
show collections
```

**db.createCollection()** - Crear colección
```javascript
db.createCollection("mi_coleccion")

// Con opciones
db.createCollection("mi_coleccion", {
  capped: true,
  size: 100000,
  max: 5000
})
```

**db.collection.drop()** - Eliminar colección
```javascript
db.mi_coleccion.drop()
```

**db.collection.stats()** - Estadísticas de colección
```javascript
db.mi_coleccion.stats()
```

### Operaciones CRUD

#### Insertar Documentos

**insertOne()** - Insertar un documento
```javascript
db.usuarios.insertOne({
  nombre: "Juan Pérez",
  edad: 30,
  email: "juan@example.com"
})
```

**insertMany()** - Insertar múltiples documentos
```javascript
db.usuarios.insertMany([
  { nombre: "Ana García", edad: 25, email: "ana@example.com" },
  { nombre: "Luis Rodríguez", edad: 35, email: "luis@example.com" }
])
```

#### Consultar Documentos

**find()** - Buscar documentos
```javascript
// Buscar todos
db.usuarios.find()

// Con filtro
db.usuarios.find({ edad: { $gte: 18 } })

// Con proyección
db.usuarios.find({}, { nombre: 1, email: 1, _id: 0 })

// Con límite y ordenamiento
db.usuarios.find().sort({ edad: -1 }).limit(5)

// Buscar uno
db.usuarios.findOne({ email: "juan@example.com" })
```

**Operadores de consulta:**
```javascript
// Operadores de comparación
db.productos.find({ precio: { $gt: 100 } })        // mayor que
db.productos.find({ precio: { $gte: 100 } })       // mayor o igual
db.productos.find({ precio: { $lt: 100 } })        // menor que
db.productos.find({ precio: { $lte: 100 } })       // menor o igual
db.productos.find({ precio: { $ne: 100 } })        // no igual
db.productos.find({ categoria: { $in: ["libro", "revista"] } })

// Operadores lógicos
db.productos.find({
  $and: [
    { precio: { $gte: 50 } },
    { categoria: "libro" }
  ]
})

db.productos.find({
  $or: [
    { precio: { $lt: 20 } },
    { categoria: "oferta" }
  ]
})

// Operadores de elemento
db.usuarios.find({ telefono: { $exists: true } })
db.usuarios.find({ edad: { $type: "number" } })

// Operadores de array
db.productos.find({ tags: "nuevo" })                // elemento en array
db.productos.find({ tags: { $all: ["nuevo", "popular"] } })
db.productos.find({ "comentarios.2": { $exists: true } })

// Expresiones regulares
db.usuarios.find({ nombre: /^Juan/ })
db.usuarios.find({ email: { $regex: "@gmail\\.com$" } })
```

#### Actualizar Documentos

**updateOne()** - Actualizar un documento
```javascript
db.usuarios.updateOne(
  { email: "juan@example.com" },
  { $set: { edad: 31 } }
)
```

**updateMany()** - Actualizar múltiples documentos
```javascript
db.usuarios.updateMany(
  { edad: { $lt: 18 } },
  { $set: { categoria: "menor" } }
)
```

**replaceOne()** - Reemplazar documento completo
```javascript
db.usuarios.replaceOne(
  { email: "juan@example.com" },
  { nombre: "Juan Carlos", edad: 32, email: "juan@example.com" }
)
```

**Operadores de actualización:**
```javascript
// $set - establecer campo
db.usuarios.updateOne(
  { _id: ObjectId("...") },
  { $set: { nombre: "Nuevo Nombre", "direccion.ciudad": "Madrid" } }
)

// $unset - eliminar campo
db.usuarios.updateOne(
  { _id: ObjectId("...") },
  { $unset: { telefono: "" } }
)

// $inc - incrementar valor numérico
db.productos.updateOne(
  { _id: ObjectId("...") },
  { $inc: { precio: 10, stock: -1 } }
)

// $push/$addToSet - agregar a array
db.usuarios.updateOne(
  { _id: ObjectId("...") },
  { $push: { hobbies: "lectura" } }
)

db.usuarios.updateOne(
  { _id: ObjectId("...") },
  { $addToSet: { tags: "premium" } }
)

// $pull/$pop - remover de array
db.usuarios.updateOne(
  { _id: ObjectId("...") },
  { $pull: { hobbies: "televisión" } }
)

// $rename - renombrar campo
db.usuarios.updateMany(
  {},
  { $rename: { "telefono": "movil" } }
)
```

#### Eliminar Documentos

**deleteOne()** - Eliminar un documento
```javascript
db.usuarios.deleteOne({ email: "juan@example.com" })
```

**deleteMany()** - Eliminar múltiples documentos
```javascript
db.usuarios.deleteMany({ edad: { $lt: 18 } })
```

### Agregación

**aggregate()** - Pipeline de agregación
```javascript
// Ejemplo básico
db.ventas.aggregate([
  { $match: { fecha: { $gte: new Date("2024-01-01") } } },
  { $group: { _id: "$producto", total: { $sum: "$cantidad" } } },
  { $sort: { total: -1 } }
])

// Operadores de agregación comunes
db.ventas.aggregate([
  // $match - filtrar documentos
  { $match: { estado: "completada" } },
  
  // $group - agrupar y agregar
  { $group: {
    _id: "$vendedor",
    totalVentas: { $sum: "$monto" },
    ventasPromedio: { $avg: "$monto" },
    maxVenta: { $max: "$monto" },
    minVenta: { $min: "$monto" },
    cantidadVentas: { $count: {} }
  }},
  
  // $project - proyectar campos
  { $project: {
    vendedor: "$_id",
    totalVentas: 1,
    ventasPromedio: { $round: ["$ventasPromedio", 2] },
    _id: 0
  }},
  
  // $sort - ordenar
  { $sort: { totalVentas: -1 } },
  
  // $limit - limitar resultados
  { $limit: 10 }
])

// $lookup - join entre colecciones
db.pedidos.aggregate([
  {
    $lookup: {
      from: "clientes",
      localField: "cliente_id",
      foreignField: "_id",
      as: "cliente_info"
    }
  }
])

// $unwind - desarmar arrays
db.productos.aggregate([
  { $unwind: "$tags" },
  { $group: { _id: "$tags", count: { $sum: 1 } } }
])
```

### Índices

**Crear índices:**
```javascript
// Índice simple
db.usuarios.createIndex({ email: 1 })

// Índice compuesto
db.productos.createIndex({ categoria: 1, precio: -1 })

// Índice de texto
db.articulos.createIndex({ titulo: "text", contenido: "text" })

// Índice único
db.usuarios.createIndex({ email: 1 }, { unique: true })

// Índice parcial
db.productos.createIndex(
  { precio: 1 },
  { partialFilterExpression: { precio: { $gt: 100 } } }
)

// Índice TTL (Time To Live)
db.sesiones.createIndex(
  { fecha_creacion: 1 },
  { expireAfterSeconds: 3600 }
)
```

**Gestionar índices:**
```javascript
// Listar índices
db.usuarios.getIndexes()

// Eliminar índice
db.usuarios.dropIndex({ email: 1 })
db.usuarios.dropIndex("email_1")

// Reindexar colección
db.usuarios.reIndex()

// Estadísticas de uso de índices
db.usuarios.find({ email: "test@example.com" }).explain("executionStats")
```

### Información y Estadísticas

**Información del servidor:**
```javascript
// Versión de MongoDB
db.version()

// Estado del servidor
db.serverStatus()

// Estadísticas de operaciones
db.runCommand({ serverStatus: 1 }).opcounters

// Información de replicación
rs.status()
rs.config()

// Usuarios y roles
db.runCommand({ usersInfo: 1 })
```

**Información de rendimiento:**
```javascript
// Operaciones actuales
db.currentOp()

// Estadísticas de colección
db.mi_coleccion.stats()

// Profiler de consultas
db.setProfilingLevel(2)  // Profiling completo
db.setProfilingLevel(1, { slowms: 100 })  // Solo consultas lentas
db.system.profile.find().sort({ ts: -1 }).limit(5)
```

## Herramientas de Administración

### mongodump / mongorestore

**mongodump** - Crear backup de base de datos
```bash
# Backup completo
mongodump --host localhost --port 27017

# Backup de base de datos específica
mongodump --host localhost --db mi_base_datos --out /backup/

# Backup con autenticación
mongodump --username admin --password --authenticationDatabase admin --db mi_base_datos

# Backup de colección específica
mongodump --db mi_base_datos --collection mi_coleccion --out /backup/

# Backup con consulta específica
mongodump --db mi_base_datos --collection usuarios --query '{"edad": {"$gte": 18}}'
```

**mongorestore** - Restaurar backup
```bash
# Restaurar backup completo
mongorestore /backup/

# Restaurar base de datos específica
mongorestore --db nueva_base_datos /backup/mi_base_datos/

# Restaurar con mapeo de base de datos
mongorestore --db nueva_base_datos /backup/mi_base_datos/

# Restaurar colección específica
mongorestore --db mi_base_datos --collection mi_coleccion /backup/mi_base_datos/mi_coleccion.bson
```

### mongoexport / mongoimport

**mongoexport** - Exportar datos en JSON/CSV
```bash
# Exportar colección en JSON
mongoexport --db mi_base_datos --collection usuarios --out usuarios.json

# Exportar en CSV
mongoexport --db mi_base_datos --collection usuarios --type=csv --fields nombre,email,edad --out usuarios.csv

# Exportar con consulta
mongoexport --db mi_base_datos --collection usuarios --query '{"edad": {"$gte": 18}}' --out adultos.json

# Exportar con formato pretty
mongoexport --db mi_base_datos --collection usuarios --jsonArray --pretty --out usuarios_pretty.json
```

**mongoimport** - Importar datos desde JSON/CSV
```bash
# Importar desde JSON
mongoimport --db mi_base_datos --collection usuarios --file usuarios.json

# Importar desde CSV
mongoimport --db mi_base_datos --collection usuarios --type csv --headerline --file usuarios.csv

# Importar con upsert
mongoimport --db mi_base_datos --collection usuarios --file usuarios.json --upsert

# Importar array JSON
mongoimport --db mi_base_datos --collection usuarios --jsonArray --file usuarios.json
```

### mongostat / mongotop

**mongostat** - Estadísticas en tiempo real
```bash
# Estadísticas básicas
mongostat

# Con intervalo específico
mongostat --host localhost:27017 5

# Con autenticación
mongostat --username admin --password --authenticationDatabase admin
```

**mongotop** - Tiempo de lectura/escritura por colección
```bash
# Top de colecciones
mongotop

# Con intervalo específico
mongotop 10
```

## Gestión de Usuarios y Seguridad

### Autenticación y Autorización

**Crear usuarios:**
```javascript
// Cambiar a base de datos admin
use admin

// Crear usuario administrador
db.createUser({
  user: "admin",
  pwd: "contraseña_segura",
  roles: [
    { role: "userAdminAnyDatabase", db: "admin" },
    { role: "readWriteAnyDatabase", db: "admin" }
  ]
})

// Crear usuario para base de datos específica
use mi_base_datos
db.createUser({
  user: "app_user",
  pwd: "contraseña_app",
  roles: [
    { role: "readWrite", db: "mi_base_datos" }
  ]
})

// Crear usuario con roles personalizados
db.createUser({
  user: "readonly_user",
  pwd: "contraseña_readonly",
  roles: [
    { role: "read", db: "mi_base_datos" }
  ]
})
```

**Gestionar usuarios:**
```javascript
// Listar usuarios
db.getUsers()

// Cambiar contraseña
db.changeUserPassword("usuario", "nueva_contraseña")

// Otorgar rol
db.grantRolesToUser("usuario", [{ role: "readWrite", db: "otra_base_datos" }])

// Revocar rol
db.revokeRolesFromUser("usuario", [{ role: "read", db: "mi_base_datos" }])

// Eliminar usuario
db.dropUser("usuario")
```

### Roles Personalizados

```javascript
// Crear rol personalizado
db.createRole({
  role: "reportReader",
  privileges: [
    {
      resource: { db: "mi_base_datos", collection: "reportes" },
      actions: ["find", "listIndexes"]
    }
  ],
  roles: []
})

// Listar roles
db.getRoles()

// Información de rol
db.getRole("reportReader", { showPrivileges: true })
```

## Replicación y Sharding

### Replica Sets

**Configurar replica set:**
```javascript
// Inicializar replica set
rs.initiate({
  _id: "miReplicaSet",
  members: [
    { _id: 0, host: "servidor1:27017" },
    { _id: 1, host: "servidor2:27017" },
    { _id: 2, host: "servidor3:27017" }
  ]
})

// Agregar miembro
rs.add("servidor4:27017")

// Agregar miembro secundario
rs.addArb("servidor5:27017")

// Ver estado
rs.status()

// Ver configuración
rs.config()

// Forzar elección
rs.stepDown()
```

### Sharding

**Comandos de sharding:**
```javascript
// Habilitar sharding en base de datos
sh.enableSharding("mi_base_datos")

// Shard de colección
sh.shardCollection("mi_base_datos.mi_coleccion", { campo_shard: 1 })

// Estado del cluster
sh.status()

// Información de shards
db.adminCommand("listShards")

// Balanceador
sh.startBalancer()
sh.stopBalancer()
sh.isBalancerRunning()
```

## Variables de Entorno

- `MONGO_URL`: URL de conexión por defecto
- `MONGODB_URI`: URI de conexión (alternativa)
- `MONGO_INITDB_ROOT_USERNAME`: Usuario root inicial
- `MONGO_INITDB_ROOT_PASSWORD`: Contraseña root inicial
- `MONGO_INITDB_DATABASE`: Base de datos inicial

## Archivos de Configuración

- `mongod.conf`: Configuración del servidor MongoDB
- `.mongorc.js`: Script de inicialización del shell
- `keyfile`: Archivo de clave para replica sets

## Ejemplo mongod.conf

```yaml
# mongod.conf
storage:
  dbPath: /var/lib/mongodb
  journal:
    enabled: true

systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log

net:
  port: 27017
  bindIp: 127.0.0.1

security:
  authorization: enabled
  keyFile: /etc/mongodb/keyfile

replication:
  replSetName: "miReplicaSet"
```

## Scripts de Utilidad

### Script de Backup Automatizado

```bash
#!/bin/bash
# backup_mongodb.sh

DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_DIR="/backups/mongodb"
DB_NAME="mi_base_datos"

mkdir -p $BACKUP_DIR

mongodump \
  --host localhost:27017 \
  --username backup_user \
  --password backup_pass \
  --authenticationDatabase admin \
  --db $DB_NAME \
  --out $BACKUP_DIR/backup_$DATE

# Comprimir backup
tar -czf $BACKUP_DIR/backup_${DB_NAME}_${DATE}.tar.gz $BACKUP_DIR/backup_$DATE

# Limpiar backup sin comprimir
rm -rf $BACKUP_DIR/backup_$DATE

echo "Backup completado: backup_${DB_NAME}_${DATE}.tar.gz"
```

### Script de Monitoreo

```javascript
// monitoreo.js
print("=== MONITOREO MONGODB ===");
print("Fecha: " + new Date());

print("\n--- INFORMACIÓN GENERAL ---");
print("Versión: " + db.version());
print("Base de datos actual: " + db.getName());

print("\n--- ESTADÍSTICAS DE SERVIDOR ---");
var serverStatus = db.serverStatus();
print("Uptime: " + serverStatus.uptime + " segundos");
print("Conexiones actuales: " + serverStatus.connections.current);
print("Operaciones por segundo:");
print("  Insert: " + serverStatus.opcounters.insert);
print("  Query: " + serverStatus.opcounters.query);
print("  Update: " + serverStatus.opcounters.update);
print("  Delete: " + serverStatus.opcounters.delete);

print("\n--- USO DE MEMORIA ---");
print("Memoria virtual: " + serverStatus.mem.virtual + " MB");
print("Memoria residente: " + serverStatus.mem.resident + " MB");

print("\n--- COLECCIONES ---");
db.runCommand("listCollections").cursor.firstBatch.forEach(
  function(collection) {
    print("- " + collection.name);
  }
);
```

## Ejemplos de Uso Común

### Aplicación de Blog

```javascript
// Crear colecciones
use blog

// Insertar posts
db.posts.insertMany([
  {
    titulo: "Mi primer post",
    contenido: "Este es el contenido del post...",
    autor: "Juan Pérez",
    fecha: new Date(),
    tags: ["tutorial", "mongodb"],
    comentarios: [
      {
        autor: "Ana García",
        comentario: "Excelente post!",
        fecha: new Date()
      }
    ]
  }
])

// Buscar posts por tag
db.posts.find({ tags: "mongodb" })

// Agregar comentario
db.posts.updateOne(
  { _id: ObjectId("...") },
  {
    $push: {
      comentarios: {
        autor: "Luis Rodríguez",
        comentario: "Muy útil, gracias!",
        fecha: new Date()
      }
    }
  }
)

// Posts más recientes
db.posts.find().sort({ fecha: -1 }).limit(5)
```

### Sistema de E-commerce

```javascript
use ecommerce

// Productos con inventario
db.productos.insertOne({
  nombre: "Laptop Gaming",
  precio: 1299.99,
  categoria: "electrónica",
  stock: 15,
  especificaciones: {
    cpu: "Intel i7",
    ram: "16GB",
    storage: "512GB SSD"
  },
  tags: ["gaming", "laptop", "intel"],
  fecha_creacion: new Date()
})

// Buscar productos por rango de precio
db.productos.find({
  precio: { $gte: 500, $lte: 1500 },
  stock: { $gt: 0 }
})

// Actualizar stock después de venta
db.productos.updateOne(
  { _id: ObjectId("...") },
  { $inc: { stock: -1 } }
)

// Productos más vendidos (usando agregación)
db.ventas.aggregate([
  { $group: {
    _id: "$producto_id",
    total_vendido: { $sum: "$cantidad" }
  }},
  { $sort: { total_vendido: -1 } },
  { $limit: 10 },
  { $lookup: {
    from: "productos",
    localField: "_id",
    foreignField: "_id",
    as: "producto_info"
  }}
])
```
