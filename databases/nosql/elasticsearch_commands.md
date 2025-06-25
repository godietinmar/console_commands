# Comandos Elasticsearch

Este archivo contiene una lista de comandos para Elasticsearch usando curl, herramientas de línea de comandos y APIs REST, organizados por categoría.

## Herramientas de Línea de Comandos

### curl (Cliente HTTP)

**Descripción:**  
Herramienta principal para interactuar con la API REST de Elasticsearch.

**Sintaxis básica:**
```bash
curl -X [MÉTODO] "http://localhost:9200/[endpoint]" -H "Content-Type: application/json" -d '[datos]'
```

**Opciones comunes:**
- `-X`: Método HTTP (GET, POST, PUT, DELETE)
- `-H`: Headers HTTP
- `-d`: Datos del cuerpo de la request
- `-s`: Modo silencioso
- `-i`: Incluir headers de respuesta
- `-u`: Autenticación básica
- `--cacert`: Certificado CA para HTTPS

### Elasticsearch APIs

```bash
# Variables de entorno útiles
export ES_HOST="localhost:9200"
export ES_USER="elastic"
export ES_PASS="password"

# Para cluster con autenticación
alias escurl='curl -u $ES_USER:$ES_PASS -H "Content-Type: application/json"'

# Para cluster sin autenticación
alias escurl='curl -H "Content-Type: application/json"'
```

### Kibana Dev Tools

```json
// Sintaxis en Kibana Dev Tools (sin curl)
GET /_cluster/health
POST /mi_indice/_doc
{
  "campo": "valor"
}
```

## Información del Cluster

### Estado del Cluster

```bash
# Estado general del cluster
curl -X GET "localhost:9200/_cluster/health?pretty"

# Estado detallado con métricas
curl -X GET "localhost:9200/_cluster/health?level=indices&pretty"

# Información básica del cluster
curl -X GET "localhost:9200/?pretty"

# Estadísticas del cluster
curl -X GET "localhost:9200/_cluster/stats?pretty"

# Configuración del cluster
curl -X GET "localhost:9200/_cluster/settings?pretty"

# Estado de los nodos
curl -X GET "localhost:9200/_nodes?pretty"

# Estadísticas de nodos específicas
curl -X GET "localhost:9200/_nodes/stats?pretty"

# Información de tareas en ejecución
curl -X GET "localhost:9200/_tasks?pretty"

# Información de shards
curl -X GET "localhost:9200/_cat/shards?v"
```

### Información de Nodos

```bash
# Listar todos los nodos
curl -X GET "localhost:9200/_cat/nodes?v"

# Información detallada de nodos
curl -X GET "localhost:9200/_nodes/stats/indices,os,process,jvm,transport,http,fs,thread_pool?pretty"

# Información de un nodo específico
curl -X GET "localhost:9200/_nodes/node-1?pretty"

# Uso de memoria por nodo
curl -X GET "localhost:9200/_cat/nodes?v&h=name,heap.percent,ram.percent,cpu,load_1m,load_5m,load_15m"

# Información de plugins instalados
curl -X GET "localhost:9200/_nodes/plugins?pretty"
```

## Gestión de Índices

### Crear Índices

```bash
# Crear índice básico
curl -X PUT "localhost:9200/mi_indice?pretty"

# Crear índice con configuración específica
curl -X PUT "localhost:9200/productos?pretty" -H 'Content-Type: application/json' -d'
{
  "settings": {
    "number_of_shards": 3,
    "number_of_replicas": 1,
    "refresh_interval": "30s"
  }
}'

# Crear índice con mapping
curl -X PUT "localhost:9200/usuarios?pretty" -H 'Content-Type: application/json' -d'
{
  "settings": {
    "number_of_shards": 1,
    "number_of_replicas": 0
  },
  "mappings": {
    "properties": {
      "nombre": {
        "type": "text",
        "analyzer": "standard"
      },
      "email": {
        "type": "keyword"
      },
      "edad": {
        "type": "integer"
      },
      "fecha_registro": {
        "type": "date",
        "format": "yyyy-MM-dd||yyyy-MM-dd HH:mm:ss"
      },
      "activo": {
        "type": "boolean"
      },
      "direccion": {
        "type": "nested",
        "properties": {
          "calle": {"type": "text"},
          "ciudad": {"type": "keyword"},
          "codigo_postal": {"type": "keyword"}
        }
      }
    }
  }
}'

# Crear índice con analizadores personalizados
curl -X PUT "localhost:9200/documentos?pretty" -H 'Content-Type: application/json' -d'
{
  "settings": {
    "analysis": {
      "analyzer": {
        "mi_analizador": {
          "type": "custom",
          "tokenizer": "standard",
          "filter": ["lowercase", "asciifolding", "stop"]
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "titulo": {
        "type": "text",
        "analyzer": "mi_analizador"
      },
      "contenido": {
        "type": "text",
        "analyzer": "mi_analizador"
      }
    }
  }
}'

# Crear índice con template
curl -X PUT "localhost:9200/_template/logs_template?pretty" -H 'Content-Type: application/json' -d'
{
  "index_patterns": ["logs-*"],
  "settings": {
    "number_of_shards": 1,
    "number_of_replicas": 0
  },
  "mappings": {
    "properties": {
      "timestamp": {"type": "date"},
      "level": {"type": "keyword"},
      "message": {"type": "text"},
      "host": {"type": "keyword"}
    }
  }
}'
```

