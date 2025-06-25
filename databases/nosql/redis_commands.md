# Comandos Redis

Este archivo contiene una lista de comandos Redis para línea de comandos y operaciones de base de datos, organizados por categoría.

## Herramientas de Línea de Comandos

### redis-cli (Cliente de Redis)

**Descripción:**  
Cliente de línea de comandos para interactuar con Redis.

**Sintaxis:**
```bash
redis-cli [opciones] [comando]
```

**Opciones comunes:**
- `-h`: Host del servidor Redis (por defecto localhost)
- `-p`: Puerto del servidor (por defecto 6379)
- `-a`: Contraseña de autenticación
- `-n`: Número de base de datos (0-15)
- `-r`: Repetir comando N veces
- `-i`: Intervalo entre repeticiones
- `-c`: Modo cluster
- `--latency`: Modo latencia
- `--stat`: Estadísticas en tiempo real
- `--bigkeys`: Encontrar claves grandes
- `--scan`: Escanear todas las claves
- `--pattern`: Patrón para filtrar claves
- `--csv`: Salida en formato CSV
- `--raw`: Salida en formato raw
- `--no-raw`: Salida formateada

**Ejemplos:**
```bash
# Conectar a servidor local
redis-cli

# Conectar a servidor remoto
redis-cli -h servidor.example.com -p 6379

# Conectar con contraseña
redis-cli -a mi_contraseña

# Conectar a base de datos específica
redis-cli -n 2

# Ejecutar comando específico
redis-cli GET mi_clave

# Ejecutar comando con repetición
redis-cli -r 100 -i 1 INFO replication

# Modo estadísticas
redis-cli --stat

# Encontrar claves grandes
redis-cli --bigkeys

# Escanear claves con patrón
redis-cli --scan --pattern "user:*"

# Salida en CSV
redis-cli --csv LRANGE lista 0 -1
```

### redis-server

**Descripción:**  
Servidor Redis.

**Ejemplos:**
```bash
# Iniciar servidor con configuración por defecto
redis-server

# Iniciar con archivo de configuración
redis-server /etc/redis/redis.conf

# Iniciar con opciones específicas
redis-server --port 6380 --databases 32
```

### redis-benchmark

**Descripción:**  
Herramienta de benchmark para Redis.

**Ejemplos:**
```bash
# Benchmark básico
redis-benchmark

# Benchmark con parámetros específicos
redis-benchmark -h servidor -p 6379 -n 100000 -c 50

# Benchmark de comandos específicos
redis-benchmark -t set,get -n 100000

# Benchmark con tamaño de datos específico
redis-benchmark -d 100
```

## Comandos Redis por Tipo de Datos

### Comandos Generales

**Información del servidor:**
```redis
# Información general
INFO

# Información específica
INFO server
INFO memory
INFO replication
INFO cluster

# Configuración
CONFIG GET *
CONFIG GET maxmemory
CONFIG SET maxmemory 2gb

# Tiempo del servidor
TIME

# Última vez que se guardó
LASTSAVE

# Guardar base de datos
SAVE
BGSAVE

# Limpiar base de datos
FLUSHDB        # BD actual
FLUSHALL       # Todas las BDs

# Cambiar base de datos
SELECT 0
SELECT 15
```

**Gestión de claves:**
```redis
# Listar todas las claves
KEYS *
KEYS user:*
KEYS *:email

# Escanear claves (más eficiente que KEYS)
SCAN 0
SCAN 0 MATCH user:* COUNT 100

# Verificar existencia
EXISTS mi_clave
EXISTS clave1 clave2 clave3

# Tipo de dato
TYPE mi_clave

# Eliminar claves
DEL clave1
DEL clave1 clave2 clave3
UNLINK clave1  # Eliminación asíncrona

# Renombrar clave
RENAME vieja_clave nueva_clave
RENAMENX vieja_clave nueva_clave  # Solo si no existe

# Expiración
EXPIRE mi_clave 3600        # Expira en 3600 segundos
EXPIREAT mi_clave 1609459200  # Expira en timestamp Unix
TTL mi_clave                # Tiempo restante
PTTL mi_clave               # Tiempo en milisegundos
PERSIST mi_clave            # Quitar expiración

# Información de clave
OBJECT ENCODING mi_clave
MEMORY USAGE mi_clave
```

