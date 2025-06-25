# ASP.NET Core Commands

ASP.NET Core es un framework web de código abierto y multiplataforma desarrollado por Microsoft para construir aplicaciones web modernas y servicios web.

## Instalación

### Instalar .NET SDK
```bash
# Ubuntu/Debian
wget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
sudo apt-get update
sudo apt-get install -y dotnet-sdk-8.0

# macOS con Homebrew
brew install dotnet

# Windows con Chocolatey
choco install dotnet-sdk
```

### Verificar instalación
```bash
dotnet --version
```

### Listar SDKs instalados
```bash
dotnet --list-sdks
```

### Listar runtimes instalados
```bash
dotnet --list-runtimes
```

## Creación de Proyectos

### Crear nueva aplicación web
```bash
dotnet new webapp -n MyWebApp
```

### Crear API web
```bash
dotnet new webapi -n MyWebApi
```

### Crear aplicación MVC
```bash
dotnet new mvc -n MyMvcApp
```

### Crear aplicación Blazor Server
```bash
dotnet new blazorserver -n MyBlazorApp
```

### Crear aplicación Blazor WebAssembly
```bash
dotnet new blazorwasm -n MyBlazorWasmApp
```

### Crear aplicación con autenticación
```bash
dotnet new webapp --auth Individual -n MySecureApp
```

### Ver plantillas disponibles
```bash
dotnet new --list
```

## Comandos de Desarrollo

### Ejecutar aplicación
```bash
dotnet run
```

### Ejecutar en puerto específico
```bash
dotnet run --urls "https://localhost:5001;http://localhost:5000"
```

### Ejecutar con perfil específico
```bash
dotnet run --launch-profile "Development"
```

### Ejecutar con hot reload
```bash
dotnet watch run
```

### Compilar aplicación
```bash
dotnet build
```

### Compilar para producción
```bash
dotnet build --configuration Release
```

### Limpiar build
```bash
dotnet clean
```

## Comandos de Paquetes

### Agregar paquete NuGet
```bash
dotnet add package EntityFramework
```

### Agregar paquete con versión específica
```bash
dotnet add package Microsoft.EntityFrameworkCore --version 8.0.0
```

### Remover paquete
```bash
dotnet remove package EntityFramework
```

### Listar paquetes
```bash
dotnet list package
```

### Listar paquetes desactualizados
```bash
dotnet list package --outdated
```

### Restaurar paquetes
```bash
dotnet restore
```

## Comandos de Entity Framework

### Instalar herramientas de EF
```bash
dotnet tool install --global dotnet-ef
```

### Crear migración
```bash
dotnet ef migrations add InitialCreate
```

### Aplicar migraciones
```bash
dotnet ef database update
```

### Ver migraciones
```bash
dotnet ef migrations list
```

### Remover última migración
```bash
dotnet ef migrations remove
```

### Generar script SQL
```bash
dotnet ef migrations script
```

### Crear base de datos
```bash
dotnet ef database drop
dotnet ef database update
```

### Scaffolding desde base de datos existente
```bash
dotnet ef dbcontext scaffold "Server=localhost;Database=MyDb;Trusted_Connection=true;" Microsoft.EntityFrameworkCore.SqlServer
```

## Comandos de Testing

### Crear proyecto de tests
```bash
dotnet new xunit -n MyApp.Tests
```

### Ejecutar tests
```bash
dotnet test
```

### Ejecutar tests con coverage
```bash
dotnet test --collect:"XPlat Code Coverage"
```

### Ejecutar tests específicos
```bash
dotnet test --filter "FullyQualifiedName~UnitTest1"
```

### Ejecutar tests con logger
```bash
dotnet test --logger "console;verbosity=detailed"
```

### Generar reporte de coverage
```bash
dotnet test --collect:"XPlat Code Coverage" --results-directory TestResults
```

## Comandos de Publicación

### Publicar aplicación
```bash
dotnet publish
```

### Publicar para producción
```bash
dotnet publish --configuration Release
```

### Publicar para plataforma específica
```bash
dotnet publish --runtime win-x64 --self-contained true
dotnet publish --runtime linux-x64 --self-contained true
```

### Publicar como archivo único
```bash
dotnet publish --runtime win-x64 --self-contained true --output ./publish /p:PublishSingleFile=true
```

### Publicar con AOT (Ahead of Time)
```bash
dotnet publish --runtime linux-x64 --self-contained true /p:PublishAot=true
```

