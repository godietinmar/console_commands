# Comandos Docker

Este archivo contiene una lista de comandos comunes de Docker para gestionar contenedores, imágenes, redes y volúmenes.

## Gestión de Contenedores

### docker run

**Descripción:**  
Crea y arranca un nuevo contenedor a partir de una imagen.

**Sintaxis:**
```bash
docker run [opciones] imagen [comando] [args...]
```

**Opciones comunes:**
- `-d`, `--detach`: Ejecutar en segundo plano
- `-p`, `--publish`: Mapear puertos (host:contenedor)
- `-v`, `--volume`: Montar volumen
- `-e`, `--env`: Establecer variables de entorno
- `--name`: Asignar nombre al contenedor
- `--rm`: Eliminar el contenedor automáticamente al finalizar
- `--network`: Conectar a una red específica
- `-it`: Modo interactivo con terminal

**Ejemplos:**
```bash
# Ejecutar contenedor en primer plano
docker run nginx

# Ejecutar en segundo plano con nombre y mapeo de puertos
docker run -d --name mi-web -p 8080:80 nginx

# Ejecutar con volumen montado
docker run -v /ruta/local:/ruta/contenedor nginx

# Ejecutar con variables de entorno
docker run -e MYSQL_ROOT_PASSWORD=secreto mysql

# Ejecutar en modo interactivo
docker run -it ubuntu bash
```

### docker ps

**Descripción:**  
Lista los contenedores en ejecución.

**Sintaxis:**
```bash
docker ps [opciones]
```

**Opciones comunes:**
- `-a`, `--all`: Mostrar todos los contenedores (incluidos los detenidos)
- `-q`, `--quiet`: Mostrar solo IDs
- `-s`, `--size`: Mostrar tamaños de archivos
- `-n`, `--last`: Mostrar n últimos contenedores creados

**Ejemplos:**
```bash
# Mostrar contenedores en ejecución
docker ps

# Mostrar todos los contenedores
docker ps -a

# Mostrar solo IDs de contenedores en ejecución
docker ps -q

# Mostrar los 5 últimos contenedores
docker ps -n 5
```

### docker stop

**Descripción:**  
Detiene uno o más contenedores en ejecución.

**Sintaxis:**
```bash
docker stop [opciones] contenedor [contenedor...]
```

**Opciones comunes:**
- `-t`, `--time`: Segundos a esperar antes de forzar el cierre

**Ejemplos:**
```bash
# Detener un contenedor por nombre
docker stop mi-contenedor

# Detener un contenedor por ID
docker stop abc123

# Detener múltiples contenedores
docker stop contenedor1 contenedor2

# Detener todos los contenedores en ejecución
docker stop $(docker ps -q)
```

### docker start

**Descripción:**  
Inicia uno o más contenedores detenidos.

**Sintaxis:**
```bash
docker start [opciones] contenedor [contenedor...]
```

**Opciones comunes:**
- `-a`, `--attach`: Adjuntar salida estándar/error
- `-i`, `--interactive`: Adjuntar entrada estándar

**Ejemplos:**
```bash
# Iniciar un contenedor
docker start mi-contenedor

# Iniciar un contenedor en modo interactivo
docker start -i mi-contenedor

# Iniciar múltiples contenedores
docker start contenedor1 contenedor2
```

### docker restart

**Descripción:**  
Reinicia uno o más contenedores.

**Sintaxis:**
```bash
docker restart [opciones] contenedor [contenedor...]
```

**Opciones comunes:**
- `-t`, `--time`: Segundos a esperar antes de forzar el reinicio

**Ejemplos:**
```bash
# Reiniciar un contenedor
docker restart mi-contenedor

# Reiniciar con tiempo de espera
docker restart -t 30 mi-contenedor
```

### docker rm

**Descripción:**  
Elimina uno o más contenedores.

**Sintaxis:**
```bash
docker rm [opciones] contenedor [contenedor...]
```

**Opciones comunes:**
- `-f`, `--force`: Forzar eliminación de contenedor en ejecución
- `-v`, `--volumes`: Eliminar volúmenes asociados

**Ejemplos:**
```bash
# Eliminar un contenedor detenido
docker rm mi-contenedor

# Eliminar un contenedor en ejecución
docker rm -f mi-contenedor

# Eliminar contenedor y sus volúmenes
docker rm -v mi-contenedor

# Eliminar todos los contenedores detenidos
docker rm $(docker ps -aq -f status=exited)
```

