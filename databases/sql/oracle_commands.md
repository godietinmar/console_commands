# Comandos Oracle (SQL*Plus)

Este archivo contiene una lista de comandos para Oracle Database usando SQL*Plus y otras herramientas, organizados por categoría.

## Herramientas de Línea de Comandos

### sqlplus (Cliente principal)

**Descripción:**  
Cliente de línea de comandos principal para Oracle Database.

**Sintaxis:**
```bash
sqlplus [opciones] [logon] [@script]
```

**Formas de conexión:**
- `username/password@connect_identifier`
- `username/password@//host:port/service_name`
- `username/password@host:port:SID`
- `/nolog` - Iniciar sin conectar
- `/ as sysdba` - Conexión privilegiada

**Opciones comunes:**
- `-S`: Modo silencioso
- `-L`: Solo un intento de conexión
- `-R 2`: Nivel de restricción
- `-M "markup"`: Formato de salida
- `-NOLOGINTIME`: No mostrar tiempo de login

**Ejemplos:**
```bash
# Conectar con usuario normal
sqlplus usuario/contraseña@servidor

# Conectar como SYSDBA
sqlplus sys/contraseña@servidor as sysdba

# Conectar con Easy Connect
sqlplus usuario/contraseña@//servidor:1521/servicio

# Conectar y ejecutar script
sqlplus usuario/contraseña@servidor @script.sql

# Iniciar sin conexión
sqlplus /nolog

# Modo silencioso
sqlplus -S usuario/contraseña@servidor

# Conectar con autenticación OS
sqlplus / as sysdba
```

### sqlldr (SQL*Loader)

**Descripción:**  
Herramienta para carga masiva de datos desde archivos externos.

**Sintaxis:**
```bash
sqlldr [username/password@connect_identifier] [opciones]
```

**Opciones comunes:**
- `CONTROL`: Archivo de control
- `DATA`: Archivo de datos
- `LOG`: Archivo de log
- `BAD`: Archivo de registros rechazados
- `DISCARD`: Archivo de registros descartados
- `ERRORS`: Número máximo de errores
- `ROWS`: Número de filas por commit
- `BINDSIZE`: Tamaño del buffer
- `READSIZE`: Tamaño de lectura
- `DIRECT`: Carga directa (true/false)
- `PARALLEL`: Carga paralela (true/false)

**Ejemplos:**
```bash
# Carga básica
sqlldr usuario/contraseña@servidor control=datos.ctl

# Carga con parámetros específicos
sqlldr usuario/contraseña@servidor control=datos.ctl log=carga.log bad=errores.bad errors=100

# Carga directa
sqlldr usuario/contraseña@servidor control=datos.ctl direct=true

# Carga paralela
sqlldr usuario/contraseña@servidor control=datos.ctl parallel=true
```

### exp/expdp (Export)

**Descripción:**  
Herramientas para exportar datos y metadatos de Oracle.

**exp (Legacy):**
```bash
# Exportar base de datos completa
exp usuario/contraseña@servidor full=y file=full_export.dmp

# Exportar esquema específico
exp usuario/contraseña@servidor owner=mi_esquema file=esquema.dmp

# Exportar tablas específicas
exp usuario/contraseña@servidor tables=tabla1,tabla2 file=tablas.dmp
```

**expdp (Data Pump - Recomendado):**
```bash
# Exportar esquema completo
expdp usuario/contraseña@servidor schemas=mi_esquema directory=DATA_PUMP_DIR dumpfile=esquema.dmp

# Exportar tabla específica
expdp usuario/contraseña@servidor tables=mi_esquema.mi_tabla directory=DATA_PUMP_DIR dumpfile=tabla.dmp

# Exportar base de datos completa
expdp system/contraseña@servidor full=y directory=DATA_PUMP_DIR dumpfile=full_db.dmp

# Exportar con compresión
expdp usuario/contraseña@servidor schemas=mi_esquema directory=DATA_PUMP_DIR dumpfile=esquema.dmp compression=all
```

### imp/impdp (Import)

**Descripción:**  
Herramientas para importar datos y metadatos a Oracle.

**imp (Legacy):**
```bash
# Importar archivo completo
imp usuario/contraseña@servidor full=y file=full_export.dmp

# Importar esquema específico
imp usuario/contraseña@servidor fromuser=origen_esquema touser=destino_esquema file=esquema.dmp
```

**impdp (Data Pump - Recomendado):**
```bash
# Importar esquema completo
impdp usuario/contraseña@servidor schemas=mi_esquema directory=DATA_PUMP_DIR dumpfile=esquema.dmp

# Importar con mapeo de esquema
impdp usuario/contraseña@servidor remap_schema=origen:destino directory=DATA_PUMP_DIR dumpfile=esquema.dmp

# Importar solo metadatos
impdp usuario/contraseña@servidor content=metadata_only directory=DATA_PUMP_DIR dumpfile=esquema.dmp
```

