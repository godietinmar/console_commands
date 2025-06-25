# 🐹 Comandos Go

## Herramientas de Línea de Comandos

### go
**Descripción:** Herramienta principal de Go para compilar, ejecutar y gestionar código
**Sintaxis básica:**
```bash
go [comando] [argumentos]
```

### gofmt
**Descripción:** Formateador de código Go
**Sintaxis básica:**
```bash
gofmt [opciones] [archivos]
```

### go mod
**Descripción:** Gestor de módulos de Go
**Sintaxis básica:**
```bash
go mod [comando] [argumentos]
```

### go test
**Descripción:** Herramienta de testing de Go
**Sintaxis básica:**
```bash
go test [opciones] [paquetes]
```

---

## Instalación y Configuración

### Instalar Go
```bash
# Descargar e instalar Go (Linux/macOS)
wget https://go.dev/dl/go1.21.0.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.21.0.linux-amd64.tar.gz

# Configurar PATH
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
echo 'export GOPATH=$HOME/go' >> ~/.bashrc
echo 'export PATH=$PATH:$GOPATH/bin' >> ~/.bashrc
source ~/.bashrc

# Verificar instalación
go version

# Ver configuración de Go
go env

# Ver variables específicas
go env GOPATH
go env GOROOT
```

### Configuración del Entorno
```bash
# Ver todas las variables de entorno
go env

# Establecer proxy de módulos
go env -w GOPROXY=https://proxy.golang.org,direct

# Configurar sum database
go env -w GOSUMDB=sum.golang.org

# Habilitar módulos
go env -w GO111MODULE=on

# Configurar directorio de caché
go env -w GOCACHE=/path/to/cache

# Resetear configuración
go env -u GOPROXY
```

---

## Gestión de Proyectos y Módulos

### Crear y Configurar Módulos
```bash
# Crear nuevo módulo
go mod init mi-proyecto

# Crear módulo con dominio
go mod init github.com/usuario/mi-proyecto

# Ver información del módulo
go list -m all

# Agregar dependencia
go get github.com/gin-gonic/gin

# Agregar versión específica
go get github.com/gin-gonic/gin@v1.9.0

# Agregar dependencia de desarrollo
go get -t github.com/stretchr/testify

# Actualizar dependencias
go get -u ./...

# Actualizar dependencia específica
go get -u github.com/gin-gonic/gin

# Remover dependencias no utilizadas
go mod tidy

# Descargar dependencias
go mod download

# Verificar dependencias
go mod verify

# Ver grafo de dependencias
go mod graph
```

### Workspace (Go 1.18+)
```bash
# Crear workspace
go work init

# Agregar módulo al workspace
go work use ./mi-modulo

# Ver configuración del workspace
go work edit -print

# Sincronizar workspace
go work sync
```

---

## Compilación y Ejecución

### Comandos Básicos
```bash
# Ejecutar código directamente
go run main.go

# Ejecutar con argumentos
go run main.go arg1 arg2

# Compilar a ejecutable
go build

# Compilar con nombre específico
go build -o mi_programa

# Compilar todos los archivos
go build .

# Compilar paquete específico
go build ./cmd/server

# Instalar ejecutable en GOPATH/bin
go install

# Compilar para múltiples plataformas
GOOS=linux GOARCH=amd64 go build -o mi_programa_linux
GOOS=windows GOARCH=amd64 go build -o mi_programa.exe
GOOS=darwin GOARCH=amd64 go build -o mi_programa_mac
```

### Optimización de Build
```bash
# Compilar sin información de debug
go build -ldflags="-s -w"

# Compilar estáticamente
CGO_ENABLED=0 go build -a -ldflags '-extldflags "-static"'

# Compilar con información de versión
go build -ldflags "-X main.version=1.0.0"

# Compilar con tags
go build -tags production

# Ver información del ejecutable
go version mi_programa
```

---

## Testing

### Ejecutar Tests
```bash
# Ejecutar todos los tests
go test ./...

# Ejecutar tests del paquete actual
go test

# Ejecutar con verbose
go test -v

# Ejecutar test específico
go test -run TestFunctionName

# Ejecutar tests con patrón
go test -run "Test.*API"

# Ejecutar tests de benchmark
go test -bench=.

# Ejecutar benchmark específico
go test -bench=BenchmarkMyFunction

# Ejecutar tests con cobertura
go test -cover

# Generar reporte de cobertura
go test -coverprofile=coverage.out
go tool cover -html=coverage.out -o coverage.html

# Tests con race detection
go test -race
```

