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

## MongoDB for AI/ML Applications

### Vector Similarity Search

#### Storing and Querying Embeddings
```javascript
// Crear colección para embeddings
use ai_database

// Crear índice vectorial para búsqueda de similaridad
db.embeddings.createIndex({
  "vector": "2dsphere"
})

// Insertar documentos con embeddings
db.embeddings.insertMany([
  {
    _id: ObjectId(),
    text: "Machine learning is a subset of artificial intelligence",
    vector: [0.1, 0.2, -0.3, 0.4, -0.1, 0.8, 0.2, -0.5],
    metadata: {
      source: "textbook",
      category: "AI",
      timestamp: new Date()
    }
  },
  {
    _id: ObjectId(),
    text: "Deep learning uses neural networks with multiple layers",
    vector: [0.2, 0.1, -0.2, 0.5, -0.2, 0.7, 0.3, -0.4],
    metadata: {
      source: "article",
      category: "ML",
      timestamp: new Date()
    }
  }
])

// Búsqueda de similaridad usando agregación
db.embeddings.aggregate([
  {
    $addFields: {
      similarity: {
        $let: {
          vars: {
            queryVector: [0.15, 0.15, -0.25, 0.45, -0.15, 0.75, 0.25, -0.45]
          },
          in: {
            $divide: [
              {
                $reduce: {
                  input: { $range: [0, { $size: "$vector" }] },
                  initialValue: 0,
                  in: {
                    $add: [
                      "$$value",
                      {
                        $multiply: [
                          { $arrayElemAt: ["$vector", "$$this"] },
                          { $arrayElemAt: ["$$vars.queryVector", "$$this"] }
                        ]
                      }
                    ]
                  }
                }
              },
              {
                $multiply: [
                  {
                    $sqrt: {
                      $reduce: {
                        input: "$vector",
                        initialValue: 0,
                        in: { $add: ["$$value", { $multiply: ["$$this", "$$this"] }] }
                      }
                    }
                  },
                  {
                    $sqrt: {
                      $reduce: {
                        input: "$$vars.queryVector",
                        initialValue: 0,
                        in: { $add: ["$$value", { $multiply: ["$$this", "$$this"] }] }
                      }
                    }
                  }
                ]
              }
            ]
          }
        }
      }
    }
  },
  { $sort: { similarity: -1 } },
  { $limit: 5 }
])
```

#### Text Embeddings with MongoDB
```javascript
// Colección para almacenar embeddings de texto
db.text_embeddings.createIndex({ "embedding": "2dsphere" })

// Función para calcular distancia coseno
function cosineSimilarity(vecA, vecB) {
  let dotProduct = 0;
  let normA = 0;
  let normB = 0;
  
  for (let i = 0; i < vecA.length; i++) {
    dotProduct += vecA[i] * vecB[i];
    normA += vecA[i] * vecA[i];
    normB += vecB[i] * vecB[i];
  }
  
  return dotProduct / (Math.sqrt(normA) * Math.sqrt(normB));
}

// Insertar documentos con embeddings
db.text_embeddings.insertMany([
  {
    document_id: "doc_001",
    text: "Python is a programming language",
    embedding: Array.from({length: 384}, () => Math.random() - 0.5),
    metadata: {
      language: "en",
      category: "programming",
      tokens: 6
    }
  },
  {
    document_id: "doc_002", 
    text: "JavaScript is used for web development",
    embedding: Array.from({length: 384}, () => Math.random() - 0.5),
    metadata: {
      language: "en",
      category: "programming",
      tokens: 6
    }
  }
])

// Búsqueda semántica
db.text_embeddings.find({
  metadata: { category: "programming" }
}).forEach(doc => {
  // En una aplicación real, calcularías la similitud aquí
  print(`${doc.document_id}: ${doc.text}`)
})
```

### Machine Learning Model Storage

