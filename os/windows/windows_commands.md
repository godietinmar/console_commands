# Comandos de Windows (CMD y PowerShell)

Este archivo contiene comandos esenciales para Windows, incluyendo tanto comandos de Command Prompt (CMD) como PowerShell.

## Navegación y Gestión de Archivos (CMD)

### dir

**Descripción:**  
Lista el contenido de un directorio.

**Sintaxis:**
```cmd
dir [ruta] [opciones]
```

**Opciones comunes:**
- `/a`: Muestra archivos ocultos y del sistema
- `/s`: Lista subdirectorios recursivamente
- `/p`: Pausa después de cada pantalla completa
- `/o`: Ordena la lista (n=nombre, s=tamaño, d=fecha)

**Ejemplos:**
```cmd
# Listar archivos en el directorio actual
dir

# Listar archivos incluyendo ocultos
dir /a

# Listar recursivamente
dir /s

# Ordenar por fecha
dir /od
```

### cd

**Descripción:**  
Cambia el directorio actual.

**Sintaxis:**
```cmd
cd [ruta]
```

**Ejemplos:**
```cmd
# Ir al directorio raíz
cd \

# Ir a un directorio específico
cd "C:\Program Files"

# Ir al directorio padre
cd ..

# Mostrar directorio actual
cd
```

### md/mkdir

**Descripción:**  
Crea un nuevo directorio.

**Sintaxis:**
```cmd
md nombre_directorio
mkdir nombre_directorio
```

**Ejemplos:**
```cmd
# Crear un directorio
md nueva_carpeta

# Crear estructura de directorios
md "carpeta\subcarpeta\otra_carpeta"
```

### rd/rmdir

**Descripción:**  
Elimina un directorio.

**Sintaxis:**
```cmd
rd [opciones] nombre_directorio
rmdir [opciones] nombre_directorio
```

**Opciones comunes:**
- `/s`: Elimina directorio y todo su contenido
- `/q`: Modo silencioso (no pide confirmación)

**Ejemplos:**
```cmd
# Eliminar directorio vacío
rd carpeta_vacia

# Eliminar directorio y contenido
rd /s /q carpeta_con_contenido
```

### copy

**Descripción:**  
Copia archivos.

**Sintaxis:**
```cmd
copy origen destino
```

**Ejemplos:**
```cmd
# Copiar archivo
copy archivo.txt C:\destino\

# Copiar con nuevo nombre
copy archivo.txt archivo_copia.txt

# Copiar múltiples archivos
copy *.txt C:\destino\
```

### xcopy

**Descripción:**  
Copia archivos y directorios con más opciones.

**Sintaxis:**
```cmd
xcopy origen destino [opciones]
```

**Opciones comunes:**
- `/s`: Copia subdirectorios (excepto vacíos)
- `/e`: Copia subdirectorios (incluso vacíos)
- `/y`: Sobrescribe sin pedir confirmación
- `/d`: Copia solo archivos más nuevos

**Ejemplos:**
```cmd
# Copiar directorio completo
xcopy C:\origen C:\destino /s /e

# Backup incremental
xcopy C:\datos C:\backup /d /e /y
```

### robocopy

**Descripción:**  
Herramienta robusta de copia de archivos (recomendada para backups).

**Sintaxis:**
```cmd
robocopy origen destino [archivo] [opciones]
```

**Opciones comunes:**
- `/s`: Copia subdirectorios (excepto vacíos)
- `/e`: Copia subdirectorios (incluso vacíos)
- `/mir`: Sincroniza directorios (mirror)
- `/z`: Copia reiniciable
- `/log`: Crea archivo de log

**Ejemplos:**
```cmd
# Sincronizar directorios
robocopy C:\origen C:\destino /mir

# Backup con log
robocopy C:\datos C:\backup /e /z /log:backup.log

# Copiar solo archivos específicos
robocopy C:\origen C:\destino *.doc /s
```

## Manejo de Archivos y Texto (CMD)

### type

**Descripción:**  
Muestra el contenido de un archivo de texto.

**Sintaxis:**
```cmd
type archivo.txt
```

### find

**Descripción:**  
Busca texto en archivos.

**Sintaxis:**
```cmd
find "texto" archivo.txt
```

**Opciones comunes:**
- `/i`: Ignora mayúsculas/minúsculas
- `/n`: Muestra números de línea
- `/c`: Cuenta líneas que contienen el texto

