# 🔷 Comandos C# / .NET

## Herramientas de Línea de Comandos

### dotnet
**Descripción:** CLI de .NET para crear, compilar, ejecutar y publicar aplicaciones .NET
**Sintaxis básica:**
```bash
dotnet [comando] [opciones] [argumentos]
```

### csc
**Descripción:** Compilador de C# (Roslyn)
**Sintaxis básica:**
```bash
csc [opciones] archivo.cs
```

### nuget
**Descripción:** Gestor de paquetes para .NET
**Sintaxis básica:**
```bash
nuget [comando] [opciones]
```

---

## Gestión de Proyectos

### Crear Proyectos
```bash
# Ver plantillas disponibles
dotnet new --list

# Crear aplicación de consola
dotnet new console -n MiApp

# Crear API web
dotnet new webapi -n MiAPI

# Crear aplicación MVC
dotnet new mvc -n MiWebApp

# Crear biblioteca de clases
dotnet new classlib -n MiBiblioteca

# Crear proyecto Blazor Server
dotnet new blazorserver -n MiBlazorApp

# Crear proyecto Blazor WebAssembly
dotnet new blazorwasm -n MiBlazorWasmApp

# Crear proyecto de pruebas xUnit
dotnet new xunit -n MiApp.Tests

# Crear proyecto WPF
dotnet new wpf -n MiAppWPF

# Crear proyecto WinForms
dotnet new winforms -n MiAppWinForms
```

### Gestión de Soluciones
```bash
# Crear solución
dotnet new sln -n MiSolucion

# Agregar proyecto a solución
dotnet sln add MiApp/MiApp.csproj

# Remover proyecto de solución
dotnet sln remove MiApp/MiApp.csproj

# Listar proyectos en solución
dotnet sln list

# Compilar toda la solución
dotnet build MiSolucion.sln
```

---

## Compilación y Ejecución

### Build y Run
```bash
# Compilar proyecto
dotnet build

# Compilar en modo Release
dotnet build -c Release

# Compilar proyecto específico
dotnet build MiApp/MiApp.csproj

# Ejecutar aplicación
dotnet run

# Ejecutar con argumentos
dotnet run -- arg1 arg2

# Ejecutar proyecto específico
dotnet run --project MiApp/MiApp.csproj

# Ejecutar DLL compilada
dotnet MiApp.dll
```

### Publicación
```bash
# Publicar aplicación
dotnet publish

# Publicar para producción
dotnet publish -c Release

# Publicar auto-contenida para Windows
dotnet publish -r win-x64 --self-contained

# Publicar auto-contenida para Linux
dotnet publish -r linux-x64 --self-contained

# Publicar como ejecutable único
dotnet publish -r win-x64 -p:PublishSingleFile=true

# Publicar sin dependencias de runtime
dotnet publish --self-contained false

# Publicar con AOT (Ahead of Time)
dotnet publish -c Release -r linux-x64 --self-contained -p:PublishAot=true
```

---

## Gestión de Paquetes NuGet

### Comandos Básicos
```bash
# Agregar paquete
dotnet add package Newtonsoft.Json

# Agregar versión específica
dotnet add package Microsoft.EntityFrameworkCore --version 7.0.0

# Agregar desde fuente específica
dotnet add package MiPaquete --source https://api.nuget.org/v3/index.json

# Listar paquetes
dotnet list package

# Listar paquetes desactualizados
dotnet list package --outdated

# Actualizar paquetes
dotnet add package Newtonsoft.Json

# Remover paquete
dotnet remove package Newtonsoft.Json
```

### Restauración de Paquetes
```bash
# Restaurar paquetes
dotnet restore

# Restaurar sin cache
dotnet restore --no-cache

# Restaurar desde fuente específica
dotnet restore --source https://api.nuget.org/v3/index.json

# Forzar evaluación de dependencias
dotnet restore --force
```

---

## Testing

### Comandos de Test
```bash
# Ejecutar tests
dotnet test

# Ejecutar tests con detalles
dotnet test --logger trx --logger "console;verbosity=detailed"

# Ejecutar tests de proyecto específico
dotnet test MiApp.Tests/MiApp.Tests.csproj

# Ejecutar tests con cobertura
dotnet test --collect:"XPlat Code Coverage"

# Ejecutar tests por categoría
dotnet test --filter Category=Unit

# Ejecutar test específico
dotnet test --filter "FullyQualifiedName~MiTest"

# Ejecutar tests en paralelo
dotnet test --parallel
```

