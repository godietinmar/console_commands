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

## Docker for AI/ML Applications

### AI/ML Docker Images

#### TensorFlow Containers
```bash
# Ejecutar TensorFlow con Jupyter
docker run -it --rm \
    -p 8888:8888 \
    -v $(pwd):/tf/notebooks \
    tensorflow/tensorflow:latest-jupyter

# TensorFlow con GPU
docker run -it --rm --gpus all \
    -p 8888:8888 \
    -v $(pwd):/tf/notebooks \
    tensorflow/tensorflow:latest-gpu-jupyter

# TensorFlow Serving
docker run -t --rm \
    -p 8501:8501 \
    -v $(pwd)/saved_model:/models/my_model \
    -e MODEL_NAME=my_model \
    tensorflow/serving

# TensorFlow Lite
docker run -it --rm \
    -v $(pwd):/workspace \
    tensorflow/tensorflow:latest \
    python -c "
import tensorflow as tf
converter = tf.lite.TFLiteConverter.from_saved_model('/workspace/saved_model')
tflite_model = converter.convert()
with open('/workspace/model.tflite', 'wb') as f:
    f.write(tflite_model)
print('Model converted to TensorFlow Lite')
"
```

#### PyTorch Containers
```bash
# PyTorch con Jupyter
docker run -it --rm \
    -p 8888:8888 \
    -v $(pwd):/workspace/notebooks \
    pytorch/pytorch:latest \
    jupyter lab --ip=0.0.0.0 --port=8888 --allow-root

# PyTorch con GPU
docker run -it --rm --gpus all \
    -v $(pwd):/workspace \
    pytorch/pytorch:latest-cuda \
    python -c "
import torch
print(f'CUDA available: {torch.cuda.is_available()}')
print(f'CUDA devices: {torch.cuda.device_count()}')
"

# Entrenamiento distribuido con PyTorch
docker run -it --rm --gpus all \
    -v $(pwd):/workspace \
    --network host \
    pytorch/pytorch:latest-cuda \
    python -m torch.distributed.launch \
    --nproc_per_node=2 \
    --nnodes=1 \
    --node_rank=0 \
    --master_addr=localhost \
    --master_port=1234 \
    train.py
```

#### Hugging Face Transformers
```bash
# Hugging Face Transformers
docker run -it --rm \
    -p 8080:8080 \
    -v $(pwd):/app \
    huggingface/transformers-pytorch-gpu:latest \
    python -c "
from transformers import pipeline
nlp = pipeline('sentiment-analysis')
result = nlp('I love this Docker container!')
print(result)
"

# Text Generation API
docker run -d \
    --name text-generator \
    -p 8080:80 \
    --gpus all \
    huggingface/text-generation-inference:latest \
    --model-id microsoft/DialoGPT-medium
```

### Custom AI/ML Dockerfiles

#### Python ML Environment
```bash
# Crear Dockerfile para entorno ML
cat > Dockerfile.ml << 'EOF'
FROM python:3.9-slim

# Instalar dependencias del sistema
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    software-properties-common \
    git \
    && rm -rf /var/lib/apt/lists/*

# Establecer directorio de trabajo
WORKDIR /app

# Copiar requirements
COPY requirements.txt .

# Instalar dependencias Python
RUN pip install --no-cache-dir -r requirements.txt

# Copiar código de la aplicación
COPY . .

# Exponer puerto
EXPOSE 8000

# Comando por defecto
CMD ["python", "app.py"]
EOF

# Crear requirements.txt para ML
cat > requirements.txt << 'EOF'
numpy==1.21.0
pandas==1.3.3
scikit-learn==1.0.2
tensorflow==2.8.0
torch==1.11.0
transformers==4.18.0
fastapi==0.75.0
uvicorn==0.17.6
jupyter==1.0.0
matplotlib==3.5.1
seaborn==0.11.2
plotly==5.6.0
streamlit==1.8.1
opencv-python==4.5.5.64
pillow==9.0.1
requests==2.27.1
aiofiles==0.8.0
python-multipart==0.0.5
EOF

# Construir imagen
docker build -f Dockerfile.ml -t my-ml-app .

# Ejecutar contenedor
docker run -d \
    --name ml-app \
    -p 8000:8000 \
    -v $(pwd)/data:/app/data \
    -v $(pwd)/models:/app/models \
    my-ml-app
```

