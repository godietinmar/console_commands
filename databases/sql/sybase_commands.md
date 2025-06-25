# Comandos Sybase ASE (ISQL)

Este archivo contiene una lista de comandos para Sybase Adaptive Server Enterprise usando ISQL, organizados por categoría.

## Herramientas de Línea de Comandos

### isql (Cliente de Sybase ASE)

**Descripción:**  
Utilidad de línea de comandos interactiva para Sybase ASE.

**Sintaxis:**
```bash
isql [opciones]
```

**Opciones comunes:**
- `-S`: Servidor
- `-U`: Usuario
- `-P`: Contraseña
- `-D`: Base de datos
- `-i`: Archivo de entrada
- `-o`: Archivo de salida
- `-e`: Mostrar comandos
- `-v`: Modo verbose
- `-w`: Ancho de línea
- `-s`: Separador de columnas
- `-h`: Ocultar encabezados
- `-n`: Remover numeración
- `-b`: Abortar en error
- `-X`: Usar encriptación
- `-z`: Cambiar contraseña
- `-J`: Charset del cliente
- `-I`: Directorio de interfaces
- `-H`: Hostname

**Ejemplos:**
```bash
# Conectar a servidor Sybase
isql -S SYBASE -U sa -P contraseña

# Conectar con base de datos específica
isql -S SYBASE -U usuario -P contraseña -D mi_base_datos

# Ejecutar script SQL
isql -S SYBASE -U sa -P contraseña -i script.sql -o resultado.txt

# Conectar con charset específico
isql -S SYBASE -U usuario -P contraseña -J utf8

# Conectar con archivo de interfaces personalizado
isql -S SYBASE -U usuario -P contraseña -I /opt/sybase/interfaces

# Conectar con hostname específico
isql -S SYBASE -U usuario -P contraseña -H workstation01

# Conectar con ancho de línea personalizado
isql -S SYBASE -U usuario -P contraseña -w 132
```

### sqlloc (Localización de servidores)

**Descripción:**  
Utilidad para localizar servidores Sybase en la red.

**Ejemplos:**
```bash
# Localizar servidores Sybase
sqlloc

# Localizar con timeout específico
sqlloc -t 30
```

### bcp (Bulk Copy Program)

**Descripción:**  
Utilidad para transferencia masiva de datos en Sybase ASE.

**Sintaxis:**
```bash
bcp [base_datos.][propietario.]tabla {in | out} archivo [opciones]
```

**Opciones comunes:**
- `-S`: Servidor
- `-U`: Usuario
- `-P`: Contraseña
- `-c`: Formato carácter
- `-n`: Formato nativo
- `-t`: Terminador de campo
- `-r`: Terminador de registro
- `-f`: Archivo de formato
- `-F`: Primera fila
- `-L`: Última fila
- `-b`: Tamaño de lote
- `-e`: Archivo de errores
- `-T`: Texto truncado
- `-E`: Mantener valores de identidad

**Ejemplos:**
```bash
# Exportar tabla
bcp mi_base_datos.dbo.mi_tabla out datos.txt -c -S SYBASE -U sa -P contraseña

# Importar datos
bcp mi_base_datos.dbo.mi_tabla in datos.txt -c -S SYBASE -U sa -P contraseña

# Exportar con formato nativo
bcp mi_base_datos.dbo.mi_tabla out datos.dat -n -S SYBASE -U sa -P contraseña

# Importar con separador personalizado
bcp mi_base_datos.dbo.mi_tabla in datos.csv -c -t"," -S SYBASE -U sa -P contraseña

# Exportar con archivo de errores
bcp mi_base_datos.dbo.mi_tabla out datos.txt -c -e errores.txt -S SYBASE -U sa -P contraseña
```

## Comandos ISQL Específicos

### Comandos de Control

**go** - Ejecutar lote de comandos
```sql
SELECT @@version
go
```

**reset** - Limpiar buffer
```sql
reset
```

**vi** - Editar comando en editor
```sql
vi
```

**!!** - Ejecutar comando del sistema
```sql
!! ls -la
!! ps -ef | grep sybase
```

### Comandos de Configuración

**:r** - Leer archivo
```sql
:r /path/to/script.sql
go
```

## Comandos T-SQL Específicos de Sybase ASE

### Información del Sistema

