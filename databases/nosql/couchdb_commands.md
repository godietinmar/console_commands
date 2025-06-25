# Comandos CouchDB

Este archivo contiene una lista de comandos para Apache CouchDB usando curl, línea de comandos y herramientas administrativas, organizados por categoría.

## Introducción a CouchDB

CouchDB es una base de datos NoSQL orientada a documentos que utiliza HTTP REST API para todas las operaciones. Los comandos se ejecutan principalmente a través de HTTP usando herramientas como curl.

**URL base:** `http://localhost:5984`
**Puerto por defecto:** 5984
**Interfaz web:** Fauxton en `http://localhost:5984/_utils`

## Herramientas de Línea de Comandos

### curl (Cliente HTTP principal)

**Descripción:**  
CouchDB utiliza HTTP REST API, por lo que curl es la herramienta principal para interactuar desde línea de comandos.

**Sintaxis básica:**
```bash
curl [opciones] URL
```

**Opciones comunes:**
- `-X`: Método HTTP (GET, POST, PUT, DELETE)
- `-H`: Headers HTTP
- `-d`: Datos a enviar
- `-u`: Autenticación usuario:contraseña
- `-v`: Modo verbose
- `-s`: Modo silencioso
- `-i`: Incluir headers de respuesta
- `-L`: Seguir redirecciones

**Ejemplos básicos:**
```bash
# Verificar si CouchDB está ejecutándose
curl http://localhost:5984

# Con autenticación
curl -u admin:contraseña http://localhost:5984

# Información del servidor
curl http://localhost:5984/_all_dbs

# Crear base de datos
curl -X PUT http://localhost:5984/mi_base_datos

# Eliminar base de datos
curl -X DELETE http://localhost:5984/mi_base_datos
```

### couchdb-dump / couchdb-load

**Descripción:**  
Herramientas de terceros para backup y restore.

**Instalación:**
```bash
npm install -g couchdb-dump
```

**Ejemplos:**
```bash
# Backup de base de datos
couchdb-dump -h localhost -d mi_base_datos > backup.json

# Restore de base de datos
cat backup.json | couchdb-load -h localhost -d nueva_base_datos
```

## Comandos Básicos de CouchDB

### Información del Servidor

```bash
# Información general del servidor
curl http://localhost:5984

# Listar todas las bases de datos
curl http://localhost:5984/_all_dbs

# Información de configuración
curl http://localhost:5984/_config

# Estadísticas del servidor
curl http://localhost:5984/_stats

# Información de nodos activos
curl http://localhost:5984/_membership

# Logs del servidor
curl http://localhost:5984/_log

# UUIDs únicos
curl http://localhost:5984/_uuids
curl http://localhost:5984/_uuids?count=10
```

### Gestión de Bases de Datos

```bash
# Crear base de datos
curl -X PUT http://localhost:5984/mi_base_datos

# Información de base de datos
curl http://localhost:5984/mi_base_datos

# Eliminar base de datos
curl -X DELETE http://localhost:5984/mi_base_datos

# Verificar si existe base de datos
curl -I http://localhost:5984/mi_base_datos

# Compactar base de datos
curl -X POST http://localhost:5984/mi_base_datos/_compact \
     -H "Content-Type: application/json"

# Información de seguridad
curl http://localhost:5984/mi_base_datos/_security

# Configurar seguridad
curl -X PUT http://localhost:5984/mi_base_datos/_security \
     -H "Content-Type: application/json" \
     -d '{
       "admins": {
         "names": ["admin"],
         "roles": ["admin_role"]
       },
       "members": {
         "names": ["user1"],
         "roles": ["user_role"]
       }
     }'
```

## Operaciones CRUD con Documentos

### Crear Documentos

```bash
# Crear documento con ID automático
curl -X POST http://localhost:5984/mi_base_datos \
     -H "Content-Type: application/json" \
     -d '{
       "nombre": "Juan Pérez",
       "edad": 30,
       "email": "juan@example.com",
       "activo": true
     }'

# Crear documento con ID específico
curl -X PUT http://localhost:5984/mi_base_datos/usuario_001 \
     -H "Content-Type: application/json" \
     -d '{
       "nombre": "Ana García",
       "edad": 25,
       "email": "ana@example.com",
       "activo": true
     }'

# Crear documento con adjuntos
curl -X PUT http://localhost:5984/mi_base_datos/doc_con_adjunto \
     -H "Content-Type: application/json" \
     -d '{
       "titulo": "Documento con imagen",
       "_attachments": {
         "image.png": {
           "content_type": "image/png",
           "data": "iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVR42mP8/5+hHgAHggJ/PchI7wAAAABJRU5ErkJggg=="
         }
       }
     }'
```