### Strings (Cadenas)

**Operaciones básicas:**
```redis
# Establecer valor
SET mi_clave "mi_valor"
SET usuario:1:nombre "Juan Pérez"

# Establecer con opciones
SET contador 1 EX 3600        # Con expiración
SET mutex "locked" NX         # Solo si no existe
SET config "value" XX         # Solo si existe

# Obtener valor
GET mi_clave
GET usuario:1:nombre

# Establecer múltiples
MSET clave1 valor1 clave2 valor2 clave3 valor3

# Obtener múltiples
MGET clave1 clave2 clave3

# Establecer y obtener anterior
GETSET mi_clave "nuevo_valor"

# Agregar al final
APPEND mi_clave " - agregado"

# Longitud de string
STRLEN mi_clave

# Substring
GETRANGE mi_clave 0 4
SETRANGE mi_clave 5 "reemplazo"
```

**Operaciones numéricas:**
```redis
# Incrementar
INCR contador
INCRBY contador 5
INCRBYFLOAT precio 10.50

# Decrementar
DECR contador
DECRBY contador 3
```

**Bits:**
```redis
# Operaciones con bits
SETBIT bitmap 0 1
GETBIT bitmap 0
BITCOUNT bitmap
BITOP AND resultado bitmap1 bitmap2
```

### Listas

**Operaciones básicas:**
```redis
# Agregar elementos
LPUSH mi_lista elemento1 elemento2    # Al inicio
RPUSH mi_lista elemento3 elemento4    # Al final

# Obtener elementos
LRANGE mi_lista 0 -1      # Toda la lista
LRANGE mi_lista 0 4       # Primeros 5 elementos
LINDEX mi_lista 0         # Elemento en índice 0
LLEN mi_lista             # Longitud de lista

# Quitar elementos
LPOP mi_lista             # Del inicio
RPOP mi_lista             # Del final
LREM mi_lista 2 "valor"   # Quitar 2 ocurrencias de "valor"
LTRIM mi_lista 0 99       # Mantener solo elementos 0-99

# Modificar elementos
LSET mi_lista 0 "nuevo_valor"

# Insertar elemento
LINSERT mi_lista BEFORE "valor_existente" "nuevo_valor"
LINSERT mi_lista AFTER "valor_existente" "nuevo_valor"
```

**Operaciones de bloqueo:**
```redis
# Pop con bloqueo (esperar hasta que haya elementos)
BLPOP mi_lista 10         # Timeout de 10 segundos
BRPOP mi_lista 0          # Sin timeout

# Mover entre listas
RPOPLPUSH origen destino
BRPOPLPUSH origen destino 10
```

### Sets (Conjuntos)

**Operaciones básicas:**
```redis
# Agregar miembros
SADD mi_set miembro1 miembro2 miembro3

# Obtener miembros
SMEMBERS mi_set           # Todos los miembros
SCARD mi_set              # Número de miembros
SISMEMBER mi_set miembro1 # Verificar membresía
SRANDMEMBER mi_set        # Miembro aleatorio
SRANDMEMBER mi_set 3      # 3 miembros aleatorios

# Quitar miembros
SREM mi_set miembro1 miembro2
SPOP mi_set               # Quitar y retornar aleatorio
SPOP mi_set 2             # Quitar y retornar 2 aleatorios

# Escanear set
SSCAN mi_set 0
SSCAN mi_set 0 MATCH "*patrón*"
```