### Información de Índices

```bash
# Listar todos los índices
curl -X GET "localhost:9200/_cat/indices?v"

# Información detallada de índices
curl -X GET "localhost:9200/_cat/indices?v&s=store.size:desc"

# Información de un índice específico
curl -X GET "localhost:9200/usuarios?pretty"

# Mapping de un índice
curl -X GET "localhost:9200/usuarios/_mapping?pretty"

# Settings de un índice
curl -X GET "localhost:9200/usuarios/_settings?pretty"

# Estadísticas de índices
curl -X GET "localhost:9200/usuarios/_stats?pretty"

# Contar documentos en índice
curl -X GET "localhost:9200/usuarios/_count?pretty"

# Tamaño de índices
curl -X GET "localhost:9200/_cat/indices?v&h=index,docs.count,store.size,pri.store.size"

# Información de shards por índice
curl -X GET "localhost:9200/_cat/shards/usuarios?v"
```

### Modificar Índices

```bash
# Actualizar settings de índice
curl -X PUT "localhost:9200/usuarios/_settings?pretty" -H 'Content-Type: application/json' -d'
{
  "index": {
    "refresh_interval": "10s",
    "number_of_replicas": 2
  }
}'

# Agregar mapping a índice existente
curl -X PUT "localhost:9200/usuarios/_mapping?pretty" -H 'Content-Type: application/json' -d'
{
  "properties": {
    "telefono": {
      "type": "keyword"
    },
    "skills": {
      "type": "text",
      "analyzer": "standard"
    }
  }
}'

# Cerrar índice
curl -X POST "localhost:9200/usuarios/_close?pretty"

# Abrir índice
curl -X POST "localhost:9200/usuarios/_open?pretty"

# Refresh manual de índice
curl -X POST "localhost:9200/usuarios/_refresh?pretty"

# Flush índice
curl -X POST "localhost:9200/usuarios/_flush?pretty"

# Optimizar índice (force merge)
curl -X POST "localhost:9200/usuarios/_forcemerge?max_num_segments=1&pretty"
```

### Eliminar Índices

```bash
# Eliminar índice específico
curl -X DELETE "localhost:9200/usuarios?pretty"

# Eliminar múltiples índices
curl -X DELETE "localhost:9200/logs-2023-*?pretty"

# Eliminar índices con patrón
curl -X DELETE "localhost:9200/temp_*?pretty"

# Verificar antes de eliminar
curl -X GET "localhost:9200/_cat/indices/logs-2023-*?v"
```

## Operaciones CRUD

### Crear Documentos (Index)

```bash
# Insertar documento con ID específico
curl -X PUT "localhost:9200/usuarios/_doc/1?pretty" -H 'Content-Type: application/json' -d'
{
  "nombre": "Juan Pérez",
  "email": "juan@example.com",
  "edad": 30,
  "fecha_registro": "2024-01-01",
  "activo": true,
  "direccion": {
    "calle": "Calle Mayor 123",
    "ciudad": "Madrid",
    "codigo_postal": "28001"
  },
  "tags": ["cliente", "premium"]
}'

# Insertar documento con ID autogenerado
curl -X POST "localhost:9200/usuarios/_doc?pretty" -H 'Content-Type: application/json' -d'
{
  "nombre": "Ana García",
  "email": "ana@example.com",
  "edad": 25,
  "fecha_registro": "2024-01-02",
  "activo": true
}'

# Insertar múltiples documentos (bulk)
curl -X POST "localhost:9200/_bulk?pretty" -H 'Content-Type: application/json' -d'
{"index":{"_index":"usuarios","_id":"2"}}
{"nombre":"Luis Rodríguez","email":"luis@example.com","edad":35,"activo":true}
{"index":{"_index":"usuarios","_id":"3"}}
{"nombre":"María López","email":"maria@example.com","edad":28,"activo":false}
{"index":{"_index":"productos","_id":"1"}}
{"nombre":"Laptop Gaming","categoria":"electrónica","precio":1299.99,"stock":15}
'

# Insertar solo si no existe
curl -X PUT "localhost:9200/usuarios/_create/4?pretty" -H 'Content-Type: application/json' -d'
{
  "nombre": "Carlos Sánchez",
  "email": "carlos@example.com",
  "edad": 32,
  "activo": true
}'

# Bulk insert desde archivo
echo '{"index":{"_index":"logs","_id":"1"}}
{"timestamp":"2024-01-01T10:00:00","level":"INFO","message":"Aplicación iniciada","host":"server1"}
{"index":{"_index":"logs","_id":"2"}}
{"timestamp":"2024-01-01T10:01:00","level":"ERROR","message":"Error de conexión","host":"server1"}' > bulk_data.json

curl -X POST "localhost:9200/_bulk?pretty" -H 'Content-Type: application/json' --data-binary @bulk_data.json
```