**Ejemplos:**
```cmd
# Buscar texto en archivo
find "error" logfile.txt

# Buscar ignorando mayúsculas
find /i "ERROR" logfile.txt

# Contar ocurrencias
find /c "warning" logfile.txt
```

### findstr

**Descripción:**  
Versión más avanzada de find con expresiones regulares.

**Sintaxis:**
```cmd
findstr [opciones] cadena archivo
```

**Opciones comunes:**
- `/i`: Ignora mayúsculas/minúsculas
- `/n`: Muestra números de línea
- `/r`: Usa expresiones regulares
- `/s`: Busca en subdirectorios

**Ejemplos:**
```cmd
# Buscar con expresiones regulares
findstr /r "^Error.*" logfile.txt

# Buscar en múltiples archivos
findstr /s "TODO" *.cs

# Buscar múltiples patrones
findstr "error warning" logfile.txt
```

## Gestión del Sistema (CMD)

### tasklist

**Descripción:**  
Muestra los procesos en ejecución.

**Sintaxis:**
```cmd
tasklist [opciones]
```

**Opciones comunes:**
- `/fo`: Formato de salida (table, list, csv)
- `/fi`: Filtro

**Ejemplos:**
```cmd
# Listar todos los procesos
tasklist

# Listar en formato CSV
tasklist /fo csv

# Filtrar por nombre de proceso
tasklist /fi "imagename eq notepad.exe"
```

### taskkill

**Descripción:**  
Termina procesos.

**Sintaxis:**
```cmd
taskkill [opciones] /pid PID | /im nombre_imagen
```

**Opciones comunes:**
- `/f`: Fuerza la terminación
- `/t`: Termina el proceso y sus procesos hijo

**Ejemplos:**
```cmd
# Terminar proceso por PID
taskkill /pid 1234

# Terminar proceso por nombre
taskkill /im notepad.exe

# Forzar terminación
taskkill /f /im proceso.exe
```

### net

**Descripción:**  
Administra servicios de red, usuarios y recursos compartidos.

**Sintaxis:**
```cmd
net comando [opciones]
```

**Comandos comunes:**
- `start`: Inicia un servicio
- `stop`: Detiene un servicio  
- `user`: Administra cuentas de usuario
- `share`: Administra recursos compartidos

**Ejemplos:**
```cmd
# Iniciar servicio
net start "Nombre del Servicio"

# Detener servicio
net stop "Nombre del Servicio"

# Ver usuarios locales
net user

# Crear usuario
net user nuevo_usuario contraseña /add
```

### sc

**Descripción:**  
Administra servicios del sistema.

**Sintaxis:**
```cmd
sc comando nombre_servicio [opciones]
```

**Comandos comunes:**
- `query`: Consulta estado del servicio
- `start`: Inicia servicio
- `stop`: Detiene servicio
- `config`: Configura servicio

**Ejemplos:**
```cmd
# Ver estado de servicio
sc query "Spooler"

# Iniciar servicio
sc start "Spooler"

# Configurar inicio automático
sc config "Spooler" start= auto
```

## Comandos de Red (CMD)

### ping

**Descripción:**  
Prueba conectividad de red.

**Sintaxis:**
```cmd
ping [opciones] destino
```

**Opciones comunes:**
- `-t`: Ping continuo
- `-n`: Número de paquetes
- `-l`: Tamaño del paquete

**Ejemplos:**
```cmd
# Ping básico
ping google.com

# Ping continuo
ping -t 192.168.1.1

# Ping con 10 paquetes
ping -n 10 google.com
```

### ipconfig

**Descripción:**  
Muestra y configura la configuración de red.

**Sintaxis:**
```cmd
ipconfig [opciones]
```

**Opciones comunes:**
- `/all`: Muestra configuración completa
- `/release`: Libera dirección IP
- `/renew`: Renueva dirección IP
- `/flushdns`: Limpia caché DNS

**Ejemplos:**
```cmd
# Mostrar configuración básica
ipconfig

# Mostrar configuración completa
ipconfig /all

# Renovar IP
ipconfig /release
ipconfig /renew

# Limpiar caché DNS
ipconfig /flushdns
```

### netstat

**Descripción:**  
Muestra estadísticas de red y conexiones.

**Sintaxis:**
```cmd
netstat [opciones]
```

**Opciones comunes:**
- `-a`: Muestra todas las conexiones
- `-n`: Muestra direcciones numéricas
- `-o`: Muestra PID del proceso
- `-r`: Muestra tabla de enrutamiento

