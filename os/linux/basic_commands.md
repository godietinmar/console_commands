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
