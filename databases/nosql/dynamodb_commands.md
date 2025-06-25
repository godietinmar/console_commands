# Comandos DynamoDB (AWS CLI)

Este archivo contiene una lista de comandos para Amazon DynamoDB usando AWS CLI y herramientas de línea de comandos, organizados por categoría.

## Herramientas de Línea de Comandos

### aws dynamodb (AWS CLI)

**Descripción:**  
Interfaz de línea de comandos principal para interactuar con DynamoDB.

**Prerequisitos:**
```bash
# Instalar AWS CLI
pip install awscli

# Configurar credenciales
aws configure
# O usar variables de entorno:
# export AWS_ACCESS_KEY_ID=your_access_key
# export AWS_SECRET_ACCESS_KEY=your_secret_key
# export AWS_DEFAULT_REGION=us-east-1
```

**Sintaxis básica:**
```bash
aws dynamodb [comando] [opciones]
```

**Opciones comunes:**
- `--region`: Región de AWS
- `--endpoint-url`: URL del endpoint (para DynamoDB local)
- `--profile`: Perfil de AWS a usar
- `--output`: Formato de salida (json, table, text)
- `--cli-input-json`: Entrada en formato JSON
- `--generate-cli-skeleton`: Generar esqueleto de comando

### DynamoDB Local

```bash
# Descargar e iniciar DynamoDB Local
java -Djava.library.path=./DynamoDBLocal_lib -jar DynamoDBLocal.jar -sharedDb

# Usar con AWS CLI (agregar --endpoint-url)
aws dynamodb list-tables --endpoint-url http://localhost:8000
```

## Gestión de Tablas

### Crear Tablas

```bash
# Tabla básica con clave de partición
aws dynamodb create-table \
    --table-name Usuarios \
    --attribute-definitions \
        AttributeName=user_id,AttributeType=S \
    --key-schema \
        AttributeName=user_id,KeyType=HASH \
    --provisioned-throughput \
        ReadCapacityUnits=5,WriteCapacityUnits=5

# Tabla con clave de partición y ordenamiento
aws dynamodb create-table \
    --table-name Posts \
    --attribute-definitions \
        AttributeName=user_id,AttributeType=S \
        AttributeName=timestamp,AttributeType=N \
    --key-schema \
        AttributeName=user_id,KeyType=HASH \
        AttributeName=timestamp,KeyType=RANGE \
    --provisioned-throughput \
        ReadCapacityUnits=5,WriteCapacityUnits=5

# Tabla con índice secundario global (GSI)
aws dynamodb create-table \
    --table-name Productos \
    --attribute-definitions \
        AttributeName=producto_id,AttributeType=S \
        AttributeName=categoria,AttributeType=S \
        AttributeName=precio,AttributeType=N \
    --key-schema \
        AttributeName=producto_id,KeyType=HASH \
    --provisioned-throughput \
        ReadCapacityUnits=5,WriteCapacityUnits=5 \
    --global-secondary-indexes \
        IndexName=categoria-precio-index,KeySchema=[{AttributeName=categoria,KeyType=HASH},{AttributeName=precio,KeyType=RANGE}],Projection={ProjectionType=ALL},ProvisionedThroughput={ReadCapacityUnits=5,WriteCapacityUnits=5}

# Tabla con índice secundario local (LSI)
aws dynamodb create-table \
    --table-name Pedidos \
    --attribute-definitions \
        AttributeName=cliente_id,AttributeType=S \
        AttributeName=fecha_pedido,AttributeType=S \
        AttributeName=estado,AttributeType=S \
    --key-schema \
        AttributeName=cliente_id,KeyType=HASH \
        AttributeName=fecha_pedido,KeyType=RANGE \
    --provisioned-throughput \
        ReadCapacityUnits=5,WriteCapacityUnits=5 \
    --local-secondary-indexes \
        IndexName=estado-index,KeySchema=[{AttributeName=cliente_id,KeyType=HASH},{AttributeName=estado,KeyType=RANGE}],Projection={ProjectionType=ALL}

# Tabla con billing mode on-demand
aws dynamodb create-table \
    --table-name LogsEventos \
    --attribute-definitions \
        AttributeName=evento_id,AttributeType=S \
    --key-schema \
        AttributeName=evento_id,KeyType=HASH \
    --billing-mode PAY_PER_REQUEST
```

