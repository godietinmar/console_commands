# Comandos de macOS (Terminal)

Este archivo contiene comandos esenciales para macOS usando Terminal, incluyendo comandos específicos de macOS y comandos Unix/Linux comunes.

## Navegación y Gestión de Archivos

### ls

**Descripción:**  
Lista el contenido de un directorio.

**Sintaxis:**
```bash
ls [opciones] [ruta]
```

**Opciones comunes:**
- `-l`: Formato de lista larga
- `-a`: Muestra archivos ocultos
- `-h`: Tamaños legibles para humanos
- `-R`: Lista recursivamente
- `-G`: Colores en la salida
- `-@`: Muestra atributos extendidos

**Ejemplos:**
```bash
# Listar archivos con colores y detalles
ls -laG

# Listar archivos con atributos extendidos
ls -l@

# Listar archivos ordenados por fecha
ls -lt
```

### cd

**Descripción:**  
Cambia el directorio actual.

**Sintaxis:**
```bash
cd [ruta]
```

**Ejemplos:**
```bash
# Ir al directorio home
cd ~

# Ir a Aplicaciones
cd /Applications

# Ir al directorio anterior
cd -

# Ir al Desktop
cd ~/Desktop
```

### pwd

**Descripción:**  
Muestra el directorio de trabajo actual.

**Sintaxis:**
```bash
pwd
```

### mkdir

**Descripción:**  
Crea directorios.

**Sintaxis:**
```bash
mkdir [opciones] directorio
```

**Opciones comunes:**
- `-p`: Crea directorios padre si no existen
- `-m`: Establece permisos

**Ejemplos:**
```bash
# Crear directorio
mkdir nueva_carpeta

# Crear estructura de directorios
mkdir -p proyecto/src/components

# Crear con permisos específicos
mkdir -m 755 directorio_publico
```

### rm

**Descripción:**  
Elimina archivos y directorios.

**Sintaxis:**
```bash
rm [opciones] archivo(s)
```

**Opciones comunes:**
- `-r`: Recursivo (directorios)
- `-f`: Forzar eliminación
- `-i`: Pedir confirmación

**Ejemplos:**
```bash
# Eliminar archivo
rm archivo.txt

# Eliminar directorio y contenido
rm -rf directorio

# Eliminar con confirmación
rm -i archivo.txt
```

### cp

**Descripción:**  
Copia archivos y directorios.

**Sintaxis:**
```bash
cp [opciones] origen destino
```

**Opciones comunes:**
- `-r`: Copia recursiva
- `-p`: Preserva atributos
- `-a`: Copia archival (equivale a -pPR)
- `-X`: No copia atributos extendidos

**Ejemplos:**
```bash
# Copiar archivo
cp archivo.txt copia.txt

# Copiar directorio recursivamente
cp -r directorio/ copia_directorio/

# Copiar preservando atributos
cp -p archivo.txt ~/Desktop/
```

### mv

**Descripción:**  
Mueve o renombra archivos y directorios.

**Sintaxis:**
```bash
mv origen destino
```

**Ejemplos:**
```bash
# Renombrar archivo
mv archivo_viejo.txt archivo_nuevo.txt

# Mover archivo a directorio
mv archivo.txt ~/Documents/

# Mover directorio
mv carpeta_vieja/ ~/Desktop/carpeta_nueva/
```

## Comandos Específicos de macOS

### open

**Descripción:**  
Abre archivos, directorios o aplicaciones.

**Sintaxis:**
```bash
open [opciones] archivo/directorio/aplicación
```

**Opciones comunes:**
- `-a`: Especifica aplicación
- `-e`: Abre con TextEdit
- `-t`: Abre con editor de texto por defecto
- `-R`: Revela en Finder
- `-n`: Abre nueva instancia

**Ejemplos:**
```bash
# Abrir archivo con aplicación predeterminada
open documento.pdf

# Abrir con aplicación específica
open -a "Visual Studio Code" proyecto/

# Abrir directorio en Finder
open ~/Desktop

# Revelar archivo en Finder
open -R archivo.txt

# Abrir URL en navegador
open https://google.com

# Abrir aplicación
open -a Safari
```

### osascript

**Descripción:**  
Ejecuta scripts de AppleScript o JavaScript.

**Sintaxis:**
```bash
osascript -e "script"
```