### Leer Documentos (Get)

```bash
# Obtener documento por ID
curl -X GET "localhost:9200/usuarios/_doc/1?pretty"

# Obtener solo ciertos campos
curl -X GET "localhost:9200/usuarios/_doc/1?_source=nombre,email&pretty"

# Obtener múltiples documentos
curl -X GET "localhost:9200/_mget?pretty" -H 'Content-Type: application/json' -d'
{
  "docs": [
    {"_index": "usuarios", "_id": "1"},
    {"_index": "usuarios", "_id": "2"},
    {"_index": "productos", "_id": "1"}
  ]
}'

# Verificar si documento existe
curl -I "localhost:9200/usuarios/_doc/1"

# Obtener versión específica
curl -X GET "localhost:9200/usuarios/_doc/1?version=2&pretty"

# Obtener documento con routing
curl -X GET "localhost:9200/usuarios/_doc/1?routing=user_group_1&pretty"
```

### Actualizar Documentos (Update)

```bash
# Actualizar campos específicos
curl -X POST "localhost:9200/usuarios/_update/1?pretty" -H 'Content-Type: application/json' -d'
{
  "doc": {
    "edad": 31,
    "telefono": "+34 666 777 888"
  }
}'

# Actualizar con script
curl -X POST "localhost:9200/usuarios/_update/1?pretty" -H 'Content-Type: application/json' -d'
{
  "script": {
    "source": "ctx._source.edad += params.increment",
    "params": {
      "increment": 1
    }
  }
}'

# Upsert (actualizar o insertar)
curl -X POST "localhost:9200/usuarios/_update/5?pretty" -H 'Content-Type: application/json' -d'
{
  "doc": {
    "nombre": "Elena Torres",
    "email": "elena@example.com",
    "edad": 27
  },
  "doc_as_upsert": true
}'

# Actualizar por consulta
curl -X POST "localhost:9200/usuarios/_update_by_query?pretty" -H 'Content-Type: application/json' -d'
{
  "script": {
    "source": "ctx._source.activo = false"
  },
  "query": {
    "range": {
      "edad": {
        "gte": 65
      }
    }
  }
}'

# Bulk update
curl -X POST "localhost:9200/_bulk?pretty" -H 'Content-Type: application/json' -d'
{"update":{"_index":"usuarios","_id":"2"}}
{"doc":{"telefono":"+34 666 123 456"}}
{"update":{"_index":"usuarios","_id":"3"}}
{"doc":{"activo":true}}
'
```

### Eliminar Documentos (Delete)

```bash
# Eliminar documento por ID
curl -X DELETE "localhost:9200/usuarios/_doc/1?pretty"

# Eliminar con versión específica
curl -X DELETE "localhost:9200/usuarios/_doc/2?version=1&pretty"

# Eliminar por consulta
curl -X POST "localhost:9200/usuarios/_delete_by_query?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "term": {
      "activo": false
    }
  }
}'

# Bulk delete
curl -X POST "localhost:9200/_bulk?pretty" -H 'Content-Type: application/json' -d'
{"delete":{"_index":"usuarios","_id":"4"}}
{"delete":{"_index":"usuarios","_id":"5"}}
'
```

## Búsquedas y Consultas

### Búsquedas Básicas

```bash
# Buscar todos los documentos
curl -X GET "localhost:9200/usuarios/_search?pretty"

# Buscar con query string
curl -X GET "localhost:9200/usuarios/_search?q=nombre:Juan&pretty"

# Buscar con parámetros
curl -X GET "localhost:9200/usuarios/_search?size=10&from=0&sort=edad:desc&pretty"

# Buscar en múltiples índices
curl -X GET "localhost:9200/usuarios,productos/_search?pretty"

# Buscar con comodines en índices
curl -X GET "localhost:9200/logs-*/_search?pretty"
```