### Información de Tablas

```bash
# Listar todas las tablas
aws dynamodb list-tables

# Describir tabla específica
aws dynamodb describe-table --table-name Usuarios

# Describir tabla con formato de salida específico
aws dynamodb describe-table --table-name Usuarios --output table

# Ver solo el estado de la tabla
aws dynamodb describe-table --table-name Usuarios --query 'Table.TableStatus'

# Ver throughput provisionado
aws dynamodb describe-table --table-name Usuarios --query 'Table.ProvisionedThroughput'

# Ver índices secundarios
aws dynamodb describe-table --table-name Productos --query 'Table.GlobalSecondaryIndexes'
```

### Modificar Tablas

```bash
# Actualizar throughput provisionado
aws dynamodb update-table \
    --table-name Usuarios \
    --provisioned-throughput ReadCapacityUnits=10,WriteCapacityUnits=10

# Actualizar throughput de GSI
aws dynamodb update-table \
    --table-name Productos \
    --global-secondary-index-updates \
        '[{
            "Update": {
                "IndexName": "categoria-precio-index",
                "ProvisionedThroughput": {
                    "ReadCapacityUnits": 10,
                    "WriteCapacityUnits": 10
                }
            }
        }]'

# Cambiar a billing mode on-demand
aws dynamodb update-table \
    --table-name Usuarios \
    --billing-mode PAY_PER_REQUEST

# Habilitar streams
aws dynamodb update-table \
    --table-name Usuarios \
    --stream-specification StreamEnabled=true,StreamViewType=NEW_AND_OLD_IMAGES

# Habilitar Point-in-Time Recovery
aws dynamodb update-continuous-backups \
    --table-name Usuarios \
    --point-in-time-recovery-specification PointInTimeRecoveryEnabled=true
```

### Eliminar Tablas

```bash
# Eliminar tabla
aws dynamodb delete-table --table-name Usuarios

# Verificar eliminación
aws dynamodb describe-table --table-name Usuarios
```

## Operaciones CRUD

### Crear Items (Put)

```bash
# Insertar item básico
aws dynamodb put-item \
    --table-name Usuarios \
    --item '{
        "user_id": {"S": "user123"},
        "nombre": {"S": "Juan Pérez"},
        "edad": {"N": "30"},
        "email": {"S": "juan@example.com"},
        "activo": {"BOOL": true}
    }'

# Insertar con condición (solo si no existe)
aws dynamodb put-item \
    --table-name Usuarios \
    --item '{
        "user_id": {"S": "user124"},
        "nombre": {"S": "Ana García"},
        "edad": {"N": "25"}
    }' \
    --condition-expression "attribute_not_exists(user_id)"

# Insertar item complejo con diferentes tipos de datos
aws dynamodb put-item \
    --table-name Productos \
    --item '{
        "producto_id": {"S": "prod123"},
        "nombre": {"S": "Laptop Gaming"},
        "categoria": {"S": "electrónica"},
        "precio": {"N": "1299.99"},
        "especificaciones": {
            "M": {
                "marca": {"S": "Dell"},
                "modelo": {"S": "G5"},
                "ram": {"S": "16GB"}
            }
        },
        "tags": {"L": [{"S": "gaming"}, {"S": "laptop"}, {"S": "dell"}]},
        "disponible": {"BOOL": true},
        "fecha_creacion": {"S": "2024-01-01T10:00:00Z"}
    }'

# Usar archivo JSON para item complejo
echo '{
    "user_id": {"S": "user125"},
    "perfil": {
        "M": {
            "nombre": {"S": "Luis Rodríguez"},
            "edad": {"N": "35"},
            "direccion": {
                "M": {
                    "calle": {"S": "Calle Mayor 123"},
                    "ciudad": {"S": "Madrid"},
                    "codigo_postal": {"S": "28001"}
                }
            },
            "hobbies": {"L": [{"S": "lectura"}, {"S": "deportes"}]}
        }
    }
}' > usuario.json

aws dynamodb put-item --table-name Usuarios --item file://usuario.json
```