## Comandos de Herramientas

### Instalar herramienta global
```bash
dotnet tool install --global dotnet-aspnet-codegenerator
```

### Listar herramientas instaladas
```bash
dotnet tool list --global
```

### Actualizar herramienta
```bash
dotnet tool update --global dotnet-ef
```

### Desinstalar herramienta
```bash
dotnet tool uninstall --global dotnet-ef
```

## Comandos de Scaffolding

### Instalar generador de código
```bash
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet tool install --global dotnet-aspnet-codegenerator
```

### Generar controlador con vistas
```bash
dotnet aspnet-codegenerator controller -name ProductsController -m Product -dc ApplicationDbContext --relativeFolderPath Controllers --useDefaultLayout
```

### Generar área
```bash
dotnet aspnet-codegenerator area Admin
```

### Generar Identity
```bash
dotnet aspnet-codegenerator identity --dbContext ApplicationDbContext
```

## Comandos de Desarrollo con Docker

### Crear Dockerfile
```bash
# Dockerfile generado automáticamente con
dotnet new dockerfile
```

### Construir imagen Docker
```bash
docker build -t myapp .
```

### Ejecutar contenedor
```bash
docker run -p 8080:80 myapp
```

### Docker Compose
```bash
# Crear docker-compose.yml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "8080:80"
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
```

## Comandos de Configuración

### Ver información de configuración
```bash
dotnet --info
```

### Configurar feeds de NuGet
```bash
dotnet nuget add source https://api.nuget.org/v3/index.json --name "nuget.org"
```

### Listar fuentes de NuGet
```bash
dotnet nuget list source
```

### Limpiar cache de NuGet
```bash
dotnet nuget locals all --clear
```

## Comandos de Secrets

### Inicializar User Secrets
```bash
dotnet user-secrets init
```

### Agregar secret
```bash
dotnet user-secrets set "ConnectionStrings:DefaultConnection" "Server=localhost;Database=MyDb;Trusted_Connection=true;"
```

### Listar secrets
```bash
dotnet user-secrets list
```

### Remover secret
```bash
dotnet user-secrets remove "ConnectionStrings:DefaultConnection"
```

### Limpiar todos los secrets
```bash
dotnet user-secrets clear
```

## Comandos de Certificados

### Generar certificado de desarrollo HTTPS
```bash
dotnet dev-certs https --trust
```

### Limpiar certificados
```bash
dotnet dev-certs https --clean
```

### Verificar certificados
```bash
dotnet dev-certs https --check
```

## Comandos de Debugging

### Ejecutar con debugger
```bash
dotnet run --verbosity diagnostic
```

### Crear dump de proceso
```bash
dotnet-dump collect -p <process-id>
```

### Analizar dump
```bash
dotnet-dump analyze <dump-file>
```

### Profiling con dotnet-trace
```bash
dotnet tool install --global dotnet-trace
dotnet-trace collect --process-id <pid>
```

## Comandos de Monitoring

### Instalar herramientas de diagnóstico
```bash
dotnet tool install --global dotnet-counters
dotnet tool install --global dotnet-trace
dotnet tool install --global dotnet-dump
```

### Monitorear contadores
```bash
dotnet-counters monitor --process-id <pid>
```

### Monitorear aplicación
```bash
dotnet-counters monitor --name "MyApp"
```

## Comandos de Workloads

### Listar workloads disponibles
```bash
dotnet workload search
```

### Instalar workload
```bash
dotnet workload install maui
```

### Actualizar workloads
```bash
dotnet workload update
```

### Remover workload
```bash
dotnet workload uninstall maui
```

## Comandos de Plantillas

### Instalar plantilla personalizada
```bash
dotnet new install Microsoft.DotNet.Web.ProjectTemplates.8.0
```

### Desinstalar plantilla
```bash
dotnet new uninstall Microsoft.DotNet.Web.ProjectTemplates.8.0
```

### Crear plantilla personalizada
```bash
dotnet new template
```

## Comandos de Performance

### Ejecutar benchmark
```bash
dotnet run --configuration Release --framework net8.0
```

### Analizar rendimiento
```bash
dotnet-trace collect --format speedscope --output trace.json -- dotnet run
```

### Optimizar para tamaño
```bash
dotnet publish --configuration Release --runtime win-x64 --self-contained true /p:PublishTrimmed=true
```