### Tests de Integración
```bash
# Ejecutar solo tests cortos
go test -short

# Ejecutar tests con timeout
go test -timeout 30s

# Ejecutar tests en paralelo
go test -parallel 4

# Ejecutar tests con tags
go test -tags integration

# Generar test coverage por función
go test -covermode=count -coverprofile=coverage.out
go tool cover -func=coverage.out
```

---

## Herramientas de Desarrollo

### Formateo y Linting
```bash
# Formatear código
go fmt ./...

# Formatear archivo específico
gofmt -w main.go

# Verificar formato sin modificar
gofmt -l .

# Simplificar código
gofmt -s -w .

# Instalar golangci-lint
go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest

# Ejecutar linter
golangci-lint run

# Ejecutar con configuración específica
golangci-lint run --config .golangci.yml

# Ver todos los linters disponibles
golangci-lint help linters
```

### Herramientas de Análisis
```bash
# Análisis estático con vet
go vet ./...

# Instalar herramientas adicionales
go install golang.org/x/tools/cmd/goimports@latest
go install golang.org/x/tools/cmd/godoc@latest
go install github.com/kisielk/errcheck@latest

# Organizar imports
goimports -w .

# Verificar errores no manejados
errcheck ./...

# Generar documentación
godoc -http=:6060

# Ver documentación de paquete
go doc fmt.Println
```

---

## Profiling y Debugging

### Profiling
```bash
# Profiling de CPU
go test -cpuprofile=cpu.prof -bench=.

# Profiling de memoria
go test -memprofile=mem.prof -bench=.

# Instalar herramientas de profiling
go install github.com/google/pprof@latest

# Analizar perfil de CPU
go tool pprof cpu.prof

# Analizar perfil de memoria
go tool pprof mem.prof

# Profiling en aplicación web
import _ "net/http/pprof"

# Ver perfiles en navegador
# http://localhost:6060/debug/pprof/
```

### Debugging
```bash
# Instalar Delve debugger
go install github.com/go-delve/delve/cmd/dlv@latest

# Iniciar debugging
dlv debug

# Debug con argumentos
dlv debug -- arg1 arg2

# Debug test específico
dlv test -- -test.run TestMyFunction

# Debug ejecutable
dlv exec ./mi_programa

# Conectar a proceso
dlv attach <pid>
```

---

## Ejemplos de Uso Común

### Aplicación CLI Simple
```bash
# 1. Crear proyecto
mkdir mi-cli && cd mi-cli
go mod init github.com/usuario/mi-cli

# 2. Instalar dependencias
go get github.com/spf13/cobra
go get github.com/spf13/viper

# 3. Crear código fuente (main.go)
cat > main.go << 'EOF'
package main

import (
    "fmt"
    "os"

    "github.com/spf13/cobra"
    "github.com/spf13/viper"
)

var (
    cfgFile string
    verbose bool
)

var rootCmd = &cobra.Command{
    Use:   "mi-cli",
    Short: "Una aplicación CLI de ejemplo",
    Long:  "Una aplicación de línea de comandos construida con Go y Cobra",
}

var versionCmd = &cobra.Command{
    Use:   "version",
    Short: "Mostrar la versión",
    Run: func(cmd *cobra.Command, args []string) {
        fmt.Println("mi-cli version 1.0.0")
    },
}

var serveCmd = &cobra.Command{
    Use:   "serve",
    Short: "Iniciar servidor",
    Run: func(cmd *cobra.Command, args []string) {
        port, _ := cmd.Flags().GetInt("port")
        fmt.Printf("Iniciando servidor en puerto %d\n", port)
        
        if verbose {
            fmt.Println("Modo verbose activado")
        }
    },
}

func init() {
    cobra.OnInitialize(initConfig)
    
    rootCmd.PersistentFlags().StringVar(&cfgFile, "config", "", "archivo de configuración")
    rootCmd.PersistentFlags().BoolVarP(&verbose, "verbose", "v", false, "output verbose")
    
    serveCmd.Flags().IntP("port", "p", 8080, "puerto del servidor")
    
    rootCmd.AddCommand(versionCmd)
    rootCmd.AddCommand(serveCmd)
}

func initConfig() {
    if cfgFile != "" {
        viper.SetConfigFile(cfgFile)
    } else {
        viper.SetConfigName("config")
        viper.AddConfigPath(".")
    }
    
    viper.AutomaticEnv()
    
    if err := viper.ReadInConfig(); err == nil {
        fmt.Println("Usando archivo de configuración:", viper.ConfigFileUsed())
    }
}

func main() {
    if err := rootCmd.Execute(); err != nil {
        fmt.Println(err)
        os.Exit(1)
    }
}
EOF

# 4. Compilar y probar
go build
./mi-cli version
./mi-cli serve --port 3000 --verbose
```