**Ejemplos:**
```bash
# Mostrar notificación
osascript -e 'display notification "Tarea completada" with title "Terminal"'

# Mostrar diálogo
osascript -e 'display dialog "¿Continuar?" buttons {"No", "Sí"} default button "Sí"'

# Obtener volumen del sistema
osascript -e 'output volume of (get volume settings)'

# Establecer volumen
osascript -e 'set volume output volume 50'

# Obtener información del sistema
osascript -e 'system info'
```

### say

**Descripción:**  
Convierte texto a voz.

**Sintaxis:**
```bash
say [opciones] "texto"
```

**Opciones comunes:**
- `-v`: Especifica voz
- `-r`: Velocidad de habla
- `-o`: Guarda en archivo de audio

**Ejemplos:**
```bash
# Decir texto
say "Hola mundo"

# Usar voz específica
say -v Jorge "Hola, soy Jorge"

# Cambiar velocidad
say -r 200 "Hablando rápido"

# Guardar en archivo
say -o saludo.aiff "Hola mundo"

# Ver voces disponibles
say -v ?
```

### defaults

**Descripción:**  
Lee y modifica preferencias del sistema.

**Sintaxis:**
```bash
defaults [read|write|delete] dominio [clave] [valor]
```

**Ejemplos:**
```bash
# Mostrar archivos ocultos en Finder
defaults write com.apple.finder AppleShowAllFiles YES
killall Finder

# Cambiar ubicación de capturas de pantalla
defaults write com.apple.screencapture location ~/Desktop/Screenshots

# Acelerar animaciones del Dock
defaults write com.apple.dock autohide-time-modifier -float 0.5
killall Dock

# Mostrar extensiones de archivo
defaults write NSGlobalDomain AppleShowAllExtensions -bool true

# Deshabilitar corrección automática
defaults write NSGlobalDomain NSAutomaticSpellingCorrectionEnabled -bool false
```

### caffeinate

**Descripción:**  
Previene que el sistema entre en modo de suspensión.

**Sintaxis:**
```bash
caffeinate [opciones] [comando]
```

**Opciones comunes:**
- `-d`: Previene que la pantalla se apague
- `-i`: Previente suspensión cuando está inactivo
- `-s`: Previene suspensión
- `-t`: Tiempo en segundos

**Ejemplos:**
```bash
# Mantener despierto por 1 hora
caffeinate -t 3600

# Mantener despierto mientras ejecuta comando
caffeinate make

# Prevenir suspensión de pantalla
caffeinate -d
```

### pmset

**Descripción:**  
Administra configuración de energía.

**Sintaxis:**
```bash
pmset [opciones] configuración valor
```

**Ejemplos:**
```bash
# Ver configuración actual de energía
pmset -g

# Ver estado de la batería
pmset -g batt

# Programar apagado
sudo pmset schedule shutdown "2024-12-25 22:00:00"

# Programar encendido
sudo pmset schedule wakeorpoweron "2024-12-26 08:00:00"

# Ver horarios programados
pmset -g sched
```

### softwareupdate

**Descripción:**  
Administra actualizaciones de software del sistema.

**Sintaxis:**
```bash
softwareupdate [opciones]
```

**Opciones comunes:**
- `-l`: Lista actualizaciones disponibles
- `-i`: Instala actualización específica
- `-ia`: Instala todas las actualizaciones
- `-d`: Solo descarga

**Ejemplos:**
```bash
# Listar actualizaciones disponibles
softwareupdate -l

# Instalar todas las actualizaciones
sudo softwareupdate -ia

# Instalar actualización específica
sudo softwareupdate -i "Safari-16.1"

# Solo descargar actualizaciones
softwareupdate -d -a
```

### diskutil

**Descripción:**  
Administra discos y volúmenes.

**Sintaxis:**
```bash
diskutil comando [opciones]
```

**Ejemplos:**
```bash
# Listar todos los discos
diskutil list

# Información de disco específico
diskutil info disk0

# Montar volumen
diskutil mount /dev/disk2s1

# Desmontar volumen
diskutil unmount /Volumes/MiDisco

# Reparar permisos (macOS anterior a El Capitan)
diskutil repairPermissions /

# Verificar disco
diskutil verifyVolume /
```

### system_profiler

**Descripción:**  
Muestra información detallada del hardware y software.

**Sintaxis:**
```bash
system_profiler [tipo_datos]
```

**Ejemplos:**
```bash
# Información completa del sistema
system_profiler

# Solo información de hardware
system_profiler SPHardwareDataType

# Información de software
system_profiler SPSoftwareDataType

# Información de memoria
system_profiler SPMemoryDataType

# Información de almacenamiento
system_profiler SPStorageDataType

# Información en formato XML
system_profiler -xml SPHardwareDataType
```

