# 🌐 Comandos de Google Cloud Platform (gcloud)

Una guía completa de comandos para Google Cloud Platform usando gcloud CLI.

## Instalación y Configuración

### Instalar gcloud CLI
```bash
# Linux/macOS con curl
curl https://sdk.cloud.google.com | bash
exec -l $SHELL

# macOS con Homebrew
brew install google-cloud-sdk

# Ubuntu/Debian
sudo apt-get update
sudo apt-get install google-cloud-sdk

# CentOS/RHEL/Fedora
sudo dnf install google-cloud-sdk

# Verificar instalación
gcloud --version
```

### Configurar gcloud CLI
```bash
# Inicializar configuración
gcloud init

# Autenticación
gcloud auth login

# Autenticación con service account
gcloud auth activate-service-account --key-file=path/to/key.json

# Listar cuentas autenticadas
gcloud auth list

# Configurar proyecto por defecto
gcloud config set project PROJECT_ID

# Configurar región por defecto
gcloud config set compute/region us-central1

# Configurar zona por defecto
gcloud config set compute/zone us-central1-a

# Mostrar configuración actual
gcloud config list

# Crear nueva configuración
gcloud config configurations create development

# Cambiar entre configuraciones
gcloud config configurations activate production
```

## Compute Engine

### Instancias
```bash
# Listar instancias
gcloud compute instances list

# Crear instancia
gcloud compute instances create my-instance \
    --zone=us-central1-a \
    --machine-type=e2-medium \
    --image-family=ubuntu-2004-lts \
    --image-project=ubuntu-os-cloud \
    --boot-disk-size=10GB

# Crear instancia con startup script
gcloud compute instances create my-instance \
    --zone=us-central1-a \
    --machine-type=e2-medium \
    --image-family=ubuntu-2004-lts \
    --image-project=ubuntu-os-cloud \
    --metadata-from-file startup-script=startup.sh

# Iniciar instancia
gcloud compute instances start my-instance --zone=us-central1-a

# Detener instancia
gcloud compute instances stop my-instance --zone=us-central1-a

# Reiniciar instancia
gcloud compute instances reset my-instance --zone=us-central1-a

# Eliminar instancia
gcloud compute instances delete my-instance --zone=us-central1-a

# Describir instancia
gcloud compute instances describe my-instance --zone=us-central1-a

# Conectar por SSH
gcloud compute ssh my-instance --zone=us-central1-a

# Transferir archivos por SCP
gcloud compute scp local-file.txt my-instance:~/ --zone=us-central1-a
```

### Machine Types
```bash
# Listar tipos de máquina
gcloud compute machine-types list

# Listar tipos por zona
gcloud compute machine-types list --zones=us-central1-a

# Cambiar tipo de máquina
gcloud compute instances set-machine-type my-instance \
    --machine-type=e2-standard-2 \
    --zone=us-central1-a
```

### Imágenes
```bash
# Listar imágenes
gcloud compute images list

# Listar familias de imágenes
gcloud compute images list --no-standard-images

# Crear imagen personalizada
gcloud compute images create my-image \
    --source-disk=my-disk \
    --source-disk-zone=us-central1-a

# Eliminar imagen
gcloud compute images delete my-image
```

### Discos
```bash
# Listar discos
gcloud compute disks list

# Crear disco
gcloud compute disks create my-disk \
    --size=100GB \
    --zone=us-central1-a \
    --type=pd-standard

# Adjuntar disco a instancia
gcloud compute instances attach-disk my-instance \
    --disk=my-disk \
    --zone=us-central1-a

# Desadjuntar disco
gcloud compute instances detach-disk my-instance \
    --disk=my-disk \
    --zone=us-central1-a

# Crear snapshot
gcloud compute disks snapshot my-disk \
    --snapshot-names=my-snapshot \
    --zone=us-central1-a
```

### Redes y Firewall
```bash
# Listar redes
gcloud compute networks list

# Crear red VPC
gcloud compute networks create my-network --subnet-mode=custom

# Crear subnet
gcloud compute networks subnets create my-subnet \
    --network=my-network \
    --range=10.1.0.0/16 \
    --region=us-central1

# Listar reglas de firewall
gcloud compute firewall-rules list

# Crear regla de firewall
gcloud compute firewall-rules create allow-http \
    --allow tcp:80 \
    --source-ranges 0.0.0.0/0 \
    --description "Allow HTTP traffic"

# Eliminar regla de firewall
gcloud compute firewall-rules delete allow-http
```