### Leer Items (Get)

```bash
# Obtener item por clave primaria
aws dynamodb get-item \
    --table-name Usuarios \
    --key '{"user_id": {"S": "user123"}}'

# Obtener con proyección (solo ciertos atributos)
aws dynamodb get-item \
    --table-name Usuarios \
    --key '{"user_id": {"S": "user123"}}' \
    --projection-expression "nombre, email, edad"

# Obtener item con clave compuesta
aws dynamodb get-item \
    --table-name Posts \
    --key '{
        "user_id": {"S": "user123"},
        "timestamp": {"N": "1609459200"}
    }'

# Lectura consistente
aws dynamodb get-item \
    --table-name Usuarios \
    --key '{"user_id": {"S": "user123"}}' \
    --consistent-read

# Batch get items (múltiples items de una vez)
aws dynamodb batch-get-item \
    --request-items '{
        "Usuarios": {
            "Keys": [
                {"user_id": {"S": "user123"}},
                {"user_id": {"S": "user124"}},
                {"user_id": {"S": "user125"}}
            ]
        },
        "Productos": {
            "Keys": [
                {"producto_id": {"S": "prod123"}}
            ]
        }
    }'
```

### Actualizar Items (Update)

```bash
# Actualizar atributos específicos
aws dynamodb update-item \
    --table-name Usuarios \
    --key '{"user_id": {"S": "user123"}}' \
    --update-expression "SET edad = :edad, email = :email" \
    --expression-attribute-values '{
        ":edad": {"N": "31"},
        ":email": {"S": "juan.perez@example.com"}
    }'

# Incrementar valor numérico
aws dynamodb update-item \
    --table-name Productos \
    --key '{"producto_id": {"S": "prod123"}}' \
    --update-expression "ADD precio :incremento, visitas :uno" \
    --expression-attribute-values '{
        ":incremento": {"N": "50"},
        ":uno": {"N": "1"}
    }'

# Agregar elemento a lista
aws dynamodb update-item \
    --table-name Productos \
    --key '{"producto_id": {"S": "prod123"}}' \
    --update-expression "SET tags = list_append(tags, :nuevo_tag)" \
    --expression-attribute-values '{
        ":nuevo_tag": {"L": [{"S": "oferta"}]}
    }'

# Quitar atributo
aws dynamodb update-item \
    --table-name Usuarios \
    --key '{"user_id": {"S": "user123"}}' \
    --update-expression "REMOVE telefono"

# Actualizar con condición
aws dynamodb update-item \
    --table-name Usuarios \
    --key '{"user_id": {"S": "user123"}}' \
    --update-expression "SET activo = :estado" \
    --condition-expression "edad > :edad_minima" \
    --expression-attribute-values '{
        ":estado": {"BOOL": false},
        ":edad_minima": {"N": "18"}
    }'

# Actualizar atributo anidado
aws dynamodb update-item \
    --table-name Usuarios \
    --key '{"user_id": {"S": "user125"}}' \
    --update-expression "SET perfil.direccion.ciudad = :nueva_ciudad" \
    --expression-attribute-values '{
        ":nueva_ciudad": {"S": "Barcelona"}
    }'

# Retornar valores antes/después de actualización
aws dynamodb update-item \
    --table-name Usuarios \
    --key '{"user_id": {"S": "user123"}}' \
    --update-expression "SET edad = edad + :incremento" \
    --expression-attribute-values '{ ":incremento": {"N": "1"} }' \
    --return-values ALL_NEW
```

### Eliminar Items (Delete)

```bash
# Eliminar item por clave primaria
aws dynamodb delete-item \
    --table-name Usuarios \
    --key '{"user_id": {"S": "user123"}}'

# Eliminar con condición
aws dynamodb delete-item \
    --table-name Usuarios \
    --key '{"user_id": {"S": "user124"}}' \
    --condition-expression "activo = :estado" \
    --expression-attribute-values '{ ":estado": {"BOOL": false} }'

# Eliminar y retornar valores eliminados
aws dynamodb delete-item \
    --table-name Usuarios \
    --key '{"user_id": {"S": "user125"}}' \
    --return-values ALL_OLD

# Batch delete items
aws dynamodb batch-write-item \
    --request-items '{
        "Usuarios": [
            {
                "DeleteRequest": {
                    "Key": {"user_id": {"S": "user126"}}
                }
            },
            {
                "DeleteRequest": {
                    "Key": {"user_id": {"S": "user127"}}
                }
            }
        ]
    }'
```

