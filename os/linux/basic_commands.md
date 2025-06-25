# Comandos Básicos de Linux

Este archivo contiene una lista de comandos básicos de Linux que son comunes en la mayoría de las distribuciones.

## Navegación y Gestión de Archivos

### ls

**Descripción:**  
Lista el contenido de un directorio.

**Sintaxis:**
```bash
ls [opciones] [ruta]
```

**Opciones comunes:**
- `-l`: Formato de lista larga, muestra permisos, propietario, tamaño, etc.
- `-a`: Muestra archivos ocultos
- `-h`: Muestra tamaños en formato legible para humanos (KB, MB, etc.)
- `-R`: Lista subdirectorios recursivamente

**Ejemplos:**
```bash
# Listar archivos en el directorio actual
ls

# Listar archivos en formato largo
ls -l

# Listar archivos incluyendo ocultos en formato legible
ls -lah
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
# Ir al directorio home del usuario
cd

# Ir a un directorio específico
cd /var/www/html

# Ir al directorio padre
cd ..

# Ir al directorio anterior
cd -
```

### pwd

**Descripción:**  
Muestra el directorio de trabajo actual.

**Sintaxis:**
```bash
pwd
```

**Ejemplos:**
```bash
# Mostrar la ruta actual completa
pwd
```

### mkdir

**Descripción:**  
Crea un nuevo directorio.

**Sintaxis:**
```bash
mkdir [opciones] directorio
```

**Opciones comunes:**
- `-p`: Crea directorios padres si no existen

**Ejemplos:**
```bash
# Crear un directorio
mkdir nuevo_directorio

# Crear estructura de directorios
mkdir -p carpeta/subcarpeta/otra_carpeta
```

### rm

**Descripción:**  
Elimina archivos y directorios.

**Sintaxis:**
```bash
rm [opciones] archivo(s)
```

**Opciones comunes:**
- `-r`: Elimina directorios y su contenido recursivamente
- `-f`: Fuerza la eliminación sin pedir confirmación
- `-i`: Pide confirmación antes de cada eliminación

**Ejemplos:**
```bash
# Eliminar un archivo
rm archivo.txt

# Eliminar un directorio y su contenido
rm -rf directorio

# Eliminar con confirmación
rm -i archivo.txt
```

## Manejo de Texto y Búsqueda

### grep

**Descripción:**  
Busca patrones en archivos.

**Sintaxis:**
```bash
grep [opciones] patrón [archivo...]
```

**Opciones comunes:**
- `-i`: Ignora mayúsculas/minúsculas
- `-r`: Busca recursivamente en directorios
- `-n`: Muestra número de línea
- `-v`: Invierte la coincidencia (líneas que NO coinciden)

**Ejemplos:**
```bash
# Buscar una palabra en un archivo
grep "error" archivo.log

# Buscar recursivamente ignorando mayúsculas/minúsculas
grep -ri "palabra clave" /directorio/

# Contar ocurrencias de un patrón
grep -c "patrón" archivo.txt
```

### find

**Descripción:**  
Busca archivos y directorios en una jerarquía de directorios.

**Sintaxis:**
```bash
find [ruta] [expresión]
```

**Opciones comunes:**
- `-name`: Busca por nombre de archivo
- `-type`: Busca por tipo (f: archivo, d: directorio)
- `-size`: Busca por tamaño
- `-mtime`: Busca por fecha de modificación

**Ejemplos:**
```bash
# Encontrar archivos por nombre
find /home -name "*.txt"

# Encontrar directorios
find . -type d

# Encontrar archivos modificados en los últimos 7 días
find /var/log -type f -mtime -7
```

## Gestión del Sistema

### ps

**Descripción:**  
Muestra información sobre procesos en ejecución.

**Sintaxis:**
```bash
ps [opciones]
```

**Opciones comunes:**
- `aux`: Muestra todos los procesos de todos los usuarios
- `ef`: Formato jerárquico (árbol de procesos)

**Ejemplos:**
```bash
# Ver todos los procesos
ps aux

# Ver árbol de procesos
ps ef
```

### top

**Descripción:**  
Muestra procesos en tiempo real y estadísticas del sistema.

**Sintaxis:**
```bash
top
```