### Load Balancers
```bash
# Crear health check
gcloud compute health-checks create http my-health-check \
    --port 80

# Crear backend service
gcloud compute backend-services create my-backend-service \
    --protocol=HTTP \
    --health-checks=my-health-check \
    --global

# Crear URL map
gcloud compute url-maps create my-url-map \
    --default-service=my-backend-service

# Crear HTTP proxy
gcloud compute target-http-proxies create my-http-proxy \
    --url-map=my-url-map

# Crear forwarding rule
gcloud compute forwarding-rules create my-http-rule \
    --global \
    --target-http-proxy=my-http-proxy \
    --ports=80
```

## App Engine

### Aplicaciones
```bash
# Crear aplicación App Engine
gcloud app create --region=us-central

# Deployar aplicación
gcloud app deploy

# Deployar versión específica
gcloud app deploy --version=v2

# Listar versiones
gcloud app versions list

# Establecer tráfico entre versiones
gcloud app services set-traffic default \
    --splits=v1=0.5,v2=0.5

# Ver logs
gcloud app logs tail -s default

# Abrir aplicación en navegador
gcloud app browse

# Descripción de aplicación
gcloud app describe
```

### Servicios
```bash
# Listar servicios
gcloud app services list

# Describir servicio
gcloud app services describe default

# Eliminar versión
gcloud app versions delete v1 --service=default
```

## Cloud Storage

### Buckets
```bash
# Listar buckets
gsutil ls

# Crear bucket
gsutil mb gs://my-unique-bucket-name

# Eliminar bucket vacío
gsutil rb gs://my-unique-bucket-name

# Eliminar bucket con contenido
gsutil rm -r gs://my-unique-bucket-name
```

### Objetos
```bash
# Listar objetos en bucket
gsutil ls gs://my-bucket/

# Subir archivo
gsutil cp file.txt gs://my-bucket/

# Subir directorio
gsutil cp -r ./local-dir gs://my-bucket/

# Descargar archivo
gsutil cp gs://my-bucket/file.txt ./

# Sincronizar directorios
gsutil rsync -r ./local-dir gs://my-bucket/remote-dir

# Mover archivo
gsutil mv gs://my-bucket/old-file.txt gs://my-bucket/new-file.txt

# Eliminar archivo
gsutil rm gs://my-bucket/file.txt

# Hacer público un archivo
gsutil acl ch -u AllUsers:R gs://my-bucket/file.txt

# Configurar CORS
gsutil cors set cors.json gs://my-bucket
```

### Configuración de Bucket
```bash
# Configurar versionado
gsutil versioning set on gs://my-bucket

# Configurar lifecycle
gsutil lifecycle set lifecycle.json gs://my-bucket

# Configurar website
gsutil web set -m index.html -e 404.html gs://my-bucket

# Ver información del bucket
gsutil ls -L gs://my-bucket
```

## Cloud SQL

### Instancias
```bash
# Crear instancia MySQL
gcloud sql instances create my-instance \
    --database-version=MYSQL_8_0 \
    --tier=db-f1-micro \
    --region=us-central1

# Crear instancia PostgreSQL
gcloud sql instances create my-postgres-instance \
    --database-version=POSTGRES_13 \
    --tier=db-f1-micro \
    --region=us-central1

# Listar instancias
gcloud sql instances list

# Describir instancia
gcloud sql instances describe my-instance

# Conectar a instancia
gcloud sql connect my-instance --user=root

# Reiniciar instancia
gcloud sql instances restart my-instance

# Eliminar instancia
gcloud sql instances delete my-instance
```

### Bases de Datos
```bash
# Crear base de datos
gcloud sql databases create my-database --instance=my-instance

# Listar bases de datos
gcloud sql databases list --instance=my-instance

# Eliminar base de datos
gcloud sql databases delete my-database --instance=my-instance
```