## Comandos SQL*Plus Específicos

### Comandos de Conexión

**CONNECT** - Conectar a base de datos
```sql
CONNECT usuario/contraseña@servidor
CONNECT / AS SYSDBA
CONNECT usuario/contraseña@//servidor:1521/servicio
```

**DISCONNECT** - Desconectar
```sql
DISCONNECT
```

**EXIT** o **QUIT** - Salir
```sql
EXIT
QUIT
```

### Comandos de Formato

**SET** - Configurar opciones de sesión
```sql
-- Configurar ancho de página
SET PAGESIZE 50
SET LINESIZE 120

-- Mostrar/ocultar encabezados
SET HEADING ON
SET HEADING OFF

-- Configurar formato de números
SET NUMFORMAT 999,999.99

-- Mostrar tiempo de ejecución
SET TIMING ON

-- Mostrar comandos SQL
SET ECHO ON

-- Configurar separador
SET COLSEP |

-- Ocultar feedback
SET FEEDBACK OFF

-- Configurar formato de fecha
ALTER SESSION SET NLS_DATE_FORMAT = 'DD/MM/YYYY HH24:MI:SS';
```

**COLUMN** - Formatear columnas
```sql
-- Establecer ancho de columna
COLUMN nombre_columna FORMAT A20

-- Formato numérico
COLUMN salario FORMAT 999,999.99

-- Encabezado personalizado
COLUMN emp_name HEADING 'Employee Name'

-- Alinear columna
COLUMN cantidad JUSTIFY RIGHT
```

**BREAK** - Configurar saltos y totales
```sql
-- Salto por departamento
BREAK ON departamento

-- Salto con total
BREAK ON departamento SKIP 1 ON REPORT
COMPUTE SUM OF salario ON departamento
COMPUTE AVG OF salario ON REPORT
```

### Comandos de Archivos

**SPOOL** - Guardar salida en archivo
```sql
SPOOL resultado.txt
SELECT * FROM empleados;
SPOOL OFF
```

**@** o **START** - Ejecutar script
```sql
@mi_script.sql
START mi_script.sql

-- Con parámetros
@mi_script.sql parametro1 parametro2
```

**@@** - Ejecutar script en mismo directorio
```sql
@@script_local.sql
```

**SAVE** - Guardar buffer SQL
```sql
SAVE mi_consulta.sql
SAVE mi_consulta.sql REPLACE
```

**GET** - Cargar archivo al buffer
```sql
GET mi_consulta.sql
GET mi_consulta.sql LIST
```

**EDIT** - Editar buffer o archivo
```sql
EDIT
EDIT mi_script.sql
```

### Comandos de Buffer

**LIST** - Mostrar buffer SQL
```sql
LIST
L
```

**RUN** - Ejecutar buffer
```sql
RUN
R
/
```

**CLEAR** - Limpiar buffer
```sql
CLEAR BUFFER
CLEAR BREAKS
CLEAR COLUMNS
```

### Comandos de Información

**DESCRIBE** - Describir objeto
```sql
DESCRIBE mi_tabla
DESC mi_tabla
DESCRIBE mi_paquete.mi_procedimiento
```

**SHOW** - Mostrar configuración
```sql
SHOW USER
SHOW RELEASE
SHOW PARAMETERS
SHOW SGA
SHOW ALL
```

**HOST** - Ejecutar comando del sistema
```sql
HOST ls -la
HOST !ps -ef | grep oracle
```

## Comandos SQL Específicos de Oracle

### Información del Sistema

```sql
-- Versión de Oracle
SELECT * FROM v$version;

-- Información de instancia
SELECT instance_name, status, startup_time 
FROM v$instance;

-- Parámetros de inicialización
SELECT name, value FROM v$parameter 
WHERE name LIKE '%memory%';

-- SGA información
SELECT * FROM v$sga;

-- Tablespaces
SELECT tablespace_name, status, contents 
FROM dba_tablespaces;

-- Datafiles
SELECT file_name, tablespace_name, bytes/1024/1024 AS MB
FROM dba_data_files;
```

### Gestión de Usuarios y Esquemas

```sql
-- Crear usuario
CREATE USER nuevo_usuario 
IDENTIFIED BY contraseña
DEFAULT TABLESPACE users
TEMPORARY TABLESPACE temp;

-- Otorgar privilegios
GRANT CONNECT, RESOURCE TO nuevo_usuario;
GRANT DBA TO nuevo_usuario;

-- Otorgar cuota en tablespace
ALTER USER nuevo_usuario QUOTA 100M ON users;

-- Cambiar contraseña
ALTER USER nuevo_usuario IDENTIFIED BY nueva_contraseña;

-- Ver usuarios
SELECT username, account_status, created 
FROM dba_users;

-- Ver privilegios de usuario
SELECT * FROM dba_role_privs WHERE grantee = 'USUARIO';
SELECT * FROM dba_sys_privs WHERE grantee = 'USUARIO';
```