### Query DSL

```bash
# Match query (búsqueda de texto)
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "match": {
      "nombre": "Juan"
    }
  }
}'

# Multi-match query
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "multi_match": {
      "query": "juan email",
      "fields": ["nombre", "email"]
    }
  }
}'

# Term query (búsqueda exacta)
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "term": {
      "email.keyword": "juan@example.com"
    }
  }
}'

# Range query
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "range": {
      "edad": {
        "gte": 25,
        "lte": 35
      }
    }
  }
}'

# Bool query (consultas complejas)
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "bool": {
      "must": [
        {"match": {"nombre": "Juan"}},
        {"range": {"edad": {"gte": 18}}}
      ],
      "filter": [
        {"term": {"activo": true}}
      ],
      "must_not": [
        {"term": {"email.keyword": "spam@example.com"}}
      ]
    }
  }
}'

# Wildcard query
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "wildcard": {
      "email.keyword": "*@gmail.com"
    }
  }
}'

# Fuzzy query (búsqueda aproximada)
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "fuzzy": {
      "nombre": {
        "value": "Juen",
        "fuzziness": 1
      }
    }
  }
}'
```

### Búsquedas Avanzadas

```bash
# Búsqueda con highlighting
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "match": {
      "nombre": "Juan"
    }
  },
  "highlight": {
    "fields": {
      "nombre": {}
    }
  }
}'

# Búsqueda con agregaciones
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "size": 0,
  "aggs": {
    "edades": {
      "terms": {
        "field": "edad"
      }
    },
    "edad_promedio": {
      "avg": {
        "field": "edad"
      }
    }
  }
}'

# Búsqueda con ordenamiento múltiple
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {"edad": {"order": "desc"}},
    {"nombre.keyword": {"order": "asc"}}
  ]
}'

# Búsqueda con paginación
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "match_all": {}
  },
  "from": 10,
  "size": 5
}'

# Search After (paginación eficiente)
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {"edad": "desc"},
    {"_id": "asc"}
  ],
  "search_after": [30, "user_id_123"]
}'

# Búsqueda en campos anidados
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "nested": {
      "path": "direccion",
      "query": {
        "bool": {
          "must": [
            {"match": {"direccion.ciudad": "Madrid"}}
          ]
        }
      }
    }
  }
}'
```

### Agregaciones

```bash
# Agregación de términos
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "size": 0,
  "aggs": {
    "ciudades": {
      "terms": {
        "field": "direccion.ciudad.keyword",
        "size": 10
      }
    }
  }
}'

# Agregación de histograma
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "size": 0,
  "aggs": {
    "edades_por_rango": {
      "histogram": {
        "field": "edad",
        "interval": 10
      }
    }
  }
}'

# Agregaciones métricas
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "size": 0,
  "aggs": {
    "stats_edad": {
      "stats": {
        "field": "edad"
      }
    },
    "edad_max": {
      "max": {
        "field": "edad"
      }
    },
    "edad_min": {
      "min": {
        "field": "edad"
      }
    }
  }
}'

# Agregaciones anidadas
curl -X GET "localhost:9200/usuarios/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "size": 0,
  "aggs": {
    "ciudades": {
      "terms": {
        "field": "direccion.ciudad.keyword"
      },
      "aggs": {
        "edad_promedio": {
          "avg": {
            "field": "edad"
          }
        }
      }
    }
  }
}'

# Date histogram
curl -X GET "localhost:9200/logs/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "size": 0,
  "aggs": {
    "logs_por_dia": {
      "date_histogram": {
        "field": "timestamp",
        "calendar_interval": "day"
      }
    }
  }
}'
```

## Análisis de Texto

### Analizadores

```bash
# Probar analizador estándar
curl -X GET "localhost:9200/_analyze?pretty" -H 'Content-Type: application/json' -d'
{
  "analyzer": "standard",
  "text": "El rápido zorro marrón salta sobre el perro perezoso"
}'

# Probar analizador personalizado
curl -X GET "localhost:9200/documentos/_analyze?pretty" -H 'Content-Type: application/json' -d'
{
  "analyzer": "mi_analizador",
  "text": "Análisis de texto en español"
}'

# Probar tokenizer específico
curl -X GET "localhost:9200/_analyze?pretty" -H 'Content-Type: application/json' -d'
{
  "tokenizer": "keyword",
  "text": "usuario@ejemplo.com"
}'

# Analizar con filtros específicos
curl -X GET "localhost:9200/_analyze?pretty" -H 'Content-Type: application/json' -d'
{
  "tokenizer": "standard",
  "filter": ["lowercase", "stop"],
  "text": "The Quick Brown Fox"
}'
```