**Ejemplos:**
```cmd
# Mostrar conexiones activas
netstat -a

# Mostrar con PIDs
netstat -ano

# Mostrar tabla de enrutamiento
netstat -r
```

## PowerShell - Comandos Básicos

### Get-ChildItem

**Descripción:**  
Lista contenido de directorios (equivalente a dir/ls).

**Sintaxis:**
```powershell
Get-ChildItem [ruta] [opciones]
```

**Ejemplos:**
```powershell
# Listar archivos en directorio actual
Get-ChildItem

# Usar alias
ls
dir

# Listar archivos ocultos
Get-ChildItem -Force

# Filtrar por extensión
Get-ChildItem *.txt

# Buscar recursivamente
Get-ChildItem -Recurse -Filter "*.log"
```

### Set-Location

**Descripción:**  
Cambia el directorio actual (equivalente a cd).

**Sintaxis:**
```powershell
Set-Location [ruta]
```

**Ejemplos:**
```powershell
# Cambiar directorio
Set-Location "C:\Program Files"

# Usar alias
cd "C:\Users"
```

### Copy-Item

**Descripción:**  
Copia archivos y directorios.

**Sintaxis:**
```powershell
Copy-Item origen destino [opciones]
```

**Ejemplos:**
```powershell
# Copiar archivo
Copy-Item "archivo.txt" "C:\destino\"

# Copiar directorio recursivamente
Copy-Item "C:\origen" "C:\destino" -Recurse

# Usar alias
cp "archivo.txt" "copia.txt"
```

### Remove-Item

**Descripción:**  
Elimina archivos y directorios.

**Sintaxis:**
```powershell
Remove-Item ruta [opciones]
```

**Ejemplos:**
```powershell
# Eliminar archivo
Remove-Item "archivo.txt"

# Eliminar directorio y contenido
Remove-Item "directorio" -Recurse -Force

# Usar alias
rm "archivo.txt"
del "archivo.txt"
```

## PowerShell - Cmdlets Avanzados

### Get-Process

**Descripción:**  
Obtiene procesos en ejecución.

**Sintaxis:**
```powershell
Get-Process [nombre] [opciones]
```

**Ejemplos:**
```powershell
# Listar todos los procesos
Get-Process

# Filtrar por nombre
Get-Process notepad

# Ordenar por uso de CPU
Get-Process | Sort-Object CPU -Descending

# Mostrar propiedades específicas
Get-Process | Select-Object Name, CPU, WorkingSet
```

### Stop-Process

**Descripción:**  
Termina procesos.

**Sintaxis:**
```powershell
Stop-Process -Name nombre | -Id PID [opciones]
```

**Ejemplos:**
```powershell
# Terminar proceso por nombre
Stop-Process -Name "notepad"

# Terminar proceso por PID
Stop-Process -Id 1234

# Forzar terminación
Stop-Process -Name "programa" -Force
```

### Get-Service

**Descripción:**  
Obtiene información de servicios.

**Sintaxis:**
```powershell
Get-Service [nombre] [opciones]
```

**Ejemplos:**
```powershell
# Listar todos los servicios
Get-Service

# Filtrar servicios en ejecución
Get-Service | Where-Object {$_.Status -eq "Running"}

# Buscar servicio específico
Get-Service *print*
```

### Start-Service / Stop-Service

**Descripción:**  
Inicia o detiene servicios.

**Sintaxis:**
```powershell
Start-Service nombre
Stop-Service nombre
```

**Ejemplos:**
```powershell
# Iniciar servicio
Start-Service "Spooler"

# Detener servicio
Stop-Service "Spooler"

# Reiniciar servicio
Restart-Service "Spooler"
```

### Get-EventLog

**Descripción:**  
Lee logs de eventos del sistema.

**Sintaxis:**
```powershell
Get-EventLog -LogName nombre [opciones]
```

**Ejemplos:**
```powershell
# Ver eventos del sistema
Get-EventLog -LogName System -Newest 10

# Ver eventos de aplicación con errores
Get-EventLog -LogName Application -EntryType Error -Newest 20

# Filtrar por fuente
Get-EventLog -LogName System -Source "Service Control Manager"
```

### Test-Connection

**Descripción:**  
Prueba conectividad de red (equivalente a ping).

**Sintaxis:**
```powershell
Test-Connection destino [opciones]
```