#### Jupyter Lab con Extensiones AI
```bash
# Dockerfile para Jupyter avanzado
cat > Dockerfile.jupyter << 'EOF'
FROM jupyter/scipy-notebook:latest

USER root

# Instalar dependencias adicionales
RUN apt-get update && apt-get install -y \
    graphviz \
    && rm -rf /var/lib/apt/lists/*

USER $NB_UID

# Instalar extensiones de Jupyter
RUN pip install --no-cache-dir \
    jupyterlab-git \
    jupyterlab-lsp \
    python-lsp-server[all] \
    jupyterlab_code_formatter \
    black \
    isort

# Instalar bibliotecas de ML/AI
RUN pip install --no-cache-dir \
    tensorflow \
    torch \
    transformers \
    accelerate \
    datasets \
    wandb \
    mlflow \
    optuna \
    xgboost \
    lightgbm \
    catboost \
    shap \
    lime \
    eli5

# Habilitar extensiones
RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager

WORKDIR /home/jovyan/work
EOF

# Construir y ejecutar
docker build -f Dockerfile.jupyter -t jupyter-ai .

docker run -d \
    --name jupyter-ai \
    -p 8888:8888 \
    -v $(pwd):/home/jovyan/work \
    -e JUPYTER_ENABLE_LAB=yes \
    jupyter-ai
```

### Model Serving with Docker

#### TensorFlow Serving
```bash
# Preparar modelo para serving
mkdir -p saved_model/1

# Servir modelo con TensorFlow Serving
docker run -d \
    --name tf-serving \
    -p 8501:8501 \
    -p 8500:8500 \
    -v $(pwd)/saved_model:/models/my_model \
    -e MODEL_NAME=my_model \
    tensorflow/serving

# Probar el modelo servido
curl -X POST http://localhost:8501/v1/models/my_model:predict \
     -H "Content-Type: application/json" \
     -d '{"instances": [[1.0, 2.0, 3.0, 4.0]]}'

# Obtener metadata del modelo
curl http://localhost:8501/v1/models/my_model/metadata
```

#### MLflow Model Serving
```bash
# MLflow tracking server
docker run -d \
    --name mlflow-server \
    -p 5000:5000 \
    -v $(pwd)/mlruns:/mlflow/mlruns \
    --env BACKEND_STORE_URI=sqlite:///mlflow/mlflow.db \
    --env DEFAULT_ARTIFACT_ROOT=/mlflow/mlruns \
    python:3.9 \
    bash -c "pip install mlflow && mlflow server --host 0.0.0.0 --port 5000"

# Servir modelo con MLflow
docker run -d \
    --name mlflow-model \
    -p 1234:1234 \
    -v $(pwd)/mlruns:/mlruns \
    python:3.9 \
    bash -c "
    pip install mlflow scikit-learn &&
    mlflow models serve -m /mlruns/0/run_id/artifacts/model -h 0.0.0.0 -p 1234
    "
```

#### FastAPI ML API
```bash
# Crear API FastAPI para modelo ML
cat > app.py << 'EOF'
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
import joblib
import numpy as np
import uvicorn
from typing import List

app = FastAPI(title="ML Model API", version="1.0.0")

# Cargar modelo (ejemplo con joblib)
try:
    model = joblib.load("model.pkl")
    print("Model loaded successfully")
except Exception as e:
    print(f"Error loading model: {e}")
    model = None

class PredictionRequest(BaseModel):
    features: List[float]

class PredictionResponse(BaseModel):
    prediction: float
    probability: float = None

@app.get("/health")
async def health_check():
    return {
        "status": "healthy",
        "model_loaded": model is not None
    }

@app.post("/predict", response_model=PredictionResponse)
async def predict(request: PredictionRequest):
    if model is None:
        raise HTTPException(status_code=503, detail="Model not loaded")
    
    try:
        features = np.array(request.features).reshape(1, -1)
        prediction = model.predict(features)[0]
        
        # Si el modelo soporta probabilidades
        probability = None
        if hasattr(model, 'predict_proba'):
            probability = model.predict_proba(features)[0].max()
        
        return PredictionResponse(
            prediction=float(prediction),
            probability=float(probability) if probability else None
        )
    except Exception as e:
        raise HTTPException(status_code=400, detail=str(e))

@app.post("/batch-predict")
async def batch_predict(requests: List[PredictionRequest]):
    if model is None:
        raise HTTPException(status_code=503, detail="Model not loaded")
    
    try:
        features_list = [req.features for req in requests]
        features_array = np.array(features_list)
        predictions = model.predict(features_array)
        
        return {
            "predictions": predictions.tolist(),
            "count": len(predictions)
        }
    except Exception as e:
        raise HTTPException(status_code=400, detail=str(e))

if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000)
EOF

# Dockerfile para FastAPI ML API
cat > Dockerfile.fastapi << 'EOF'
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .
COPY model.pkl .

EXPOSE 8000

CMD ["python", "app.py"]
EOF

# Construir y ejecutar
docker build -f Dockerfile.fastapi -t ml-api .
docker run -d --name ml-api -p 8000:8000 ml-api
```

