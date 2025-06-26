# ☁️ Comandos de Azure CLI

Una guía completa de comandos para Microsoft Azure usando Azure CLI.

## Instalación y Configuración

### Instalar Azure CLI
```bash
# Linux/macOS con curl
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

# macOS con Homebrew
brew install azure-cli

# Windows con MSI
# Descargar desde: https://aka.ms/installazurecliwindows

# Verificar instalación
az --version
```

### Configurar Azure CLI
```bash
# Iniciar sesión
az login

# Iniciar sesión con service principal
az login --service-principal \
    --username <app-id> \
    --password <password-or-cert> \
    --tenant <tenant>

# Listar suscripciones
az account list

# Establecer suscripción por defecto
az account set --subscription "My Subscription"

# Mostrar suscripción actual
az account show

# Configurar valores por defecto
az configure --defaults location=eastus group=myResourceGroup
```

## Resource Groups

### Gestión de Grupos de Recursos
```bash
# Listar grupos de recursos
az group list

# Crear grupo de recursos
az group create --name myResourceGroup --location eastus

# Mostrar detalles de grupo de recursos
az group show --name myResourceGroup

# Eliminar grupo de recursos
az group delete --name myResourceGroup --yes --no-wait

# Listar recursos en un grupo
az resource list --resource-group myResourceGroup
```

## Virtual Machines

### Crear y Gestionar VMs
```bash
# Listar todas las VMs
az vm list

# Crear VM Ubuntu
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys

# Crear VM Windows
az vm create \
    --resource-group myResourceGroup \
    --name myWindowsVM \
    --image Win2019Datacenter \
    --admin-username azureuser \
    --admin-password MyPassword123!

# Iniciar VM
az vm start --resource-group myResourceGroup --name myVM

# Detener VM
az vm stop --resource-group myResourceGroup --name myVM

# Reiniciar VM
az vm restart --resource-group myResourceGroup --name myVM

# Eliminar VM
az vm delete --resource-group myResourceGroup --name myVM --yes

# Obtener información de VM
az vm show --resource-group myResourceGroup --name myVM

# Listar tamaños disponibles de VM
az vm list-sizes --location eastus

# Redimensionar VM
az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
```

### Extensiones de VM
```bash
# Listar extensiones disponibles
az vm.extension image list --location eastus

# Instalar extensión
az vm.extension.set \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --name customScript \
    --publisher Microsoft.Azure.Extensions \
    --settings '{"fileUris":["https://example.com/script.sh"],"commandToExecute":"./script.sh"}'

# Listar extensiones de VM
az vm.extension list --resource-group myResourceGroup --vm-name myVM
```

### Conexión SSH y RDP
```bash
# Obtener IP pública de VM
az vm.list-ip-addresses --resource-group myResourceGroup --name myVM

# Conectar por SSH (Linux)
az vm.run-command invoke \
    --resource-group myResourceGroup \
    --name myVM \
    --command-id RunShellScript \
    --scripts "echo Hello World"

# Habilitar auto-shutdown
az vm.auto-shutdown \
    --resource-group myResourceGroup \
    --name myVM \
    --time 1900
```

## App Service

### Web Apps
```bash
# Crear App Service Plan
az appservice plan create \
    --name myAppServicePlan \
    --resource-group myResourceGroup \
    --sku B1 \
    --is-linux

# Crear Web App
az webapp create \
    --resource-group myResourceGroup \
    --plan myAppServicePlan \
    --name myUniqueWebApp \
    --runtime "NODE|14-lts"

# Listar Web Apps
az webapp list

# Mostrar detalles de Web App
az webapp show --name myUniqueWebApp --resource-group myResourceGroup

# Configurar variables de entorno
az webapp config appsettings set \
    --resource-group myResourceGroup \
    --name myUniqueWebApp \
    --settings KEY1=VALUE1 KEY2=VALUE2

# Habilitar logs
az webapp log config \
    --resource-group myResourceGroup \
    --name myUniqueWebApp \
    --application-logging true \
    --web-server-logging filesystem

# Ver logs en tiempo real
az webapp log tail --resource-group myResourceGroup --name myUniqueWebApp

# Reiniciar Web App
az webapp restart --resource-group myResourceGroup --name myUniqueWebApp

# Eliminar Web App
az webapp delete --resource-group myResourceGroup --name myUniqueWebApp
```