#### Model Metadata and Versioning
```javascript
// Colección para metadatos de modelos ML
use ml_models

db.models.createIndex({ "name": 1, "version": 1 }, { unique: true })
db.models.createIndex({ "created_at": -1 })
db.models.createIndex({ "performance.accuracy": -1 })

// Insertar metadata de modelo
db.models.insertOne({
  name: "sentiment_classifier",
  version: "1.0.0",
  algorithm: "Random Forest",
  framework: "scikit-learn",
  hyperparameters: {
    n_estimators: 100,
    max_depth: 10,
    random_state: 42
  },
  training_data: {
    dataset: "imdb_reviews",
    samples: 50000,
    features: 10000,
    train_split: 0.8
  },
  performance: {
    accuracy: 0.89,
    precision: 0.87,
    recall: 0.91,
    f1_score: 0.89,
    auc: 0.94
  },
  artifacts: {
    model_file: "s3://models/sentiment_classifier_v1.pkl",
    vectorizer: "s3://models/tfidf_vectorizer_v1.pkl",
    config: "s3://models/config_v1.json"
  },
  created_at: new Date(),
  created_by: "data_scientist_001",
  status: "active",
  tags: ["nlp", "sentiment", "classification"]
})

// Buscar mejores modelos por métrica
db.models.find({
  name: "sentiment_classifier",
  status: "active"
}).sort({ "performance.accuracy": -1 }).limit(5)

// Comparar versiones de modelo
db.models.aggregate([
  { $match: { name: "sentiment_classifier" } },
  { $sort: { version: -1 } },
  { $project: {
    version: 1,
    accuracy: "$performance.accuracy",
    created_at: 1,
    hyperparameters: 1
  }}
])

// Actualizar estado del modelo
db.models.updateOne(
  { name: "sentiment_classifier", version: "1.0.0" },
  { 
    $set: { 
      status: "deprecated",
      deprecated_at: new Date(),
      replaced_by: "1.1.0"
    }
  }
)
```

### Training Data Management

#### Dataset Storage and Lineage
```javascript
// Colección para datasets de entrenamiento
use training_data

db.datasets.createIndex({ "name": 1, "version": 1 }, { unique: true })
db.datasets.createIndex({ "created_at": -1 })
db.datasets.createIndex({ "tags": 1 })

// Insertar dataset
db.datasets.insertOne({
  name: "customer_reviews",
  version: "2.1.0",
  description: "Customer product reviews for sentiment analysis",
  schema: {
    review_id: "string",
    product_id: "string", 
    customer_id: "string",
    review_text: "string",
    rating: "integer",
    sentiment_label: "string",
    created_date: "datetime"
  },
  statistics: {
    total_records: 125000,
    positive_samples: 67500,
    negative_samples: 42500,
    neutral_samples: 15000,
    avg_text_length: 156,
    languages: ["en", "es", "fr"]
  },
  data_sources: [
    {
      source: "ecommerce_platform",
      contribution: 0.6,
      date_range: {
        start: ISODate("2023-01-01"),
        end: ISODate("2023-12-31")
      }
    },
    {
      source: "survey_responses", 
      contribution: 0.4,
      date_range: {
        start: ISODate("2023-06-01"),
        end: ISODate("2023-12-31")
      }
    }
  ],
  preprocessing: {
    steps: [
      "text_cleaning",
      "tokenization", 
      "stopword_removal",
      "stemming"
    ],
    tools: ["nltk", "spacy"],
    parameters: {
      min_length: 10,
      max_length: 500,
      language: "english"
    }
  },
  quality_metrics: {
    completeness: 0.98,
    accuracy: 0.95,
    consistency: 0.92,
    duplicates_removed: 3420
  },
  storage: {
    location: "s3://datasets/customer_reviews_v2.1.0/",
    format: "parquet",
    size_gb: 2.4,
    partitioning: ["year", "month"]
  },
  created_at: new Date(),
  created_by: "data_team",
  tags: ["nlp", "sentiment", "ecommerce", "reviews"],
  lineage: {
    parent_datasets: ["raw_reviews_v1.0", "survey_data_v1.2"],
    transformations: ["cleaning", "labeling", "augmentation"]
  }
})

// Buscar datasets por tags
db.datasets.find({ tags: { $in: ["nlp", "sentiment"] } })

// Obtener lineage del dataset
db.datasets.aggregate([
  { $match: { name: "customer_reviews" } },
  { $sort: { version: -1 } },
  { $limit: 1 },
  { $project: {
    name: 1,
    version: 1,
    lineage: 1,
    statistics: 1
  }}
])
```