### docker exec

**Descripción:**  
Ejecuta un comando en un contenedor en ejecución.

**Sintaxis:**
```bash
docker exec [opciones] contenedor comando [args...]
```

**Opciones comunes:**
- `-d`, `--detach`: Ejecutar en segundo plano
- `-i`, `--interactive`: Mantener STDIN abierto
- `-t`, `--tty`: Asignar un pseudo-TTY
- `-e`, `--env`: Establecer variables de entorno

**Ejemplos:**
```bash
# Ejecutar shell interactivo en un contenedor
docker exec -it mi-contenedor bash

# Ejecutar comando específico
docker exec mi-contenedor ls -la

# Ejecutar con variables de entorno
docker exec -e VAR=valor mi-contenedor comando
```

### docker logs

**Descripción:**  
Muestra los logs de un contenedor.

**Sintaxis:**
```bash
docker logs [opciones] contenedor
```

**Opciones comunes:**
- `-f`, `--follow`: Seguir log en tiempo real
- `--tail`: Número de líneas a mostrar desde el final
- `--since`: Mostrar logs desde una fecha/hora
- `--until`: Mostrar logs hasta una fecha/hora
- `-t`, `--timestamps`: Mostrar marcas de tiempo

**Ejemplos:**
```bash
# Ver logs de un contenedor
docker logs mi-contenedor

# Ver y seguir logs en tiempo real
docker logs -f mi-contenedor

# Ver últimas 100 líneas
docker logs --tail 100 mi-contenedor

# Ver logs con marcas de tiempo
docker logs -t mi-contenedor

# Ver logs desde hace 1 hora
docker logs --since 1h mi-contenedor
```

### docker pause/unpause

**Descripción:**  
Pausa/reanuda todos los procesos en un contenedor.

**Sintaxis:**
```bash
docker pause contenedor [contenedor...]
docker unpause contenedor [contenedor...]
```

**Ejemplos:**
```bash
# Pausar un contenedor
docker pause mi-contenedor

# Reanudar un contenedor
docker unpause mi-contenedor
```

## Gestión de Imágenes

### docker images

**Descripción:**  
Lista las imágenes disponibles.

**Sintaxis:**
```bash
docker images [opciones] [repositorio[:tag]]
```

**Opciones comunes:**
- `-a`, `--all`: Mostrar todas las imágenes (incl. intermedias)
- `-q`, `--quiet`: Mostrar solo IDs
- `--digests`: Mostrar digests de las imágenes
- `--filter`, `-f`: Filtrar imágenes por condición

**Ejemplos:**
```bash
# Listar todas las imágenes
docker images

# Listar solo IDs
docker images -q

# Listar imágenes de un repositorio específico
docker images nginx

# Filtrar imágenes por etiqueta
docker images --filter=reference="ubuntu:20.04"
```

### docker pull

**Descripción:**  
Descarga una imagen de un registro.

**Sintaxis:**
```bash
docker pull [opciones] nombre[:tag|@digest]
```

**Opciones comunes:**
- `-a`, `--all-tags`: Descargar todas las etiquetas de la imagen
- `--platform`: Especificar plataforma para la imagen

**Ejemplos:**
```bash
# Descargar última versión de una imagen
docker pull nginx

# Descargar versión específica
docker pull nginx:1.19

# Descargar todas las etiquetas
docker pull -a nginx

# Descargar para plataforma específica
docker pull --platform linux/arm64 nginx
```

### docker rmi

**Descripción:**  
Elimina una o más imágenes.

**Sintaxis:**
```bash
docker rmi [opciones] imagen [imagen...]
```

**Opciones comunes:**
- `-f`, `--force`: Forzar eliminación de imagen

**Ejemplos:**
```bash
# Eliminar una imagen por nombre
docker rmi nginx

# Eliminar imagen por ID
docker rmi abc123

# Eliminar múltiples imágenes
docker rmi imagen1 imagen2

# Forzar eliminación de una imagen
docker rmi -f nginx:latest

# Eliminar todas las imágenes sin usar
docker rmi $(docker images -q -f "dangling=true")
```

### docker build

**Descripción:**  
Construye una imagen a partir de un Dockerfile.

**Sintaxis:**
```bash
docker build [opciones] ruta | URL | -
```