**Operaciones de conjuntos:**
```redis
# Unión
SUNION set1 set2 set3
SUNIONSTORE resultado set1 set2

# Intersección
SINTER set1 set2
SINTERSTORE resultado set1 set2

# Diferencia
SDIFF set1 set2
SDIFFSTORE resultado set1 set2

# Mover miembro entre sets
SMOVE origen destino miembro
```

### Sorted Sets (Conjuntos Ordenados)

**Operaciones básicas:**
```redis
# Agregar miembros con score
ZADD ranking 100 "jugador1" 200 "jugador2" 150 "jugador3"

# Obtener miembros
ZRANGE ranking 0 -1              # Por índice
ZRANGE ranking 0 -1 WITHSCORES   # Con scores
ZREVRANGE ranking 0 -1           # Orden inverso
ZRANGEBYSCORE ranking 100 200    # Por rango de score
ZREVRANGEBYSCORE ranking 200 100

# Información
ZCARD ranking                    # Número de miembros
ZSCORE ranking "jugador1"        # Score de miembro específico
ZRANK ranking "jugador1"         # Posición (0-based)
ZREVRANK ranking "jugador1"      # Posición inversa
ZCOUNT ranking 100 200           # Contar en rango de score

# Modificar scores
ZINCRBY ranking 50 "jugador1"    # Incrementar score

# Quitar miembros
ZREM ranking "jugador1"
ZREMRANGEBYRANK ranking 0 2      # Por rango de posición
ZREMRANGEBYSCORE ranking 0 100   # Por rango de score
```

**Operaciones de conjuntos ordenados:**
```redis
# Unión
ZUNIONSTORE resultado 2 set1 set2
ZUNIONSTORE resultado 2 set1 set2 WEIGHTS 1 2

# Intersección
ZINTERSTORE resultado 2 set1 set2
ZINTERSTORE resultado 2 set1 set2 AGGREGATE MAX
```

### Hashes

**Operaciones básicas:**
```redis
# Establecer campos
HSET usuario:1 nombre "Juan" edad 30 email "juan@example.com"
HSETNX usuario:1 telefono "123456789"  # Solo si no existe

# Obtener campos
HGET usuario:1 nombre
HMGET usuario:1 nombre edad email      # Múltiples campos
HGETALL usuario:1                      # Todos los campos
HKEYS usuario:1                        # Solo las claves
HVALS usuario:1                        # Solo los valores
HLEN usuario:1                         # Número de campos

# Verificar existencia
HEXISTS usuario:1 telefono

# Eliminar campos
HDEL usuario:1 telefono
HDEL usuario:1 campo1 campo2

# Operaciones numéricas
HINCRBY usuario:1 edad 1
HINCRBYFLOAT usuario:1 saldo 10.50

# Escanear hash
HSCAN usuario:1 0
HSCAN usuario:1 0 MATCH "*email*"
```

### HyperLogLog

**Operaciones:**
```redis
# Agregar elementos
PFADD visitantes_unicos "ip1" "ip2" "ip3"

# Contar elementos únicos aproximados
PFCOUNT visitantes_unicos

# Unir múltiples HLL
PFMERGE resultado hll1 hll2 hll3
```

### Streams

**Operaciones básicas:**
```redis
# Agregar entrada
XADD mi_stream * campo1 valor1 campo2 valor2
XADD mi_stream 1609459200000-0 evento "login" usuario "juan"

# Leer entradas
XRANGE mi_stream - +              # Todas las entradas
XRANGE mi_stream - + COUNT 10     # Primeras 10
XREVRANGE mi_stream + - COUNT 5   # Últimas 5

# Información del stream
XINFO STREAM mi_stream
XLEN mi_stream

# Eliminar entradas
XDEL mi_stream id1 id2
XTRIM mi_stream MAXLEN 1000       # Mantener últimas 1000
```

