# 🚀 Comandos de AWS CLI

Una guía completa de comandos para Amazon Web Services (AWS) usando AWS CLI.

## Instalación y Configuración

### Instalar AWS CLI
```bash
# Linux/macOS con curl
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

# macOS con Homebrew
brew install awscli

# Windows con MSI
# Descargar desde: https://awscli.amazonaws.com/AWSCLIV2.msi

# Verificar instalación
aws --version
```

### Configurar AWS CLI
```bash
# Configuración interactiva
aws configure

# Configurar con parámetros específicos
aws configure set aws_access_key_id YOUR_ACCESS_KEY
aws configure set aws_secret_access_key YOUR_SECRET_KEY
aws configure set default.region us-east-1
aws configure set default.output json

# Listar configuraciones
aws configure list

# Configurar perfiles múltiples
aws configure --profile development
aws configure --profile production
```

## EC2 (Elastic Compute Cloud)

### Instancias
```bash
# Listar todas las instancias
aws ec2 describe-instances

# Listar instancias en ejecución
aws ec2 describe-instances --filters "Name=instance-state-name,Values=running"

# Crear instancia
aws ec2 run-instances \
    --image-id ami-0abcdef1234567890 \
    --count 1 \
    --instance-type t2.micro \
    --key-name MyKeyPair \
    --security-groups MySecurityGroup

# Detener instancia
aws ec2 stop-instances --instance-ids i-1234567890abcdef0

# Iniciar instancia
aws ec2 start-instances --instance-ids i-1234567890abcdef0

# Terminar instancia
aws ec2 terminate-instances --instance-ids i-1234567890abcdef0

# Obtener información de una instancia específica
aws ec2 describe-instances --instance-ids i-1234567890abcdef0
```

### AMIs (Amazon Machine Images)
```bash
# Listar AMIs propias
aws ec2 describe-images --owners self

# Buscar AMIs públicas de Amazon Linux
aws ec2 describe-images \
    --owners amazon \
    --filters "Name=name,Values=amzn2-ami-hvm-*" "Name=state,Values=available"

# Crear AMI desde instancia
aws ec2 create-image \
    --instance-id i-1234567890abcdef0 \
    --name "My server" \
    --description "An AMI for my server"
```

### Key Pairs
```bash
# Crear key pair
aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem

# Listar key pairs
aws ec2 describe-key-pairs

# Eliminar key pair
aws ec2 delete-key-pair --key-name MyKeyPair
```

### Security Groups
```bash
# Listar security groups
aws ec2 describe-security-groups

# Crear security group
aws ec2 create-security-group \
    --group-name MySecurityGroup \
    --description "My security group"

# Añadir regla de entrada
aws ec2 authorize-security-group-ingress \
    --group-id sg-903004f8 \
    --protocol tcp \
    --port 22 \
    --cidr 203.0.113.0/24

# Eliminar security group
aws ec2 delete-security-group --group-id sg-903004f8
```

## S3 (Simple Storage Service)

### Buckets
```bash
# Listar buckets
aws s3 ls

# Crear bucket
aws s3 mb s3://my-bucket-name

# Eliminar bucket vacío
aws s3 rb s3://my-bucket-name

# Eliminar bucket con contenido
aws s3 rb s3://my-bucket-name --force
```

### Objetos
```bash
# Listar objetos en bucket
aws s3 ls s3://my-bucket-name

# Subir archivo
aws s3 cp file.txt s3://my-bucket-name/

# Subir directorio completo
aws s3 cp ./local-folder s3://my-bucket-name/remote-folder --recursive

# Descargar archivo
aws s3 cp s3://my-bucket-name/file.txt ./

# Sincronizar directorio local con bucket
aws s3 sync ./local-folder s3://my-bucket-name/

# Mover archivo
aws s3 mv s3://my-bucket-name/old-file.txt s3://my-bucket-name/new-file.txt

# Eliminar archivo
aws s3 rm s3://my-bucket-name/file.txt

# Eliminar todos los archivos de un directorio
aws s3 rm s3://my-bucket-name/folder/ --recursive
```

### Configuración de Bucket
```bash
# Configurar versionado
aws s3api put-bucket-versioning \
    --bucket my-bucket-name \
    --versioning-configuration Status=Enabled

# Configurar website estático
aws s3 website s3://my-bucket-name \
    --index-document index.html \
    --error-document error.html

# Configurar CORS
aws s3api put-bucket-cors \
    --bucket my-bucket-name \
    --cors-configuration file://cors.json
```