### Generación de Reportes
```bash
# Instalar herramienta de reportes
dotnet tool install -g dotnet-reportgenerator-globaltool

# Generar reporte de cobertura
reportgenerator -reports:"coverage.cobertura.xml" -targetdir:"coveragereport"

# Ver reporte
start coveragereport/index.html  # Windows
open coveragereport/index.html   # macOS
xdg-open coveragereport/index.html  # Linux
```

---

## Entity Framework Core

### Migraciones
```bash
# Instalar herramientas EF
dotnet tool install --global dotnet-ef

# Agregar migración
dotnet ef migrations add InitialCreate

# Aplicar migraciones
dotnet ef database update

# Revertir migración
dotnet ef database update PreviousMigration

# Listar migraciones
dotnet ef migrations list

# Remover última migración
dotnet ef migrations remove

# Generar script SQL
dotnet ef migrations script

# Crear base de datos
dotnet ef database drop
dotnet ef database update
```

### Scaffolding (Database First)
```bash
# Scaffold desde base de datos existente
dotnet ef dbcontext scaffold "Server=localhost;Database=MiDB;Trusted_Connection=true;" Microsoft.EntityFrameworkCore.SqlServer

# Scaffold con opciones específicas
dotnet ef dbcontext scaffold "connectionstring" Microsoft.EntityFrameworkCore.SqlServer \
    --output-dir Models \
    --context-dir Data \
    --context MiContexto \
    --data-annotations
```

---

## ASP.NET Core

### Desarrollo Local
```bash
# Ejecutar con hot reload
dotnet watch run

# Ejecutar en puerto específico
dotnet run --urls "https://localhost:5001;http://localhost:5000"

# Ejecutar con perfil específico
dotnet run --launch-profile "Development"

# Generar certificado de desarrollo HTTPS
dotnet dev-certs https --trust

# Limpiar certificados
dotnet dev-certs https --clean
```

### Scaffolding de Controllers y Views
```bash
# Instalar herramientas de scaffolding
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet tool install -g dotnet-aspnet-codegenerator

# Generar controller con views
dotnet aspnet-codegenerator controller -name ProductController -m Product -dc ApplicationDbContext --relativeFolderPath Controllers --useDefaultLayout

# Generar API controller
dotnet aspnet-codegenerator controller -name ProductApiController -m Product -dc ApplicationDbContext -api --relativeFolderPath Controllers/Api

# Generar Razor Pages
dotnet aspnet-codegenerator razorpage -m Product -dc ApplicationDbContext -udl -outDir Pages/Products
```

---

## Herramientas Globales

### Instalación de Herramientas
```bash
# Listar herramientas instaladas
dotnet tool list -g

# Instalar herramienta global
dotnet tool install -g dotnet-ef

# Actualizar herramienta
dotnet tool update -g dotnet-ef

# Desinstalar herramienta
dotnet tool uninstall -g dotnet-ef

# Instalar herramienta local
dotnet new tool-manifest
dotnet tool install dotnet-ef

# Restaurar herramientas locales
dotnet tool restore
```

### Herramientas Útiles
```bash
# dotnet-outdated - Verificar paquetes desactualizados
dotnet tool install -g dotnet-outdated-tool
dotnet outdated

# dotnet-format - Formatear código
dotnet tool install -g dotnet-format
dotnet format

# PowerShell - Shell multiplataforma
dotnet tool install -g PowerShell

# Swagger CLI
dotnet tool install -g swashbuckle.aspnetcore.cli
swagger tofile --output swagger.json bin/Debug/net7.0/MiAPI.dll v1
```

---

## Ejemplos de Uso Común