**Consumer Groups:**
```redis
# Crear grupo de consumidores
XGROUP CREATE mi_stream mi_grupo $ MKSTREAM

# Leer como consumidor
XREADGROUP GROUP mi_grupo consumidor1 COUNT 1 STREAMS mi_stream >

# Información de grupos
XINFO GROUPS mi_stream
XINFO CONSUMERS mi_stream mi_grupo

# Procesar mensajes pendientes
XPENDING mi_stream mi_grupo
XCLAIM mi_stream mi_grupo nuevo_consumidor 60000 id1 id2

# Confirmar procesamiento
XACK mi_stream mi_grupo id1 id2
```

## Comandos de Administración

### Monitoreo

```redis
# Monitorear comandos en tiempo real
MONITOR

# Comandos más lentos
SLOWLOG GET
SLOWLOG GET 10
SLOWLOG RESET

# Estadísticas de comandos
INFO commandstats

# Clientes conectados
CLIENT LIST
CLIENT ID
CLIENT KILL id 123
CLIENT KILL addr 192.168.1.100:12345

# Memoria
MEMORY USAGE mi_clave
MEMORY STATS
MEMORY PURGE
```

### Persistencia

```redis
# Guardar instantánea
SAVE              # Síncrono (bloquea)
BGSAVE           # Asíncrono

# Estado de guardado en background
BGSAVE
LASTSAVE

# Reescribir AOF
BGREWRITEAOF

# Debug y reparación
DEBUG OBJECT mi_clave
DEBUG SEGFAULT   # ¡Solo para testing!
```

### Replicación

```redis
# Configurar como replica
REPLICAOF servidor_maestro 6379
REPLICAOF NO ONE  # Convertir a maestro

# Información de replicación
INFO replication

# Solo lectura (en replicas)
READONLY
READWRITE
```

## Pub/Sub (Publicación/Suscripción)

**Comandos básicos:**
```redis
# Suscribirse a canales
SUBSCRIBE canal1 canal2
PSUBSCRIBE patrón*  # Con patrones

# Publicar mensaje
PUBLISH canal "mi mensaje"

# Cancelar suscripción
UNSUBSCRIBE canal1
PUNSUBSCRIBE patrón*

# Información de pub/sub
PUBSUB CHANNELS       # Listar canales activos
PUBSUB NUMSUB canal1  # Número de suscriptores
PUBSUB NUMPAT         # Número de patrones activos
```

## Transacciones

**Comandos de transacciones:**
```redis
# Iniciar transacción
MULTI

# Comandos de la transacción
SET clave1 valor1
SET clave2 valor2
INCR contador

# Ejecutar transacción
EXEC

# Cancelar transacción
DISCARD

# Watch (optimistic locking)
WATCH clave_importante
MULTI
SET clave_importante nuevo_valor
EXEC

# Deshacer watch
UNWATCH
```

## Scripting con Lua

**Ejecutar scripts:**
```redis
# Evaluar script Lua
EVAL "return redis.call('SET', KEYS[1], ARGV[1])" 1 mi_clave mi_valor

# Script más complejo
EVAL "
local current = redis.call('GET', KEYS[1])
if current == false then
  return redis.call('SET', KEYS[1], ARGV[1])
else
  return current
end
" 1 contador 1

# Cargar script
SCRIPT LOAD "return redis.call('GET', KEYS[1])"
# Retorna SHA1

# Ejecutar script cargado
EVALSHA sha1_del_script 1 mi_clave

# Gestión de scripts
SCRIPT EXISTS sha1_del_script
SCRIPT FLUSH  # Limpiar cache de scripts
SCRIPT KILL   # Matar script en ejecución
```

## Configuración

### Configuración en tiempo real

```redis
# Ver configuración
CONFIG GET *
CONFIG GET save
CONFIG GET maxmemory*

# Modificar configuración
CONFIG SET maxmemory 2gb
CONFIG SET save "900 1 300 10 60 10000"
CONFIG SET requirepass "mi_contraseña"

# Recargar configuración desde archivo
CONFIG RESETSTAT
CONFIG REWRITE  # Escribir cambios al archivo de configuración
```