## Lambda

### Funciones
```bash
# Listar funciones
aws lambda list-functions

# Crear función
aws lambda create-function \
    --function-name my-function \
    --runtime python3.9 \
    --role arn:aws:iam::123456789012:role/lambda-role \
    --handler lambda_function.lambda_handler \
    --zip-file fileb://function.zip

# Invocar función
aws lambda invoke \
    --function-name my-function \
    --payload '{"key":"value"}' \
    response.json

# Actualizar código de función
aws lambda update-function-code \
    --function-name my-function \
    --zip-file fileb://function.zip

# Eliminar función
aws lambda delete-function --function-name my-function
```

## RDS (Relational Database Service)

### Instancias de Base de Datos
```bash
# Listar instancias RDS
aws rds describe-db-instances

# Crear instancia RDS
aws rds create-db-instance \
    --db-name mydb \
    --db-instance-identifier mydbinstance \
    --allocated-storage 20 \
    --db-instance-class db.t3.micro \
    --engine mysql \
    --master-username admin \
    --master-user-password mypassword

# Crear snapshot
aws rds create-db-snapshot \
    --db-instance-identifier mydbinstance \
    --db-snapshot-identifier mydbsnapshot

# Eliminar instancia
aws rds delete-db-instance \
    --db-instance-identifier mydbinstance \
    --skip-final-snapshot
```

## IAM (Identity and Access Management)

### Usuarios
```bash
# Listar usuarios
aws iam list-users

# Crear usuario
aws iam create-user --user-name MyUser

# Crear access key para usuario
aws iam create-access-key --user-name MyUser

# Eliminar usuario
aws iam delete-user --user-name MyUser
```

### Roles y Políticas
```bash
# Listar roles
aws iam list-roles

# Crear rol
aws iam create-role \
    --role-name MyRole \
    --assume-role-policy-document file://trust-policy.json

# Adjuntar política a rol
aws iam attach-role-policy \
    --role-name MyRole \
    --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess

# Listar políticas
aws iam list-policies --scope Local
```

## CloudFormation

### Stacks
```bash
# Listar stacks
aws cloudformation list-stacks

# Crear stack
aws cloudformation create-stack \
    --stack-name my-stack \
    --template-body file://template.yaml \
    --parameters ParameterKey=KeyName,ParameterValue=MyKey

# Actualizar stack
aws cloudformation update-stack \
    --stack-name my-stack \
    --template-body file://template.yaml

# Eliminar stack
aws cloudformation delete-stack --stack-name my-stack

# Describir stack
aws cloudformation describe-stacks --stack-name my-stack
```

## ECS (Elastic Container Service)

### Clusters
```bash
# Listar clusters
aws ecs list-clusters

# Crear cluster
aws ecs create-cluster --cluster-name my-cluster

# Eliminar cluster
aws ecs delete-cluster --cluster my-cluster
```

### Tasks y Services
```bash
# Listar task definitions
aws ecs list-task-definitions

# Registrar task definition
aws ecs register-task-definition --cli-input-json file://task-definition.json

# Ejecutar task
aws ecs run-task \
    --cluster my-cluster \
    --task-definition my-task:1

# Crear service
aws ecs create-service \
    --cluster my-cluster \
    --service-name my-service \
    --task-definition my-task:1 \
    --desired-count 2
```

## CloudWatch

### Logs
```bash
# Listar log groups
aws logs describe-log-groups

# Crear log group
aws logs create-log-group --log-group-name my-log-group

# Obtener logs
aws logs filter-log-events --log-group-name my-log-group

# Eliminar log group
aws logs delete-log-group --log-group-name my-log-group
```

### Métricas
```bash
# Listar métricas
aws cloudwatch list-metrics

# Obtener estadísticas de métrica
aws cloudwatch get-metric-statistics \
    --namespace AWS/EC2 \
    --metric-name CPUUtilization \
    --dimensions Name=InstanceId,Value=i-1234567890abcdef0 \
    --statistics Average \
    --start-time 2023-01-01T00:00:00Z \
    --end-time 2023-01-01T23:59:59Z \
    --period 3600
```

## Route 53

### Hosted Zones
```bash
# Listar hosted zones
aws route53 list-hosted-zones

# Crear hosted zone
aws route53 create-hosted-zone \
    --name example.com \
    --caller-reference unique-string-$(date +%s)
```

### Records
```bash
# Listar records
aws route53 list-resource-record-sets --hosted-zone-id Z123456789

# Crear/modificar record
aws route53 change-resource-record-sets \
    --hosted-zone-id Z123456789 \
    --change-batch file://change-batch.json
```