### API REST con Gin
```bash
# 1. Crear proyecto
mkdir mi-api && cd mi-api
go mod init github.com/usuario/mi-api

# 2. Instalar dependencias
go get github.com/gin-gonic/gin
go get github.com/gin-gonic/gin/binding
go get gorm.io/gorm
go get gorm.io/driver/postgres

# 3. Crear estructura del proyecto
mkdir -p cmd/server handlers models config

# 4. Crear servidor principal (cmd/server/main.go)
cat > cmd/server/main.go << 'EOF'
package main

import (
    "log"
    "github.com/gin-gonic/gin"
    "github.com/usuario/mi-api/handlers"
)

func main() {
    r := gin.Default()
    
    // Middleware
    r.Use(gin.Logger())
    r.Use(gin.Recovery())
    
    // Rutas
    api := r.Group("/api/v1")
    {
        api.GET("/health", handlers.HealthCheck)
        api.GET("/users", handlers.GetUsers)
        api.POST("/users", handlers.CreateUser)
        api.GET("/users/:id", handlers.GetUser)
        api.PUT("/users/:id", handlers.UpdateUser)
        api.DELETE("/users/:id", handlers.DeleteUser)
    }
    
    log.Println("Servidor iniciando en :8080")
    if err := r.Run(":8080"); err != nil {
        log.Fatal("Error iniciando servidor:", err)
    }
}
EOF

# 5. Crear handlers (handlers/users.go)
cat > handlers/users.go << 'EOF'
package handlers

import (
    "net/http"
    "strconv"
    
    "github.com/gin-gonic/gin"
)

type User struct {
    ID    int    `json:"id"`
    Name  string `json:"name"`
    Email string `json:"email"`
}

var users = []User{
    {ID: 1, Name: "Juan", Email: "juan@example.com"},
    {ID: 2, Name: "María", Email: "maria@example.com"},
}

func HealthCheck(c *gin.Context) {
    c.JSON(http.StatusOK, gin.H{
        "status": "ok",
        "message": "API funcionando correctamente",
    })
}

func GetUsers(c *gin.Context) {
    c.JSON(http.StatusOK, gin.H{
        "users": users,
    })
}

func GetUser(c *gin.Context) {
    id, err := strconv.Atoi(c.Param("id"))
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{"error": "ID inválido"})
        return
    }
    
    for _, user := range users {
        if user.ID == id {
            c.JSON(http.StatusOK, user)
            return
        }
    }
    
    c.JSON(http.StatusNotFound, gin.H{"error": "Usuario no encontrado"})
}

func CreateUser(c *gin.Context) {
    var newUser User
    if err := c.ShouldBindJSON(&newUser); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
        return
    }
    
    newUser.ID = len(users) + 1
    users = append(users, newUser)
    
    c.JSON(http.StatusCreated, newUser)
}

func UpdateUser(c *gin.Context) {
    id, err := strconv.Atoi(c.Param("id"))
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{"error": "ID inválido"})
        return
    }
    
    var updatedUser User
    if err := c.ShouldBindJSON(&updatedUser); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
        return
    }
    
    for i, user := range users {
        if user.ID == id {
            users[i] = User{ID: id, Name: updatedUser.Name, Email: updatedUser.Email}
            c.JSON(http.StatusOK, users[i])
            return
        }
    }
    
    c.JSON(http.StatusNotFound, gin.H{"error": "Usuario no encontrado"})
}

func DeleteUser(c *gin.Context) {
    id, err := strconv.Atoi(c.Param("id"))
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{"error": "ID inválido"})
        return
    }
    
    for i, user := range users {
        if user.ID == id {
            users = append(users[:i], users[i+1:]...)
            c.JSON(http.StatusOK, gin.H{"message": "Usuario eliminado"})
            return
        }
    }
    
    c.JSON(http.StatusNotFound, gin.H{"error": "Usuario no encontrado"})
}
EOF

# 6. Ejecutar servidor
go run cmd/server/main.go
```