### Autenticación

```redis
# Autenticarse
AUTH contraseña

# Con usuario y contraseña (Redis 6+)
AUTH usuario contraseña

# Gestión de usuarios (Redis 6+)
ACL LIST
ACL SETUSER nuevo_usuario
ACL DELUSER usuario
ACL WHOAMI
```

## Herramientas de Administración

### redis-check-aof

```bash
# Verificar archivo AOF
redis-check-aof /var/lib/redis/appendonly.aof

# Reparar archivo AOF
redis-check-aof --fix /var/lib/redis/appendonly.aof
```

### redis-check-rdb

```bash
# Verificar archivo RDB
redis-check-rdb /var/lib/redis/dump.rdb
```

### redis-sentinel

```bash
# Iniciar Sentinel
redis-sentinel /etc/redis/sentinel.conf
```

## Archivos de Configuración

### redis.conf básico

```conf
# Configuración básica de Redis

# Red
port 6379
bind 127.0.0.1
timeout 0
tcp-keepalive 300

# General
daemonize yes
pidfile /var/run/redis/redis-server.pid
loglevel notice
logfile /var/log/redis/redis-server.log
databases 16

# Persistencia RDB
save 900 1      # Guardar si al menos 1 clave cambió en 900 seg
save 300 10     # Guardar si al menos 10 claves cambiaron en 300 seg
save 60 10000   # Guardar si al menos 10000 claves cambiaron en 60 seg
rdbcompression yes
dbfilename dump.rdb
dir /var/lib/redis/

# Persistencia AOF
appendonly yes
appendfilename "appendonly.aof"
appendfsync everysec

# Memoria
maxmemory 2gb
maxmemory-policy allkeys-lru

# Seguridad
requirepass mi_contraseña_segura

# Replicación
# replicaof masterhost 6379
# masterauth master_password
```

## Scripts de Utilidad

### Script de Backup

```bash
#!/bin/bash
# backup_redis.sh

DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_DIR="/backups/redis"
REDIS_DIR="/var/lib/redis"

mkdir -p $BACKUP_DIR

# Forzar guardado
redis-cli BGSAVE

# Esperar a que termine el guardado
while [ $(redis-cli LASTSAVE) -eq $(redis-cli LASTSAVE) ]; do
  sleep 1
done

# Copiar archivo RDB
cp $REDIS_DIR/dump.rdb $BACKUP_DIR/dump_$DATE.rdb

# Copiar archivo AOF si existe
if [ -f $REDIS_DIR/appendonly.aof ]; then
  cp $REDIS_DIR/appendonly.aof $BACKUP_DIR/appendonly_$DATE.aof
fi

# Comprimir backups
tar -czf $BACKUP_DIR/redis_backup_$DATE.tar.gz $BACKUP_DIR/*_$DATE.*

# Limpiar archivos sin comprimir
rm $BACKUP_DIR/*_$DATE.rdb $BACKUP_DIR/*_$DATE.aof 2>/dev/null

echo "Backup completado: redis_backup_$DATE.tar.gz"
```

### Script de Monitoreo

```bash
#!/bin/bash
# monitor_redis.sh

echo "=== MONITOREO REDIS ==="
echo "Fecha: $(date)"

echo -e "\n--- INFORMACIÓN GENERAL ---"
redis-cli INFO server | grep -E "(redis_version|uptime_in_seconds|process_id)"

echo -e "\n--- MEMORIA ---"
redis-cli INFO memory | grep -E "(used_memory|used_memory_human|maxmemory)"

echo -e "\n--- ESTADÍSTICAS ---"
redis-cli INFO stats | grep -E "(total_commands_processed|instantaneous_ops_per_sec|keyspace_hits|keyspace_misses)"

echo -e "\n--- CLIENTES ---"
redis-cli INFO clients | grep -E "(connected_clients|blocked_clients)"

echo -e "\n--- PERSISTENCIA ---"
redis-cli INFO persistence | grep -E "(rdb_last_save_time|aof_enabled)"

echo -e "\n--- KEYSPACE ---"
redis-cli INFO keyspace

echo -e "\n--- COMANDOS MÁS LENTOS ---"
redis-cli SLOWLOG GET 5
```