**Opciones comunes:**
- `-t`, `--tag`: Nombre y etiqueta para la imagen
- `-f`, `--file`: Nombre del Dockerfile (por defecto 'Dockerfile')
- `--no-cache`: No usar caché durante la construcción
- `--build-arg`: Variables para la construcción
- `--target`: Etapa específica en multistage build
- `--platform`: Plataforma objetivo

**Ejemplos:**
```bash
# Construir imagen desde directorio actual
docker build -t mi-app:1.0 .

# Usar Dockerfile específico
docker build -f Dockerfile.prod -t mi-app:prod .

# Construir sin caché
docker build --no-cache -t mi-app .

# Pasar argumentos de construcción
docker build --build-arg VERSION=1.2.3 -t mi-app .

# Construir etapa específica
docker build --target builder -t mi-app:build .
```

### docker tag

**Descripción:**  
Crea una etiqueta para una imagen.

**Sintaxis:**
```bash
docker tag imagen_origen usuario/repositorio[:etiqueta]
```

**Ejemplos:**
```bash
# Etiquetar una imagen
docker tag mi-app:1.0 mi-usuario/mi-app:1.0

# Crear etiqueta latest
docker tag mi-app:1.0 mi-app:latest

# Preparar para subir a Docker Hub
docker tag mi-app mi-usuario/mi-app:latest
```

### docker push

**Descripción:**  
Sube una imagen a un registro.

**Sintaxis:**
```bash
docker push nombre[:tag]
```

**Ejemplos:**
```bash
# Subir imagen a Docker Hub
docker push mi-usuario/mi-app:latest

# Subir imagen a registro privado
docker push registro-privado:5000/mi-app:1.0
```

### docker history

**Descripción:**  
Muestra el historial de una imagen.

**Sintaxis:**
```bash
docker history [opciones] imagen
```

**Opciones comunes:**
- `--no-trunc`: No truncar la salida
- `-q`, `--quiet`: Mostrar solo IDs

**Ejemplos:**
```bash
# Ver historial completo
docker history nginx

# Ver historial completo sin truncar
docker history --no-trunc nginx
```

## Gestión de Redes

### docker network ls

**Descripción:**  
Lista las redes disponibles.

**Sintaxis:**
```bash
docker network ls [opciones]
```

**Opciones comunes:**
- `-q`, `--quiet`: Mostrar solo IDs
- `--filter`, `-f`: Filtrar redes

**Ejemplos:**
```bash
# Listar todas las redes
docker network ls

# Listar solo IDs
docker network ls -q

# Filtrar por tipo
docker network ls --filter driver=bridge
```

### docker network create

**Descripción:**  
Crea una red.

**Sintaxis:**
```bash
docker network create [opciones] nombre
```

**Opciones comunes:**
- `--driver`, `-d`: Driver de red (bridge, overlay, etc.)
- `--subnet`: Subred en formato CIDR
- `--gateway`: Puerta de enlace
- `--ip-range`: Rango de IPs

**Ejemplos:**
```bash
# Crear red simple
docker network create mi-red

# Crear red con driver específico
docker network create -d bridge mi-red-bridge

# Crear red con configuración de subred
docker network create --subnet=192.168.0.0/16 --gateway=192.168.0.1 mi-red-custom
```

### docker network connect

**Descripción:**  
Conecta un contenedor a una red.

**Sintaxis:**
```bash
docker network connect [opciones] red contenedor
```

**Opciones comunes:**
- `--ip`: IP específica para el contenedor
- `--alias`: Alias para el contenedor en la red

**Ejemplos:**
```bash
# Conectar contenedor a red
docker network connect mi-red mi-contenedor

# Conectar con IP específica
docker network connect --ip 192.168.1.10 mi-red mi-contenedor

# Conectar con alias
docker network connect --alias db mi-red mi-contenedor-db
```

### docker network disconnect

**Descripción:**  
Desconecta un contenedor de una red.

**Sintaxis:**
```bash
docker network disconnect [opciones] red contenedor
```

**Opciones comunes:**
- `-f`, `--force`: Forzar desconexión

**Ejemplos:**
```bash
# Desconectar contenedor de red
docker network disconnect mi-red mi-contenedor

# Forzar desconexión
docker network disconnect -f mi-red mi-contenedor
```

### docker network rm

**Descripción:**  
Elimina una o más redes.

**Sintaxis:**
```bash
docker network rm red [red...]
```