## Administración y Monitoreo

### Configuración del Cluster

```bash
# Ver configuración actual
curl -X GET "localhost:9200/_cluster/settings?pretty"

# Actualizar configuración persistente
curl -X PUT "localhost:9200/_cluster/settings?pretty" -H 'Content-Type: application/json' -d'
{
  "persistent": {
    "cluster.routing.allocation.disk.watermark.low": "85%",
    "cluster.routing.allocation.disk.watermark.high": "90%"
  }
}'

# Configuración temporal
curl -X PUT "localhost:9200/_cluster/settings?pretty" -H 'Content-Type: application/json' -d'
{
  "transient": {
    "cluster.routing.allocation.enable": "all"
  }
}'

# Resetear configuración
curl -X PUT "localhost:9200/_cluster/settings?pretty" -H 'Content-Type: application/json' -d'
{
  "persistent": {
    "cluster.routing.allocation.disk.watermark.low": null
  }
}'
```

### Gestión de Shards

```bash
# Ver estado de shards
curl -X GET "localhost:9200/_cat/shards?v"

# Información detallada de shards
curl -X GET "localhost:9200/_cat/shards?v&h=index,shard,prirep,state,docs,store,node"

# Mover shard manualmente
curl -X POST "localhost:9200/_cluster/reroute?pretty" -H 'Content-Type: application/json' -d'
{
  "commands": [
    {
      "move": {
        "index": "usuarios",
        "shard": 0,
        "from_node": "node1",
        "to_node": "node2"
      }
    }
  ]
}'

# Asignar shard no asignado
curl -X POST "localhost:9200/_cluster/reroute?pretty" -H 'Content-Type: application/json' -d'
{
  "commands": [
    {
      "allocate_primary": {
        "index": "usuarios",
        "shard": 0,
        "node": "node1",
        "accept_data_loss": true
      }
    }
  ]
}'

# Habilitar/deshabilitar asignación de shards
curl -X PUT "localhost:9200/_cluster/settings?pretty" -H 'Content-Type: application/json' -d'
{
  "persistent": {
    "cluster.routing.allocation.enable": "none"
  }
}'
```

### Monitoreo y Estadísticas

```bash
# Estadísticas generales
curl -X GET "localhost:9200/_stats?pretty"

# Estadísticas de índices específicos
curl -X GET "localhost:9200/usuarios/_stats?pretty"

# Estadísticas de nodos
curl -X GET "localhost:9200/_nodes/stats?pretty"

# Información de memoria
curl -X GET "localhost:9200/_cat/nodes?v&h=name,heap.percent,heap.current,heap.max,ram.percent,ram.current,ram.max"

# Información de CPU y carga
curl -X GET "localhost:9200/_cat/nodes?v&h=name,cpu,load_1m,load_5m,load_15m"

# Información de disco
curl -X GET "localhost:9200/_cat/nodes?v&h=name,disk.used_percent,disk.used,disk.total"

# Thread pools
curl -X GET "localhost:9200/_cat/thread_pool?v"

# Información de recovery
curl -X GET "localhost:9200/_cat/recovery?v"

# Información detallada del cluster
curl -X GET "localhost:9200/_cluster/state?pretty"
```

## Snapshots y Restore

### Configurar Repositorio

```bash
# Registrar repositorio de snapshots (filesystem)
curl -X PUT "localhost:9200/_snapshot/backup_repo?pretty" -H 'Content-Type: application/json' -d'
{
  "type": "fs",
  "settings": {
    "location": "/opt/elasticsearch/backups",
    "compress": true
  }
}'

# Registrar repositorio S3
curl -X PUT "localhost:9200/_snapshot/s3_repo?pretty" -H 'Content-Type: application/json' -d'
{
  "type": "s3",
  "settings": {
    "bucket": "mi-bucket-elasticsearch",
    "region": "us-east-1",
    "base_path": "snapshots"
  }
}'

# Ver repositorios configurados
curl -X GET "localhost:9200/_snapshot?pretty"

# Verificar repositorio
curl -X POST "localhost:9200/_snapshot/backup_repo/_verify?pretty"
```

### Crear Snapshots