### Experiment Tracking

#### ML Experiments and Runs
```javascript
// Colección para experimentos ML
use ml_experiments

db.experiments.createIndex({ "name": 1 })
db.experiments.createIndex({ "created_at": -1 })
db.runs.createIndex({ "experiment_id": 1 })
db.runs.createIndex({ "status": 1 })
db.runs.createIndex({ "metrics.accuracy": -1 })

// Crear experimento
db.experiments.insertOne({
  _id: ObjectId("64a1b2c3d4e5f6789012345a"),
  name: "sentiment_analysis_optimization",
  description: "Optimizing sentiment analysis model performance",
  objective: "maximize_accuracy",
  created_at: new Date(),
  created_by: "ml_engineer_001",
  status: "active",
  tags: ["nlp", "optimization", "sentiment"]
})

// Registrar run de experimento
db.runs.insertOne({
  experiment_id: ObjectId("64a1b2c3d4e5f6789012345a"),
  run_id: "run_001",
  name: "rf_baseline",
  algorithm: "RandomForestClassifier",
  hyperparameters: {
    n_estimators: 100,
    max_depth: 10,
    min_samples_split: 2,
    random_state: 42
  },
  dataset: {
    name: "customer_reviews",
    version: "2.1.0",
    train_size: 100000,
    test_size: 25000
  },
  metrics: {
    accuracy: 0.87,
    precision: 0.85,
    recall: 0.89,
    f1_score: 0.87,
    auc: 0.92,
    training_time_seconds: 125.6,
    inference_time_ms: 2.3
  },
  artifacts: {
    model: "s3://experiments/run_001/model.pkl",
    plots: ["s3://experiments/run_001/confusion_matrix.png"],
    logs: "s3://experiments/run_001/training.log"
  },
  environment: {
    python_version: "3.9.7",
    packages: {
      "scikit-learn": "1.0.2",
      "pandas": "1.3.3",
      "numpy": "1.21.0"
    },
    hardware: {
      cpu_cores: 8,
      memory_gb: 32,
      gpu: null
    }
  },
  started_at: new Date(),
  finished_at: new Date(),
  duration_seconds: 156,
  status: "completed",
  notes: "Baseline model with default parameters"
})

// Buscar mejores runs por métrica
db.runs.find({
  experiment_id: ObjectId("64a1b2c3d4e5f6789012345a"),
  status: "completed"
}).sort({ "metrics.accuracy": -1 }).limit(10)

// Comparar hiperparámetros de top runs
db.runs.aggregate([
  { $match: { 
    experiment_id: ObjectId("64a1b2c3d4e5f6789012345a"),
    status: "completed"
  }},
  { $sort: { "metrics.accuracy": -1 } },
  { $limit: 5 },
  { $project: {
    run_id: 1,
    accuracy: "$metrics.accuracy",
    hyperparameters: 1,
    training_time: "$metrics.training_time_seconds"
  }}
])
```

### Real-time AI Data Processing