### Usuarios
```bash
# Crear usuario
gcloud sql users create my-user \
    --instance=my-instance \
    --password=my-password

# Listar usuarios
gcloud sql users list --instance=my-instance

# Cambiar password
gcloud sql users set-password my-user \
    --instance=my-instance \
    --password=new-password

# Eliminar usuario
gcloud sql users delete my-user --instance=my-instance
```

### Backups
```bash
# Crear backup
gcloud sql backups create --instance=my-instance

# Listar backups
gcloud sql backups list --instance=my-instance

# Restaurar desde backup
gcloud sql backups restore BACKUP_ID \
    --restore-instance=my-instance
```

## Cloud Functions

### Funciones
```bash
# Deployar función HTTP
gcloud functions deploy my-function \
    --runtime=python39 \
    --trigger-http \
    --entry-point=hello_world \
    --source=.

# Deployar función con trigger de Cloud Storage
gcloud functions deploy my-function \
    --runtime=python39 \
    --trigger-bucket=my-bucket \
    --entry-point=process_file \
    --source=.

# Deployar función con trigger de Pub/Sub
gcloud functions deploy my-function \
    --runtime=python39 \
    --trigger-topic=my-topic \
    --entry-point=process_message \
    --source=.

# Listar funciones
gcloud functions list

# Describir función
gcloud functions describe my-function

# Invocar función
gcloud functions call my-function --data='{"name":"World"}'

# Ver logs
gcloud functions logs read my-function

# Eliminar función
gcloud functions delete my-function
```

## Google Kubernetes Engine (GKE)

### Clusters
```bash
# Crear cluster
gcloud container clusters create my-cluster \
    --zone=us-central1-a \
    --num-nodes=3

# Crear cluster con autopilot
gcloud container clusters create-auto my-autopilot-cluster \
    --region=us-central1

# Listar clusters
gcloud container clusters list

# Obtener credenciales
gcloud container clusters get-credentials my-cluster \
    --zone=us-central1-a

# Redimensionar cluster
gcloud container clusters resize my-cluster \
    --num-nodes=5 \
    --zone=us-central1-a

# Actualizar cluster
gcloud container clusters upgrade my-cluster \
    --zone=us-central1-a

# Eliminar cluster
gcloud container clusters delete my-cluster \
    --zone=us-central1-a
```

### Node Pools
```bash
# Crear node pool
gcloud container node-pools create my-node-pool \
    --cluster=my-cluster \
    --zone=us-central1-a \
    --num-nodes=2 \
    --machine-type=e2-medium

# Listar node pools
gcloud container node-pools list --cluster=my-cluster \
    --zone=us-central1-a

# Eliminar node pool
gcloud container node-pools delete my-node-pool \
    --cluster=my-cluster \
    --zone=us-central1-a
```

## Cloud Run

### Servicios
```bash
# Deployar desde código fuente
gcloud run deploy my-service \
    --source=. \
    --region=us-central1 \
    --allow-unauthenticated

# Deployar desde imagen
gcloud run deploy my-service \
    --image=gcr.io/PROJECT_ID/my-image \
    --region=us-central1 \
    --allow-unauthenticated

# Listar servicios
gcloud run services list

# Describir servicio
gcloud run services describe my-service \
    --region=us-central1

# Configurar variables de entorno
gcloud run services update my-service \
    --update-env-vars=KEY1=VALUE1,KEY2=VALUE2 \
    --region=us-central1

# Ver logs
gcloud logs tail "resource.type=cloud_run_revision"

# Eliminar servicio
gcloud run services delete my-service \
    --region=us-central1
```

## Cloud Build

### Builds
```bash
# Ejecutar build desde código fuente
gcloud builds submit --tag gcr.io/PROJECT_ID/my-image

# Ejecutar build con archivo de configuración
gcloud builds submit --config=cloudbuild.yaml

# Listar builds
gcloud builds list

# Describir build
gcloud builds describe BUILD_ID

# Ver logs de build
gcloud builds log BUILD_ID

# Cancelar build
gcloud builds cancel BUILD_ID
```