### Deployment
```bash
# Configurar deployment desde GitHub
az webapp deployment source config \
    --name myUniqueWebApp \
    --resource-group myResourceGroup \
    --repo-url https://github.com/user/repo \
    --branch master \
    --manual-integration

# Deployment desde ZIP
az webapp deployment source config-zip \
    --resource-group myResourceGroup \
    --name myUniqueWebApp \
    --src app.zip

# Configurar deployment slots
az webapp deployment slot create \
    --resource-group myResourceGroup \
    --name myUniqueWebApp \
    --slot staging

# Swap deployment slots
az webapp deployment slot swap \
    --resource-group myResourceGroup \
    --name myUniqueWebApp \
    --slot staging \
    --target-slot production
```

## Storage Account

### Cuentas de Almacenamiento
```bash
# Crear storage account
az storage account create \
    --name mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --sku Standard_LRS

# Listar storage accounts
az storage account list

# Obtener keys de storage account
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount

# Obtener connection string
az storage account show-connection-string \
    --resource-group myResourceGroup \
    --name mystorageaccount

# Configurar variable de entorno
export AZURE_STORAGE_CONNECTION_STRING="DefaultEndpointsProtocol=https;..."
```

### Blob Storage
```bash
# Crear contenedor
az storage container create --name mycontainer

# Listar contenedores
az storage container list

# Subir archivo
az storage blob upload \
    --container-name mycontainer \
    --name myblob \
    --file ./myfile.txt

# Listar blobs
az storage blob list --container-name mycontainer

# Descargar blob
az storage blob download \
    --container-name mycontainer \
    --name myblob \
    --file ./downloaded-file.txt

# Eliminar blob
az storage blob delete --container-name mycontainer --name myblob

# Generar SAS token
az storage blob generate-sas \
    --container-name mycontainer \
    --name myblob \
    --permissions r \
    --expiry 2024-12-31
```

### File Share
```bash
# Crear file share
az storage share create --name myshare

# Subir archivo a file share
az storage file upload \
    --share-name myshare \
    --source ./myfile.txt

# Listar archivos
az storage file list --share-name myshare

# Descargar archivo
az storage file download \
    --share-name myshare \
    --path myfile.txt \
    --dest ./downloaded-file.txt
```

## Azure SQL Database

### Servidores SQL
```bash
# Crear SQL Server
az sql server create \
    --name mysqlserver \
    --resource-group myResourceGroup \
    --location eastus \
    --admin-user myadmin \
    --admin-password MyPassword123!

# Listar SQL Servers
az sql server list

# Configurar firewall
az sql server firewall-rule create \
    --resource-group myResourceGroup \
    --server mysqlserver \
    --name AllowYourIp \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 0.0.0.0
```

### Bases de Datos
```bash
# Crear base de datos
az sql db create \
    --resource-group myResourceGroup \
    --server mysqlserver \
    --name mydatabase \
    --service-objective S0

# Listar bases de datos
az sql db list --resource-group myResourceGroup --server mysqlserver

# Mostrar detalles de base de datos
az sql db show \
    --resource-group myResourceGroup \
    --server mysqlserver \
    --name mydatabase

# Eliminar base de datos
az sql db delete \
    --resource-group myResourceGroup \
    --server mysqlserver \
    --name mydatabase
```

## Azure Container Instances (ACI)

### Contenedores
```bash
# Crear container instance
az container create \
    --resource-group myResourceGroup \
    --name mycontainer \
    --image nginx \
    --dns-name-label mycontainer-dns \
    --ports 80

# Listar container instances
az container list

# Mostrar logs
az container logs --resource-group myResourceGroup --name mycontainer

# Mostrar detalles
az container show --resource-group myResourceGroup --name mycontainer

# Eliminar container instance
az container delete --resource-group myResourceGroup --name mycontainer
```

## Azure Kubernetes Service (AKS)

### Clusters
```bash
# Crear AKS cluster
az aks create \
    --resource-group myResourceGroup \
    --name myAKSCluster \
    --node-count 1 \
    --enable-addons monitoring \
    --generate-ssh-keys

# Obtener credenciales
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster

# Listar clusters
az aks list

# Escalar cluster
az aks scale \
    --resource-group myResourceGroup \
    --name myAKSCluster \
    --node-count 3

# Actualizar cluster
az aks upgrade \
    --resource-group myResourceGroup \
    --name myAKSCluster \
    --kubernetes-version 1.21.2

# Eliminar cluster
az aks delete --resource-group myResourceGroup --name myAKSCluster
```