## Consultas y Escaneos

### Query (Consultas)

```bash
# Query básico por clave de partición
aws dynamodb query \
    --table-name Posts \
    --key-condition-expression "user_id = :user_id" \
    --expression-attribute-values '{
        ":user_id": {"S": "user123"}
    }'

# Query con clave de ordenamiento
aws dynamodb query \
    --table-name Posts \
    --key-condition-expression "user_id = :user_id AND #timestamp > :fecha" \
    --expression-attribute-names '{"#timestamp": "timestamp"}' \
    --expression-attribute-values '{
        ":user_id": {"S": "user123"},
        ":fecha": {"N": "1609459200"}
    }'

# Query con filtro adicional
aws dynamodb query \
    --table-name Posts \
    --key-condition-expression "user_id = :user_id" \
    --filter-expression "contains(titulo, :palabra)" \
    --expression-attribute-values '{
        ":user_id": {"S": "user123"},
        ":palabra": {"S": "DynamoDB"}
    }'

# Query en índice secundario global
aws dynamodb query \
    --table-name Productos \
    --index-name categoria-precio-index \
    --key-condition-expression "categoria = :cat AND precio BETWEEN :min_precio AND :max_precio" \
    --expression-attribute-values '{
        ":cat": {"S": "electrónica"},
        ":min_precio": {"N": "500"},
        ":max_precio": {"N": "2000"}
    }'

# Query con proyección específica
aws dynamodb query \
    --table-name Posts \
    --key-condition-expression "user_id = :user_id" \
    --projection-expression "titulo, fecha_creacion, #likes" \
    --expression-attribute-names '{"#likes": "likes"}' \
    --expression-attribute-values '{
        ":user_id": {"S": "user123"}
    }'

# Query con límite y orden
aws dynamodb query \
    --table-name Posts \
    --key-condition-expression "user_id = :user_id" \
    --expression-attribute-values '{
        ":user_id": {"S": "user123"}
    }' \
    --scan-index-forward false \
    --limit 10

# Query paginado
aws dynamodb query \
    --table-name Posts \
    --key-condition-expression "user_id = :user_id" \
    --expression-attribute-values '{
        ":user_id": {"S": "user123"}
    }' \
    --limit 5 \
    --exclusive-start-key '{
        "user_id": {"S": "user123"},
        "timestamp": {"N": "1609459300"}
    }'
```

### Scan (Escaneos)

```bash
# Scan completo de tabla
aws dynamodb scan --table-name Usuarios

# Scan con filtro
aws dynamodb scan \
    --table-name Usuarios \
    --filter-expression "edad BETWEEN :min_edad AND :max_edad" \
    --expression-attribute-values '{
        ":min_edad": {"N": "25"},
        ":max_edad": {"N": "35"}
    }'

# Scan con proyección
aws dynamodb scan \
    --table-name Usuarios \
    --projection-expression "user_id, nombre, edad"

# Scan paralelo (dividir en segmentos)
aws dynamodb scan \
    --table-name Usuarios \
    --total-segments 4 \
    --segment 0

# Scan con múltiples filtros
aws dynamodb scan \
    --table-name Productos \
    --filter-expression "categoria = :cat AND precio < :max_precio AND disponible = :disp" \
    --expression-attribute-values '{
        ":cat": {"S": "electrónica"},
        ":max_precio": {"N": "1000"},
        ":disp": {"BOOL": true}
    }'

# Scan con límite
aws dynamodb scan \
    --table-name Usuarios \
    --limit 50

# Scan usando índice
aws dynamodb scan \
    --table-name Productos \
    --index-name categoria-precio-index
```

## Operaciones Batch

### Batch Write

