# Comandos SQL Server (ISQL/SQLCMD)

Este archivo contiene una lista de comandos para SQL Server usando ISQL y SQLCMD, organizados por categoría.

## Herramientas de Línea de Comandos

### sqlcmd (Cliente moderno)

**Descripción:**  
Utilidad de línea de comandos para SQL Server (reemplaza a isql).

**Sintaxis:**
```bash
sqlcmd [opciones]
```

**Opciones comunes:**
- `-S`: Servidor (nombre o IP)
- `-d`: Base de datos
- `-U`: Usuario (autenticación SQL)
- `-P`: Contraseña
- `-E`: Autenticación Windows
- `-i`: Archivo de entrada
- `-o`: Archivo de salida
- `-Q`: Ejecutar consulta y salir
- `-q`: Ejecutar consulta y mantener sesión
- `-b`: Terminar en caso de error
- `-v`: Variable de scripting
- `-W`: Remover espacios finales
- `-s`: Separador de columnas
- `-h`: Encabezados cada N filas

**Ejemplos:**
```bash
# Conectar con autenticación Windows
sqlcmd -S servidor -E

# Conectar con autenticación SQL
sqlcmd -S servidor -U usuario -P contraseña

# Conectar a base de datos específica
sqlcmd -S servidor -d mi_base_datos -E

# Ejecutar consulta específica
sqlcmd -S servidor -E -Q "SELECT @@VERSION"

# Ejecutar script SQL
sqlcmd -S servidor -E -i script.sql -o resultado.txt

# Conectar con instancia nombrada
sqlcmd -S servidor\instancia -E

# Conectar con puerto específico
sqlcmd -S servidor,1433 -E
```

### isql (Cliente legacy)

**Descripción:**  
Utilidad legacy de línea de comandos para SQL Server (obsoleta, usar sqlcmd).

**Sintaxis:**
```bash
isql [opciones]
```

**Opciones comunes:**
- `-S`: Servidor
- `-d`: Base de datos
- `-U`: Usuario
- `-P`: Contraseña
- `-E`: Autenticación Windows
- `-i`: Archivo de entrada
- `-o`: Archivo de salida
- `-Q`: Ejecutar consulta y salir

**Ejemplos:**
```bash
# Conectar con autenticación Windows
isql -S servidor -E

# Conectar con autenticación SQL
isql -S servidor -U usuario -P contraseña

# Ejecutar script
isql -S servidor -E -i script.sql
```

## Comandos SQLCMD Específicos

### Comandos de Conexión

**:CONNECT** - Conectar a servidor
```sql
:CONNECT servidor
:CONNECT servidor -U usuario -P contraseña
```

**:EXIT** o **QUIT** - Salir
```sql
:EXIT
QUIT
```

### Comandos de Archivos

**:r** - Leer archivo SQL
```sql
:r C:\scripts\mi_script.sql
```

**:out** - Redirigir salida
```sql
:out C:\resultados\salida.txt
-- consultas aquí
:out stdout
```

**:!! ** - Ejecutar comando del sistema
```sql
:!! dir
:!! copy archivo1.txt archivo2.txt
```

### Variables de SQLCMD

**:setvar** - Definir variable
```sql
:setvar nombrevar valor
:setvar servidor "MiServidor"
:setvar basedatos "MiBaseDatos"
```

**Usar variables:**
```sql
USE $(basedatos)
SELECT * FROM sys.databases WHERE name = '$(basedatos)'
```

### Comandos de Control

**:ON ERROR** - Control de errores
```sql
:ON ERROR EXIT
:ON ERROR IGNORE
```

**:PERFTRACE** - Traza de rendimiento
```sql
:PERFTRACE C:\trace\rendimiento.txt
```

## Herramientas de Administración

### bcp (Bulk Copy Program)

**Descripción:**  
Utilidad para importar/exportar datos masivamente.

**Sintaxis:**
```bash
bcp {tabla_origen | consulta} {in | out | queryout | format} archivo [opciones]
```

**Opciones comunes:**
- `-S`: Servidor
- `-d`: Base de datos
- `-U`: Usuario
- `-P`: Contraseña
- `-T`: Autenticación Windows
- `-c`: Formato caracter
- `-n`: Formato nativo
- `-t`: Terminador de campo
- `-r`: Terminador de fila
- `-f`: Archivo de formato
- `-F`: Primera fila
- `-L`: Última fila
- `-b`: Tamaño de lote