### API REST Completa
```bash
# 1. Crear proyecto API
dotnet new webapi -n MiAPI
cd MiAPI

# 2. Agregar Entity Framework
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Tools

# 3. Agregar autenticación JWT
dotnet add package Microsoft.AspNetCore.Authentication.JwtBearer

# 4. Crear modelo
cat > Models/Product.cs << 'EOF'
namespace MiAPI.Models
{
    public class Product
    {
        public int Id { get; set; }
        public string Name { get; set; } = string.Empty;
        public decimal Price { get; set; }
        public string Description { get; set; } = string.Empty;
    }
}
EOF

# 5. Crear DbContext
cat > Data/ApplicationDbContext.cs << 'EOF'
using Microsoft.EntityFrameworkCore;
using MiAPI.Models;

namespace MiAPI.Data
{
    public class ApplicationDbContext : DbContext
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options) { }
        
        public DbSet<Product> Products { get; set; }
    }
}
EOF

# 6. Agregar migración
dotnet ef migrations add InitialCreate

# 7. Ejecutar
dotnet run
```

### Aplicación Blazor Server
```bash
# 1. Crear proyecto Blazor
dotnet new blazorserver -n MiBlazorApp
cd MiBlazorApp

# 2. Agregar Entity Framework
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Tools

# 3. Ejecutar con hot reload
dotnet watch run

# 4. Navegar a https://localhost:5001
```

### Microservicio con Docker
```bash
# 1. Crear API
dotnet new webapi -n MiMicroservicio
cd MiMicroservicio

# 2. Crear Dockerfile
cat > Dockerfile << 'EOF'
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["MiMicroservicio.csproj", "."]
RUN dotnet restore "./MiMicroservicio.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "MiMicroservicio.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MiMicroservicio.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MiMicroservicio.dll"]
EOF

# 3. Construir imagen Docker
docker build -t mi-microservicio .

# 4. Ejecutar contenedor
docker run -p 8080:80 mi-microservicio
```

---

## Scripts de Utilidad

### Script de Build Completo
```bash
#!/bin/bash
# build.sh - Script de construcción completa para .NET

echo "🏗️  Iniciando build de proyecto .NET..."

# Limpiar build anterior
echo "🧹 Limpiando build anterior..."
dotnet clean

# Restaurar paquetes
echo "📦 Restaurando paquetes NuGet..."
dotnet restore

if [ $? -ne 0 ]; then
    echo "❌ Error restaurando paquetes"
    exit 1
fi

# Compilar solución
echo "⚙️  Compilando solución..."
dotnet build --no-restore -c Release

if [ $? -ne 0 ]; then
    echo "❌ Error en compilación"
    exit 1
fi

# Ejecutar tests
echo "🧪 Ejecutando tests..."
dotnet test --no-build -c Release --logger trx --collect:"XPlat Code Coverage"

if [ $? -ne 0 ]; then
    echo "❌ Fallos en tests"
    exit 1
fi

# Publicar aplicación
echo "📋 Publicando aplicación..."
dotnet publish --no-build -c Release -o ./publish

echo "🎉 Build completo exitoso!"
echo "📁 Artefactos en: ./publish"
```

### Script de Desarrollo
```bash
#!/bin/bash
# dev.sh - Script para desarrollo local

# Función para setup inicial
setup() {
    echo "🔧 Configurando entorno de desarrollo..."
    
    # Instalar herramientas globales
    dotnet tool install -g dotnet-ef
    dotnet tool install -g dotnet-format
    dotnet tool install -g dotnet-outdated-tool
    
    # Configurar certificados HTTPS
    dotnet dev-certs https --trust
    
    echo "✅ Setup completo"
}

# Función para ejecutar con hot reload
dev_run() {
    echo "🚀 Iniciando aplicación con hot reload..."
    dotnet watch run --urls "https://localhost:5001;http://localhost:5000"
}

# Función para formatear código
format_code() {
    echo "🎨 Formateando código..."
    dotnet format
}

# Función para verificar paquetes desactualizados
check_outdated() {
    echo "📊 Verificando paquetes desactualizados..."
    dotnet outdated
}

# Función para ejecutar análisis completo
analyze() {
    echo "🔍 Ejecutando análisis de código..."
    
    # Formatear código
    format_code
    
    # Verificar paquetes
    check_outdated
    
    # Ejecutar tests con cobertura
    dotnet test --collect:"XPlat Code Coverage"
    
    # Análisis de seguridad (requiere herramientas adicionales)
    # dotnet list package --vulnerable
}

# Menú interactivo
echo "🛠️  Herramientas de Desarrollo .NET"
echo "1. Setup inicial"
echo "2. Ejecutar con hot reload"
echo "3. Formatear código"
echo "4. Verificar paquetes desactualizados"
echo "5. Análisis completo"
echo "6. Generar migración EF"

read -p "Selecciona una opción: " option

case $option in
    1) setup ;;
    2) dev_run ;;
    3) format_code ;;
    4) check_outdated ;;
    5) analyze ;;
    6) 
        read -p "Nombre de la migración: " migration_name
        dotnet ef migrations add "$migration_name"
        ;;
    *) echo "Opción inválida" ;;
esac
```