```bash
# Insertar y eliminar múltiples items
aws dynamodb batch-write-item \
    --request-items '{
        "Usuarios": [
            {
                "PutRequest": {
                    "Item": {
                        "user_id": {"S": "user201"},
                        "nombre": {"S": "María López"},
                        "edad": {"N": "28"}
                    }
                }
            },
            {
                "PutRequest": {
                    "Item": {
                        "user_id": {"S": "user202"},
                        "nombre": {"S": "Carlos Sánchez"},
                        "edad": {"N": "32"}
                    }
                }
            },
            {
                "DeleteRequest": {
                    "Key": {"user_id": {"S": "user_old"}}
                }
            }
        ]
    }'

# Usar archivo JSON para batch grande
echo '{
    "Usuarios": [
        {
            "PutRequest": {
                "Item": {
                    "user_id": {"S": "user203"},
                    "nombre": {"S": "Elena Torres"},
                    "edad": {"N": "27"},
                    "email": {"S": "elena@example.com"}
                }
            }
        },
        {
            "PutRequest": {
                "Item": {
                    "user_id": {"S": "user204"},
                    "nombre": {"S": "Pedro Ruiz"},
                    "edad": {"N": "29"},
                    "email": {"S": "pedro@example.com"}
                }
            }
        }
    ]
}' > batch_items.json

aws dynamodb batch-write-item --request-items file://batch_items.json
```

## Transacciones

### Transacciones de Escritura

```bash
# Transacción que actualiza múltiples items
aws dynamodb transact-write-items \
    --transact-items '[
        {
            "Update": {
                "TableName": "Usuarios",
                "Key": {"user_id": {"S": "user123"}},
                "UpdateExpression": "ADD creditos :creditos",
                "ExpressionAttributeValues": {":creditos": {"N": "-100"}},
                "ConditionExpression": "creditos >= :creditos"
            }
        },
        {
            "Put": {
                "TableName": "Transacciones",
                "Item": {
                    "transaccion_id": {"S": "txn123"},
                    "user_id": {"S": "user123"},
                    "tipo": {"S": "compra"},
                    "monto": {"N": "100"},
                    "fecha": {"S": "2024-01-01T12:00:00Z"}
                }
            }
        }
    ]'

# Transacción con múltiples condiciones
aws dynamodb transact-write-items \
    --transact-items '[
        {
            "Update": {
                "TableName": "Productos",
                "Key": {"producto_id": {"S": "prod123"}},
                "UpdateExpression": "ADD stock :cantidad",
                "ExpressionAttributeValues": {":cantidad": {"N": "-1"}},
                "ConditionExpression": "stock > :min_stock",
                "ExpressionAttributeValues": {":min_stock": {"N": "0"}}
            }
        },
        {
            "Put": {
                "TableName": "Pedidos",
                "Item": {
                    "pedido_id": {"S": "order123"},
                    "producto_id": {"S": "prod123"},
                    "cliente_id": {"S": "user123"},
                    "cantidad": {"N": "1"},
                    "estado": {"S": "pendiente"}
                },
                "ConditionExpression": "attribute_not_exists(pedido_id)"
            }
        }
    ]'
```

### Transacciones de Lectura

```bash
# Leer múltiples items en una transacción
aws dynamodb transact-get-items \
    --transact-items '[
        {
            "Get": {
                "TableName": "Usuarios",
                "Key": {"user_id": {"S": "user123"}}
            }
        },
        {
            "Get": {
                "TableName": "Productos",
                "Key": {"producto_id": {"S": "prod123"}}
            }
        }
    ]'
```

## Backup y Restore

### Backups On-Demand

```bash
# Crear backup
aws dynamodb create-backup \
    --table-name Usuarios \
    --backup-name backup-usuarios-2024-01-01

# Listar backups
aws dynamodb list-backups --table-name Usuarios

# Describir backup específico
aws dynamodb describe-backup --backup-arn arn:aws:dynamodb:region:account:table/Usuarios/backup/01234567890123-abcdefgh

# Restaurar desde backup
aws dynamodb restore-table-from-backup \
    --target-table-name UsuariosRestaurada \
    --backup-arn arn:aws:dynamodb:region:account:table/Usuarios/backup/01234567890123-abcdefgh

# Eliminar backup
aws dynamodb delete-backup --backup-arn arn:aws:dynamodb:region:account:table/Usuarios/backup/01234567890123-abcdefgh
```