```sql
-- Versión de Sybase ASE
SELECT @@version
go

-- Información del servidor
SELECT @@servername, @@version
go

-- Bases de datos disponibles
SELECT name FROM sysdatabases
go

-- Usuarios en base de datos actual
SELECT name FROM sysusers
go

-- Tablas de usuario
SELECT name FROM sysobjects WHERE type = 'U'
go

-- Configuración del servidor
SELECT name, value FROM sysconfigures
go
```

### Gestión de Bases de Datos

```sql
-- Crear base de datos
CREATE DATABASE mi_base_datos
ON mi_device = 100
LOG ON mi_log_device = 20
go

-- Cambiar a base de datos
USE mi_base_datos
go

-- Información de dispositivos
SELECT name, phyname, size FROM sysdevices
go

-- Información de segmentos
SELECT name FROM syssegments
go

-- Uso de espacio en base de datos
sp_spaceused
go

-- Uso de espacio de tabla específica
sp_spaceused mi_tabla
go
```

### Gestión de Usuarios y Permisos

```sql
-- Crear login
sp_addlogin nuevo_usuario, contraseña
go

-- Crear usuario en base de datos
sp_adduser nuevo_usuario
go

-- Agregar a grupo
sp_addgroup mi_grupo
go
sp_changegroup mi_grupo, nuevo_usuario
go

-- Otorgar permisos
GRANT SELECT, INSERT ON mi_tabla TO nuevo_usuario
go

-- Revocar permisos
REVOKE INSERT ON mi_tabla FROM nuevo_usuario
go

-- Ver permisos de tabla
sp_helprotect mi_tabla
go

-- Cambiar propietario de objeto
sp_changeobjectowner "mi_tabla", "nuevo_propietario"
go
```

### Información de Tablas y Objetos

```sql
-- Describir tabla
sp_help mi_tabla
go

-- Información de columnas
sp_columns mi_tabla
go

-- Información de índices
sp_helpindex mi_tabla
go

-- Información de llaves foráneas
sp_helpconstraint mi_tabla
go

-- Procedimientos almacenados
SELECT name FROM sysobjects WHERE type = 'P'
go

-- Triggers
SELECT name FROM sysobjects WHERE type = 'TR'
go

-- Vistas
SELECT name FROM sysobjects WHERE type = 'V'
go
```

### Monitoreo y Performance

```sql
-- Procesos activos
sp_who
go

-- Información detallada de procesos
sp_who2
go

-- Locks del sistema
sp_lock
go

-- Estadísticas de I/O
sp_sysmon "00:01:00"
go

-- Información de caché
sp_cacheconfig
go

-- Estadísticas de tabla
UPDATE STATISTICS mi_tabla
go

-- Verificar consistencia
DBCC CHECKTABLE(mi_tabla)
go

-- Verificar base de datos
DBCC CHECKDB(mi_base_datos)
go
```

### Backup y Recovery

```sql
-- Dump de base de datos
DUMP DATABASE mi_base_datos TO "/backups/mi_base_datos.dump"
go

-- Dump de log de transacciones
DUMP TRANSACTION mi_base_datos TO "/backups/mi_base_datos_log.dump"
go

-- Load de base de datos
LOAD DATABASE mi_base_datos FROM "/backups/mi_base_datos.dump"
go

-- Load de log de transacciones
LOAD TRANSACTION mi_base_datos FROM "/backups/mi_base_datos_log.dump"
go

-- Verificar dumps
LOAD DATABASE mi_base_datos FROM "/backups/mi_base_datos.dump" 
WITH HEADERONLY
go
```

### Gestión de Dispositivos

```sql
-- Crear dispositivo
DISK INIT 
NAME = "mi_device",
PHYSNAME = "/sybase/data/mi_device.dat",
SIZE = 100
go

-- Información de dispositivos
sp_helpdevice
go

-- Extender base de datos
ALTER DATABASE mi_base_datos
ON mi_device = 50
go

-- Crear dispositivo de log
DISK INIT 
NAME = "mi_log_device",
PHYSNAME = "/sybase/logs/mi_log_device.dat",
SIZE = 50
go
```

### Procedimientos del Sistema Comunes

```sql
-- Ayuda general
sp_help
go

-- Ayuda de procedimiento
sp_help sp_who
go

-- Configuración del servidor
sp_configure
go

-- Información de servidor
sp_server_info
go

-- Estadísticas de motor
sp_monitor
go

-- Información de memoria
sp_monitorconfig "memory"
go

-- Información de tempdb
sp_tempdb
go
```