### Node Pools
```bash
# Añadir node pool
az aks nodepool add \
    --resource-group myResourceGroup \
    --cluster-name myAKSCluster \
    --name mynodepool \
    --node-count 1

# Listar node pools
az aks nodepool list --resource-group myResourceGroup --cluster-name myAKSCluster

# Eliminar node pool
az aks nodepool delete \
    --resource-group myResourceGroup \
    --cluster-name myAKSCluster \
    --name mynodepool
```

## Azure Functions

### Function Apps
```bash
# Crear Function App
az functionapp create \
    --resource-group myResourceGroup \
    --consumption-plan-location eastus \
    --runtime node \
    --runtime-version 14 \
    --functions-version 3 \
    --name myFunctionApp \
    --storage-account mystorageaccount

# Listar Function Apps
az functionapp list

# Configurar app settings
az functionapp config appsettings set \
    --name myFunctionApp \
    --resource-group myResourceGroup \
    --settings KEY1=VALUE1

# Deployment desde ZIP
az functionapp deployment source config-zip \
    --resource-group myResourceGroup \
    --name myFunctionApp \
    --src function-app.zip

# Ver logs
az functionapp log tail --name myFunctionApp --resource-group myResourceGroup
```

## Azure Key Vault

### Key Vaults
```bash
# Crear Key Vault
az keyvault create \
    --name myKeyVault \
    --resource-group myResourceGroup \
    --location eastus

# Listar Key Vaults
az keyvault list

# Configurar access policy
az keyvault set-policy \
    --name myKeyVault \
    --upn user@domain.com \
    --secret-permissions get list set delete
```

### Secrets
```bash
# Crear secret
az keyvault secret set \
    --vault-name myKeyVault \
    --name MySecret \
    --value "MySecretValue"

# Obtener secret
az keyvault secret show --vault-name myKeyVault --name MySecret

# Listar secrets
az keyvault secret list --vault-name myKeyVault

# Eliminar secret
az keyvault secret delete --vault-name myKeyVault --name MySecret
```

### Keys
```bash
# Crear key
az keyvault key create \
    --vault-name myKeyVault \
    --name MyKey \
    --kty RSA \
    --size 2048

# Listar keys
az keyvault key list --vault-name myKeyVault

# Mostrar key
az keyvault key show --vault-name myKeyVault --name MyKey
```

## Azure Monitor

### Log Analytics
```bash
# Crear workspace
az monitor log-analytics workspace create \
    --resource-group myResourceGroup \
    --workspace-name myWorkspace

# Listar workspaces
az monitor log-analytics workspace list

# Ejecutar query
az monitor log-analytics query \
    --workspace myWorkspace \
    --analytics-query "Heartbeat | take 10"
```

### Application Insights
```bash
# Crear Application Insights
az monitor app-insights component create \
    --app myAppInsights \
    --location eastus \
    --resource-group myResourceGroup

# Mostrar detalles
az monitor app-insights component show \
    --app myAppInsights \
    --resource-group myResourceGroup
```

## Azure DevOps

### Organizaciones y Proyectos
```bash
# Configurar organización por defecto
az devops configure --defaults organization=https://dev.azure.com/myorg

# Listar proyectos
az devops project list

# Crear proyecto
az devops project create --name MyProject

# Mostrar detalles de proyecto
az devops project show --project MyProject
```

### Repositorios
```bash
# Listar repositorios
az repos list --project MyProject

# Crear repositorio
az repos create --name MyRepo --project MyProject

# Importar repositorio
az repos import create \
    --git-source-url https://github.com/user/repo \
    --repository MyRepo \
    --project MyProject
```

### Pipelines
```bash
# Listar pipelines
az pipelines list --project MyProject

# Crear pipeline
az pipelines create \
    --name MyPipeline \
    --repository https://github.com/user/repo \
    --branch master \
    --yml-path azure-pipelines.yml

# Ejecutar pipeline
az pipelines run --name MyPipeline --project MyProject

# Mostrar resultados de pipeline
az pipelines runs list --project MyProject
```

## Azure Resource Manager (ARM)

### Templates
```bash
# Validar template
az deployment group validate \
    --resource-group myResourceGroup \
    --template-file azuredeploy.json \
    --parameters azuredeploy.parameters.json

# Deployment de template
az deployment group create \
    --resource-group myResourceGroup \
    --template-file azuredeploy.json \
    --parameters azuredeploy.parameters.json

# Listar deployments
az deployment group list --resource-group myResourceGroup

# Mostrar deployment
az deployment group show \
    --resource-group myResourceGroup \
    --name myDeployment
```