**Teclas útiles durante la ejecución:**
- `q`: Salir
- `k`: Matar un proceso (requiere PID)
- `r`: Cambiar la prioridad de un proceso
- `h`: Mostrar ayuda

### systemctl

**Descripción:**  
Controla el sistema systemd y servicios.

**Sintaxis:**
```bash
systemctl [comando] [servicio]
```

**Comandos comunes:**
- `start`: Inicia un servicio
- `stop`: Detiene un servicio
- `restart`: Reinicia un servicio
- `status`: Muestra el estado de un servicio
- `enable`: Habilita un servicio para que se inicie con el sistema
- `disable`: Deshabilita el inicio automático

**Ejemplos:**
```bash
# Ver estado de un servicio
systemctl status apache2

# Iniciar un servicio
systemctl start mysql

# Habilitar inicio automático
systemctl enable ssh
```

## Redes

### ping

**Descripción:**  
Envía paquetes ICMP a un host para comprobar conectividad.

**Sintaxis:**
```bash
ping [opciones] host
```

**Opciones comunes:**
- `-c`: Número de paquetes a enviar
- `-i`: Intervalo entre paquetes (en segundos)

**Ejemplos:**
```bash
# Comprobar conectividad con un sitio
ping google.com

# Enviar 5 paquetes y parar
ping -c 5 192.168.1.1
```

### netstat

**Descripción:**  
Muestra conexiones de red, tablas de enrutamiento e interfaces.

**Sintaxis:**
```bash
netstat [opciones]
```

**Opciones comunes:**
- `-t`: Muestra conexiones TCP
- `-u`: Muestra conexiones UDP
- `-l`: Muestra puertos en escucha
- `-n`: Muestra direcciones numéricas
- `-p`: Muestra el programa asociado a cada conexión

**Ejemplos:**
```bash
# Ver puertos TCP en escucha
netstat -tln

# Ver todas las conexiones con programas asociados
netstat -tuplan
```

## Compresión de Archivos

### tar

**Descripción:**  
Empaqueta y desempaqueta archivos.

**Sintaxis:**
```bash
tar [opciones] [archivo_destino] [archivos_origen]
```

**Opciones comunes:**
- `-c`: Crear nuevo archivo
- `-x`: Extraer archivos
- `-f`: Nombre del archivo
- `-z`: Comprimir con gzip
- `-j`: Comprimir con bzip2
- `-v`: Modo verbose (muestra progreso)

**Ejemplos:**
```bash
# Crear un archivo tar comprimido
tar -czvf archivo.tar.gz directorio/

# Extraer un archivo tar.gz
tar -xzvf archivo.tar.gz

# Extraer en un directorio específico
tar -xzvf archivo.tar.gz -C /directorio/destino/
```

### zip/unzip

**Descripción:**  
Comprime y descomprime archivos en formato ZIP.

**Sintaxis:**
```bash
zip [opciones] [archivo_zip] [archivos]
unzip [opciones] [archivo_zip]
```

**Opciones comunes (zip):**
- `-r`: Recursivo (incluye subdirectorios)
- `-q`: Modo silencioso

**Opciones comunes (unzip):**
- `-d`: Directorio de destino
- `-q`: Modo silencioso

**Ejemplos:**
```bash
# Comprimir un directorio
zip -r archivo.zip directorio/

# Descomprimir un archivo ZIP
unzip archivo.zip

# Descomprimir en un directorio específico
unzip archivo.zip -d /directorio/destino/
```

## Comandos Avanzados de Administración del Sistema

### crontab

**Descripción:**  
Administra tareas programadas (cron jobs).

**Sintaxis:**
```bash
crontab [opciones]
```

**Opciones comunes:**
- `-e`: Edita el crontab del usuario actual
- `-l`: Lista las tareas programadas
- `-r`: Elimina todas las tareas del crontab
- `-u`: Especifica un usuario (solo root)

**Formato del crontab:**
```
* * * * * comando
| | | | |
| | | | +--- Día de la semana (0-6, 0=Domingo)
| | | +----- Mes (1-12)
| | +------- Día del mes (1-31)
| +--------- Hora (0-23)
+----------- Minuto (0-59)
```

**Ejemplos:**
```bash
# Editar crontab
crontab -e

# Ejemplos de cron jobs:
# Ejecutar backup diario a las 2:30 AM
30 2 * * * /scripts/backup.sh

# Ejecutar limpieza de logs cada lunes a las 3:00 AM
0 3 * * 1 /scripts/clean_logs.sh

# Ejecutar cada 5 minutos
*/5 * * * * /scripts/monitor.sh
```