### Leer Documentos

```bash
# Obtener documento por ID
curl http://localhost:5984/mi_base_datos/usuario_001

# Obtener con información de revisión
curl http://localhost:5984/mi_base_datos/usuario_001?revs_info=true

# Obtener revisión específica
curl http://localhost:5984/mi_base_datos/usuario_001?rev=1-967a00dff5e02add41819138abb3284d

# Obtener solo headers (verificar existencia)
curl -I http://localhost:5984/mi_base_datos/usuario_001

# Obtener múltiples documentos
curl -X POST http://localhost:5984/mi_base_datos/_all_docs \
     -H "Content-Type: application/json" \
     -d '{
       "keys": ["usuario_001", "usuario_002", "usuario_003"]
     }'

# Obtener documentos con contenido
curl -X POST http://localhost:5984/mi_base_datos/_all_docs?include_docs=true \
     -H "Content-Type: application/json" \
     -d '{
       "keys": ["usuario_001", "usuario_002"]
     }'

# Listar todos los documentos
curl http://localhost:5984/mi_base_datos/_all_docs

# Listar con contenido de documentos
curl http://localhost:5984/mi_base_datos/_all_docs?include_docs=true

# Paginar resultados
curl "http://localhost:5984/mi_base_datos/_all_docs?limit=10&skip=20"

# Obtener adjunto
curl http://localhost:5984/mi_base_datos/doc_con_adjunto/image.png
```

### Actualizar Documentos

```bash
# Actualizar documento (requiere revision _rev)
curl -X PUT http://localhost:5984/mi_base_datos/usuario_001 \
     -H "Content-Type: application/json" \
     -d '{
       "_rev": "1-967a00dff5e02add41819138abb3284d",
       "nombre": "Juan Carlos Pérez",
       "edad": 31,
       "email": "juan.carlos@example.com",
       "activo": true,
       "telefono": "123-456-7890"
     }'

# Actualización parcial usando función de actualización (si está definida)
curl -X POST http://localhost:5984/mi_base_datos/_design/updates/_update/campo/usuario_001 \
     -H "Content-Type: application/json" \
     -d '{"campo": "telefono", "valor": "987-654-3210"}'
```

### Eliminar Documentos

```bash
# Eliminar documento (requiere revision _rev)
curl -X DELETE http://localhost:5984/mi_base_datos/usuario_001?rev=2-967a00dff5e02add41819138abb3284d

# Verificar eliminación
curl http://localhost:5984/mi_base_datos/usuario_001
```

## Vistas (Views) y Design Documents

### Crear Design Documents con Vistas

```bash
# Crear design document con vista map
curl -X PUT http://localhost:5984/mi_base_datos/_design/usuarios \
     -H "Content-Type: application/json" \
     -d '{
       "views": {
         "por_edad": {
           "map": "function(doc) { if (doc.edad) { emit(doc.edad, doc.nombre); } }"
         },
         "activos": {
           "map": "function(doc) { if (doc.activo === true) { emit(doc._id, doc); } }"
         },
         "por_email": {
           "map": "function(doc) { if (doc.email) { emit(doc.email, doc); } }"
         }
       }
     }'

# Vista con función reduce
curl -X PUT http://localhost:5984/mi_base_datos/_design/estadisticas \
     -H "Content-Type: application/json" \
     -d '{
       "views": {
         "edad_promedio": {
           "map": "function(doc) { if (doc.edad) { emit(doc._id, doc.edad); } }",
           "reduce": "function(keys, values) { return sum(values) / values.length; }"
         },
         "total_por_activo": {
           "map": "function(doc) { emit(doc.activo, 1); }",
           "reduce": "_count"
         }
       }
     }'
```

### Consultar Vistas