## Azure Active Directory

### Usuarios
```bash
# Listar usuarios
az ad user list

# Crear usuario
az ad user create \
    --display-name "John Doe" \
    --password "MyPassword123!" \
    --user-principal-name john@domain.onmicrosoft.com

# Mostrar usuario
az ad user show --id john@domain.onmicrosoft.com

# Eliminar usuario
az ad user delete --id john@domain.onmicrosoft.com
```

### Grupos
```bash
# Listar grupos
az ad group list

# Crear grupo
az ad group create \
    --display-name "My Group" \
    --mail-nickname mygroup

# Añadir miembro a grupo
az ad group member add \
    --group "My Group" \
    --member-id user-object-id
```

### Service Principals
```bash
# Crear service principal
az ad sp create-for-rbac --name MyServicePrincipal

# Listar service principals
az ad sp list --display-name MyServicePrincipal

# Asignar rol
az role assignment create \
    --assignee service-principal-id \
    --role Contributor \
    --scope /subscriptions/subscription-id
```

## Azure Network

### Virtual Networks
```bash
# Crear virtual network
az network vnet create \
    --resource-group myResourceGroup \
    --name myVNet \
    --address-prefix 10.0.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.0.1.0/24

# Listar virtual networks
az network vnet list

# Crear subnet
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --name mySubnet2 \
    --address-prefix 10.0.2.0/24
```

### Load Balancers
```bash
# Crear load balancer
az network lb create \
    --resource-group myResourceGroup \
    --name myLoadBalancer \
    --public-ip-address myPublicIP \
    --frontend-ip-name myFrontEnd \
    --backend-pool-name myBackEndPool

# Crear regla de load balancer
az network lb rule create \
    --resource-group myResourceGroup \
    --lb-name myLoadBalancer \
    --name myHTTPRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEnd \
    --backend-pool-name myBackEndPool
```

### Network Security Groups
```bash
# Crear NSG
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup

# Crear regla de NSG
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleHTTP \
    --protocol tcp \
    --direction inbound \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 80 \
    --access allow \
    --priority 200
```

## Azure Backup

### Recovery Services Vault
```bash
# Crear Recovery Services Vault
az backup vault create \
    --resource-group myResourceGroup \
    --name myRecoveryServicesVault \
    --location eastus

# Habilitar backup para VM
az backup protection enable-for-vm \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --vm myVM \
    --policy-name DefaultPolicy

# Ejecutar backup
az backup protection backup-now \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --container-name myVM \
    --item-name myVM \
    --backup-management-type AzureIaasVM
```

## Azure AI Services

### Cognitive Services
```bash
# Crear Cognitive Services account
az cognitiveservices account create \
    --name myCognitiveService \
    --resource-group myResourceGroup \
    --kind CognitiveServices \
    --sku S0 \
    --location eastus

# Listar Cognitive Services
az cognitiveservices account list

# Obtener keys de Cognitive Services
az cognitiveservices account keys list \
    --name myCognitiveService \
    --resource-group myResourceGroup

# Mostrar detalles del servicio
az cognitiveservices account show \
    --name myCognitiveService \
    --resource-group myResourceGroup

# Regenerar key
az cognitiveservices account keys regenerate \
    --name myCognitiveService \
    --resource-group myResourceGroup \
    --key-name key1
```

### Azure OpenAI Service
```bash
# Crear Azure OpenAI resource
az cognitiveservices account create \
    --name myOpenAI \
    --resource-group myResourceGroup \
    --kind OpenAI \
    --sku S0 \
    --location eastus

# Listar modelos disponibles
az cognitiveservices account list-models \
    --name myOpenAI \
    --resource-group myResourceGroup

# Crear deployment de modelo
az cognitiveservices account deployment create \
    --name myOpenAI \
    --resource-group myResourceGroup \
    --deployment-name text-davinci-003 \
    --model-name text-davinci-003 \
    --model-version "1" \
    --model-format OpenAI \
    --scale-settings-scale-type "Standard"

# Listar deployments
az cognitiveservices account deployment list \
    --name myOpenAI \
    --resource-group myResourceGroup

# Eliminar deployment
az cognitiveservices account deployment delete \
    --name myOpenAI \
    --resource-group myResourceGroup \
    --deployment-name text-davinci-003
```