### Point-in-Time Recovery

```bash
# Habilitar PITR
aws dynamodb update-continuous-backups \
    --table-name Usuarios \
    --point-in-time-recovery-specification PointInTimeRecoveryEnabled=true

# Ver estado de PITR
aws dynamodb describe-continuous-backups --table-name Usuarios

# Restaurar a punto específico en el tiempo
aws dynamodb restore-table-to-point-in-time \
    --source-table-name Usuarios \
    --target-table-name UsuariosRestauradaPITR \
    --restore-date-time 2024-01-01T12:00:00
```

## Export e Import

### Export a S3

```bash
# Exportar tabla completa a S3
aws dynamodb export-table-to-point-in-time \
    --table-arn arn:aws:dynamodb:region:account:table/Usuarios \
    --s3-bucket mi-bucket-exports \
    --export-format DYNAMODB_JSON

# Exportar con filtro de tiempo
aws dynamodb export-table-to-point-in-time \
    --table-arn arn:aws:dynamodb:region:account:table/Usuarios \
    --s3-bucket mi-bucket-exports \
    --export-time 2024-01-01T00:00:00

# Ver estado de export
aws dynamodb describe-export --export-arn arn:aws:dynamodb:region:account:table/Usuarios/export/01234567890123-abcdefgh
```

## Monitoreo y Estadísticas

### Métricas y Logs

```bash
# Ver métricas de CloudWatch (requiere aws logs)
aws logs describe-log-groups --log-group-name-prefix "/aws/dynamodb"

# Obtener métricas de throughput
aws cloudwatch get-metric-statistics \
    --namespace AWS/DynamoDB \
    --metric-name ConsumedReadCapacityUnits \
    --dimensions Name=TableName,Value=Usuarios \
    --start-time 2024-01-01T00:00:00Z \
    --end-time 2024-01-01T23:59:59Z \
    --period 3600 \
    --statistics Sum

# Ver throttling
aws cloudwatch get-metric-statistics \
    --namespace AWS/DynamoDB \
    --metric-name ThrottledRequests \
    --dimensions Name=TableName,Value=Usuarios \
    --start-time 2024-01-01T00:00:00Z \
    --end-time 2024-01-01T23:59:59Z \
    --period 3600 \
    --statistics Sum
```

## Scripts de Utilidad

### Script de Backup Automatizado

```bash
#!/bin/bash
# backup_dynamodb.sh

TABLES=("Usuarios" "Productos" "Pedidos")
DATE=$(date +%Y%m%d_%H%M%S)
REGION="us-east-1"

for table in "${TABLES[@]}"; do
    echo "Creando backup para tabla: $table"
    
    aws dynamodb create-backup \
        --table-name $table \
        --backup-name "backup-${table}-${DATE}" \
        --region $REGION
    
    if [ $? -eq 0 ]; then
        echo "Backup creado exitosamente para $table"
    else
        echo "Error al crear backup para $table"
    fi
done

echo "Proceso de backup completado"
```

### Script de Migración de Datos

```bash
#!/bin/bash
# migrate_dynamodb.sh

SOURCE_TABLE="UsuariosOld"
TARGET_TABLE="UsuariosNew"
REGION="us-east-1"

# Escanear tabla origen y migrar a tabla destino
aws dynamodb scan \
    --table-name $SOURCE_TABLE \
    --region $REGION \
    --output json | \
jq -r '.Items[] | @base64' | \
while read item; do
    decoded_item=$(echo $item | base64 --decode)
    
    aws dynamodb put-item \
        --table-name $TARGET_TABLE \
        --item "$decoded_item" \
        --region $REGION
        
    echo "Item migrado: $(echo $decoded_item | jq -r '.user_id.S')"
done

echo "Migración completada"
```

### Script de Monitoreo