### Triggers
```bash
# Crear trigger desde GitHub
gcloud builds triggers create github \
    --repo-name=my-repo \
    --repo-owner=my-github-username \
    --branch-pattern=".*" \
    --build-config=cloudbuild.yaml

# Listar triggers
gcloud builds triggers list

# Ejecutar trigger manualmente
gcloud builds triggers run my-trigger --branch=main

# Eliminar trigger
gcloud builds triggers delete TRIGGER_ID
```

## Cloud Pub/Sub

### Topics
```bash
# Crear topic
gcloud pubsub topics create my-topic

# Listar topics
gcloud pubsub topics list

# Publicar mensaje
gcloud pubsub topics publish my-topic --message="Hello World"

# Eliminar topic
gcloud pubsub topics delete my-topic
```

### Subscriptions
```bash
# Crear subscription
gcloud pubsub subscriptions create my-subscription \
    --topic=my-topic

# Listar subscriptions
gcloud pubsub subscriptions list

# Recibir mensajes
gcloud pubsub subscriptions pull my-subscription --auto-ack

# Eliminar subscription
gcloud pubsub subscriptions delete my-subscription
```

## Cloud IAM

### Políticas
```bash
# Ver política IAM del proyecto
gcloud projects get-iam-policy PROJECT_ID

# Añadir rol a usuario
gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="user:user@example.com" \
    --role="roles/editor"

# Añadir rol a service account
gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="serviceAccount:my-sa@PROJECT_ID.iam.gserviceaccount.com" \
    --role="roles/storage.admin"

# Remover rol
gcloud projects remove-iam-policy-binding PROJECT_ID \
    --member="user:user@example.com" \
    --role="roles/editor"
```

### Service Accounts
```bash
# Crear service account
gcloud iam service-accounts create my-service-account \
    --description="My service account" \
    --display-name="My Service Account"

# Listar service accounts
gcloud iam service-accounts list

# Crear key para service account
gcloud iam service-accounts keys create key.json \
    --iam-account=my-service-account@PROJECT_ID.iam.gserviceaccount.com

# Listar keys
gcloud iam service-accounts keys list \
    --iam-account=my-service-account@PROJECT_ID.iam.gserviceaccount.com

# Eliminar service account
gcloud iam service-accounts delete \
    my-service-account@PROJECT_ID.iam.gserviceaccount.com
```

## Cloud Firestore

### Bases de Datos
```bash
# Crear índice
gcloud firestore indexes composite create \
    --collection-group=my-collection \
    --field-config field-path=field1,order=ascending \
    --field-config field-path=field2,order=descending

# Listar índices
gcloud firestore indexes composite list

# Importar datos
gcloud firestore import gs://my-bucket/export-folder

# Exportar datos
gcloud firestore export gs://my-bucket/export-folder
```

## Cloud Monitoring

### Alertas
```bash
# Crear política de alerta
gcloud alpha monitoring policies create --policy-from-file=policy.yaml

# Listar políticas de alerta
gcloud alpha monitoring policies list

# Habilitar política
gcloud alpha monitoring policies update POLICY_ID --update-enabled=true
```

## Cloud Logging

### Logs
```bash
# Ver logs recientes
gcloud logging read "timestamp >= \"2023-01-01T00:00:00Z\""

# Ver logs de recurso específico
gcloud logging read "resource.type=gce_instance"

# Ver logs con filtro
gcloud logging read "severity>=ERROR"

# Crear sink
gcloud logging sinks create my-sink \
    storage.googleapis.com/my-bucket \
    --log-filter="severity>=ERROR"

# Listar sinks
gcloud logging sinks list

# Eliminar sink
gcloud logging sinks delete my-sink
```

## Cloud DNS

### Zonas DNS
```bash
# Crear zona DNS
gcloud dns managed-zones create my-zone \
    --dns-name=example.com. \
    --description="My DNS zone"

# Listar zonas
gcloud dns managed-zones list

# Describir zona
gcloud dns managed-zones describe my-zone
```

### Records DNS
```bash
# Iniciar transacción
gcloud dns record-sets transaction start --zone=my-zone

# Añadir record A
gcloud dns record-sets transaction add 1.2.3.4 \
    --name=www.example.com. \
    --ttl=300 \
    --type=A \
    --zone=my-zone

# Ejecutar transacción
gcloud dns record-sets transaction execute --zone=my-zone

# Listar records
gcloud dns record-sets list --zone=my-zone
```