### Script de Deploy a Azure
```bash
#!/bin/bash
# deploy-azure.sh - Script de despliegue a Azure

APP_NAME="mi-webapp"
RESOURCE_GROUP="mi-grupo-recursos"
PLAN_NAME="mi-plan-app-service"

echo "🚀 Desplegando aplicación .NET a Azure..."

# Login a Azure (si no está logueado)
az account show &>/dev/null || az login

# Crear grupo de recursos si no existe
echo "📋 Verificando grupo de recursos..."
az group create --name $RESOURCE_GROUP --location "East US" --output none

# Crear plan de App Service si no existe
echo "⚙️  Verificando plan de App Service..."
az appservice plan create \
    --name $PLAN_NAME \
    --resource-group $RESOURCE_GROUP \
    --sku B1 \
    --is-linux \
    --output none

# Crear Web App si no existe
echo "🌐 Verificando Web App..."
az webapp create \
    --name $APP_NAME \
    --resource-group $RESOURCE_GROUP \
    --plan $PLAN_NAME \
    --runtime "DOTNETCORE:7.0" \
    --output none

# Build y publicar aplicación
echo "📦 Construyendo aplicación..."
dotnet publish -c Release -o ./publish

# Crear archivo ZIP para deploy
echo "🗜️  Creando paquete de despliegue..."
cd publish
zip -r ../deploy.zip .
cd ..

# Deploy a Azure
echo "🚁 Desplegando a Azure..."
az webapp deploy \
    --resource-group $RESOURCE_GROUP \
    --name $APP_NAME \
    --src-path deploy.zip \
    --type zip

# Configurar variables de entorno si existen
if [ -f "appsettings.Production.json" ]; then
    echo "⚙️  Configurando variables de entorno..."
    # Aquí agregarías configuración específica
fi

# Verificar despliegue
echo "🔍 Verificando despliegue..."
WEBAPP_URL="https://${APP_NAME}.azurewebsites.net"
HTTP_STATUS=$(curl -s -o /dev/null -w "%{http_code}" $WEBAPP_URL)

if [ $HTTP_STATUS -eq 200 ]; then
    echo "✅ Despliegue exitoso!"
    echo "🌐 Aplicación disponible en: $WEBAPP_URL"
else
    echo "❌ Error en el despliegue (HTTP $HTTP_STATUS)"
    echo "📋 Logs de la aplicación:"
    az webapp log tail --resource-group $RESOURCE_GROUP --name $APP_NAME
fi

# Limpiar archivos temporales
rm -f deploy.zip
rm -rf publish
```

---

## Configuraciones y Optimización

### Configuración de Performance
```bash
# Variables de entorno para optimización
export DOTNET_ReadyToRun=1
export DOTNET_TieredPGO=1
export DOTNET_TC_QuickJitForLoops=1

# Configuración de GC
export DOTNET_gcServer=1
export DOTNET_GCRetainVM=1

# Logging optimizado para producción
export DOTNET_ENVIRONMENT=Production
export Logging__LogLevel__Default=Warning
```

### Diagnósticos y Profiling
```bash
# Instalar herramientas de diagnóstico
dotnet tool install -g dotnet-counters
dotnet tool install -g dotnet-trace
dotnet tool install -g dotnet-dump

# Monitoreo en tiempo real
dotnet-counters monitor --process-id <pid>

# Captura de traces
dotnet-trace collect --process-id <pid> --output trace.nettrace

# Análisis de memoria
dotnet-dump collect --process-id <pid> --output dump.dmp

# Ver información de ensamblados cargados
dotnet-gcdump collect --process-id <pid>
```

Esta documentación cubre los comandos más importantes de .NET y C#, desde desarrollo básico hasta despliegue en producción.