### Microservicio con gRPC
```bash
# 1. Crear proyecto
mkdir grpc-service && cd grpc-service
go mod init github.com/usuario/grpc-service

# 2. Instalar dependencias
go get google.golang.org/grpc
go get google.golang.org/protobuf

# 3. Instalar herramientas de protobuf
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest

# 4. Crear definición protobuf (proto/user.proto)
mkdir proto
cat > proto/user.proto << 'EOF'
syntax = "proto3";

package user;

option go_package = "github.com/usuario/grpc-service/proto";

service UserService {
    rpc GetUser(GetUserRequest) returns (GetUserResponse);
    rpc CreateUser(CreateUserRequest) returns (CreateUserResponse);
}

message GetUserRequest {
    int32 id = 1;
}

message GetUserResponse {
    int32 id = 1;
    string name = 2;
    string email = 3;
}

message CreateUserRequest {
    string name = 1;
    string email = 2;
}

message CreateUserResponse {
    int32 id = 1;
    string name = 2;
    string email = 3;
}
EOF

# 5. Generar código Go
protoc --go_out=. --go-grpc_out=. proto/user.proto

# 6. Implementar servidor
cat > server/main.go << 'EOF'
package main

import (
    "context"
    "log"
    "net"
    
    "google.golang.org/grpc"
    pb "github.com/usuario/grpc-service/proto"
)

type server struct {
    pb.UnimplementedUserServiceServer
}

func (s *server) GetUser(ctx context.Context, req *pb.GetUserRequest) (*pb.GetUserResponse, error) {
    return &pb.GetUserResponse{
        Id:    req.Id,
        Name:  "Usuario " + string(req.Id),
        Email: "user@example.com",
    }, nil
}

func (s *server) CreateUser(ctx context.Context, req *pb.CreateUserRequest) (*pb.CreateUserResponse, error) {
    return &pb.CreateUserResponse{
        Id:    1,
        Name:  req.Name,
        Email: req.Email,
    }, nil
}

func main() {
    lis, err := net.Listen("tcp", ":50051")
    if err != nil {
        log.Fatalf("Error listening: %v", err)
    }
    
    s := grpc.NewServer()
    pb.RegisterUserServiceServer(s, &server{})
    
    log.Println("Servidor gRPC iniciando en :50051")
    if err := s.Serve(lis); err != nil {
        log.Fatalf("Error serving: %v", err)
    }
}
EOF

# 7. Ejecutar servidor
mkdir server
go run server/main.go
```

---

## Scripts de Utilidad