### AI/ML Docker Compose Stacks

#### Full ML Pipeline Stack
```bash
# Crear docker-compose.yml para stack ML completo
cat > docker-compose.ml.yml << 'EOF'
version: '3.8'

services:
  # Jupyter Lab para desarrollo
  jupyter:
    image: jupyter/tensorflow-notebook:latest
    ports:
      - "8888:8888"
    volumes:
      - ./notebooks:/home/jovyan/work
      - ./data:/home/jovyan/work/data
      - ./models:/home/jovyan/work/models
    environment:
      - JUPYTER_ENABLE_LAB=yes
    networks:
      - ml-network

  # MLflow tracking server
  mlflow:
    image: python:3.9
    ports:
      - "5000:5000"
    volumes:
      - ./mlruns:/mlflow/mlruns
      - ./mlflow.db:/mlflow/mlflow.db
    command: >
      bash -c "
      pip install mlflow &&
      mlflow server 
        --backend-store-uri sqlite:///mlflow/mlflow.db 
        --default-artifact-root /mlflow/mlruns 
        --host 0.0.0.0 
        --port 5000
      "
    networks:
      - ml-network

  # Model serving API
  model-api:
    build:
      context: .
      dockerfile: Dockerfile.fastapi
    ports:
      - "8000:8000"
    volumes:
      - ./models:/app/models
    environment:
      - MODEL_PATH=/app/models/model.pkl
    depends_on:
      - mlflow
    networks:
      - ml-network

  # Redis para caché
  redis:
    image: redis:alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    networks:
      - ml-network

  # PostgreSQL para metadatos
  postgres:
    image: postgres:13
    environment:
      POSTGRES_DB: mlops
      POSTGRES_USER: mluser
      POSTGRES_PASSWORD: mlpass
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    networks:
      - ml-network

  # Grafana para monitoreo
  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
    volumes:
      - grafana_data:/var/lib/grafana
    networks:
      - ml-network

  # Prometheus para métricas
  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus_data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
    networks:
      - ml-network

volumes:
  redis_data:
  postgres_data:
  grafana_data:
  prometheus_data:

networks:
  ml-network:
    driver: bridge
EOF

# Iniciar stack completo
docker-compose -f docker-compose.ml.yml up -d

# Ver logs
docker-compose -f docker-compose.ml.yml logs -f

# Escalar servicio de API
docker-compose -f docker-compose.ml.yml up -d --scale model-api=3
```

### GPU Support for AI/ML

#### NVIDIA Docker for AI
```bash
# Verificar soporte GPU
docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi

# TensorFlow con GPU
docker run -it --rm --gpus all \
    -v $(pwd):/workspace \
    tensorflow/tensorflow:latest-gpu \
    python -c "
import tensorflow as tf
print('GPU Available:', tf.test.is_gpu_available())
print('GPU Devices:', tf.config.list_physical_devices('GPU'))
"

# PyTorch con GPU
docker run -it --rm --gpus all \
    -v $(pwd):/workspace \
    pytorch/pytorch:latest-cuda \
    python -c "
import torch
print('CUDA Available:', torch.cuda.is_available())
print('GPU Count:', torch.cuda.device_count())
print('Current GPU:', torch.cuda.current_device())
"

# Entrenamiento distribuido multi-GPU
docker run -it --rm --gpus all \
    -v $(pwd):/workspace \
    --shm-size=1g \
    --ipc=host \
    pytorch/pytorch:latest-cuda \
    python -m torch.distributed.launch \
    --nproc_per_node=$(nvidia-smi -L | wc -l) \
    train_distributed.py
```