```bash
# Consultar vista básica
curl http://localhost:5984/mi_base_datos/_design/usuarios/_view/por_edad

# Vista con parámetros
curl "http://localhost:5984/mi_base_datos/_design/usuarios/_view/por_edad?startkey=25&endkey=35"

# Vista con inclusión de documentos
curl "http://localhost:5984/mi_base_datos/_design/usuarios/_view/activos?include_docs=true"

# Vista con límite y salto
curl "http://localhost:5984/mi_base_datos/_design/usuarios/_view/por_edad?limit=10&skip=5"

# Vista en orden descendente
curl "http://localhost:5984/mi_base_datos/_design/usuarios/_view/por_edad?descending=true"

# Vista con clave específica
curl "http://localhost:5984/mi_base_datos/_design/usuarios/_view/por_email?key=\"juan@example.com\""

# Vista con múltiples claves
curl -X POST http://localhost:5984/mi_base_datos/_design/usuarios/_view/por_edad \
     -H "Content-Type: application/json" \
     -d '{
       "keys": [25, 30, 35]
     }'

# Vista con reduce
curl http://localhost:5984/mi_base_datos/_design/estadisticas/_view/edad_promedio

# Vista sin reduce (group_level=0)
curl "http://localhost:5984/mi_base_datos/_design/estadisticas/_view/total_por_activo?group=true"
```

## Índices y Consultas

### Índices Mango (CouchDB 2.0+)

```bash
# Crear índice simple
curl -X POST http://localhost:5984/mi_base_datos/_index \
     -H "Content-Type: application/json" \
     -d '{
       "index": {
         "fields": ["edad"]
       },
       "name": "edad-index",
       "type": "json"
     }'

# Crear índice compuesto
curl -X POST http://localhost:5984/mi_base_datos/_index \
     -H "Content-Type: application/json" \
     -d '{
       "index": {
         "fields": ["activo", "edad"]
       },
       "name": "activo-edad-index"
     }'

# Crear índice de texto completo
curl -X POST http://localhost:5984/mi_base_datos/_index \
     -H "Content-Type: application/json" \
     -d '{
       "index": {
         "fields": [
           {"name": "nombre", "type": "string"},
           {"name": "email", "type": "string"}
         ]
       },
       "name": "texto-index",
       "type": "text"
     }'

# Listar índices
curl http://localhost:5984/mi_base_datos/_index
```

### Consultas Mango

```bash
# Consulta simple
curl -X POST http://localhost:5984/mi_base_datos/_find \
     -H "Content-Type: application/json" \
     -d '{
       "selector": {
         "edad": {"$gt": 25}
       }
     }'

# Consulta con múltiples condiciones
curl -X POST http://localhost:5984/mi_base_datos/_find \
     -H "Content-Type: application/json" \
     -d '{
       "selector": {
         "activo": true,
         "edad": {"$gte": 18, "$lt": 65}
       },
       "fields": ["nombre", "edad", "email"],
       "sort": [{"edad": "asc"}],
       "limit": 10
     }'

# Consulta con operadores lógicos
curl -X POST http://localhost:5984/mi_base_datos/_find \
     -H "Content-Type: application/json" \
     -d '{
       "selector": {
         "$or": [
           {"edad": {"$lt": 18}},
           {"edad": {"$gt": 65}}
         ]
       }
     }'

# Consulta de texto completo
curl -X POST http://localhost:5984/mi_base_datos/_find \
     -H "Content-Type: application/json" \
     -d '{
       "selector": {
         "$text": "juan garcia"
       },
       "fields": ["nombre", "email"]
     }'

# Explicar plan de consulta
curl -X POST http://localhost:5984/mi_base_datos/_explain \
     -H "Content-Type: application/json" \
     -d '{
       "selector": {
         "edad": {"$gt": 25}
       }
     }'
```

## Replicación

### Configurar Replicación

```bash
# Replicación continua
curl -X POST http://localhost:5984/_replicate \
     -H "Content-Type: application/json" \
     -d '{
       "source": "mi_base_datos",
       "target": "http://servidor2:5984/mi_base_datos_replica",
       "continuous": true
     }'

# Replicación con filtro
curl -X POST http://localhost:5984/_replicate \
     -H "Content-Type: application/json" \
     -d '{
       "source": "mi_base_datos",
       "target": "mi_base_datos_filtrada",
       "filter": "usuarios/solo_activos",
       "continuous": true
     }'

# Replicación con autenticación
curl -X POST http://localhost:5984/_replicate \
     -H "Content-Type: application/json" \
     -d '{
       "source": {
         "url": "http://servidor1:5984/mi_base_datos",
         "auth": {
           "basic": {
             "username": "user1",
             "password": "pass1"
           }
         }
       },
       "target": "mi_base_datos_local"
     }'

# Estado de replicación
curl http://localhost:5984/_active_tasks

# Cancelar replicación
curl -X POST http://localhost:5984/_replicate \
     -H "Content-Type: application/json" \
     -d '{
       "source": "mi_base_datos",
       "target": "mi_base_datos_replica",
       "cancel": true
     }'
```