## Cloud Composer (Apache Airflow)

### Environments
```bash
# Crear environment
gcloud composer environments create my-environment \
    --location=us-central1 \
    --python-version=3

# Listar environments
gcloud composer environments list

# Describir environment
gcloud composer environments describe my-environment \
    --location=us-central1

# Ejecutar comando Airflow
gcloud composer environments run my-environment \
    --location=us-central1 \
    dags list

# Eliminar environment
gcloud composer environments delete my-environment \
    --location=us-central1
```

## Cloud Spanner

### Instancias
```bash
# Crear instancia
gcloud spanner instances create my-instance \
    --config=regional-us-central1 \
    --description="My Spanner instance" \
    --nodes=1

# Listar instancias
gcloud spanner instances list

# Crear base de datos
gcloud spanner databases create my-database \
    --instance=my-instance

# Ejecutar SQL
gcloud spanner databases execute-sql my-database \
    --instance=my-instance \
    --sql="SELECT 1"
```

## BigQuery

### Datasets
```bash
# Crear dataset
bq mk my_dataset

# Listar datasets
bq ls

# Describir dataset
bq show my_dataset

# Eliminar dataset
bq rm -r my_dataset
```

### Tablas
```bash
# Crear tabla
bq mk my_dataset.my_table schema.json

# Listar tablas
bq ls my_dataset

# Cargar datos desde archivo
bq load my_dataset.my_table data.csv

# Ejecutar query
bq query --use_legacy_sql=false 'SELECT * FROM my_dataset.my_table LIMIT 10'

# Exportar tabla
bq extract my_dataset.my_table gs://my-bucket/export.csv
```

## Comandos Útiles Generales

### Proyectos
```bash
# Listar proyectos
gcloud projects list

# Crear proyecto
gcloud projects create PROJECT_ID

# Establecer proyecto actual
gcloud config set project PROJECT_ID

# Obtener información del proyecto
gcloud projects describe PROJECT_ID

# Eliminar proyecto
gcloud projects delete PROJECT_ID
```

### Facturación
```bash
# Listar cuentas de facturación
gcloud billing accounts list

# Vincular proyecto a cuenta de facturación
gcloud billing projects link PROJECT_ID \
    --billing-account=BILLING_ACCOUNT_ID
```

### APIs y Servicios
```bash
# Listar APIs habilitadas
gcloud services list --enabled

# Habilitar API
gcloud services enable compute.googleapis.com

# Deshabilitar API
gcloud services disable compute.googleapis.com

# Listar APIs disponibles
gcloud services list --available
```

### Información y Ayuda
```bash
# Información de gcloud
gcloud info

# Ayuda general
gcloud help

# Ayuda de comando específico
gcloud compute instances create --help

# Actualizar gcloud
gcloud components update

# Instalar componentes adicionales
gcloud components install kubectl
```

## Scripts de Automatización

### Script de Backup de Compute Engine
```bash
#!/bin/bash
# backup-instances.sh
PROJECT_ID="my-project"
ZONE="us-central1-a"

for instance in $(gcloud compute instances list --zones=$ZONE --format="value(name)"); do
    echo "Creating snapshot for instance: $instance"
    gcloud compute disks snapshot $instance \
        --zone=$ZONE \
        --snapshot-names=$instance-$(date +%Y%m%d-%H%M%S)
done
```

### Script de Monitoreo de Recursos
```bash
#!/bin/bash
# monitor-resources.sh
echo "=== Compute Instances ==="
gcloud compute instances list

echo "=== Cloud Storage Buckets ==="
gsutil ls

echo "=== App Engine Services ==="
gcloud app services list

echo "=== Cloud SQL Instances ==="
gcloud sql instances list
```

---

## 📚 Recursos Adicionales