```bash
# Crear snapshot de todos los índices
curl -X PUT "localhost:9200/_snapshot/backup_repo/snapshot_1?wait_for_completion=true&pretty" -H 'Content-Type: application/json' -d'
{
  "indices": "*",
  "ignore_unavailable": true,
  "include_global_state": false
}'

# Crear snapshot de índices específicos
curl -X PUT "localhost:9200/_snapshot/backup_repo/snapshot_usuarios?pretty" -H 'Content-Type: application/json' -d'
{
  "indices": "usuarios,productos",
  "ignore_unavailable": true,
  "include_global_state": false,
  "metadata": {
    "taken_by": "admin",
    "taken_because": "backup routine"
  }
}'

# Snapshot incremental
curl -X PUT "localhost:9200/_snapshot/backup_repo/snapshot_incremental?pretty" -H 'Content-Type: application/json' -d'
{
  "indices": "usuarios",
  "ignore_unavailable": true,
  "partial": false
}'

# Ver estado de snapshots
curl -X GET "localhost:9200/_snapshot/backup_repo/_all?pretty"

# Ver información específica de snapshot
curl -X GET "localhost:9200/_snapshot/backup_repo/snapshot_1?pretty"

# Ver estado actual de snapshot
curl -X GET "localhost:9200/_snapshot/backup_repo/snapshot_1/_status?pretty"
```

### Restaurar Snapshots

```bash
# Restaurar snapshot completo
curl -X POST "localhost:9200/_snapshot/backup_repo/snapshot_1/_restore?wait_for_completion=true&pretty" -H 'Content-Type: application/json' -d'
{
  "indices": "*",
  "ignore_unavailable": true,
  "include_global_state": false
}'

# Restaurar índices específicos con renombrado
curl -X POST "localhost:9200/_snapshot/backup_repo/snapshot_usuarios/_restore?pretty" -H 'Content-Type: application/json' -d'
{
  "indices": "usuarios",
  "rename_pattern": "usuarios",
  "rename_replacement": "usuarios_restored",
  "ignore_unavailable": true
}'

# Restaurar con configuración personalizada
curl -X POST "localhost:9200/_snapshot/backup_repo/snapshot_1/_restore?pretty" -H 'Content-Type: application/json' -d'
{
  "indices": "usuarios",
  "index_settings": {
    "index.number_of_replicas": 0
  },
  "ignore_index_settings": [
    "index.refresh_interval"
  ]
}'

# Ver estado de restore
curl -X GET "localhost:9200/_cat/recovery?v"
```

### Eliminar Snapshots

```bash
# Eliminar snapshot específico
curl -X DELETE "localhost:9200/_snapshot/backup_repo/snapshot_1?pretty"

# Eliminar múltiples snapshots
curl -X DELETE "localhost:9200/_snapshot/backup_repo/snapshot_*?pretty"
```

## Scripts de Utilidad

### Script de Backup Automatizado

```bash
#!/bin/bash
# backup_elasticsearch.sh

ES_HOST="localhost:9200"
REPO_NAME="backup_repo"
DATE=$(date +%Y%m%d_%H%M%S)
SNAPSHOT_NAME="auto_backup_${DATE}"

# Función para logging
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1"
}

# Crear snapshot
log "Iniciando backup: $SNAPSHOT_NAME"

response=$(curl -s -X PUT "${ES_HOST}/_snapshot/${REPO_NAME}/${SNAPSHOT_NAME}?wait_for_completion=true" \
    -H 'Content-Type: application/json' -d'
{
  "indices": "*",
  "ignore_unavailable": true,
  "include_global_state": false,
  "metadata": {
    "taken_by": "automated_script",
    "taken_because": "scheduled_backup"
  }
}')

# Verificar resultado
if echo "$response" | grep -q '"state":"SUCCESS"'; then
    log "Backup completado exitosamente: $SNAPSHOT_NAME"
else
    log "Error en backup: $response"
    exit 1
fi

# Limpiar snapshots antiguos (mantener últimos 7)
log "Limpiando snapshots antiguos..."

snapshots=$(curl -s -X GET "${ES_HOST}/_snapshot/${REPO_NAME}/_all" | \
    jq -r '.snapshots[] | select(.snapshot | startswith("auto_backup_")) | .snapshot' | \
    sort -r | tail -n +8)

for snapshot in $snapshots; do
    log "Eliminando snapshot antiguo: $snapshot"
    curl -s -X DELETE "${ES_HOST}/_snapshot/${REPO_NAME}/${snapshot}"
done

log "Proceso de backup completado"
```

### Script de Monitoreo de Cluster