### Replicación Programada

```bash
# Crear documento de replicación en _replicator
curl -X PUT http://localhost:5984/_replicator/mi_replicacion \
     -H "Content-Type: application/json" \
     -d '{
       "source": "mi_base_datos",
       "target": "http://servidor2:5984/mi_base_datos_replica",
       "continuous": true,
       "owner": "admin"
     }'

# Listar replicaciones
curl http://localhost:5984/_replicator/_all_docs?include_docs=true

# Eliminar replicación
curl -X DELETE http://localhost:5984/_replicator/mi_replicacion?rev=1-abc123
```

## Administración y Configuración

### Gestión de Usuarios

```bash
# Crear usuario administrador
curl -X PUT http://localhost:5984/_config/admins/admin \
     -d '"contraseña_segura"'

# Crear usuario normal
curl -X PUT http://localhost:5984/_users/org.couchdb.user:usuario1 \
     -H "Content-Type: application/json" \
     -d '{
       "name": "usuario1",
       "password": "contraseña123",
       "roles": ["usuario"],
       "type": "user"
     }'

# Cambiar contraseña
curl -X PUT http://localhost:5984/_users/org.couchdb.user:usuario1 \
     -H "Content-Type: application/json" \
     -d '{
       "_rev": "1-abc123...",
       "name": "usuario1",
       "password": "nueva_contraseña",
       "roles": ["usuario"],
       "type": "user"
     }'

# Información de sesión actual
curl http://localhost:5984/_session

# Login
curl -X POST http://localhost:5984/_session \
     -H "Content-Type: application/json" \
     -d '{
       "name": "admin",
       "password": "contraseña"
     }'

# Logout
curl -X DELETE http://localhost:5984/_session
```

### Configuración del Servidor

```bash
# Ver configuración completa
curl http://localhost:5984/_config

# Ver sección específica
curl http://localhost:5984/_config/httpd

# Cambiar configuración
curl -X PUT http://localhost:5984/_config/httpd/max_connections \
     -d '"2048"'

# Configuraciones comunes
curl -X PUT http://localhost:5984/_config/query_servers/javascript \
     -d '"/usr/bin/couchjs /usr/share/couchdb/server/main.js"'

curl -X PUT http://localhost:5984/_config/couchdb/max_document_size \
     -d '"4294967296"'  # 4GB

curl -X PUT http://localhost:5984/_config/httpd/timeout \
     -d '"300000"'  # 5 minutos
```

## Backup y Restore

### Backup Manual

```bash
# Backup de base de datos completa
curl http://localhost:5984/mi_base_datos/_all_docs?include_docs=true > backup_mi_base_datos.json

# Backup de documentos específicos
curl -X POST http://localhost:5984/mi_base_datos/_all_docs?include_docs=true \
     -H "Content-Type: application/json" \
     -d '{
       "keys": ["doc1", "doc2", "doc3"]
     }' > backup_parcial.json

# Backup de design documents
curl http://localhost:5984/mi_base_datos/_all_docs?include_docs=true&startkey="_design/"&endkey="_design0" > backup_design_docs.json
```

### Restore Manual

```bash
# Restore usando bulk insert
# Primero procesar el JSON para formato bulk
cat backup_mi_base_datos.json | jq '{docs: [.rows[].doc]}' > bulk_docs.json

curl -X POST http://localhost:5984/nueva_base_datos/_bulk_docs \
     -H "Content-Type: application/json" \
     -d @bulk_docs.json
```

## Monitoreo y Estadísticas

### Estadísticas del Servidor

```bash
# Estadísticas generales
curl http://localhost:5984/_stats

# Estadísticas específicas
curl http://localhost:5984/_stats/couchdb/request_time
curl http://localhost:5984/_stats/httpd/requests
curl http://localhost:5984/_stats/couchdb/database_writes

# Tareas activas
curl http://localhost:5984/_active_tasks

# Información de nodos (cluster)
curl http://localhost:5984/_membership
curl http://localhost:5984/_cluster_setup
```

### Logs y Debugging

```bash
# Ver logs
curl http://localhost:5984/_log

# Logs con filtro de nivel
curl "http://localhost:5984/_log?level=error"

# Logs recientes
curl "http://localhost:5984/_log?bytes=1024"
```

## Scripts de Utilidad

### Script de Backup Automatizado