## VPC (Virtual Private Cloud)

### VPCs
```bash
# Listar VPCs
aws ec2 describe-vpcs

# Crear VPC
aws ec2 create-vpc --cidr-block 10.0.0.0/16

# Eliminar VPC
aws ec2 delete-vpc --vpc-id vpc-12345678
```

### Subnets
```bash
# Listar subnets
aws ec2 describe-subnets

# Crear subnet
aws ec2 create-subnet \
    --vpc-id vpc-12345678 \
    --cidr-block 10.0.1.0/24
```

## Elastic Load Balancer

### Application Load Balancer
```bash
# Listar load balancers
aws elbv2 describe-load-balancers

# Crear load balancer
aws elbv2 create-load-balancer \
    --name my-load-balancer \
    --subnets subnet-12345678 subnet-87654321

# Eliminar load balancer
aws elbv2 delete-load-balancer --load-balancer-arn arn:aws:elasticloadbalancing:...
```

## Auto Scaling

### Auto Scaling Groups
```bash
# Listar auto scaling groups
aws autoscaling describe-auto-scaling-groups

# Crear auto scaling group
aws autoscaling create-auto-scaling-group \
    --auto-scaling-group-name my-asg \
    --launch-configuration-name my-lc \
    --min-size 1 \
    --max-size 3 \
    --desired-capacity 2 \
    --availability-zones us-east-1a us-east-1b
```

## SNS (Simple Notification Service)

### Topics
```bash
# Listar topics
aws sns list-topics

# Crear topic
aws sns create-topic --name my-topic

# Suscribirse a topic
aws sns subscribe \
    --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic \
    --protocol email \
    --notification-endpoint my-email@example.com

# Publicar mensaje
aws sns publish \
    --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic \
    --message "Hello World"
```

## SQS (Simple Queue Service)

### Queues
```bash
# Listar queues
aws sqs list-queues

# Crear queue
aws sqs create-queue --queue-name my-queue

# Enviar mensaje
aws sqs send-message \
    --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue \
    --message-body "Hello World"

# Recibir mensajes
aws sqs receive-message \
    --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue

# Eliminar queue
aws sqs delete-queue \
    --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue
```

## Elastic Beanstalk

### Aplicaciones
```bash
# Listar aplicaciones
aws elasticbeanstalk describe-applications

# Crear aplicación
aws elasticbeanstalk create-application \
    --application-name my-app \
    --description "My application"

# Crear environment
aws elasticbeanstalk create-environment \
    --application-name my-app \
    --environment-name my-env \
    --solution-stack-name "64bit Amazon Linux 2 v5.4.6 running Node.js 14"
```

## DynamoDB

### Tablas
```bash
# Listar tablas
aws dynamodb list-tables

# Crear tabla
aws dynamodb create-table \
    --table-name Music \
    --attribute-definitions \
        AttributeName=Artist,AttributeType=S \
        AttributeName=SongTitle,AttributeType=S \
    --key-schema \
        AttributeName=Artist,KeyType=HASH \
        AttributeName=SongTitle,KeyType=RANGE \
    --provisioned-throughput \
        ReadCapacityUnits=10,WriteCapacityUnits=5

# Insertar item
aws dynamodb put-item \
    --table-name Music \
    --item \
        '{"Artist":{"S":"No One You Know"},"SongTitle":{"S":"Call Me Today"},"AlbumTitle":{"S":"Somewhat Famous"}}'

# Obtener item
aws dynamodb get-item \
    --consistent-read \
    --table-name Music \
    --key '{ "Artist": {"S": "No One You Know"}, "SongTitle": {"S": "Call Me Today"}}'

# Eliminar tabla
aws dynamodb delete-table --table-name Music
```

## CodeDeploy

### Aplicaciones
```bash
# Listar aplicaciones
aws deploy list-applications

# Crear aplicación
aws deploy create-application \
    --application-name my-app \
    --compute-platform Server

# Crear deployment
aws deploy create-deployment \
    --application-name my-app \
    --deployment-group-name my-deployment-group \
    --s3-location bucket=my-bucket,key=my-app.zip,bundleType=zip
```

## Comandos Útiles Generales

### Filtros y Consultas
```bash
# Usar JMESPath para filtrar resultados
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name]'

# Filtrar por tags
aws ec2 describe-instances --filters "Name=tag:Environment,Values=production"

# Salida en tabla
aws ec2 describe-instances --output table

# Salida en texto
aws ec2 describe-instances --output text
```