```bash
#!/bin/bash
# monitor_dynamodb.sh

TABLES=("Usuarios" "Productos" "Pedidos")
REGION="us-east-1"

echo "=== MONITOREO DYNAMODB ==="
echo "Fecha: $(date)"

for table in "${TABLES[@]}"; do
    echo -e "\n--- TABLA: $table ---"
    
    # Estado de la tabla
    status=$(aws dynamodb describe-table --table-name $table --region $REGION --query 'Table.TableStatus' --output text)
    echo "Estado: $status"
    
    # Throughput
    read_capacity=$(aws dynamodb describe-table --table-name $table --region $REGION --query 'Table.ProvisionedThroughput.ReadCapacityUnits' --output text)
    write_capacity=$(aws dynamodb describe-table --table-name $table --region $REGION --query 'Table.ProvisionedThroughput.WriteCapacityUnits' --output text)
    echo "Read Capacity: $read_capacity, Write Capacity: $write_capacity"
    
    # Conteo de items (aproximado)
    item_count=$(aws dynamodb describe-table --table-name $table --region $REGION --query 'Table.ItemCount' --output text)
    echo "Items (aprox): $item_count"
    
    # Tamaño de tabla
    table_size=$(aws dynamodb describe-table --table-name $table --region $REGION --query 'Table.TableSizeBytes' --output text)
    echo "Tamaño: $table_size bytes"
done

echo -e "\n--- MÉTRICAS RECIENTES ---"
for table in "${TABLES[@]}"; do
    echo "Throttles en $table en la última hora:"
    aws cloudwatch get-metric-statistics \
        --namespace AWS/DynamoDB \
        --metric-name ThrottledRequests \
        --dimensions Name=TableName,Value=$table \
        --start-time $(date -d '1 hour ago' -u +%Y-%m-%dT%H:%M:%S) \
        --end-time $(date -u +%Y-%m-%dT%H:%M:%S) \
        --period 3600 \
        --statistics Sum \
        --region $REGION \
        --query 'Datapoints[0].Sum' \
        --output text
done
```

### Script de Limpieza de Items Antiguos

```bash
#!/bin/bash
# cleanup_old_items.sh

TABLE_NAME="LogsEventos"
CUTOFF_DATE=$(date -d '30 days ago' +%s)  # 30 días atrás
REGION="us-east-1"

echo "Eliminando items anteriores a: $(date -d @$CUTOFF_DATE)"

# Escanear y eliminar items antiguos
aws dynamodb scan \
    --table-name $TABLE_NAME \
    --filter-expression "#timestamp < :cutoff" \
    --expression-attribute-names '{"#timestamp": "timestamp"}' \
    --expression-attribute-values "{\":cutoff\": {\"N\": \"$CUTOFF_DATE\"}}" \
    --projection-expression "evento_id" \
    --region $REGION \
    --output json | \
jq -r '.Items[].evento_id.S' | \
while read evento_id; do
    aws dynamodb delete-item \
        --table-name $TABLE_NAME \
        --key "{\"evento_id\": {\"S\": \"$evento_id\"}}" \
        --region $REGION
    
    echo "Eliminado: $evento_id"
done

echo "Limpieza completada"
```

## Ejemplos de Uso Común

### Sistema de E-commerce

```bash
# Crear tablas para e-commerce
aws dynamodb create-table \
    --table-name Productos \
    --attribute-definitions \
        AttributeName=producto_id,AttributeType=S \
        AttributeName=categoria,AttributeType=S \
        AttributeName=precio,AttributeType=N \
    --key-schema AttributeName=producto_id,KeyType=HASH \
    --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5 \
    --global-secondary-indexes \
        IndexName=categoria-precio-index,KeySchema=[{AttributeName=categoria,KeyType=HASH},{AttributeName=precio,KeyType=RANGE}],Projection={ProjectionType=ALL},ProvisionedThroughput={ReadCapacityUnits=5,WriteCapacityUnits=5}

# Insertar productos
aws dynamodb put-item \
    --table-name Productos \
    --item '{
        "producto_id": {"S": "prod_laptop_001"},
        "nombre": {"S": "Laptop Gaming Dell G5"},
        "categoria": {"S": "electrónica"},
        "precio": {"N": "1299.99"},
        "descripcion": {"S": "Laptop gaming con Intel i7 y 16GB RAM"},
        "stock": {"N": "15"},
        "marca": {"S": "Dell"},
        "rating": {"N": "4.5"},
        "disponible": {"BOOL": true}
    }'

# Buscar productos por categoría y rango de precio
aws dynamodb query \
    --table-name Productos \
    --index-name categoria-precio-index \
    --key-condition-expression "categoria = :cat AND precio BETWEEN :min AND :max" \
    --expression-attribute-values '{
        ":cat": {"S": "electrónica"},
        ":min": {"N": "500"},
        ":max": {"N": "1500"}
    }'

# Actualizar stock después de compra
aws dynamodb update-item \
    --table-name Productos \
    --key '{"producto_id": {"S": "prod_laptop_001"}}' \
    --update-expression "ADD stock :cantidad" \
    --condition-expression "stock >= :min_stock" \
    --expression-attribute-values '{
        ":cantidad": {"N": "-1"},
        ":min_stock": {"N": "1"}
    }'
```