## Herramientas Adicionales

### defncopy

**Descripción:**  
Extraer definiciones de objetos de base de datos.

**Ejemplos:**
```bash
# Extraer definición de tabla
defncopy -S SYBASE -U sa -P contraseña -D mi_base_datos out mi_tabla.sql

# Extraer todos los procedimientos
defncopy -S SYBASE -U sa -P contraseña -D mi_base_datos -P out procs.sql

# Extraer triggers
defncopy -S SYBASE -U sa -P contraseña -D mi_base_datos -T out triggers.sql
```

### ddlgen

**Descripción:**  
Generar scripts DDL para objetos de base de datos.

**Ejemplos:**
```bash
# Generar DDL para tabla
ddlgen -S SYBASE -U sa -P contraseña -D mi_base_datos -T mi_tabla

# Generar DDL para base de datos completa
ddlgen -S SYBASE -U sa -P contraseña -D mi_base_datos
```

### optdiag

**Descripción:**  
Generar estadísticas de optimización.

**Ejemplos:**
```bash
# Generar estadísticas
optdiag -S SYBASE -U sa -P contraseña -D mi_base_datos statistics mi_tabla
```

## Configuración de Conexión

### Archivo interfaces

**Ubicación típica:** `/opt/sybase/interfaces` o `$SYBASE/interfaces`

**Formato:**
```
SYBASE
    master tcp ether hostname 5000
    query tcp ether hostname 5000
```

### Variables de Entorno

- `SYBASE`: Directorio de instalación de Sybase
- `SYBASE_ASE`: Directorio de ASE
- `DSQUERY`: Servidor por defecto
- `LANG`: Idioma del cliente
- `LC_ALL`: Configuración regional

## Scripts de Utilidad

### Backup Automatizado

```sql
-- Script de backup completo
DECLARE @backup_file VARCHAR(255)
SELECT @backup_file = "/backups/mi_base_datos_" + 
                      CONVERT(VARCHAR, GETDATE(), 112) + ".dump"

DUMP DATABASE mi_base_datos TO @backup_file
go

-- Verificar backup
LOAD DATABASE mi_base_datos FROM @backup_file WITH HEADERONLY
go
```

### Mantenimiento de Estadísticas

```sql
-- Actualizar estadísticas de todas las tablas
DECLARE @table_name VARCHAR(30)
DECLARE table_cursor CURSOR FOR 
    SELECT name FROM sysobjects WHERE type = 'U'

OPEN table_cursor
FETCH table_cursor INTO @table_name

WHILE @@sqlstatus = 0
BEGIN
    PRINT "Actualizando estadísticas para: " + @table_name
    UPDATE STATISTICS @table_name
    FETCH table_cursor INTO @table_name
END

CLOSE table_cursor
DEALLOCATE CURSOR table_cursor
go
```

### Verificación de Integridad

```sql
-- Verificar integridad de todas las tablas
DECLARE @table_name VARCHAR(30)
DECLARE table_cursor CURSOR FOR 
    SELECT name FROM sysobjects WHERE type = 'U'

OPEN table_cursor
FETCH table_cursor INTO @table_name

WHILE @@sqlstatus = 0
BEGIN
    PRINT "Verificando tabla: " + @table_name
    DBCC CHECKTABLE(@table_name)
    FETCH table_cursor INTO @table_name
END

CLOSE table_cursor
DEALLOCATE CURSOR table_cursor
go
```

## Ejemplos de Uso Común

### Conexión y Consulta Básica

```bash
# Conectar y ejecutar consulta
isql -S SYBASE -U sa -P contraseña << EOF
SELECT @@version
go
SELECT name FROM sysdatabases
go
EOF
```

### Transferencia de Datos

```bash
# Exportar datos
bcp mi_base_datos.dbo.mi_tabla out datos.txt -c -S SYBASE -U sa -P contraseña

# Importar a otra base de datos
bcp nueva_base_datos.dbo.mi_tabla in datos.txt -c -S SYBASE -U sa -P contraseña
```

### Monitoreo Básico

```bash
# Script de monitoreo
isql -S SYBASE -U sa -P contraseña << EOF
sp_who
go
sp_lock
go
SELECT COUNT(*) FROM master..sysprocesses WHERE status != 'sleeping'
go
EOF
```