### Información de Objetos

```sql
-- Tablas de usuario
SELECT table_name FROM user_tables;
SELECT table_name, owner FROM all_tables WHERE owner = 'MI_ESQUEMA';

-- Estructura de tabla
SELECT column_name, data_type, nullable, data_default
FROM user_tab_columns 
WHERE table_name = 'MI_TABLA';

-- Índices
SELECT index_name, table_name, uniqueness 
FROM user_indexes;

-- Constraints
SELECT constraint_name, constraint_type, table_name
FROM user_constraints;

-- Procedimientos y funciones
SELECT object_name, object_type, status 
FROM user_objects 
WHERE object_type IN ('PROCEDURE', 'FUNCTION', 'PACKAGE');

-- Secuencias
SELECT sequence_name, min_value, max_value, increment_by
FROM user_sequences;
```

### Monitoreo y Performance

```sql
-- Sesiones activas
SELECT sid, serial#, username, status, program, machine
FROM v$session 
WHERE username IS NOT NULL;

-- Consultas en ejecución
SELECT s.sid, s.serial#, s.username, q.sql_text
FROM v$session s, v$sql q
WHERE s.sql_address = q.address
  AND s.username IS NOT NULL;

-- Wait events
SELECT event, total_waits, time_waited, average_wait
FROM v$system_event
ORDER BY time_waited DESC;

-- Top SQL por tiempo de ejecución
SELECT sql_text, executions, elapsed_time, cpu_time
FROM v$sql
ORDER BY elapsed_time DESC;

-- Uso de tablespace
SELECT tablespace_name,
       ROUND(used_mb, 2) AS used_mb,
       ROUND(free_mb, 2) AS free_mb,
       ROUND(total_mb, 2) AS total_mb,
       ROUND((used_mb/total_mb)*100, 2) AS pct_used
FROM (
  SELECT tablespace_name,
         SUM(bytes)/1024/1024 AS total_mb
  FROM dba_data_files
  GROUP BY tablespace_name
) total,
(
  SELECT tablespace_name,
         SUM(bytes)/1024/1024 AS free_mb
  FROM dba_free_space
  GROUP BY tablespace_name
) free,
(
  SELECT tablespace_name,
         total_mb - free_mb AS used_mb
  FROM total, free
  WHERE total.tablespace_name = free.tablespace_name
) used
WHERE total.tablespace_name = free.tablespace_name;
```

### Backup y Recovery

```sql
-- Información de backup
SELECT * FROM v$backup;

-- Archivelog status
SELECT name, sequence#, first_time, completion_time
FROM v$archived_log
ORDER BY sequence# DESC;

-- RMAN backup information
SELECT start_time, end_time, input_bytes, output_bytes, status
FROM v$rman_backup_job_details
ORDER BY start_time DESC;

-- Flashback query
SELECT * FROM mi_tabla 
AS OF TIMESTAMP (SYSTIMESTAMP - INTERVAL '1' HOUR);

-- Recycle bin
SELECT object_name, original_name, type, droptime
FROM recyclebin;

-- Restore from recycle bin
FLASHBACK TABLE mi_tabla TO BEFORE DROP;
```

### PL/SQL Básico

```sql
-- Bloque PL/SQL básico
DECLARE
    v_variable VARCHAR2(100);
BEGIN
    SELECT nombre INTO v_variable 
    FROM empleados 
    WHERE id = 1;
    
    DBMS_OUTPUT.PUT_LINE('Nombre: ' || v_variable);
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No se encontró el empleado');
END;
/

-- Procedimiento almacenado
CREATE OR REPLACE PROCEDURE obtener_empleado(p_id IN NUMBER)
IS
    v_nombre VARCHAR2(100);
BEGIN
    SELECT nombre INTO v_nombre 
    FROM empleados 
    WHERE id = p_id;
    
    DBMS_OUTPUT.PUT_LINE('Empleado: ' || v_nombre);
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Empleado no encontrado');
END;
/

-- Ejecutar procedimiento
EXEC obtener_empleado(1);
```

## Herramientas Adicionales

### RMAN (Recovery Manager)

**Descripción:**  
Herramienta de backup y recovery de Oracle.

**Ejemplos:**
```bash
# Conectar a RMAN
rman target /
rman target sys/contraseña@servidor

# Backup completo
BACKUP DATABASE;

# Backup incremental
BACKUP INCREMENTAL LEVEL 1 DATABASE;

# Backup de archivelog
BACKUP ARCHIVELOG ALL;

# Lista de backups
LIST BACKUP;

# Restore y recover
RESTORE DATABASE;
RECOVER DATABASE;
```