**Ejemplos:**
```bash
# Eliminar una red
docker network rm mi-red

# Eliminar múltiples redes
docker network rm red1 red2

# Eliminar todas las redes no utilizadas
docker network prune
```

### docker network inspect

**Descripción:**  
Muestra información detallada de una red.

**Sintaxis:**
```bash
docker network inspect [opciones] red [red...]
```

**Opciones comunes:**
- `-f`, `--format`: Formato de salida específico

**Ejemplos:**
```bash
# Inspeccionar una red
docker network inspect mi-red

# Obtener información específica
docker network inspect -f '{{.IPAM.Config}}' mi-red
```

## Gestión de Volúmenes

### docker volume ls

**Descripción:**  
Lista los volúmenes disponibles.

**Sintaxis:**
```bash
docker volume ls [opciones]
```

**Opciones comunes:**
- `-q`, `--quiet`: Mostrar solo IDs
- `--filter`, `-f`: Filtrar volúmenes

**Ejemplos:**
```bash
# Listar todos los volúmenes
docker volume ls

# Listar solo IDs
docker volume ls -q

# Filtrar por nombre
docker volume ls -f name=mi-vol
```

### docker volume create

**Descripción:**  
Crea un volumen.

**Sintaxis:**
```bash
docker volume create [opciones] [nombre]
```

**Opciones comunes:**
- `--driver`, `-d`: Driver de volumen
- `--opt`, `-o`: Opciones del driver
- `--label`: Añadir metadatos

**Ejemplos:**
```bash
# Crear volumen simple
docker volume create mi-volumen

# Crear con driver específico
docker volume create --driver local mi-volumen

# Crear con opciones
docker volume create --opt type=nfs --opt device=:/path mi-volumen-nfs
```

### docker volume rm

**Descripción:**  
Elimina uno o más volúmenes.

**Sintaxis:**
```bash
docker volume rm volumen [volumen...]
```

**Ejemplos:**
```bash
# Eliminar un volumen
docker volume rm mi-volumen

# Eliminar múltiples volúmenes
docker volume rm vol1 vol2

# Eliminar todos los volúmenes no utilizados
docker volume prune
```

### docker volume inspect

**Descripción:**  
Muestra información detallada de un volumen.

**Sintaxis:**
```bash
docker volume inspect [opciones] volumen [volumen...]
```

**Opciones comunes:**
- `-f`, `--format`: Formato de salida específico

**Ejemplos:**
```bash
# Inspeccionar un volumen
docker volume inspect mi-volumen

# Obtener información específica
docker volume inspect -f '{{.Mountpoint}}' mi-volumen
```

## Comandos del Sistema

### docker info

**Descripción:**  
Muestra información del sistema Docker.

**Sintaxis:**
```bash
docker info [opciones]
```

**Opciones comunes:**
- `-f`, `--format`: Formato de salida específico

**Ejemplos:**
```bash
# Ver información general
docker info

# Ver información específica
docker info --format '{{.ContainersRunning}}'
```

### docker version

**Descripción:**  
Muestra la versión de Docker.

**Sintaxis:**
```bash
docker version [opciones]
```

**Opciones comunes:**
- `-f`, `--format`: Formato de salida específico

**Ejemplos:**
```bash
# Ver información completa de versión
docker version

# Ver solo versión del cliente
docker version --format '{{.Client.Version}}'
```

### docker system df

**Descripción:**  
Muestra el uso de espacio de Docker.

**Sintaxis:**
```bash
docker system df [opciones]
```

**Opciones comunes:**
- `-v`, `--verbose`: Mostrar información detallada

**Ejemplos:**
```bash
# Ver uso de espacio general
docker system df

# Ver uso detallado
docker system df -v
```

### docker system prune

**Descripción:**  
Elimina recursos no utilizados.

**Sintaxis:**
```bash
docker system prune [opciones]
```

**Opciones comunes:**
- `-a`, `--all`: Eliminar todas las imágenes no usadas
- `--volumes`: Eliminar también volúmenes
- `-f`, `--force`: No pedir confirmación

**Ejemplos:**
```bash
# Eliminar recursos básicos no utilizados
docker system prune

# Eliminar todo lo no utilizado (incl. volúmenes)
docker system prune -af --volumes
```

## Docker Compose

### docker-compose up