```bash
#!/bin/bash
# monitor_elasticsearch.sh

ES_HOST="localhost:9200"
ALERT_EMAIL="admin@example.com"

# Función para enviar alerta
send_alert() {
    local message="$1"
    echo "ALERTA: $message"
    # echo "$message" | mail -s "Elasticsearch Alert" "$ALERT_EMAIL"
}

# Verificar estado del cluster
cluster_health=$(curl -s "${ES_HOST}/_cluster/health" | jq -r '.status')

case $cluster_health in
    "green")
        echo "Cluster status: GREEN - OK"
        ;;
    "yellow")
        echo "Cluster status: YELLOW - Warning"
        unassigned_shards=$(curl -s "${ES_HOST}/_cluster/health" | jq -r '.unassigned_shards')
        if [ "$unassigned_shards" -gt 0 ]; then
            send_alert "Cluster en estado YELLOW - $unassigned_shards shards sin asignar"
        fi
        ;;
    "red")
        echo "Cluster status: RED - Critical"
        send_alert "Cluster en estado RED - Revisar inmediatamente"
        ;;
    *)
        echo "No se pudo obtener estado del cluster"
        send_alert "No se puede conectar al cluster Elasticsearch"
        ;;
esac

# Verificar uso de memoria
curl -s "${ES_HOST}/_cat/nodes?h=name,heap.percent" | while read node heap_percent; do
    if [ "$heap_percent" -gt 85 ]; then
        send_alert "Nodo $node usando ${heap_percent}% de heap memory"
    fi
done

# Verificar uso de disco
curl -s "${ES_HOST}/_cat/nodes?h=name,disk.used_percent" | while read node disk_percent; do
    if [ "$disk_percent" -gt 85 ]; then
        send_alert "Nodo $node usando ${disk_percent}% de disco"
    fi
done

# Verificar índices grandes
curl -s "${ES_HOST}/_cat/indices?h=index,store.size" | while read index size; do
    # Convertir tamaño a bytes para comparación
    size_bytes=$(echo "$size" | sed 's/[^0-9.]//g')
    size_unit=$(echo "$size" | sed 's/[0-9.]//g')
    
    case $size_unit in
        "gb"|"GB")
            if (( $(echo "$size_bytes > 50" | bc -l) )); then
                echo "Índice $index es grande: $size"
            fi
            ;;
    esac
done
```

### Script de Reindexado

```bash
#!/bin/bash
# reindex_elasticsearch.sh

ES_HOST="localhost:9200"
SOURCE_INDEX="$1"
TARGET_INDEX="$2"

if [ $# -ne 2 ]; then
    echo "Uso: $0 <source_index> <target_index>"
    exit 1
fi

echo "Reindexando de $SOURCE_INDEX a $TARGET_INDEX..."

# Crear índice destino con configuración optimizada
curl -X PUT "${ES_HOST}/${TARGET_INDEX}" -H 'Content-Type: application/json' -d'
{
  "settings": {
    "number_of_shards": 1,
    "number_of_replicas": 0,
    "refresh_interval": -1
  }
}' > /dev/null

# Copiar mapping del índice origen
mapping=$(curl -s "${ES_HOST}/${SOURCE_INDEX}/_mapping" | jq ".\"${SOURCE_INDEX}\".mappings")
curl -X PUT "${ES_HOST}/${TARGET_INDEX}/_mapping" \
    -H 'Content-Type: application/json' \
    -d "$mapping" > /dev/null

# Iniciar reindex
task_id=$(curl -s -X POST "${ES_HOST}/_reindex?wait_for_completion=false" \
    -H 'Content-Type: application/json' -d"
{
  \"source\": {
    \"index\": \"${SOURCE_INDEX}\"
  },
  \"dest\": {
    \"index\": \"${TARGET_INDEX}\"
  }
}" | jq -r '.task')

echo "Reindex iniciado con task ID: $task_id"

# Monitorear progreso
while true; do
    status=$(curl -s "${ES_HOST}/_tasks/${task_id}" | jq -r '.completed')
    
    if [ "$status" = "true" ]; then
        echo "Reindex completado"
        break
    fi
    
    progress=$(curl -s "${ES_HOST}/_tasks/${task_id}" | jq -r '.task.status.created // 0')
    echo "Documentos procesados: $progress"
    sleep 5
done

# Restaurar configuración del índice
curl -X PUT "${ES_HOST}/${TARGET_INDEX}/_settings" -H 'Content-Type: application/json' -d'
{
  "index": {
    "number_of_replicas": 1,
    "refresh_interval": "1s"
  }
}' > /dev/null

echo "Reindex de $SOURCE_INDEX a $TARGET_INDEX completado"
```

### Script de Optimización de Índices