### Sistema de Sesiones de Usuario

```bash
# Crear tabla de sesiones con TTL
aws dynamodb create-table \
    --table-name Sesiones \
    --attribute-definitions AttributeName=session_id,AttributeType=S \
    --key-schema AttributeName=session_id,KeyType=HASH \
    --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5

# Habilitar TTL
aws dynamodb update-time-to-live \
    --table-name Sesiones \
    --time-to-live-specification Enabled=true,AttributeName=expires_at

# Crear sesión
EXPIRY=$(($(date +%s) + 3600))  # Expira en 1 hora
aws dynamodb put-item \
    --table-name Sesiones \
    --item "{
        \"session_id\": {\"S\": \"sess_$(uuidgen)\"},
        \"user_id\": {\"S\": \"user123\"},
        \"created_at\": {\"N\": \"$(date +%s)\"},
        \"expires_at\": {\"N\": \"$EXPIRY\"},
        \"ip_address\": {\"S\": \"192.168.1.100\"},
        \"user_agent\": {\"S\": \"Mozilla/5.0...\"}
    }"

# Validar sesión
aws dynamodb get-item \
    --table-name Sesiones \
    --key '{"session_id": {"S": "sess_abc123"}}' \
    --projection-expression "user_id, expires_at"
```

### Sistema de Logs y Métricas

```bash
# Crear tabla para logs con TTL automático
aws dynamodb create-table \
    --table-name ApplicationLogs \
    --attribute-definitions \
        AttributeName=log_id,AttributeType=S \
        AttributeName=timestamp,AttributeType=N \
        AttributeName=level,AttributeType=S \
    --key-schema \
        AttributeName=log_id,KeyType=HASH \
    --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5 \
    --global-secondary-indexes \
        IndexName=timestamp-level-index,KeySchema=[{AttributeName=timestamp,KeyType=HASH},{AttributeName=level,KeyType=RANGE}],Projection={ProjectionType=ALL},ProvisionedThroughput={ReadCapacityUnits=5,WriteCapacityUnits=5}

# Insertar log entry
aws dynamodb put-item \
    --table-name ApplicationLogs \
    --item "{
        \"log_id\": {\"S\": \"log_$(uuidgen)\"},
        \"timestamp\": {\"N\": \"$(date +%s)\"},
        \"level\": {\"S\": \"ERROR\"},
        \"message\": {\"S\": \"Database connection failed\"},
        \"application\": {\"S\": \"api-gateway\"},
        \"details\": {
            \"M\": {
                \"error_code\": {\"S\": \"DB_CONN_001\"},
                \"retry_count\": {\"N\": \"3\"},
                \"duration_ms\": {\"N\": \"5000\"}
            }
        },
        \"ttl\": {\"N\": \"$(($(date +%s) + 2592000))\"}
    }"

# Consultar logs por tiempo y nivel
aws dynamodb query \
    --table-name ApplicationLogs \
    --index-name timestamp-level-index \
    --key-condition-expression "#ts BETWEEN :start AND :end AND #level = :level" \
    --expression-attribute-names '{
        "#ts": "timestamp",
        "#level": "level"
    }' \
    --expression-attribute-values '{
        ":start": {"N": "'$(($(date +%s) - 3600))'"},
        ":end": {"N": "'$(date +%s)'"},
        ":level": {"S": "ERROR"}
    }'
```