### AI/ML Monitoring and Logging

#### Containerized Model Monitoring
```bash
# Prometheus config para monitoreo ML
cat > prometheus.yml << 'EOF'
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'ml-api'
    static_configs:
      - targets: ['model-api:8000']
    metrics_path: /metrics
    scrape_interval: 5s

  - job_name: 'mlflow'
    static_configs:
      - targets: ['mlflow:5000']
    scrape_interval: 30s
EOF

# Agregar métricas a FastAPI
cat >> app.py << 'EOF'

from prometheus_client import Counter, Histogram, generate_latest, CONTENT_TYPE_LATEST
import time

# Métricas Prometheus
prediction_counter = Counter('ml_predictions_total', 'Total predictions made')
prediction_histogram = Histogram('ml_prediction_duration_seconds', 'Time spent on predictions')
error_counter = Counter('ml_prediction_errors_total', 'Total prediction errors')

@app.middleware("http")
async def add_process_time_header(request, call_next):
    start_time = time.time()
    response = await call_next(request)
    process_time = time.time() - start_time
    response.headers["X-Process-Time"] = str(process_time)
    return response

@app.get("/metrics")
async def get_metrics():
    return Response(generate_latest(), media_type=CONTENT_TYPE_LATEST)
EOF

echo "AI/ML Docker configuration completed!"
```

### Automation Scripts for AI/ML Docker

#### Model Training Pipeline Script
```bash
#!/bin/bash
# train_model_docker.sh
cat > train_model_docker.sh << 'EOF'
#!/bin/bash

set -e

echo "Starting ML training pipeline with Docker..."

# Variables
MODEL_NAME=${1:-"my_model"}
DATA_PATH=${2:-"./data"}
OUTPUT_PATH=${3:-"./models"}

# Crear directorios si no existen
mkdir -p $DATA_PATH $OUTPUT_PATH

# Generar datos sintéticos si no existen
if [ ! -f "$DATA_PATH/train.csv" ]; then
    echo "Generating synthetic training data..."
    docker run --rm \
        -v $(pwd)/$DATA_PATH:/data \
        python:3.9 \
        python -c "
import pandas as pd
import numpy as np

# Generar datos sintéticos
np.random.seed(42)
X = np.random.randn(1000, 5)
y = (X.sum(axis=1) + np.random.randn(1000) * 0.1) > 0

df = pd.DataFrame(X, columns=[f'feature_{i}' for i in range(5)])
df['target'] = y.astype(int)

df.to_csv('/data/train.csv', index=False)
print(f'Generated {len(df)} training samples')
"
fi

# Entrenar modelo
echo "Training model: $MODEL_NAME"
docker run --rm \
    -v $(pwd)/$DATA_PATH:/data \
    -v $(pwd)/$OUTPUT_PATH:/models \
    python:3.9 \
    bash -c "
pip install pandas scikit-learn joblib &&
python -c \"
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score
import joblib

# Cargar datos
df = pd.read_csv('/data/train.csv')
X = df.drop('target', axis=1)
y = df['target']

# Dividir datos
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Entrenar modelo
model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X_train, y_train)

# Evaluar
train_acc = accuracy_score(y_train, model.predict(X_train))
test_acc = accuracy_score(y_test, model.predict(X_test))

print(f'Train Accuracy: {train_acc:.3f}')
print(f'Test Accuracy: {test_acc:.3f}')

# Guardar modelo
joblib.dump(model, '/models/${MODEL_NAME}.pkl')
print('Model saved successfully')
\"
"

# Validar modelo guardado
echo "Validating saved model..."
docker run --rm \
    -v $(pwd)/$OUTPUT_PATH:/models \
    python:3.9 \
    bash -c "
pip install joblib numpy &&
python -c \"
import joblib
import numpy as np

# Cargar modelo
model = joblib.load('/models/${MODEL_NAME}.pkl')
print('Model loaded successfully')

# Hacer predicción de prueba
test_input = np.random.randn(1, 5)
prediction = model.predict(test_input)
print(f'Test prediction: {prediction[0]}')
\"
"

echo "Training pipeline completed successfully!"
echo "Model saved to: $OUTPUT_PATH/${MODEL_NAME}.pkl"
EOF

chmod +x train_model_docker.sh

# Ejecutar pipeline
./train_model_docker.sh my_model ./data ./models
```