### adrci (Automatic Diagnostic Repository Command Interpreter)

**Descripción:**  
Herramienta para gestionar logs y diagnósticos.

**Ejemplos:**
```bash
# Iniciar adrci
adrci

# Comandos dentro de adrci
show homes
set homepath diag/rdbms/orcl/orcl
show alert
show incident
purge -age 30
```

### dbca (Database Configuration Assistant)

**Descripción:**  
Asistente gráfico para crear/configurar bases de datos.

**Modo silencioso:**
```bash
dbca -silent -createDatabase \
     -templateName General_Purpose.dbc \
     -gdbname orcl \
     -sid orcl \
     -responseFile NO_VALUE \
     -characterSet AL32UTF8 \
     -memoryPercentage 30 \
     -emConfiguration LOCAL
```

## Variables de Entorno Oracle

- `ORACLE_HOME`: Directorio de instalación
- `ORACLE_SID`: Identificador de instancia
- `ORACLE_BASE`: Directorio base de Oracle
- `TNS_ADMIN`: Directorio de configuración de red
- `PATH`: Debe incluir $ORACLE_HOME/bin
- `LD_LIBRARY_PATH`: Para librerías Oracle
- `NLS_LANG`: Configuración de idioma

## Archivos de Configuración

- `tnsnames.ora`: Configuración de conexiones de red
- `listener.ora`: Configuración del listener
- `sqlnet.ora`: Configuración de red SQL*Net
- `init.ora` / `spfile.ora`: Parámetros de inicialización

## Ejemplo de tnsnames.ora

```
ORCL =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = servidor)(PORT = 1521))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = orcl)
    )
  )
```

## Scripts de Utilidad

### Script de Backup Automatizado

```sql
-- Script para backup con RMAN
CONNECT TARGET /
RUN {
  ALLOCATE CHANNEL disk1 DEVICE TYPE DISK;
  BACKUP DATABASE FORMAT '/backup/db_%U.bak';
  BACKUP ARCHIVELOG ALL FORMAT '/backup/arch_%U.bak';
  DELETE NOPROMPT OBSOLETE;
  RELEASE CHANNEL disk1;
}
EXIT;
```

### Script de Monitoreo

```sql
-- Script de monitoreo de performance
SET PAGESIZE 50
SET LINESIZE 120
SPOOL monitoreo.txt

SELECT 'FECHA: ' || TO_CHAR(SYSDATE, 'DD/MM/YYYY HH24:MI:SS') FROM dual;

SELECT 'SESIONES ACTIVAS' FROM dual;
SELECT COUNT(*) FROM v$session WHERE status = 'ACTIVE';

SELECT 'TOP 5 WAIT EVENTS' FROM dual;
SELECT * FROM (
  SELECT event, time_waited 
  FROM v$system_event 
  ORDER BY time_waited DESC
) WHERE rownum <= 5;

SELECT 'USO DE TABLESPACE' FROM dual;
-- Query de uso de tablespace aquí

SPOOL OFF
```

### Generación de DDL

```sql
-- Habilitar DBMS_METADATA
SET LONG 10000
SET PAGESIZE 0

-- Generar DDL de tabla
SELECT DBMS_METADATA.GET_DDL('TABLE', 'MI_TABLA', 'MI_ESQUEMA') FROM dual;

-- Generar DDL de índices
SELECT DBMS_METADATA.GET_DDL('INDEX', index_name, owner) 
FROM dba_indexes 
WHERE table_name = 'MI_TABLA' AND owner = 'MI_ESQUEMA';
```

## Ejemplos de Uso Común

### Conexión y Consulta Básica

```bash
# Script automatizado
sqlplus -S usuario/contraseña@servidor << EOF
SET HEADING OFF
SET FEEDBACK OFF
SELECT 'Conectado a: ' || instance_name FROM v$instance;
SELECT 'Fecha: ' || TO_CHAR(SYSDATE, 'DD/MM/YYYY HH24:MI:SS') FROM dual;
EXIT;
EOF
```

### Carga de Datos con SQL*Loader

```bash
# Archivo de control (datos.ctl)
cat > datos.ctl << EOF
LOAD DATA
INFILE 'datos.csv'
INTO TABLE empleados
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
(id, nombre, salario, departamento)
EOF

# Ejecutar carga
sqlldr usuario/contraseña@servidor control=datos.ctl
```

### Export/Import de Esquema

```bash
# Export
expdp usuario/contraseña@servidor schemas=MI_ESQUEMA directory=DATA_PUMP_DIR dumpfile=esquema.dmp logfile=export.log

# Import
impdp usuario/contraseña@servidor schemas=MI_ESQUEMA directory=DATA_PUMP_DIR dumpfile=esquema.dmp logfile=import.log
```