## Administración del Sistema

### launchctl

**Descripción:**  
Administra servicios del sistema (daemons y agents).

**Sintaxis:**
```bash
launchctl comando [opciones]
```

**Ejemplos:**
```bash
# Listar servicios cargados
launchctl list

# Cargar servicio
launchctl load ~/Library/LaunchAgents/com.ejemplo.servicio.plist

# Descargar servicio
launchctl unload ~/Library/LaunchAgents/com.ejemplo.servicio.plist

# Iniciar servicio
launchctl start com.ejemplo.servicio

# Detener servicio
launchctl stop com.ejemplo.servicio

# Ver servicios del sistema
sudo launchctl list | grep -v com.apple
```

### dscl

**Descripción:**  
Administra Directory Service (usuarios y grupos).

**Sintaxis:**
```bash
dscl [ruta_directorio] comando [opciones]
```

**Ejemplos:**
```bash
# Listar usuarios locales
dscl . list /Users

# Información de usuario específico
dscl . read /Users/usuario

# Crear usuario
sudo dscl . create /Users/nuevousuario

# Cambiar shell de usuario
sudo dscl . change /Users/usuario UserShell /bin/bash /bin/zsh

# Listar grupos
dscl . list /Groups
```

### scutil

**Descripción:**  
Administra configuración del sistema.

**Sintaxis:**
```bash
scutil [opciones]
```

**Ejemplos:**
```bash
# Ver nombre del computador
scutil --get ComputerName

# Establecer nombre del computador
sudo scutil --set ComputerName "NuevoNombre"

# Ver nombre de host
scutil --get HostName

# Ver configuración de red
scutil --nwi

# Información de DNS
scutil --dns
```

### networksetup

**Descripción:**  
Configura interfaces de red.

**Sintaxis:**
```bash
networksetup comando [opciones]
```

**Ejemplos:**
```bash
# Listar interfaces de red
networksetup -listallhardwareports

# Ver configuración de Wi-Fi
networksetup -getairportnetwork en0

# Conectar a red Wi-Fi
networksetup -setairportnetwork en0 "NombreRed" "contraseña"

# Configurar IP estática
sudo networksetup -setmanual "Ethernet" 192.168.1.100 255.255.255.0 192.168.1.1

# Usar DHCP
sudo networksetup -setdhcp "Ethernet"

# Ver servidores DNS
networksetup -getdnsservers "Wi-Fi"
```

## Herramientas de Desarrollo

### xcode-select

**Descripción:**  
Administra herramientas de desarrollo de Xcode.

**Sintaxis:**
```bash
xcode-select comando [opciones]
```

**Ejemplos:**
```bash
# Ver ruta de herramientas de desarrollo
xcode-select -p

# Instalar herramientas de línea de comandos
xcode-select --install

# Cambiar ruta de herramientas
sudo xcode-select -s /Applications/Xcode.app/Contents/Developer

# Resetear a valores por defecto
sudo xcode-select --reset
```

### xcrun

**Descripción:**  
Ejecuta herramientas de desarrollo de Xcode.

**Sintaxis:**
```bash
xcrun herramienta [opciones]
```

**Ejemplos:**
```bash
# Compilar archivo C
xcrun clang programa.c -o programa

# Ver versión de Swift
xcrun swift --version

# Localizar herramienta
xcrun --find clang

# Crear archivo de encabezado
xcrun -sdk macosx --show-sdk-path
```

### brew (Homebrew)

**Descripción:**  
Gestor de paquetes para macOS (requiere instalación previa).

**Sintaxis:**
```bash
brew comando [opciones] [paquete]
```

**Ejemplos:**
```bash
# Instalar paquete
brew install wget

# Buscar paquete
brew search python

# Actualizar Homebrew
brew update

# Actualizar todos los paquetes
brew upgrade

# Listar paquetes instalados
brew list

# Desinstalar paquete
brew uninstall wget

# Ver información de paquete
brew info git

# Limpiar archivos antiguos
brew cleanup
```

## Administración de Archivos Avanzada

### ditto

**Descripción:**  
Copia archivos preservando metadatos y recursos de macOS.

**Sintaxis:**
```bash
ditto [opciones] origen destino
```

**Opciones comunes:**
- `-v`: Verbose
- `-x`: Preserva atributos extendidos
- `-c`: Crea archivo ZIP
- `-k`: Extrae archivo ZIP

**Ejemplos:**
```bash
# Copia completa preservando metadatos
ditto -v origen/ destino/

# Crear archivo ZIP
ditto -c -k --sequesterRsrc carpeta/ archivo.zip

# Extraer archivo ZIP
ditto -x -k archivo.zip destino/
```