### Script de Desarrollo Go
```bash
#!/bin/bash
# go-dev.sh - Herramientas de desarrollo Go

# Función para setup inicial
setup() {
    echo "🐹 Configurando entorno de desarrollo Go..."
    
    # Verificar instalación de Go
    if ! command -v go &> /dev/null; then
        echo "❌ Go no está instalado"
        echo "💡 Instala Go desde: https://golang.org/dl/"
        exit 1
    fi
    
    echo "✅ Go version: $(go version)"
    
    # Instalar herramientas útiles
    echo "🔧 Instalando herramientas de desarrollo..."
    go install golang.org/x/tools/cmd/goimports@latest
    go install golang.org/x/tools/cmd/godoc@latest
    go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest
    go install github.com/go-delve/delve/cmd/dlv@latest
    go install github.com/kisielk/errcheck@latest
    go install honnef.co/go/tools/cmd/staticcheck@latest
    
    # Crear estructura de proyecto si no existe
    if [ ! -f "go.mod" ]; then
        echo "📦 Inicializando módulo Go..."
        read -p "Nombre del módulo (ej: github.com/usuario/proyecto): " module_name
        go mod init "$module_name"
    fi
    
    echo "✅ Setup completo"
}

# Función para desarrollo con hot reload
dev_watch() {
    echo "👀 Iniciando desarrollo con auto-reload..."
    
    # Instalar air si no está disponible
    if ! command -v air &> /dev/null; then
        echo "📦 Instalando air para hot reload..."
        go install github.com/cosmtrek/air@latest
    fi
    
    # Crear configuración de air si no existe
    if [ ! -f ".air.toml" ]; then
        air init
    fi
    
    # Iniciar air
    air
}

# Función para análisis completo
analyze() {
    echo "🔍 Ejecutando análisis completo..."
    
    # Formatear código
    echo "🎨 Formateando código..."
    go fmt ./...
    goimports -w .
    
    # Verificar con vet
    echo "🔍 Ejecutando go vet..."
    go vet ./...
    
    # Ejecutar golangci-lint
    echo "📝 Ejecutando linters..."
    golangci-lint run
    
    # Verificar errores no manejados
    echo "❌ Verificando errores no manejados..."
    errcheck ./...
    
    # Análisis estático adicional
    echo "🔬 Análisis estático..."
    staticcheck ./...
    
    # Ejecutar tests
    echo "🧪 Ejecutando tests..."
    go test -race -cover ./...
    
    # Verificar dependencias
    echo "📦 Verificando dependencias..."
    go mod tidy
    go mod verify
}

# Función para benchmarking
benchmark() {
    echo "⚡ Ejecutando benchmarks..."
    
    # Ejecutar benchmarks
    go test -bench=. -benchmem ./...
    
    # Generar perfil de CPU si hay benchmarks
    if go test -bench=. -list | grep -q "Benchmark"; then
        echo "📊 Generando perfil de CPU..."
        go test -bench=. -cpuprofile=cpu.prof
        
        echo "💾 Perfil guardado en cpu.prof"
        echo "💡 Para analizar: go tool pprof cpu.prof"
    fi
}

# Función para optimizar build
optimize() {
    echo "🚀 Optimizando build..."
    
    # Build optimizado
    echo "🏗️  Compilando versión optimizada..."
    go build -ldflags="-s -w" -o ./bin/$(basename $PWD)
    
    # Verificar tamaño
    if [ -f "./bin/$(basename $PWD)" ]; then
        echo "📏 Tamaño del ejecutable:"
        ls -lh "./bin/$(basename $PWD)"
    fi
    
    # Build para múltiples plataformas
    echo "🌍 Compilando para múltiples plataformas..."
    platforms=("linux/amd64" "darwin/amd64" "windows/amd64")
    
    for platform in "${platforms[@]}"; do
        IFS="/" read -r os arch <<< "$platform"
        output="./bin/$(basename $PWD)-$os-$arch"
        
        if [ "$os" = "windows" ]; then
            output="$output.exe"
        fi
        
        echo "Building for $os/$arch..."
        GOOS=$os GOARCH=$arch go build -ldflags="-s -w" -o "$output"
        
        if [ $? -eq 0 ]; then
            echo "✅ $os/$arch: $(ls -lh $output | awk '{print $5}')"
        else
            echo "❌ $os/$arch: failed"
        fi
    done
}

# Función para documentación
docs() {
    echo "📚 Generando documentación..."
    
    # Iniciar servidor de documentación
    echo "🌐 Iniciando servidor de documentación en http://localhost:6060"
    godoc -http=:6060 &
    GODOC_PID=$!
    
    echo "📖 Documentación disponible en:"
    echo "   - Paquetes locales: http://localhost:6060/pkg/"
    echo "   - Tu proyecto: http://localhost:6060/pkg/$(go list -m)/"
    
    echo "Presiona Ctrl+C para detener el servidor"
    
    trap "kill $GODOC_PID" EXIT
    wait $GODOC_PID
}

# Función para tests con cobertura
test_coverage() {
    echo "🧪 Ejecutando tests con cobertura..."
    
    # Ejecutar tests con cobertura
    go test -coverprofile=coverage.out ./...
    
    if [ -f "coverage.out" ]; then
        # Mostrar cobertura por función
        echo "📊 Cobertura por función:"
        go tool cover -func=coverage.out
        
        # Generar reporte HTML
        go tool cover -html=coverage.out -o coverage.html
        echo "📋 Reporte HTML generado: coverage.html"
        
        # Abrir en navegador si está disponible
        if command -v xdg-open &> /dev/null; then
            xdg-open coverage.html
        elif command -v open &> /dev/null; then
            open coverage.html
        fi
    fi
}

# Menú interactivo
echo "🐹 Herramientas de Desarrollo Go"
echo "1. Setup inicial"
echo "2. Desarrollo con hot reload"
echo "3. Análisis completo"
echo "4. Benchmarking"
echo "5. Optimizar build"
echo "6. Documentación"
echo "7. Tests con cobertura"
echo "8. Profiling"

read -p "Selecciona una opción: " option

case $option in
    1) setup ;;
    2) dev_watch ;;
    3) analyze ;;
    4) benchmark ;;
    5) optimize ;;
    6) docs ;;
    7) test_coverage ;;
    8) 
        echo "🔬 Iniciando profiling..."
        echo "💡 Ejecuta tu aplicación y visita: http://localhost:6060/debug/pprof/"
        ;;
    *) echo "Opción inválida" ;;
esac
```