- [Documentación oficial de gcloud CLI](https://cloud.google.com/sdk/docs)
- [Referencia de comandos gcloud](https://cloud.google.com/sdk/gcloud/reference)
- [Google Cloud CLI GitHub Repository](https://github.com/GoogleCloudPlatform/cloud-sdk-docker)
- [Ejemplos y tutoriales de GCP](https://cloud.google.com/docs/tutorials)

## Google Cloud AI/ML Services

### Vertex AI
```bash
# Habilitar Vertex AI API
gcloud services enable aiplatform.googleapis.com

# Crear dataset
gcloud ai datasets create \
    --display-name=my-dataset \
    --metadata-schema-uri=gs://google-cloud-aiplatform/schema/dataset/metadata/image_1.0.0.yaml \
    --region=us-central1

# Listar datasets
gcloud ai datasets list --region=us-central1

# Crear training job
gcloud ai custom-jobs create \
    --region=us-central1 \
    --display-name=my-training-job \
    --config=training-config.yaml

# Listar training jobs
gcloud ai custom-jobs list --region=us-central1

# Crear modelo
gcloud ai models upload \
    --region=us-central1 \
    --display-name=my-model \
    --container-image-uri=gcr.io/my-project/my-model:latest

# Deploy modelo a endpoint
gcloud ai endpoints create \
    --region=us-central1 \
    --display-name=my-endpoint

gcloud ai endpoints deploy-model ENDPOINT_ID \
    --region=us-central1 \
    --model=MODEL_ID \
    --display-name=my-deployment \
    --machine-type=n1-standard-4

# Hacer predicción
gcloud ai endpoints predict ENDPOINT_ID \
    --region=us-central1 \
    --json-request=prediction-input.json

# Listar modelos
gcloud ai models list --region=us-central1

# Listar endpoints
gcloud ai endpoints list --region=us-central1
```

### AutoML
```bash
# Crear dataset de AutoML Vision
gcloud ai datasets create \
    --display-name=automl-vision-dataset \
    --metadata-schema-uri=gs://google-cloud-aiplatform/schema/dataset/metadata/image_1.0.0.yaml \
    --region=us-central1

# Importar datos a dataset
gcloud ai datasets import-data DATASET_ID \
    --region=us-central1 \
    --import-schema-uri=gs://google-cloud-aiplatform/schema/dataset/ioformat/image_classification_single_label_io_format_1.0.0.yaml \
    --data-source-uris=gs://my-bucket/training-data.csv

# Entrenar modelo AutoML
gcloud ai training-pipelines create \
    --region=us-central1 \
    --display-name=automl-training \
    --training-task-definition=gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_image_classification_1.0.0.yaml \
    --training-task-inputs-file=automl-config.json

# Crear dataset de AutoML Tables
gcloud ai datasets create \
    --display-name=automl-tables-dataset \
    --metadata-schema-uri=gs://google-cloud-aiplatform/schema/dataset/metadata/tabular_1.0.0.yaml \
    --region=us-central1
```

### Vision AI
```bash
# Detectar etiquetas en imagen
gcloud ml vision detect-labels gs://my-bucket/image.jpg

# Detectar texto en imagen
gcloud ml vision detect-text gs://my-bucket/document.jpg

# Detectar caras
gcloud ml vision detect-faces gs://my-bucket/people.jpg

# Detectar objetos
gcloud ml vision detect-objects gs://my-bucket/scene.jpg

# Análisis de imagen completo
gcloud ml vision detect-labels,detect-text,detect-faces gs://my-bucket/image.jpg

# Detectar contenido explícito
gcloud ml vision detect-safe-search gs://my-bucket/image.jpg

# Detectar puntos de referencia
gcloud ml vision detect-landmarks gs://my-bucket/landmark.jpg

# OCR con Document AI
gcloud documentai processors process \
    --processor=PROCESSOR_ID \
    --location=us \
    --input-mime-type=application/pdf \
    --raw-document-file-path=document.pdf
```

### Natural Language AI
```bash
# Analizar sentimiento
gcloud ml language analyze-sentiment --content="I love this product!"

# Detectar entidades
gcloud ml language analyze-entities --content="Google Cloud is based in California"

# Análisis de sintaxis
gcloud ml language analyze-syntax --content="The quick brown fox jumps over the lazy dog"

# Clasificar texto
gcloud ml language classify-text --content="This is a technology article about machine learning"

# Análisis desde archivo
gcloud ml language analyze-sentiment --content-file=review.txt

# Análisis en lote
gcloud ml language analyze-sentiment \
    --content="First review text" \
    --content="Second review text"
```

### Speech-to-Text
```bash
# Transcribir audio
gcloud ml speech recognize gs://my-bucket/audio.wav \
    --language-code=en-US

# Transcripción con configuración avanzada
gcloud ml speech recognize gs://my-bucket/audio.wav \
    --language-code=en-US \
    --enable-automatic-punctuation \
    --enable-word-time-offsets \
    --model=latest_long

# Transcripción de audio largo (asíncrona)
gcloud ml speech recognize-long-running gs://my-bucket/long-audio.wav \
    --language-code=en-US \
    --async

# Obtener resultado de operación asíncrona
gcloud ml speech operations describe OPERATION_ID

# Transcripción en tiempo real
gcloud ml speech recognize-streaming \
    --language-code=en-US \
    --sample-rate=16000 \
    --encoding=LINEAR16
```

### Text-to-Speech
```bash
# Sintetizar voz
gcloud ml text-to-speech synthesize \
    --text="Hello, this is Google Cloud Text-to-Speech" \
    --output-file=output.mp3 \
    --voice-name=en-US-Wavenet-D

# Listar voces disponibles
gcloud ml text-to-speech voices list

# Sintetizar con SSML
gcloud ml text-to-speech synthesize \
    --ssml='<speak>Hello <break time="2s"/> World!</speak>' \
    --output-file=ssml-output.mp3 \
    --voice-name=en-US-Neural2-F

# Sintetizar en diferentes idiomas
gcloud ml text-to-speech synthesize \
    --text="Hola, ¿cómo estás?" \
    --output-file=spanish.mp3 \
    --voice-name=es-ES-Neural2-A \
    --language-code=es-ES
```

### Translation AI
```bash
# Traducir texto
gcloud ml translate detect-language "Hello World"

# Traducir con idiomas específicos
gcloud ml translate translate "Hello World" \
    --source-language=en \
    --target-language=es

# Traducir múltiples textos
gcloud ml translate translate \
    "Hello" "Goodbye" "Thank you" \
    --target-language=fr

# Listar idiomas soportados
gcloud ml translate languages list

# Traducir documento
gcloud ml translate translate-document \
    --source-file=document.txt \
    --target-language=es \
    --output-file=documento.txt
```

### Video Intelligence AI
```bash
# Analizar video
gcloud ml video-intelligence detect-labels gs://my-bucket/video.mp4

# Detectar cambios de escena
gcloud ml video-intelligence detect-shots gs://my-bucket/video.mp4

# Detectar contenido explícito en video
gcloud ml video-intelligence detect-explicit-content gs://my-bucket/video.mp4

# Transcribir audio de video
gcloud ml video-intelligence transcribe-speech gs://my-bucket/video.mp4 \
    --language-code=en-US

# Detectar texto en video
gcloud ml video-intelligence detect-text gs://my-bucket/video.mp4

# Análisis completo de video
gcloud ml video-intelligence detect-labels,detect-shots,transcribe-speech \
    gs://my-bucket/video.mp4 \
    --language-code=en-US \
    --async
```

### BigQuery ML
```bash
# Crear modelo de ML en BigQuery
bq query --use_legacy_sql=false '
CREATE MODEL `my_project.my_dataset.my_model`
OPTIONS(model_type="linear_reg") AS
SELECT
  feature1,
  feature2,
  target
FROM
  `my_project.my_dataset.training_data`'

# Evaluar modelo
bq query --use_legacy_sql=false '
SELECT
  *
FROM
  ML.EVALUATE(MODEL `my_project.my_dataset.my_model`,
    (SELECT * FROM `my_project.my_dataset.test_data`))'

# Hacer predicciones
bq query --use_legacy_sql=false '
SELECT
  *
FROM
  ML.PREDICT(MODEL `my_project.my_dataset.my_model`,
    (SELECT * FROM `my_project.my_dataset.new_data`))'

# Listar modelos de ML
bq ls --format=prettyjson my_dataset
```

### AI Platform Notebooks
```bash
# Crear instancia de notebook
gcloud notebooks instances create my-notebook \
    --vm-image-project=deeplearning-platform-release \
    --vm-image-family=tf2-latest-gpu \
    --machine-type=n1-standard-4 \
    --location=us-central1-b

# Listar instancias de notebook
gcloud notebooks instances list

# Iniciar instancia
gcloud notebooks instances start my-notebook \
    --location=us-central1-b

# Detener instancia
gcloud notebooks instances stop my-notebook \
    --location=us-central1-b

# Eliminar instancia
gcloud notebooks instances delete my-notebook \
    --location=us-central1-b
```

### Dialogflow
```bash
# Crear agente
gcloud dialogflow agents create \
    --display-name="My Agent" \
    --default-language-code=en \
    --time-zone="America/New_York"

# Listar agentes
gcloud dialogflow agents list

# Crear intent
gcloud dialogflow intents create \
    --agent=AGENT_ID \
    --display-name="greeting" \
    --training-phrases="Hello,Hi,Good morning"

# Entrenar agente
gcloud dialogflow agents train AGENT_ID

# Detectar intent
gcloud dialogflow detect-intent \
    --agent=AGENT_ID \
    --session-id=test-session \
    --query-text="Hello there"
```

### Firebase ML
```bash
# Configurar Firebase CLI
npm install -g firebase-tools
firebase login

# Inicializar proyecto Firebase ML
firebase init ml

# Deploy modelo personalizado
firebase ml:deploy my-model \
    --model-file=model.tflite

# Listar modelos
firebase ml:list

# Eliminar modelo
firebase ml:delete my-model
```

### Scripts de Automatización para AI/ML

#### Script de Análisis de Imágenes en Lote
```bash
#!/bin/bash
# batch-image-analysis.sh
BUCKET="my-images-bucket"
PREFIX="uploads/"

# Analizar todas las imágenes en el bucket
gsutil ls gs://$BUCKET/$PREFIX*.jpg | while read -r image; do
    echo "Analyzing image: $image"
    
    # Detectar etiquetas
    gcloud ml vision detect-labels "$image" > "${image##*/}-labels.json"
    
    # Detectar texto
    gcloud ml vision detect-text "$image" > "${image##*/}-text.json"
    
    echo "Results saved for $image"
done
```

#### Script de Transcripción Masiva
```bash
#!/bin/bash
# batch-transcription.sh
BUCKET="my-audio-bucket"

# Transcribir todos los archivos de audio
gsutil ls gs://$BUCKET/*.wav | while read -r audio; do
    echo "Transcribing: $audio"
    
    gcloud ml speech recognize "$audio" \
        --language-code=en-US \
        --enable-automatic-punctuation > "${audio##*/}-transcript.json"
    
    echo "Transcription completed for $audio"
done
```

#### Script de Monitoreo de ML
```bash
#!/bin/bash
# monitor-ml-services.sh
echo "=== Vertex AI Models ==="
gcloud ai models list --region=us-central1

echo "=== Vertex AI Endpoints ==="
gcloud ai endpoints list --region=us-central1

echo "=== AI Platform Notebooks ==="
gcloud notebooks instances list

echo "=== BigQuery ML Models ==="
bq ls --format=table my_ml_dataset
```

#### Script de Limpieza de Recursos ML
```bash
#!/bin/bash
# cleanup-ml-resources.sh
REGION="us-central1"

echo "Cleaning up Vertex AI resources..."

# Eliminar endpoints sin tráfico
gcloud ai endpoints list --region=$REGION --format="value(name)" | while read -r endpoint; do
    TRAFFIC=$(gcloud ai endpoints describe $endpoint --region=$REGION --format="value(trafficSplit)" 2>/dev/null)
    if [[ -z "$TRAFFIC" ]]; then
        echo "Deleting unused endpoint: $endpoint"
        gcloud ai endpoints delete $endpoint --region=$REGION --quiet
    fi
done

# Detener notebooks inactivos
gcloud notebooks instances list --format="value(name,state)" | grep STOPPED | while read -r notebook state; do
    echo "Found stopped notebook: $notebook"
    # Opcional: eliminar notebooks detenidos por más de X días
done

echo "Cleanup completed!"
```