### Computer Vision
```bash
# Crear Computer Vision service
az cognitiveservices account create \
    --name myComputerVision \
    --resource-group myResourceGroup \
    --kind ComputerVision \
    --sku S1 \
    --location eastus

# Analizar imagen (usando REST API con curl)
ENDPOINT=$(az cognitiveservices account show --name myComputerVision --resource-group myResourceGroup --query "properties.endpoint" --output tsv)
KEY=$(az cognitiveservices account keys list --name myComputerVision --resource-group myResourceGroup --query "key1" --output tsv)

curl -H "Ocp-Apim-Subscription-Key: $KEY" \
     -H "Content-Type: application/json" \
     -d '{"url":"https://example.com/image.jpg"}' \
     "$ENDPOINT/vision/v3.2/analyze?visualFeatures=Categories,Description,Faces,Objects,Tags"
```

### Speech Services
```bash
# Crear Speech service
az cognitiveservices account create \
    --name mySpeechService \
    --resource-group myResourceGroup \
    --kind SpeechServices \
    --sku S0 \
    --location eastus

# Obtener token de acceso
ENDPOINT=$(az cognitiveservices account show --name mySpeechService --resource-group myResourceGroup --query "properties.endpoint" --output tsv)
KEY=$(az cognitiveservices account keys list --name mySpeechService --resource-group myResourceGroup --query "key1" --output tsv)

curl -X POST \
     -H "Ocp-Apim-Subscription-Key: $KEY" \
     -H "Content-Type: application/x-www-form-urlencoded" \
     -d "" \
     "$ENDPOINT/sts/v1.0/issuetoken"
```

### Text Analytics
```bash
# Crear Text Analytics service
az cognitiveservices account create \
    --name myTextAnalytics \
    --resource-group myResourceGroup \
    --kind TextAnalytics \
    --sku S \
    --location eastus

# Análisis de sentimientos (usando REST API)
ENDPOINT=$(az cognitiveservices account show --name myTextAnalytics --resource-group myResourceGroup --query "properties.endpoint" --output tsv)
KEY=$(az cognitiveservices account keys list --name myTextAnalytics --resource-group myResourceGroup --query "key1" --output tsv)

curl -X POST \
     -H "Ocp-Apim-Subscription-Key: $KEY" \
     -H "Content-Type: application/json" \
     -d '{
       "documents": [
         {
           "language": "es",
           "id": "1",
           "text": "Este servicio es fantástico"
         }
       ]
     }' \
     "$ENDPOINT/text/analytics/v3.1/sentiment"
```

### Translator
```bash
# Crear Translator service
az cognitiveservices account create \
    --name myTranslator \
    --resource-group myResourceGroup \
    --kind TextTranslation \
    --sku S1 \
    --location global

# Traducir texto (usando REST API)
KEY=$(az cognitiveservices account keys list --name myTranslator --resource-group myResourceGroup --query "key1" --output tsv)

curl -X POST \
     -H "Ocp-Apim-Subscription-Key: $KEY" \
     -H "Content-Type: application/json" \
     -d '[{"Text":"Hello World"}]' \
     "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&to=es"
```

### Azure Machine Learning
```bash
# Instalar extensión de ML
az extension add --name ml

# Crear workspace de ML
az ml workspace create \
    --name myMLWorkspace \
    --resource-group myResourceGroup \
    --location eastus

# Configurar workspace por defecto
az configure --defaults workspace=myMLWorkspace group=myResourceGroup

# Listar workspaces
az ml workspace list

# Crear compute instance
az ml compute create \
    --name mycompute \
    --type ComputeInstance \
    --size Standard_DS3_v2

# Listar compute instances
az ml compute list

# Crear datastore
az ml datastore create \
    --name mydatastore \
    --type AzureBlobStorage \
    --account-name mystorageaccount \
    --container-name mycontainer

# Crear dataset
az ml dataset create \
    --name mydataset \
    --datastore mydatastore \
    --path path/to/data

# Listar datasets
az ml dataset list

# Enviar job de entrenamiento
az ml job create --file train-job.yml

# Listar jobs
az ml job list

# Mostrar detalles de job
az ml job show --name job-name

# Crear model
az ml model create \
    --name mymodel \
    --version 1 \
    --path ./model \
    --type mlflow_model

# Listar modelos
az ml model list

# Crear endpoint
az ml online-endpoint create \
    --name myendpoint \
    --auth-mode key

# Deploy modelo a endpoint
az ml online-deployment create \
    --name mydeployment \
    --endpoint myendpoint \
    --model mymodel:1 \
    --instance-type Standard_DS3_v2 \
    --instance-count 1

# Probar endpoint
az ml online-endpoint invoke \
    --name myendpoint \
    --request-file test-data.json
```