```bash
#!/bin/bash
# backup_couchdb.sh

COUCHDB_URL="http://localhost:5984"
BACKUP_DIR="/backups/couchdb"
DATE=$(date +%Y%m%d_%H%M%S)
USERNAME="admin"
PASSWORD="contraseña"

mkdir -p $BACKUP_DIR

# Obtener lista de bases de datos
DBS=$(curl -s -u $USERNAME:$PASSWORD $COUCHDB_URL/_all_dbs | jq -r '.[]' | grep -v '^_')

for db in $DBS; do
    echo "Backing up database: $db"
    
    # Backup de documentos
    curl -s -u $USERNAME:$PASSWORD \
         $COUCHDB_URL/$db/_all_docs?include_docs=true \
         > $BACKUP_DIR/${db}_${DATE}.json
    
    # Backup de design documents
    curl -s -u $USERNAME:$PASSWORD \
         "$COUCHDB_URL/$db/_all_docs?include_docs=true&startkey=\"_design/\"&endkey=\"_design0\"" \
         > $BACKUP_DIR/${db}_design_${DATE}.json
done

# Comprimir backups
tar -czf $BACKUP_DIR/couchdb_backup_${DATE}.tar.gz $BACKUP_DIR/*_${DATE}.json

# Limpiar archivos JSON
rm $BACKUP_DIR/*_${DATE}.json

echo "Backup completado: couchdb_backup_${DATE}.tar.gz"
```

### Script de Monitoreo

```bash
#!/bin/bash
# monitor_couchdb.sh

COUCHDB_URL="http://localhost:5984"

echo "=== MONITOREO COUCHDB ==="
echo "Fecha: $(date)"

echo -e "\n--- INFORMACIÓN GENERAL ---"
curl -s $COUCHDB_URL | jq '.'

echo -e "\n--- BASES DE DATOS ---"
curl -s $COUCHDB_URL/_all_dbs | jq -r '.[]'

echo -e "\n--- ESTADÍSTICAS ---"
curl -s $COUCHDB_URL/_stats | jq '{
  request_time: .couchdb.request_time.current,
  database_reads: .couchdb.database_reads.current,
  database_writes: .couchdb.database_writes.current,
  http_requests: .httpd.requests.current
}'

echo -e "\n--- TAREAS ACTIVAS ---"
curl -s $COUCHDB_URL/_active_tasks | jq '.'

echo -e "\n--- INFORMACIÓN DE MEMORIA ---"
curl -s $COUCHDB_URL/_stats/couchdb/open_databases | jq '.current'
```

### Script de Mantenimiento

```bash
#!/bin/bash
# maintenance_couchdb.sh

COUCHDB_URL="http://localhost:5984"
USERNAME="admin"
PASSWORD="contraseña"

echo "Iniciando mantenimiento de CouchDB..."

# Obtener lista de bases de datos
DBS=$(curl -s -u $USERNAME:$PASSWORD $COUCHDB_URL/_all_dbs | jq -r '.[]' | grep -v '^_')

for db in $DBS; do
    echo "Compactando base de datos: $db"
    
    # Compactar base de datos
    curl -X POST -u $USERNAME:$PASSWORD \
         $COUCHDB_URL/$db/_compact \
         -H "Content-Type: application/json"
    
    # Compactar vistas
    DESIGN_DOCS=$(curl -s -u $USERNAME:$PASSWORD \
                  "$COUCHDB_URL/$db/_all_docs?startkey=\"_design/\"&endkey=\"_design0\"" | \
                  jq -r '.rows[].id' | sed 's/_design\///')
    
    for design_doc in $DESIGN_DOCS; do
        echo "Compactando vistas: $design_doc"
        curl -X POST -u $USERNAME:$PASSWORD \
             $COUCHDB_URL/$db/_compact/$design_doc \
             -H "Content-Type: application/json"
    done
done

echo "Mantenimiento completado."
```

## Ejemplos de Uso Común

### Blog con Comentarios