### awk

**Descripción:**  
Procesador de texto potente para análisis y manipulación de archivos.

**Sintaxis:**
```bash
awk 'programa' [archivo...]
```

**Ejemplos:**
```bash
# Imprimir la primera columna de un archivo
awk '{print $1}' archivo.txt

# Imprimir líneas donde la tercera columna sea mayor a 100
awk '$3 > 100' archivo.txt

# Calcular suma de la segunda columna
awk '{sum += $2} END {print sum}' archivo.txt

# Imprimir número de línea con cada línea
awk '{print NR, $0}' archivo.txt

# Procesar archivos CSV
awk -F',' '{print $1, $3}' archivo.csv
```

### sed

**Descripción:**  
Editor de flujo para filtrar y transformar texto.

**Sintaxis:**
```bash
sed [opciones] 'comando' [archivo...]
```

**Opciones comunes:**
- `-i`: Edita el archivo en lugar (modifica el archivo original)
- `-e`: Permite múltiples comandos
- `-n`: Suprime salida automática

**Ejemplos:**
```bash
# Reemplazar primera ocurrencia en cada línea
sed 's/texto_viejo/texto_nuevo/' archivo.txt

# Reemplazar todas las ocurrencias
sed 's/texto_viejo/texto_nuevo/g' archivo.txt

# Eliminar líneas que contengan una palabra
sed '/palabra/d' archivo.txt

# Insertar texto en línea específica
sed '3i\Texto a insertar' archivo.txt

# Editar archivo directamente
sed -i 's/viejo/nuevo/g' archivo.txt
```

### rsync

**Descripción:**  
Sincroniza archivos y directorios eficientemente.

**Sintaxis:**
```bash
rsync [opciones] origen destino
```

**Opciones comunes:**
- `-a`: Modo archivo (preserva enlaces, permisos, tiempos, etc.)
- `-v`: Verbose (muestra progreso)
- `-z`: Comprime datos durante la transferencia
- `-P`: Muestra progreso y permite reanudar transferencias
- `--delete`: Elimina archivos en destino que no existen en origen
- `--exclude`: Excluye archivos/directorios

**Ejemplos:**
```bash
# Sincronizar directorios locales
rsync -av /origen/ /destino/

# Sincronizar con servidor remoto
rsync -avz /local/ usuario@servidor:/remoto/

# Backup con exclusiones
rsync -av --exclude='*.tmp' --exclude='logs/' /datos/ /backup/

# Sincronización con eliminación de archivos extra
rsync -av --delete /origen/ /destino/
```

### lsof

**Descripción:**  
Lista archivos abiertos y procesos que los usan.

**Sintaxis:**
```bash
lsof [opciones] [archivo/directorio]
```

**Opciones comunes:**
- `-i`: Muestra conexiones de red
- `-p`: Filtra por PID
- `-u`: Filtra por usuario
- `-c`: Filtra por comando

**Ejemplos:**
```bash
# Ver archivos abiertos por un proceso específico
lsof -p 1234

# Ver procesos usando un archivo específico
lsof /var/log/syslog

# Ver conexiones de red
lsof -i

# Ver conexiones en puerto específico
lsof -i :80

# Ver archivos abiertos por usuario
lsof -u usuario
```

### ss

**Descripción:**  
Muestra estadísticas de sockets (reemplazo moderno de netstat).

**Sintaxis:**
```bash
ss [opciones]
```

**Opciones comunes:**
- `-t`: Muestra sockets TCP
- `-u`: Muestra sockets UDP
- `-l`: Muestra sockets en escucha
- `-p`: Muestra procesos
- `-n`: Muestra números de puerto en lugar de nombres

**Ejemplos:**
```bash
# Ver conexiones TCP
ss -t

# Ver puertos en escucha con procesos
ss -tlnp

# Ver conexiones establecidas
ss -o state established

# Ver estadísticas de memoria de sockets
ss -m
```

### tcpdump

**Descripción:**  
Captura y analiza tráfico de red.

**Sintaxis:**
```bash
tcpdump [opciones] [expresión]
```