**Ejemplos:**
```bash
# Exportar tabla a archivo
bcp mi_base_datos.dbo.mi_tabla out datos.txt -c -T -S servidor

# Importar desde archivo
bcp mi_base_datos.dbo.mi_tabla in datos.txt -c -T -S servidor

# Exportar con consulta
bcp "SELECT * FROM mi_base_datos.dbo.mi_tabla WHERE fecha > '2024-01-01'" queryout datos.txt -c -T -S servidor

# Generar archivo de formato
bcp mi_base_datos.dbo.mi_tabla format nul -c -f formato.fmt -T -S servidor

# Importar con separador personalizado
bcp mi_base_datos.dbo.mi_tabla in datos.csv -t"," -r"\n" -T -S servidor
```

### osql (Legacy)

**Descripción:**  
Utilidad legacy (obsoleta, usar sqlcmd).

**Ejemplos:**
```bash
# Conectar y ejecutar consulta
osql -S servidor -E -Q "SELECT @@VERSION"
```

## Comandos T-SQL Específicos de SQL Server

### Información del Sistema

```sql
-- Versión de SQL Server
SELECT @@VERSION;

-- Información del servidor
SELECT SERVERPROPERTY('ProductVersion') AS Version,
       SERVERPROPERTY('ProductLevel') AS ServicePack,
       SERVERPROPERTY('Edition') AS Edition;

-- Bases de datos
SELECT name, database_id, create_date 
FROM sys.databases;

-- Configuración del servidor
SELECT name, value, description 
FROM sys.configurations
ORDER BY name;
```

### Gestión de Bases de Datos

```sql
-- Crear base de datos
CREATE DATABASE mi_base_datos
ON (NAME = 'mi_base_datos_data',
    FILENAME = 'C:\Data\mi_base_datos.mdf',
    SIZE = 100MB,
    MAXSIZE = 1GB,
    FILEGROWTH = 10MB)
LOG ON (NAME = 'mi_base_datos_log',
        FILENAME = 'C:\Logs\mi_base_datos.ldf',
        SIZE = 10MB,
        MAXSIZE = 100MB,
        FILEGROWTH = 1MB);

-- Cambiar propietario
ALTER AUTHORIZATION ON DATABASE::mi_base_datos TO nuevo_propietario;

-- Cambiar modo de recuperación
ALTER DATABASE mi_base_datos SET RECOVERY FULL;

-- Respaldar base de datos
BACKUP DATABASE mi_base_datos 
TO DISK = 'C:\Backups\mi_base_datos.bak';

-- Restaurar base de datos
RESTORE DATABASE mi_base_datos 
FROM DISK = 'C:\Backups\mi_base_datos.bak';
```

### Gestión de Usuarios y Seguridad

```sql
-- Crear login
CREATE LOGIN nuevo_usuario 
WITH PASSWORD = 'Contraseña123!';

-- Crear usuario en base de datos
USE mi_base_datos;
CREATE USER nuevo_usuario FOR LOGIN nuevo_usuario;

-- Agregar a rol
ALTER ROLE db_datareader ADD MEMBER nuevo_usuario;

-- Otorgar permisos específicos
GRANT SELECT, INSERT ON dbo.mi_tabla TO nuevo_usuario;

-- Ver logins
SELECT name, type_desc, create_date 
FROM sys.server_principals 
WHERE type IN ('S', 'U');

-- Ver usuarios de base de datos
SELECT name, type_desc, create_date 
FROM sys.database_principals 
WHERE type IN ('S', 'U');
```

### Información de Tablas y Esquemas

```sql
-- Listar tablas
SELECT TABLE_SCHEMA, TABLE_NAME, TABLE_TYPE
FROM INFORMATION_SCHEMA.TABLES
WHERE TABLE_TYPE = 'BASE TABLE';

-- Estructura de tabla
SELECT COLUMN_NAME, DATA_TYPE, IS_NULLABLE, COLUMN_DEFAULT
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'mi_tabla';

-- Índices de tabla
SELECT i.name AS IndexName, 
       c.name AS ColumnName,
       i.type_desc AS IndexType
FROM sys.indexes i
JOIN sys.index_columns ic ON i.object_id = ic.object_id AND i.index_id = ic.index_id
JOIN sys.columns c ON ic.object_id = c.object_id AND ic.column_id = c.column_id
WHERE i.object_id = OBJECT_ID('dbo.mi_tabla');
```

### Monitoreo y Performance