**Descripción:**  
Crea y arranca servicios definidos en docker-compose.yml.

**Sintaxis:**
```bash
docker-compose up [opciones] [servicio...]
```

**Opciones comunes:**
- `-d`: Ejecutar en segundo plano
- `--build`: Construir imágenes antes de iniciar
- `--no-deps`: No iniciar servicios vinculados
- `--scale`: Escalar servicios
- `--force-recreate`: Recrear contenedores

**Ejemplos:**
```bash
# Iniciar todos los servicios
docker-compose up

# Iniciar en segundo plano
docker-compose up -d

# Iniciar servicios específicos
docker-compose up web db

# Iniciar con reconstrucción de imágenes
docker-compose up --build

# Escalar un servicio
docker-compose up --scale web=3
```

### docker-compose down

**Descripción:**  
Detiene y elimina servicios, redes, volúmenes y contenedores.

**Sintaxis:**
```bash
docker-compose down [opciones]
```

**Opciones comunes:**
- `--rmi`: Eliminar imágenes (all, local)
- `-v`, `--volumes`: Eliminar volúmenes
- `--remove-orphans`: Eliminar contenedores huérfanos

**Ejemplos:**
```bash
# Detener y eliminar contenedores y redes
docker-compose down

# Eliminar también volúmenes
docker-compose down -v

# Eliminar contenedores, redes, volúmenes e imágenes
docker-compose down --rmi all -v
```

### docker-compose ps

**Descripción:**  
Lista los contenedores de los servicios.

**Sintaxis:**
```bash
docker-compose ps [opciones] [servicio...]
```

**Opciones comunes:**
- `-q`: Mostrar solo IDs
- `--services`: Listar servicios
- `--filter`: Filtrar servicios

**Ejemplos:**
```bash
# Listar todos los contenedores
docker-compose ps

# Listar contenedores de un servicio
docker-compose ps web

# Listar solo IDs
docker-compose ps -q
```

### docker-compose logs

**Descripción:**  
Muestra logs de los servicios.

**Sintaxis:**
```bash
docker-compose logs [opciones] [servicio...]
```

**Opciones comunes:**
- `-f`: Seguir log en tiempo real
- `--tail`: Número de líneas a mostrar
- `--no-color`: Sin colorear la salida

**Ejemplos:**
```bash
# Ver logs de todos los servicios
docker-compose logs

# Seguir logs en tiempo real
docker-compose logs -f

# Ver logs de un servicio específico
docker-compose logs web

# Ver últimas 100 líneas
docker-compose logs --tail=100
```

### docker-compose build

**Descripción:**  
Construye o reconstruye servicios.

**Sintaxis:**
```bash
docker-compose build [opciones] [servicio...]
```

**Opciones comunes:**
- `--no-cache`: No usar caché
- `--pull`: Siempre intentar descargar nuevas imágenes
- `--build-arg`: Variables para la construcción

**Ejemplos:**
```bash
# Construir todos los servicios
docker-compose build

# Construir servicio específico
docker-compose build web

# Construir sin caché
docker-compose build --no-cache
```

### docker-compose run

**Descripción:**  
Ejecuta un comando único en un servicio.

**Sintaxis:**
```bash
docker-compose run [opciones] servicio [comando] [args...]
```

**Opciones comunes:**
- `--rm`: Eliminar contenedor al finalizar
- `-d`: Ejecutar en segundo plano
- `--no-deps`: No iniciar servicios vinculados
- `-e`: Establecer variables de entorno

**Ejemplos:**
```bash
# Ejecutar comando en un servicio
docker-compose run web ls -la

# Ejecutar shell interactivo
docker-compose run --rm web bash

# Ejecutar con variables de entorno
docker-compose run -e DEBUG=1 web python test.py
```

### docker-compose exec

**Descripción:**  
Ejecuta un comando en un contenedor en ejecución.

**Sintaxis:**
```bash
docker-compose exec [opciones] servicio comando [args...]
```

**Opciones comunes:**
- `-T`: Deshabilitar pseudo-TTY
- `-e`: Establecer variables de entorno
- `--index`: Índice del contenedor si hay múltiples instancias

**Ejemplos:**
```bash
# Ejecutar comando en un servicio
docker-compose exec web ls -la

# Ejecutar shell interactivo
docker-compose exec db bash

# Ejecutar en instancia específica (si está escalado)
docker-compose exec --index=2 web bash
```