### Comandos de Ayuda
```bash
# Ayuda general
aws help

# Ayuda de servicio específico
aws ec2 help

# Ayuda de comando específico
aws ec2 describe-instances help
```

### Variables de Entorno
```bash
# Configurar región
export AWS_DEFAULT_REGION=us-west-2

# Configurar perfil
export AWS_PROFILE=production

# Configurar salida por defecto
export AWS_DEFAULT_OUTPUT=json
```

## Scripts de Automatización

### Script de Backup de S3
```bash
#!/bin/bash
# backup-s3.sh
BUCKET_NAME="my-backup-bucket"
LOCAL_DIR="/path/to/backup"
DATE=$(date +%Y%m%d)

aws s3 sync $LOCAL_DIR s3://$BUCKET_NAME/backup-$DATE/
```

### Script de Monitoreo de Instancias
```bash
#!/bin/bash
# check-instances.sh
aws ec2 describe-instances \
    --query 'Reservations[*].Instances[*].[InstanceId,State.Name,InstanceType]' \
    --output table
```

---

## AWS AI/ML Services

### Amazon SageMaker
```bash
# Crear notebook instance
aws sagemaker create-notebook-instance \
    --notebook-instance-name my-notebook \
    --instance-type ml.t3.medium \
    --role-arn arn:aws:iam::123456789012:role/MySageMakerRole

# Listar notebook instances
aws sagemaker list-notebook-instances

# Iniciar notebook instance
aws sagemaker start-notebook-instance \
    --notebook-instance-name my-notebook

# Detener notebook instance
aws sagemaker stop-notebook-instance \
    --notebook-instance-name my-notebook

# Crear training job
aws sagemaker create-training-job \
    --training-job-name my-training-job \
    --algorithm-specification TrainingImage=382416733822.dkr.ecr.us-east-1.amazonaws.com/xgboost:latest,TrainingInputMode=File \
    --role-arn arn:aws:iam::123456789012:role/MySageMakerRole \
    --input-data-config file://input-data-config.json \
    --output-data-config S3OutputPath=s3://my-bucket/output \
    --resource-config InstanceType=ml.m5.large,InstanceCount=1,VolumeSizeInGB=10 \
    --stopping-condition MaxRuntimeInSeconds=3600

# Listar training jobs
aws sagemaker list-training-jobs

# Crear modelo
aws sagemaker create-model \
    --model-name my-model \
    --primary-container Image=382416733822.dkr.ecr.us-east-1.amazonaws.com/xgboost:latest,ModelDataUrl=s3://my-bucket/model.tar.gz \
    --execution-role-arn arn:aws:iam::123456789012:role/MySageMakerRole

# Crear endpoint configuration
aws sagemaker create-endpoint-config \
    --endpoint-config-name my-endpoint-config \
    --production-variants VariantName=AllTraffic,ModelName=my-model,InitialInstanceCount=1,InstanceType=ml.t2.medium

# Crear endpoint
aws sagemaker create-endpoint \
    --endpoint-name my-endpoint \
    --endpoint-config-name my-endpoint-config

# Listar endpoints
aws sagemaker list-endpoints
```

### Amazon Bedrock
```bash
# Listar modelos disponibles
aws bedrock list-foundation-models

# Listar custom models
aws bedrock list-custom-models

# Crear job de fine-tuning
aws bedrock create-model-customization-job \
    --job-name my-fine-tuning-job \
    --custom-model-name my-custom-model \
    --role-arn arn:aws:iam::123456789012:role/BedrockRole \
    --base-model-identifier anthropic.claude-v2 \
    --training-data-config S3Uri=s3://my-bucket/training-data \
    --output-data-config S3Uri=s3://my-bucket/output

# Invocar modelo (usando AWS CLI con Bedrock Runtime)
aws bedrock-runtime invoke-model \
    --model-id anthropic.claude-v2 \
    --body '{"prompt":"Human: Hello\n\nAssistant:","max_tokens_to_sample":100}' \
    --content-type application/json \
    output.json

# Listar jobs de fine-tuning
aws bedrock list-model-customization-jobs
```