#### Feature Store
```javascript
// Colección para feature store
use feature_store

db.features.createIndex({ "entity_id": 1, "feature_name": 1, "timestamp": -1 })
db.features.createIndex({ "feature_group": 1 })
db.features.createIndex({ "timestamp": -1 })

// Insertar features en tiempo real
db.features.insertMany([
  {
    entity_id: "user_12345",
    feature_group: "user_behavior", 
    feature_name: "avg_session_duration",
    value: 285.6,
    timestamp: new Date(),
    metadata: {
      computation_method: "rolling_7_days",
      data_source: "user_sessions",
      version: "1.0"
    }
  },
  {
    entity_id: "user_12345",
    feature_group: "user_behavior",
    feature_name: "total_purchases_30d", 
    value: 3,
    timestamp: new Date(),
    metadata: {
      computation_method: "count",
      data_source: "purchase_events",
      version: "1.0"
    }
  }
])

// Obtener features más recientes para una entidad
db.features.aggregate([
  { $match: { entity_id: "user_12345" } },
  { $sort: { timestamp: -1 } },
  { $group: {
    _id: { 
      entity_id: "$entity_id",
      feature_name: "$feature_name"
    },
    latest_value: { $first: "$value" },
    latest_timestamp: { $first: "$timestamp" },
    feature_group: { $first: "$feature_group" }
  }},
  { $project: {
    _id: 0,
    entity_id: "$_id.entity_id",
    feature_name: "$_id.feature_name",
    value: "$latest_value",
    timestamp: "$latest_timestamp",
    feature_group: 1
  }}
])

// Feature drift detection
db.features.aggregate([
  { $match: { 
    feature_name: "avg_session_duration",
    timestamp: { $gte: new Date(Date.now() - 7*24*60*60*1000) }
  }},
  { $group: {
    _id: {
      $dateToString: { 
        format: "%Y-%m-%d",
        date: "$timestamp"
      }
    },
    avg_value: { $avg: "$value" },
    std_dev: { $stdDevPop: "$value" },
    count: { $sum: 1 }
  }},
  { $sort: { _id: 1 } }
])
```

### Model Monitoring and Analytics

#### Prediction Logging
```javascript
// Colección para logs de predicciones
use model_monitoring

db.predictions.createIndex({ "model_id": 1, "timestamp": -1 })
db.predictions.createIndex({ "prediction_id": 1 }, { unique: true })
db.predictions.createIndex({ "user_id": 1 })

// Log de predicción en tiempo real
db.predictions.insertOne({
  prediction_id: "pred_" + new Date().getTime(),
  model_id: "sentiment_classifier_v1.0.0",
  user_id: "user_67890",
  input_data: {
    text: "This product is amazing! I love it.",
    preprocessed_features: [0.1, 0.8, 0.2, -0.1, 0.9]
  },
  prediction: {
    class: "positive",
    confidence: 0.94,
    probabilities: {
      positive: 0.94,
      negative: 0.03,
      neutral: 0.03
    }
  },
  metadata: {
    request_id: "req_abc123",
    api_version: "v2",
    response_time_ms: 45,
    model_version: "1.0.0",
    feature_version: "2.1"
  },
  timestamp: new Date(),
  feedback: null  // Se actualizará cuando se reciba feedback
})

// Monitoreo de distribución de predicciones
db.predictions.aggregate([
  { $match: { 
    model_id: "sentiment_classifier_v1.0.0",
    timestamp: { $gte: new Date(Date.now() - 24*60*60*1000) }
  }},
  { $group: {
    _id: "$prediction.class",
    count: { $sum: 1 },
    avg_confidence: { $avg: "$prediction.confidence" }
  }},
  { $sort: { count: -1 } }
])

// Actualizar con feedback real
db.predictions.updateOne(
  { prediction_id: "pred_1672531200000" },
  { 
    $set: { 
      feedback: {
        actual_label: "positive",
        correct: true,
        user_rating: 5,
        feedback_timestamp: new Date()
      }
    }
  }
)

// Calcular accuracy en tiempo real
db.predictions.aggregate([
  { $match: { 
    model_id: "sentiment_classifier_v1.0.0",
    feedback: { $ne: null },
    timestamp: { $gte: new Date(Date.now() - 7*24*60*60*1000) }
  }},
  { $project: {
    correct: { $eq: ["$prediction.class", "$feedback.actual_label"] }
  }},
  { $group: {
    _id: null,
    total_predictions: { $sum: 1 },
    correct_predictions: { $sum: { $cond: ["$correct", 1, 0] } }
  }},
  { $project: {
    _id: 0,
    total_predictions: 1,
    correct_predictions: 1,
    accuracy: { $divide: ["$correct_predictions", "$total_predictions"] }
  }}
])
```