**Opciones comunes:**
- `-i`: Especifica interfaz de red
- `-w`: Guarda captura en archivo
- `-r`: Lee captura desde archivo
- `-n`: No resuelve nombres
- `-c`: Número de paquetes a capturar

**Ejemplos:**
```bash
# Capturar tráfico en interfaz específica
tcpdump -i eth0

# Capturar tráfico HTTP
tcpdump -i eth0 port 80

# Guardar captura en archivo
tcpdump -i eth0 -w captura.pcap

# Filtrar por host
tcpdump host 192.168.1.100

# Capturar solo paquetes TCP SYN
tcpdump 'tcp[tcpflags] & tcp-syn != 0'
```

### strace

**Descripción:**  
Rastrea llamadas al sistema y señales de un proceso.

**Sintaxis:**
```bash
strace [opciones] [comando]
```

**Opciones comunes:**
- `-p`: Attach a proceso existente
- `-o`: Salida a archivo
- `-e`: Filtrar llamadas específicas
- `-c`: Mostrar resumen estadístico

**Ejemplos:**
```bash
# Rastrear llamadas de un comando
strace ls

# Rastrear proceso existente
strace -p 1234

# Filtrar solo llamadas de archivo
strace -e trace=file comando

# Guardar salida en archivo
strace -o trace.log comando
```

### iptables

**Descripción:**  
Administra reglas de firewall del kernel de Linux.

**Sintaxis:**
```bash
iptables [opciones] [cadena] [regla]
```

**Cadenas principales:**
- `INPUT`: Paquetes entrantes
- `OUTPUT`: Paquetes salientes
- `FORWARD`: Paquetes reenviados

**Ejemplos:**
```bash
# Ver reglas actuales
iptables -L

# Permitir tráfico SSH
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Bloquear IP específica
iptables -A INPUT -s 192.168.1.100 -j DROP

# Permitir tráfico web
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Limpiar todas las reglas
iptables -F
```

### htop

**Descripción:**  
Monitor de procesos interactivo mejorado (alternativa a top).

**Sintaxis:**
```bash
htop
```

**Teclas útiles:**
- `F1`: Ayuda
- `F2`: Configuración
- `F3`: Buscar proceso
- `F4`: Filtrar procesos
- `F5`: Vista de árbol
- `F6`: Ordenar por columna
- `F9`: Matar proceso
- `F10`: Salir

### iostat

**Descripción:**  
Muestra estadísticas de CPU y I/O de dispositivos.

**Sintaxis:**
```bash
iostat [opciones] [intervalo] [contador]
```

**Opciones comunes:**
- `-x`: Muestra estadísticas extendidas
- `-d`: Solo dispositivos
- `-c`: Solo CPU

**Ejemplos:**
```bash
# Mostrar estadísticas cada 2 segundos
iostat 2

# Mostrar estadísticas extendidas de dispositivos
iostat -x 1

# Mostrar solo estadísticas de CPU
iostat -c 1
```

### nmap

**Descripción:**  
Escáner de red y auditoría de seguridad.

**Sintaxis:**
```bash
nmap [opciones] objetivo
```

**Opciones comunes:**
- `-sS`: Escaneo TCP SYN
- `-sU`: Escaneo UDP
- `-p`: Especifica puertos
- `-O`: Detección de OS
- `-A`: Escaneo agresivo

**Ejemplos:**
```bash
# Escaneo básico de host
nmap 192.168.1.1

# Escaneo de rango de red
nmap 192.168.1.0/24

# Escaneo de puertos específicos
nmap -p 80,443,22 192.168.1.1

# Escaneo con detección de servicios
nmap -sV 192.168.1.1

# Escaneo completo
nmap -A 192.168.1.1
```

### fail2ban

**Descripción:**  
Protege servicios contra ataques de fuerza bruta.

**Sintaxis:**
```bash
fail2ban-client [comando]
```

**Comandos comunes:**
- `status`: Muestra estado general
- `start`: Inicia el servicio
- `stop`: Detiene el servicio
- `reload`: Recarga configuración

**Ejemplos:**
```bash
# Ver estado general
fail2ban-client status

# Ver estado de jail específico
fail2ban-client status sshd

# Desbanear IP
fail2ban-client set sshd unbanip 192.168.1.100

# Recargar configuración
fail2ban-client reload
```