**Ejemplos:**
```powershell
# Ping básico
Test-Connection google.com

# Ping con número específico de paquetes
Test-Connection 192.168.1.1 -Count 5

# Ping silencioso (solo resultado)
Test-Connection google.com -Quiet
```

### Get-WmiObject

**Descripción:**  
Obtiene información del sistema usando WMI.

**Sintaxis:**
```powershell
Get-WmiObject -Class clase [opciones]
```

**Ejemplos:**
```powershell
# Información del sistema operativo
Get-WmiObject -Class Win32_OperatingSystem

# Información del procesador
Get-WmiObject -Class Win32_Processor

# Información de discos
Get-WmiObject -Class Win32_LogicalDisk

# Procesos en ejecución
Get-WmiObject -Class Win32_Process
```

### Invoke-WebRequest

**Descripción:**  
Realiza peticiones HTTP.

**Sintaxis:**
```powershell
Invoke-WebRequest -Uri url [opciones]
```

**Ejemplos:**
```powershell
# Petición GET simple
Invoke-WebRequest -Uri "https://api.github.com"

# Descargar archivo
Invoke-WebRequest -Uri "https://ejemplo.com/archivo.zip" -OutFile "archivo.zip"

# Petición POST con datos
Invoke-WebRequest -Uri "https://api.ejemplo.com" -Method POST -Body "datos"

# Usar alias
curl "https://google.com"
wget "https://archivo.com/file.zip" -O "file.zip"
```

## Administración de Archivos Comprimidos

### Compress-Archive

**Descripción:**  
Crea archivos ZIP.

**Sintaxis:**
```powershell
Compress-Archive -Path origen -DestinationPath destino.zip
```

**Ejemplos:**
```powershell
# Comprimir archivo
Compress-Archive -Path "archivo.txt" -DestinationPath "archivo.zip"

# Comprimir directorio
Compress-Archive -Path "C:\carpeta" -DestinationPath "backup.zip"

# Agregar a archivo existente
Compress-Archive -Path "nuevo.txt" -DestinationPath "archivo.zip" -Update
```

### Expand-Archive

**Descripción:**  
Extrae archivos ZIP.

**Sintaxis:**
```powershell
Expand-Archive -Path archivo.zip -DestinationPath destino
```

**Ejemplos:**
```powershell
# Extraer archivo ZIP
Expand-Archive -Path "archivo.zip" -DestinationPath "C:\extraido"

# Forzar sobrescritura
Expand-Archive -Path "archivo.zip" -DestinationPath "C:\extraido" -Force
```

## Variables de Entorno

### set (CMD)

**Descripción:**  
Muestra o establece variables de entorno en CMD.

**Sintaxis:**
```cmd
set [variable=[valor]]
```

**Ejemplos:**
```cmd
# Mostrar todas las variables
set

# Mostrar variable específica
set PATH

# Establecer variable
set MI_VARIABLE=valor

# Agregar al PATH
set PATH=%PATH%;C:\nueva\ruta
```

### Get-Variable / Set-Variable (PowerShell)

**Descripción:**  
Administra variables en PowerShell.

**Sintaxis:**
```powershell
Get-Variable [nombre]
Set-Variable -Name nombre -Value valor
```

**Ejemplos:**
```powershell
# Mostrar todas las variables
Get-Variable

# Crear variable
$miVariable = "valor"
Set-Variable -Name "miVar" -Value "valor"

# Mostrar variable de entorno
$env:PATH

# Modificar variable de entorno
$env:PATH += ";C:\nueva\ruta"
```

## Permisos y Seguridad

### icacls

**Descripción:**  
Administra permisos de archivos y directorios.

**Sintaxis:**
```cmd
icacls archivo [opciones]
```

**Ejemplos:**
```cmd
# Ver permisos de archivo
icacls archivo.txt

# Dar control total al usuario
icacls "C:\carpeta" /grant usuario:F

# Remover permisos
icacls "C:\carpeta" /remove usuario

# Aplicar recursivamente
icacls "C:\carpeta" /grant usuario:F /T
```

### Get-Acl / Set-Acl (PowerShell)

**Descripción:**  
Administra listas de control de acceso.

**Sintaxis:**
```powershell
Get-Acl ruta
Set-Acl ruta -AclObject acl
```

**Ejemplos:**
```powershell
# Ver permisos
Get-Acl "C:\archivo.txt"

# Copiar permisos de un archivo a otro
$acl = Get-Acl "C:\origen.txt"
Set-Acl "C:\destino.txt" -AclObject $acl
```