```sql
-- Procesos activos
SELECT session_id, login_name, host_name, program_name, 
       status, cpu_time, memory_usage, last_request_start_time
FROM sys.dm_exec_sessions
WHERE is_user_process = 1;

-- Consultas en ejecución
SELECT s.session_id, r.status, r.command, 
       SUBSTRING(st.text, (r.statement_start_offset/2)+1,
                ((CASE r.statement_end_offset 
                   WHEN -1 THEN DATALENGTH(st.text)
                   ELSE r.statement_end_offset 
                 END - r.statement_start_offset)/2) + 1) AS statement_text
FROM sys.dm_exec_requests r
JOIN sys.dm_exec_sessions s ON r.session_id = s.session_id
CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS st;

-- Esperas del sistema
SELECT wait_type, waiting_tasks_count, wait_time_ms, 
       max_wait_time_ms, signal_wait_time_ms
FROM sys.dm_os_wait_stats
ORDER BY wait_time_ms DESC;

-- Uso de espacio de bases de datos
SELECT DB_NAME(database_id) AS DatabaseName,
       type_desc AS FileType,
       size * 8 / 1024 AS SizeMB,
       max_size * 8 / 1024 AS MaxSizeMB
FROM sys.master_files;
```

### Jobs y Maintenance

```sql
-- Ver jobs del SQL Agent
SELECT j.name AS JobName, 
       j.enabled, 
       ja.last_run_date,
       ja.last_run_time,
       ja.last_run_outcome
FROM msdb.dbo.sysjobs j
LEFT JOIN msdb.dbo.sysjobactivity ja ON j.job_id = ja.job_id;

-- Ejecutar job
EXEC msdb.dbo.sp_start_job @job_name = 'NombreDelJob';

-- Historial de backups
SELECT s.database_name, s.backup_start_date, s.backup_finish_date,
       s.backup_size/1024/1024 AS BackupSizeMB, s.type, m.physical_device_name
FROM msdb.dbo.backupset s
JOIN msdb.dbo.backupmediafamily m ON s.media_set_id = m.media_set_id
ORDER BY s.backup_start_date DESC;
```

## Scripts de Utilidad

### Backup Completo con T-SQL

```sql
-- Backup full
DECLARE @BackupFile NVARCHAR(255)
SET @BackupFile = 'C:\Backups\' + DB_NAME() + '_' + 
                  CONVERT(VARCHAR, GETDATE(), 112) + '.bak'

BACKUP DATABASE [mi_base_datos] 
TO DISK = @BackupFile
WITH FORMAT, INIT, NAME = 'Backup Completo', 
     SKIP, NOREWIND, NOUNLOAD, STATS = 10;
```

### Verificar Integridad

```sql
-- DBCC CHECKDB para verificar integridad
DBCC CHECKDB('mi_base_datos') WITH NO_INFOMSGS;

-- Verificar tabla específica
DBCC CHECKTABLE('dbo.mi_tabla') WITH NO_INFOMSGS;
```

### Mantenimiento de Índices

```sql
-- Reorganizar índices
ALTER INDEX ALL ON dbo.mi_tabla REORGANIZE;

-- Reconstruir índices
ALTER INDEX ALL ON dbo.mi_tabla REBUILD;

-- Estadísticas de fragmentación
SELECT OBJECT_NAME(object_id) AS TableName,
       index_id, avg_fragmentation_in_percent
FROM sys.dm_db_index_physical_stats(DB_ID(), NULL, NULL, NULL, 'LIMITED')
WHERE avg_fragmentation_in_percent > 10;
```

## Variables de Entorno

- `SQLCMDSERVER`: Servidor por defecto
- `SQLCMDUSER`: Usuario por defecto
- `SQLCMDPASSWORD`: Contraseña por defecto
- `SQLCMDDBNAME`: Base de datos por defecto
- `SQLCMDWORKSTATION`: Nombre de estación de trabajo

## Archivos de Configuración

- `sqlcmd.exe.config`: Configuración de SQLCMD
- Scripts de inicio: archivos .sql ejecutados al iniciar SQLCMD

## Ejemplos de Uso Común

### Script de Backup Automatizado

```bash
# Backup con SQLCMD
sqlcmd -S servidor -E -Q "BACKUP DATABASE mi_base_datos TO DISK = 'C:\Backups\backup_%date:~-4,4%%date:~-10,2%%date:~-7,2%.bak'"
```

### Ejecución de Scripts con Variables

```bash
# Definir variables y ejecutar script
sqlcmd -S servidor -E -v servidor="MiServidor" basedatos="MiBD" -i mantenimiento.sql
```

### Monitoreo Básico

```bash
# Ver procesos activos
sqlcmd -S servidor -E -Q "SELECT COUNT(*) AS Conexiones FROM sys.dm_exec_sessions WHERE is_user_process = 1"

# Ver tamaño de bases de datos
sqlcmd -S servidor -E -Q "SELECT name, (size * 8)/1024 AS SizeMB FROM sys.master_files WHERE type = 0"
```