### Azure Bot Service
```bash
# Crear Bot
az bot create \
    --resource-group myResourceGroup \
    --name myBot \
    --kind webapp \
    --location eastus \
    --microsoft-app-id app-id \
    --microsoft-app-password app-password

# Configurar canal de Teams
az bot msteams create \
    --resource-group myResourceGroup \
    --name myBot

# Configurar canal de Slack
az bot slack create \
    --resource-group myResourceGroup \
    --name myBot \
    --client-id slack-client-id \
    --client-secret slack-client-secret \
    --verification-token slack-verification-token

# Listar bots
az bot list

# Mostrar detalles del bot
az bot show \
    --resource-group myResourceGroup \
    --name myBot
```

### Custom Vision
```bash
# Crear Custom Vision project (requiere SDK)
# Primero instalar el SDK
pip install azure-cognitiveservices-vision-customvision

# Script de Python para crear proyecto
python3 << EOF
from azure.cognitiveservices.vision.customvision.training import CustomVisionTrainingClient
from azure.cognitiveservices.vision.customvision.prediction import CustomVisionPredictionClient
from msrest.authentication import ApiKeyCredentials

# Configurar credenciales
training_key = "your-training-key"
prediction_key = "your-prediction-key"
endpoint = "your-endpoint"

credentials = ApiKeyCredentials(in_headers={"Training-key": training_key})
trainer = CustomVisionTrainingClient(endpoint, credentials)

# Crear proyecto
project = trainer.create_project("My Project")
print(f"Created project: {project.id}")
EOF
```

### Form Recognizer
```bash
# Crear Form Recognizer service
az cognitiveservices account create \
    --name myFormRecognizer \
    --resource-group myResourceGroup \
    --kind FormRecognizer \
    --sku S0 \
    --location eastus

# Analizar formulario (usando REST API)
ENDPOINT=$(az cognitiveservices account show --name myFormRecognizer --resource-group myResourceGroup --query "properties.endpoint" --output tsv)
KEY=$(az cognitiveservices account keys list --name myFormRecognizer --resource-group myResourceGroup --query "key1" --output tsv)

curl -X POST \
     -H "Ocp-Apim-Subscription-Key: $KEY" \
     -H "Content-Type: application/json" \
     -d '{"source":"https://example.com/document.pdf"}' \
     "$ENDPOINT/formrecognizer/v2.1/layout/analyze"
```

### Scripts de Automatización para AI

#### Script de Monitoreo de Servicios AI
```bash
#!/bin/bash
# monitor-ai-services.sh
echo "=== Cognitive Services ==="
az cognitiveservices account list --output table

echo "=== Machine Learning Workspaces ==="
az ml workspace list --output table

echo "=== Bot Services ==="
az bot list --output table
```

#### Script de Configuración AI completa
```bash
#!/bin/bash
# setup-ai-environment.sh
RESOURCE_GROUP="myAIResourceGroup"
LOCATION="eastus"

echo "Creating resource group..."
az group create --name $RESOURCE_GROUP --location $LOCATION

echo "Creating Cognitive Services..."
az cognitiveservices account create \
    --name myCognitiveServices \
    --resource-group $RESOURCE_GROUP \
    --kind CognitiveServices \
    --sku S0 \
    --location $LOCATION

echo "Creating ML Workspace..."
az ml workspace create \
    --name myMLWorkspace \
    --resource-group $RESOURCE_GROUP \
    --location $LOCATION

echo "Creating OpenAI Service..."
az cognitiveservices account create \
    --name myOpenAI \
    --resource-group $RESOURCE_GROUP \
    --kind OpenAI \
    --sku S0 \
    --location $LOCATION

echo "AI environment setup complete!"
```

---

## 📚 Recursos Adicionales

- [Documentación oficial de Azure CLI](https://docs.microsoft.com/en-us/cli/azure/)
- [Referencia de comandos Azure CLI](https://docs.microsoft.com/en-us/cli/azure/reference-index)
- [Azure CLI GitHub Repository](https://github.com/Azure/azure-cli)
- [Ejemplos de Azure CLI](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-tutorial-use-azure-cli)