```bash
# Crear base de datos
curl -X PUT http://localhost:5984/blog

# Crear post
curl -X PUT http://localhost:5984/blog/post_001 \
     -H "Content-Type: application/json" \
     -d '{
       "tipo": "post",
       "titulo": "Mi primer post",
       "contenido": "Este es el contenido del post...",
       "autor": "Juan Pérez",
       "fecha": "2024-01-01T10:00:00Z",
       "tags": ["tutorial", "couchdb"],
       "publicado": true
     }'

# Crear comentario
curl -X PUT http://localhost:5984/blog/comment_001 \
     -H "Content-Type: application/json" \
     -d '{
       "tipo": "comentario",
       "post_id": "post_001",
       "autor": "Ana García",
       "comentario": "Excelente post!",
       "fecha": "2024-01-01T11:00:00Z"
     }'

# Vista para posts publicados
curl -X PUT http://localhost:5984/blog/_design/blog \
     -H "Content-Type: application/json" \
     -d '{
       "views": {
         "posts_publicados": {
           "map": "function(doc) { if (doc.tipo === \"post\" && doc.publicado) { emit(doc.fecha, doc); } }"
         },
         "comentarios_por_post": {
           "map": "function(doc) { if (doc.tipo === \"comentario\") { emit(doc.post_id, doc); } }"
         }
       }
     }'

# Consultar posts publicados
curl "http://localhost:5984/blog/_design/blog/_view/posts_publicados?descending=true"

# Consultar comentarios de un post
curl "http://localhost:5984/blog/_design/blog/_view/comentarios_por_post?key=\"post_001\""
```

### Sistema de Inventario

```bash
# Crear base de datos
curl -X PUT http://localhost:5984/inventario

# Crear producto
curl -X PUT http://localhost:5984/inventario/producto_001 \
     -H "Content-Type: application/json" \
     -d '{
       "tipo": "producto",
       "nombre": "Laptop Gaming",
       "categoria": "electrónica",
       "precio": 1299.99,
       "stock": 10,
       "especificaciones": {
         "marca": "Dell",
         "modelo": "G5",
         "ram": "16GB",
         "storage": "512GB SSD"
       },
       "fecha_creacion": "2024-01-01T00:00:00Z"
     }'

# Crear movimiento de stock
curl -X POST http://localhost:5984/inventario \
     -H "Content-Type: application/json" \
     -d '{
       "tipo": "movimiento",
       "producto_id": "producto_001",
       "tipo_movimiento": "venta",
       "cantidad": -1,
       "fecha": "2024-01-01T12:00:00Z",
       "usuario": "vendedor1"
     }'

# Vista para productos por categoría
curl -X PUT http://localhost:5984/inventario/_design/inventario \
     -H "Content-Type: application/json" \
     -d '{
       "views": {
         "productos_por_categoria": {
           "map": "function(doc) { if (doc.tipo === \"producto\") { emit(doc.categoria, doc); } }"
         },
         "movimientos_por_producto": {
           "map": "function(doc) { if (doc.tipo === \"movimiento\") { emit(doc.producto_id, doc); } }"
         },
         "stock_actual": {
           "map": "function(doc) { if (doc.tipo === \"producto\") { emit(doc._id, doc.stock); } else if (doc.tipo === \"movimiento\") { emit(doc.producto_id, doc.cantidad); } }",
           "reduce": "function(keys, values) { return sum(values); }"
         }
       }
     }'
```

### Sistema de Usuarios y Sesiones

```bash
# Crear base de datos
curl -X PUT http://localhost:5984/usuarios

# Crear usuario
curl -X PUT http://localhost:5984/usuarios/user_001 \
     -H "Content-Type: application/json" \
     -d '{
       "tipo": "usuario",
       "username": "juan.perez",
       "email": "juan@example.com",
       "perfil": {
         "nombre": "Juan Pérez",
         "edad": 30,
         "ciudad": "Madrid"
       },
       "activo": true,
       "fecha_registro": "2024-01-01T00:00:00Z"
     }'

# Crear sesión
curl -X POST http://localhost:5984/usuarios \
     -H "Content-Type: application/json" \
     -d '{
       "tipo": "sesion",
       "usuario_id": "user_001",
       "session_id": "sess_abc123",
       "ip": "192.168.1.100",
       "user_agent": "Mozilla/5.0...",
       "inicio": "2024-01-01T10:00:00Z",
       "ultimo_acceso": "2024-01-01T10:00:00Z",
       "activa": true
     }'

# Vista para usuarios activos
curl -X PUT http://localhost:5984/usuarios/_design/usuarios \
     -H "Content-Type: application/json" \
     -d '{
       "views": {
         "usuarios_activos": {
           "map": "function(doc) { if (doc.tipo === \"usuario\" && doc.activo) { emit(doc.username, doc); } }"
         },
         "sesiones_activas": {
           "map": "function(doc) { if (doc.tipo === \"sesion\" && doc.activa) { emit(doc.usuario_id, doc); } }"
         }
       }
     }'
```