### AI/ML Configuration and Settings

#### Model Configuration Management
```javascript
// Colección para configuraciones de modelos
use model_configs

db.configs.createIndex({ "model_name": 1, "environment": 1 }, { unique: true })
db.configs.createIndex({ "updated_at": -1 })

// Configuración de modelo en producción
db.configs.insertOne({
  model_name: "recommendation_engine",
  environment: "production",
  version: "2.3.1",
  config: {
    inference: {
      batch_size: 64,
      max_latency_ms: 100,
      timeout_seconds: 30,
      retry_attempts: 3
    },
    preprocessing: {
      text_normalization: true,
      feature_scaling: "standard",
      missing_value_strategy: "median"
    },
    postprocessing: {
      confidence_threshold: 0.7,
      max_recommendations: 10,
      diversity_factor: 0.3
    },
    monitoring: {
      log_predictions: true,
      sample_rate: 0.1,
      alert_thresholds: {
        latency_ms: 200,
        error_rate: 0.05,
        confidence_drop: 0.1
      }
    }
  },
  feature_flags: {
    enable_a_b_testing: true,
    use_new_algorithm: false,
    enable_caching: true
  },
  scaling: {
    min_instances: 2,
    max_instances: 10,
    target_cpu_percent: 70,
    scale_up_cooldown: 300,
    scale_down_cooldown: 600
  },
  created_at: new Date(),
  updated_at: new Date(),
  updated_by: "ml_ops_team"
})

// Obtener configuración actual
db.configs.findOne({
  model_name: "recommendation_engine",
  environment: "production"
})

// Actualizar configuración
db.configs.updateOne(
  { 
    model_name: "recommendation_engine",
    environment: "production"
  },
  { 
    $set: { 
      "config.inference.batch_size": 128,
      "updated_at": new Date(),
      "updated_by": "performance_team"
    }
  }
)
```

### AI/ML Automation Scripts

#### Model Deployment Pipeline
```bash
#!/bin/bash
# MongoDB script para pipeline de deployment

mongosh --eval "
use ml_deployment

// Registrar nuevo deployment
db.deployments.insertOne({
  model_name: 'sentiment_classifier',
  version: '1.2.0',
  environment: 'staging',
  deployment_id: 'deploy_' + new Date().getTime(),
  artifacts: {
    model_file: 's3://models/sentiment_v1.2.0/model.pkl',
    config_file: 's3://models/sentiment_v1.2.0/config.json',
    requirements: 's3://models/sentiment_v1.2.0/requirements.txt'
  },
  health_checks: {
    model_load: false,
    prediction_test: false,
    performance_test: false
  },
  metrics: {
    deployment_time: null,
    first_prediction_latency: null,
    memory_usage_mb: null
  },
  status: 'deploying',
  started_at: new Date(),
  started_by: 'deployment_pipeline'
})

print('Deployment registered in MongoDB')
"

# Actualizar estado después de health checks
mongosh --eval "
use ml_deployment

db.deployments.updateOne(
  { 
    model_name: 'sentiment_classifier',
    version: '1.2.0',
    environment: 'staging',
    status: 'deploying'
  },
  {
    \$set: {
      'health_checks.model_load': true,
      'health_checks.prediction_test': true,
      'health_checks.performance_test': true,
      'metrics.deployment_time': 45.2,
      'metrics.first_prediction_latency': 23.1,
      'metrics.memory_usage_mb': 512,
      status: 'active',
      completed_at: new Date()
    }
  }
)

print('Deployment completed and updated in MongoDB')
"
```