### Script de CI/CD
```bash
#!/bin/bash
# ci-go.sh - Pipeline de CI/CD para Go

set -e

echo "🚀 Iniciando pipeline de CI/CD para Go..."

# 1. Verificar formato
echo "🎨 Verificando formato del código..."
if [ "$(gofmt -l . | wc -l)" -gt 0 ]; then
    echo "❌ Código no está formateado correctamente:"
    gofmt -l .
    echo "💡 Ejecuta: go fmt ./..."
    exit 1
fi

# 2. Verificar imports
echo "📦 Verificando imports..."
if ! command -v goimports &> /dev/null; then
    go install golang.org/x/tools/cmd/goimports@latest
fi

if [ "$(goimports -l . | wc -l)" -gt 0 ]; then
    echo "❌ Imports no están organizados correctamente:"
    goimports -l .
    echo "💡 Ejecuta: goimports -w ."
    exit 1
fi

# 3. Ejecutar go vet
echo "🔍 Ejecutando go vet..."
go vet ./...

# 4. Ejecutar linters
echo "📝 Ejecutando linters..."
if command -v golangci-lint &> /dev/null; then
    golangci-lint run
else
    echo "⚠️  golangci-lint no disponible, instalando..."
    go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest
    golangci-lint run
fi

# 5. Verificar dependencias
echo "📦 Verificando dependencias..."
go mod tidy
go mod verify

# Verificar si hay cambios en go.mod o go.sum
if ! git diff --quiet go.mod go.sum; then
    echo "❌ go.mod o go.sum han cambiado"
    echo "💡 Ejecuta: go mod tidy"
    exit 1
fi

# 6. Ejecutar tests
echo "🧪 Ejecutando tests..."
go test -race -coverprofile=coverage.out ./...

# 7. Verificar cobertura
if [ -f "coverage.out" ]; then
    COVERAGE=$(go tool cover -func=coverage.out | grep total | awk '{print $3}' | sed 's/%//')
    echo "📊 Cobertura de tests: ${COVERAGE}%"
    
    # Fallar si cobertura es menor al 80%
    if (( $(echo "$COVERAGE < 80" | bc -l) )); then
        echo "❌ Cobertura de tests muy baja (${COVERAGE}% < 80%)"
        exit 1
    fi
fi

# 8. Auditoría de seguridad
echo "🔒 Ejecutando auditoría de seguridad..."
if command -v govulncheck &> /dev/null; then
    govulncheck ./...
else
    echo "📦 Instalando govulncheck..."
    go install golang.org/x/vuln/cmd/govulncheck@latest
    govulncheck ./...
fi

# 9. Build
echo "🏗️  Compilando aplicación..."
go build -v ./...

# 10. Build optimizado
echo "📦 Compilando versión optimizada..."
go build -ldflags="-s -w" -o ./bin/$(basename $PWD)

# 11. Generar artefactos
echo "📋 Generando artefactos..."
mkdir -p artifacts

# Copiar ejecutable
if [ -f "./bin/$(basename $PWD)" ]; then
    cp "./bin/$(basename $PWD)" artifacts/
fi

# Generar reporte de cobertura si existe
if [ -f "coverage.out" ]; then
    go tool cover -html=coverage.out -o artifacts/coverage.html
fi

echo "✅ Pipeline completado exitosamente!"
echo "📁 Artefactos generados en: artifacts/"
```