### Script de Limpieza

```bash
#!/bin/bash
# cleanup_redis.sh

echo "Iniciando limpieza de Redis..."

# Eliminar claves expiradas manualmente
redis-cli --scan --pattern "*:temp:*" | xargs -r redis-cli DEL

# Eliminar claves antiguas (ejemplo para sesiones)
redis-cli --scan --pattern "session:*" | while read key; do
  ttl=$(redis-cli TTL "$key")
  if [ "$ttl" -eq -1 ]; then  # Sin expiración
    echo "Eliminando clave sin TTL: $key"
    redis-cli DEL "$key"
  fi
done

# Estadísticas de memoria después de limpieza
echo -e "\n--- MEMORIA DESPUÉS DE LIMPIEZA ---"
redis-cli INFO memory | grep -E "(used_memory_human|maxmemory_human)"

echo "Limpieza completada."
```

## Ejemplos de Uso Común

### Sistema de Cache

```redis
# Cache de usuario
SET user:1001 '{"name":"Juan","email":"juan@example.com"}' EX 3600

# Cache con namespace
SET cache:product:1001 '{"name":"Laptop","price":999.99}' EX 1800

# Invalidar cache por patrón
EVAL "
for i=1,#KEYS do
  redis.call('DEL', KEYS[i])
end
return #KEYS
" 0 cache:product:*
```

### Contador de Rate Limiting

```redis
# Rate limiting simple
SET rate_limit:user:1001 1 EX 60
INCR rate_limit:user:1001

# Rate limiting deslizante con sorted set
ZADD rate_limit:user:1001:sliding $(date +%s) "$(date +%s)"
ZREMRANGEBYSCORE rate_limit:user:1001:sliding 0 $(($(date +%s) - 3600))
ZCARD rate_limit:user:1001:sliding
```

### Sistema de Colas

```redis
# Cola simple FIFO
LPUSH cola:emails '{"to":"user@example.com","subject":"Bienvenido"}'
RPOP cola:emails

# Cola con prioridad usando sorted sets
ZADD cola:prioritaria 1 "tarea_baja_prioridad"
ZADD cola:prioritaria 10 "tarea_alta_prioridad"
ZPOPMAX cola:prioritaria  # Redis 5.0+

# Cola con workers usando listas bloqueantes
BRPOP cola:trabajos 0  # Worker esperando trabajos
```

### Sistema de Sesiones

```redis
# Crear sesión
HSET session:abc123 user_id 1001 login_time 1609459200 last_activity 1609459200
EXPIRE session:abc123 1800

# Actualizar actividad
HSET session:abc123 last_activity $(date +%s)
EXPIRE session:abc123 1800

# Verificar sesión válida
EXISTS session:abc123
HGETALL session:abc123
```

### Métricas y Contadores

```redis
# Contador de visitas diarias
INCR stats:visits:$(date +%Y-%m-%d)
EXPIRE stats:visits:$(date +%Y-%m-%d) 2592000  # 30 días

# Métricas por minuto usando HyperLogLog
PFADD unique_visitors:$(date +%Y-%m-%d:%H:%M) user_id_1001
PFCOUNT unique_visitors:$(date +%Y-%m-%d:%H:%M)

# Top productos usando sorted set
ZINCRBY top_products 1 "producto_1001"
ZREVRANGE top_products 0 9 WITHSCORES  # Top 10
```