### Amazon Rekognition
```bash
# Detectar etiquetas en imagen
aws rekognition detect-labels \
    --image S3Object='{Bucket=my-bucket,Name=image.jpg}' \
    --max-labels 10 \
    --min-confidence 75

# Detectar caras
aws rekognition detect-faces \
    --image S3Object='{Bucket=my-bucket,Name=image.jpg}' \
    --attributes ALL

# Comparar caras
aws rekognition compare-faces \
    --source-image S3Object='{Bucket=my-bucket,Name=source.jpg}' \
    --target-image S3Object='{Bucket=my-bucket,Name=target.jpg}'

# Detectar texto
aws rekognition detect-text \
    --image S3Object='{Bucket=my-bucket,Name=document.jpg}'

# Crear colección de caras
aws rekognition create-collection \
    --collection-id my-face-collection

# Indexar cara en colección
aws rekognition index-faces \
    --collection-id my-face-collection \
    --image S3Object='{Bucket=my-bucket,Name=person.jpg}' \
    --external-image-id person-001

# Buscar caras
aws rekognition search-faces-by-image \
    --collection-id my-face-collection \
    --image S3Object='{Bucket=my-bucket,Name=search.jpg}' \
    --max-faces 5
```

### Amazon Textract
```bash
# Detectar texto en documento
aws textract detect-document-text \
    --document S3Object='{Bucket=my-bucket,Name=document.pdf}'

# Analizar documento (formularios y tablas)
aws textract analyze-document \
    --document S3Object='{Bucket=my-bucket,Name=form.pdf}' \
    --feature-types TABLES FORMS

# Iniciar análisis asíncrono
aws textract start-document-analysis \
    --document-location S3Object='{Bucket=my-bucket,Name=large-document.pdf}' \
    --feature-types TABLES FORMS

# Obtener resultados de análisis asíncrono
aws textract get-document-analysis \
    --job-id job-id-from-start-command
```

### Amazon Comprehend
```bash
# Detectar sentimiento
aws comprehend detect-sentiment \
    --text "I love this product!" \
    --language-code en

# Detectar entidades
aws comprehend detect-entities \
    --text "Amazon Web Services is based in Seattle" \
    --language-code en

# Detectar frases clave
aws comprehend detect-key-phrases \
    --text "Machine learning is transforming the way we work" \
    --language-code en

# Detectar idioma
aws comprehend detect-dominant-language \
    --text "Bonjour, comment allez-vous?"

# Análisis de sentimiento por lotes
aws comprehend start-sentiment-detection-job \
    --input-data-config S3Uri=s3://my-bucket/input/,InputFormat=ONE_DOC_PER_LINE \
    --output-data-config S3Uri=s3://my-bucket/output/ \
    --data-access-role-arn arn:aws:iam::123456789012:role/ComprehendRole \
    --language-code en \
    --job-name sentiment-analysis-job

# Listar jobs de análisis
aws comprehend list-sentiment-detection-jobs
```

### Amazon Polly
```bash
# Sintetizar voz
aws polly synthesize-speech \
    --output-format mp3 \
    --voice-id Joanna \
    --text "Hello, this is Amazon Polly speaking" \
    speech.mp3

# Listar voces disponibles
aws polly describe-voices

# Sintetizar con SSML
aws polly synthesize-speech \
    --output-format mp3 \
    --voice-id Matthew \
    --text-type ssml \
    --text '<speak>Hello <break time="2s"/> World!</speak>' \
    ssml-speech.mp3

# Crear lexicon personalizado
aws polly put-lexicon \
    --name my-lexicon \
    --content file://lexicon.xml

# Listar lexicons
aws polly list-lexicons
```

### Amazon Transcribe
```bash
# Iniciar job de transcripción
aws transcribe start-transcription-job \
    --transcription-job-name my-transcription \
    --language-code en-US \
    --media-format mp3 \
    --media MediaFileUri=s3://my-bucket/audio.mp3

# Obtener resultado de transcripción
aws transcribe get-transcription-job \
    --transcription-job-name my-transcription

# Listar jobs de transcripción
aws transcribe list-transcription-jobs

# Transcripción en tiempo real (streaming)
aws transcribe start-stream-transcription \
    --language-code en-US \
    --media-encoding pcm \
    --sample-rate 16000
```

### Amazon Translate
```bash
# Traducir texto
aws translate translate-text \
    --source-language-code en \
    --target-language-code es \
    --text "Hello, how are you?"

# Traducir documento
aws translate start-text-translation-job \
    --job-name translate-job \
    --source-language-code en \
    --target-language-codes es fr de \
    --input-data-config S3Uri=s3://my-bucket/input/,ContentType=text/plain \
    --output-data-config S3Uri=s3://my-bucket/output/ \
    --data-access-role-arn arn:aws:iam::123456789012:role/TranslateRole

# Obtener resultado de traducción por lotes
aws translate describe-text-translation-job \
    --job-id job-id-from-start-command

# Listar jobs de traducción
aws translate list-text-translation-jobs
```