### Script de Deploy
```bash
#!/bin/bash
# deploy-go.sh - Script de despliegue para aplicaciones Go

APP_NAME="mi-app-go"
VERSION=${1:-$(git describe --tags --always)}
DEPLOY_USER="deploy"
DEPLOY_HOST="servidor.com"
DEPLOY_PATH="/opt/apps/$APP_NAME"

echo "🚀 Desplegando $APP_NAME versión $VERSION..."

# 1. Ejecutar tests
echo "🧪 Ejecutando tests..."
go test -race ./...

if [ $? -ne 0 ]; then
    echo "❌ Tests fallidos, cancelando deploy"
    exit 1
fi

# 2. Build optimizado
echo "🏗️  Compilando aplicación..."
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build \
    -ldflags="-s -w -X main.version=$VERSION" \
    -o $APP_NAME

if [ $? -ne 0 ]; then
    echo "❌ Error en compilación"
    exit 1
fi

# 3. Crear paquete de deploy
echo "📦 Creando paquete..."
tar -czf ${APP_NAME}-${VERSION}.tar.gz \
    $APP_NAME \
    config/ \
    migrations/ \
    static/ \
    templates/ 2>/dev/null || true

# 4. Subir al servidor
echo "📤 Subiendo al servidor..."
scp ${APP_NAME}-${VERSION}.tar.gz $DEPLOY_USER@$DEPLOY_HOST:/tmp/

# 5. Deploy en servidor
echo "🚁 Desplegando en servidor..."
ssh $DEPLOY_USER@$DEPLOY_HOST << EOF
    # Crear backup
    if [ -f "$DEPLOY_PATH/$APP_NAME" ]; then
        echo "💾 Creando backup..."
        sudo cp $DEPLOY_PATH/$APP_NAME $DEPLOY_PATH/${APP_NAME}.backup
    fi
    
    # Crear directorio si no existe
    sudo mkdir -p $DEPLOY_PATH
    
    # Extraer nueva versión
    cd /tmp
    tar -xzf ${APP_NAME}-${VERSION}.tar.gz
    
    # Mover archivos
    sudo mv $APP_NAME $DEPLOY_PATH/
    
    # Configurar permisos
    sudo chmod +x $DEPLOY_PATH/$APP_NAME
    sudo chown deploy:deploy $DEPLOY_PATH/$APP_NAME
    
    # Reiniciar servicio
    sudo systemctl restart $APP_NAME
    
    # Verificar estado
    sleep 3
    if sudo systemctl is-active --quiet $APP_NAME; then
        echo "✅ Servicio iniciado correctamente"
    else
        echo "❌ Error iniciando servicio"
        sudo journalctl -u $APP_NAME --lines=10
        exit 1
    fi
    
    # Limpiar archivos temporales
    rm /tmp/${APP_NAME}-${VERSION}.tar.gz
EOF

# 6. Verificar deploy
echo "🔍 Verificando deploy..."
sleep 5

HTTP_STATUS=$(curl -s -o /dev/null -w "%{http_code}" http://$DEPLOY_HOST:8080/health || echo "000")

if [ "$HTTP_STATUS" = "200" ]; then
    echo "✅ Deploy exitoso!"
    echo "🌐 Aplicación disponible en: http://$DEPLOY_HOST:8080"
else
    echo "❌ Error en deploy (HTTP $HTTP_STATUS)"
    
    # Revertir si hay backup
    ssh $DEPLOY_USER@$DEPLOY_HOST << EOF
        if [ -f "$DEPLOY_PATH/${APP_NAME}.backup" ]; then
            echo "🔄 Revirtiendo a versión anterior..."
            sudo mv $DEPLOY_PATH/${APP_NAME}.backup $DEPLOY_PATH/$APP_NAME
            sudo systemctl restart $APP_NAME
        fi
EOF
fi

# Limpiar archivos locales
rm -f $APP_NAME ${APP_NAME}-${VERSION}.tar.gz

echo "🎉 Deploy completado!"
```

---

## Configuraciones y Optimización

### Configuración de Performance
```bash
# Variables de entorno para optimización
export GOMAXPROCS=$(nproc)
export GOGC=100
export GOMEMLIMIT=1GiB

# Build flags para optimización
go build -ldflags="-s -w" \
         -gcflags="-m" \
         -buildmode=pie

# Para aplicaciones que usan mucha memoria
export GOGC=50

# Para aplicaciones con muchas goroutines
export GOMAXPROCS=1
```

### Configuración de Profiling en Producción
```go
// main.go - Agregar endpoints de profiling
import (
    _ "net/http/pprof"
    "net/http"
)

func main() {
    // Iniciar servidor de profiling en puerto separado
    go func() {
        log.Println("Profiling server: http://localhost:6060/debug/pprof/")
        log.Println(http.ListenAndServe("localhost:6060", nil))
    }()
    
    // Tu aplicación principal...
}
```

Esta documentación cubre los comandos más importantes de Go, desde desarrollo básico hasta optimización y despliegue en producción.