```bash
#!/bin/bash
# optimize_elasticsearch.sh

ES_HOST="localhost:9200"

# Obtener lista de índices
indices=$(curl -s "${ES_HOST}/_cat/indices?h=index" | grep -v "^\.")

for index in $indices; do
    echo "Optimizando índice: $index"
    
    # Force merge para reducir segmentos
    curl -s -X POST "${ES_HOST}/${index}/_forcemerge?max_num_segments=1" > /dev/null
    
    # Verificar número de segmentos después
    segments=$(curl -s "${ES_HOST}/_cat/segments/${index}?h=segments.count" | awk '{sum+=$1} END {print sum}')
    echo "Índice $index ahora tiene $segments segmentos"
done

echo "Optimización completada"
```

## Ejemplos de Uso Común

### Sistema de Logs

```bash
# Crear índice para logs con mapping optimizado
curl -X PUT "localhost:9200/logs-app" -H 'Content-Type: application/json' -d'
{
  "settings": {
    "number_of_shards": 3,
    "number_of_replicas": 1,
    "index.refresh_interval": "5s"
  },
  "mappings": {
    "properties": {
      "timestamp": {
        "type": "date",
        "format": "yyyy-MM-dd HH:mm:ss||yyyy-MM-dd||epoch_millis"
      },
      "level": {
        "type": "keyword"
      },
      "logger": {
        "type": "keyword"
      },
      "message": {
        "type": "text",
        "analyzer": "standard"
      },
      "exception": {
        "type": "text"
      },
      "host": {
        "type": "keyword"
      },
      "application": {
        "type": "keyword"
      }
    }
  }
}'

# Insertar logs de ejemplo
curl -X POST "localhost:9200/logs-app/_doc" -H 'Content-Type: application/json' -d'
{
  "timestamp": "2024-01-01 10:30:15",
  "level": "ERROR",
  "logger": "com.app.database",
  "message": "Connection timeout to database",
  "host": "server-01",
  "application": "api-gateway"
}'

# Buscar errores en las últimas 24 horas
curl -X GET "localhost:9200/logs-app/_search" -H 'Content-Type: application/json' -d'
{
  "query": {
    "bool": {
      "must": [
        {"term": {"level": "ERROR"}},
        {"range": {
          "timestamp": {
            "gte": "now-24h"
          }
        }}
      ]
    }
  },
  "sort": [{"timestamp": {"order": "desc"}}]
}'

# Agregación de errores por aplicación
curl -X GET "localhost:9200/logs-app/_search" -H 'Content-Type: application/json' -d'
{
  "size": 0,
  "query": {
    "term": {"level": "ERROR"}
  },
  "aggs": {
    "errores_por_app": {
      "terms": {
        "field": "application",
        "size": 10
      }
    }
  }
}'
```

### Sistema de Búsqueda de Productos

```bash
# Crear índice de productos con búsqueda optimizada
curl -X PUT "localhost:9200/productos" -H 'Content-Type: application/json' -d'
{
  "settings": {
    "analysis": {
      "analyzer": {
        "producto_analyzer": {
          "type": "custom",
          "tokenizer": "standard",
          "filter": ["lowercase", "asciifolding", "stop"]
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "nombre": {
        "type": "text",
        "analyzer": "producto_analyzer",
        "fields": {
          "keyword": {"type": "keyword"}
        }
      },
      "descripcion": {
        "type": "text",
        "analyzer": "producto_analyzer"
      },
      "categoria": {
        "type": "keyword"
      },
      "precio": {
        "type": "float"
      },
      "marca": {
        "type": "keyword"
      },
      "tags": {
        "type": "keyword"
      },
      "rating": {
        "type": "float"
      },
      "disponible": {
        "type": "boolean"
      },
      "fecha_creacion": {
        "type": "date"
      }
    }
  }
}'

# Búsqueda multi-campo con boost
curl -X GET "localhost:9200/productos/_search" -H 'Content-Type: application/json' -d'
{
  "query": {
    "multi_match": {
      "query": "laptop gaming",
      "fields": ["nombre^2", "descripcion", "tags"],
      "type": "best_fields"
    }
  },
  "filter": {
    "bool": {
      "must": [
        {"term": {"disponible": true}},
        {"range": {"precio": {"lte": 2000}}}
      ]
    }
  }
}'

# Búsqueda con agregaciones para filtros
curl -X GET "localhost:9200/productos/_search" -H 'Content-Type: application/json' -d'
{
  "query": {
    "match": {"categoria": "electrónica"}
  },
  "aggs": {
    "marcas": {
      "terms": {"field": "marca"}
    },
    "rango_precios": {
      "range": {
        "field": "precio",
        "ranges": [
          {"to": 500},
          {"from": 500, "to": 1000},
          {"from": 1000, "to": 2000},
          {"from": 2000}
        ]
      }
    },
    "rating_promedio": {
      "avg": {"field": "rating"}
    }
  }
}'
```