### Amazon Lex
```bash
# Crear bot
aws lex put-bot \
    --name OrderPizza \
    --description "Bot to order pizza" \
    --intents Intent=OrderPizza \
    --clarification-prompt Messages='[{Content="I did not understand, can you repeat?",ContentType="PlainText"}]' \
    --abortion-statement Messages='[{Content="Sorry, I could not understand. Goodbye.",ContentType="PlainText"}]' \
    --idle-session-ttl-in-seconds 300 \
    --data-privacy ChildDirected=false \
    --locale en-US

# Crear intent
aws lex put-intent \
    --name OrderPizza \
    --description "Intent to order pizza" \
    --sample-utterances "I would like to order a pizza" "Can I get a pizza" \
    --fulfillment-activity Type=ReturnIntent

# Construir bot
aws lex put-bot \
    --name OrderPizza \
    --intents Intent=OrderPizza \
    --clarification-prompt Messages='[{Content="What can I help you with?",ContentType="PlainText"}]' \
    --abortion-statement Messages='[{Content="Sorry, I could not understand.",ContentType="PlainText"}]' \
    --idle-session-ttl-in-seconds 300 \
    --data-privacy ChildDirected=false \
    --locale en-US

# Probar bot
aws lex post-text \
    --bot-name OrderPizza \
    --bot-alias "\$LATEST" \
    --user-id test-user \
    --input-text "I want to order a pizza"
```

### Amazon Kendra
```bash
# Crear índice
aws kendra create-index \
    --name MyIndex \
    --description "My search index" \
    --role-arn arn:aws:iam::123456789012:role/KendraRole

# Crear data source
aws kendra create-data-source \
    --index-id index-id \
    --name MyDataSource \
    --type S3 \
    --configuration S3Configuration='{BucketName=my-bucket,InclusionPrefixes=[documents/]}' \
    --role-arn arn:aws:iam::123456789012:role/KendraRole

# Sincronizar data source
aws kendra start-data-source-sync-job \
    --id data-source-id \
    --index-id index-id

# Hacer consulta
aws kendra query \
    --index-id index-id \
    --query-text "What is machine learning?"

# Listar índices
aws kendra list-indices
```

### Scripts de Automatización para AI/ML

#### Script de Análisis de Imágenes
```bash
#!/bin/bash
# analyze-images.sh
BUCKET="my-images-bucket"
PREFIX="uploads/"

# Listar imágenes en S3
aws s3 ls s3://$BUCKET/$PREFIX --recursive | grep -E '\.(jpg|jpeg|png)$' | while read -r line; do
    # Extraer nombre del archivo
    IMAGE=$(echo $line | awk '{print $4}')
    
    echo "Analyzing image: $IMAGE"
    
    # Detectar etiquetas
    aws rekognition detect-labels \
        --image S3Object='{Bucket='$BUCKET',Name='$IMAGE'}' \
        --max-labels 5 \
        --min-confidence 80
    
    echo "---"
done
```

#### Script de Transcripción Masiva
```bash
#!/bin/bash
# batch-transcribe.sh
BUCKET="my-audio-bucket"
PREFIX="recordings/"

# Listar archivos de audio
aws s3 ls s3://$BUCKET/$PREFIX --recursive | grep -E '\.(mp3|wav|flac)$' | while read -r line; do
    # Extraer nombre del archivo
    AUDIO=$(echo $line | awk '{print $4}')
    JOB_NAME=$(basename "$AUDIO" .mp3)
    
    echo "Starting transcription for: $AUDIO"
    
    # Iniciar job de transcripción
    aws transcribe start-transcription-job \
        --transcription-job-name "$JOB_NAME-$(date +%s)" \
        --language-code en-US \
        --media-format mp3 \
        --media MediaFileUri=s3://$BUCKET/$AUDIO
done
```

#### Script de Monitoreo de ML
```bash
#!/bin/bash
# monitor-ml-services.sh
echo "=== SageMaker Training Jobs ==="
aws sagemaker list-training-jobs --output table

echo "=== SageMaker Endpoints ==="
aws sagemaker list-endpoints --output table

echo "=== Transcription Jobs ==="
aws transcribe list-transcription-jobs --output table

echo "=== Translation Jobs ==="
aws translate list-text-translation-jobs --output table
```