### mdls

**Descripción:**  
Muestra metadatos de archivos usando Spotlight.

**Sintaxis:**
```bash
mdls archivo
```

**Ejemplos:**
```bash
# Ver metadatos de archivo
mdls documento.pdf

# Ver metadatos específicos
mdls -name kMDItemDisplayName -name kMDItemContentType archivo.jpg

# Ver metadatos de imagen
mdls foto.jpg | grep -E "(kMDItemPixel|kMDItemColor)"
```

### mdfind

**Descripción:**  
Busca archivos usando Spotlight.

**Sintaxis:**
```bash
mdfind consulta
```

**Ejemplos:**
```bash
# Buscar archivos por nombre
mdfind "documento.pdf"

# Buscar por tipo de archivo
mdfind "kMDItemContentType == 'com.adobe.pdf'"

# Buscar por contenido
mdfind "texto a buscar"

# Buscar en directorio específico
mdfind -onlyin ~/Documents "proyecto"

# Contar resultados
mdfind "*.jpg" | wc -l
```

### xattr

**Descripción:**  
Administra atributos extendidos de archivos.

**Sintaxis:**
```bash
xattr [opciones] archivo
```

**Opciones comunes:**
- `-l`: Lista atributos
- `-d`: Elimina atributo
- `-c`: Elimina todos los atributos
- `-r`: Recursivo

**Ejemplos:**
```bash
# Listar atributos extendidos
xattr -l archivo.txt

# Eliminar cuarentena de archivo descargado
xattr -d com.apple.quarantine archivo.dmg

# Eliminar todos los atributos
xattr -c archivo.txt

# Aplicar recursivamente
xattr -rc directorio/
```

## Comandos de Red

### curl

**Descripción:**  
Transfiere datos desde/hacia servidores.

**Sintaxis:**
```bash
curl [opciones] URL
```

**Ejemplos:**
```bash
# Descargar archivo
curl -O https://ejemplo.com/archivo.zip

# Ver headers HTTP
curl -I https://google.com

# POST con datos
curl -X POST -d "datos=valor" https://api.ejemplo.com

# Seguir redirecciones
curl -L https://bit.ly/enlace-corto

# Descargar con barra de progreso
curl --progress-bar -O https://archivo.com/grande.zip
```

### ping

**Descripción:**  
Prueba conectividad de red.

**Sintaxis:**
```bash
ping [opciones] destino
```

**Ejemplos:**
```bash
# Ping básico
ping google.com

# Ping con número limitado de paquetes
ping -c 5 192.168.1.1

# Ping con intervalo específico
ping -i 2 google.com

# Ping con tamaño de paquete específico
ping -s 1024 google.com
```

### netstat

**Descripción:**  
Muestra estadísticas de red.

**Sintaxis:**
```bash
netstat [opciones]
```

**Ejemplos:**
```bash
# Mostrar conexiones activas
netstat -an

# Mostrar tabla de enrutamiento
netstat -rn

# Mostrar estadísticas de interfaz
netstat -i

# Mostrar procesos usando la red
netstat -p tcp
```

## Monitoreo del Sistema

### top

**Descripción:**  
Muestra procesos en tiempo real.

**Sintaxis:**
```bash
top [opciones]
```

**Ejemplos:**
```bash
# Monitor básico
top

# Ordenar por uso de CPU
top -o cpu

# Ordenar por uso de memoria
top -o mem

# Mostrar solo procesos de usuario específico
top -U usuario
```

### activity

**Descripción:**  
Interfaz de línea de comandos para Activity Monitor.

**Sintaxis:**
```bash
activity -mode [tipo]
```

**Ejemplos:**
```bash
# Monitor de CPU
activity -mode cpu

# Monitor de memoria
activity -mode mem

# Monitor de red
activity -mode net

# Monitor de disco
activity -mode disk
```

### fs_usage

**Descripción:**  
Muestra actividad del sistema de archivos en tiempo real.

**Sintaxis:**
```bash
fs_usage [opciones] [proceso]
```

**Ejemplos:**
```bash
# Monitor general del sistema de archivos
sudo fs_usage

# Monitor de proceso específico
sudo fs_usage -f pathname programa

# Filtrar por tipo de operación
sudo fs_usage -w -f pathname
```

### iotop

**Descripción:**  
Muestra actividad de I/O por proceso (requiere instalación).

**Sintaxis:**
```bash
sudo iotop
```
