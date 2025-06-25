# 🦀 Comandos Rust

## Herramientas de Línea de Comandos

### rustc
**Descripción:** Compilador de Rust
**Sintaxis básica:**
```bash
rustc [opciones] archivo.rs
```

### cargo
**Descripción:** Gestor de paquetes y herramienta de construcción de Rust
**Sintaxis básica:**
```bash
cargo [comando] [opciones] [argumentos]
```

### rustup
**Descripción:** Instalador y gestor de versiones de Rust
**Sintaxis básica:**
```bash
rustup [comando] [opciones]
```

### rustfmt
**Descripción:** Formateador de código Rust
**Sintaxis básica:**
```bash
rustfmt [opciones] archivo.rs
```

### clippy
**Descripción:** Linter de Rust para mejores prácticas
**Sintaxis básica:**
```bash
cargo clippy [opciones]
```

---

## Instalación y Configuración

### Instalar Rust
```bash
# Instalar Rust via rustup
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Recargar PATH
source ~/.cargo/env

# Verificar instalación
rustc --version
cargo --version
rustup --version

# Actualizar Rust
rustup update

# Desinstalar Rust
rustup self uninstall
```

### Gestión de Toolchains
```bash
# Listar toolchains instalados
rustup toolchain list

# Instalar toolchain específico
rustup toolchain install stable
rustup toolchain install beta
rustup toolchain install nightly

# Establecer toolchain por defecto
rustup default stable

# Usar toolchain específico
rustup run nightly cargo build

# Instalar componentes
rustup component add rustfmt
rustup component add clippy
rustup component add rust-src
rustup component add rust-analyzer

# Instalar targets
rustup target add wasm32-unknown-unknown
rustup target add x86_64-pc-windows-gnu
```

---

## Cargo - Gestión de Proyectos

### Crear y Configurar Proyectos
```bash
# Crear nuevo proyecto binario
cargo new mi_proyecto

# Crear nuevo proyecto de biblioteca
cargo new mi_lib --lib

# Crear proyecto en directorio actual
cargo init

# Crear con VCS específico
cargo new mi_proyecto --vcs git

# Crear sin inicializar VCS
cargo new mi_proyecto --vcs none
```

### Compilación y Ejecución
```bash
# Compilar proyecto
cargo build

# Compilar optimizado para producción
cargo build --release

# Compilar y ejecutar
cargo run

# Ejecutar con argumentos
cargo run -- arg1 arg2

# Ejecutar ejemplo específico
cargo run --example ejemplo_nombre

# Compilar solo verificación
cargo check

# Compilar para target específico
cargo build --target x86_64-pc-windows-gnu
```

### Testing
```bash
# Ejecutar tests
cargo test

# Ejecutar tests con output
cargo test -- --nocapture

# Ejecutar test específico
cargo test test_function_name

# Ejecutar tests de integración
cargo test --test integration_test

# Ejecutar tests de documentación
cargo test --doc

# Ejecutar tests con un solo hilo
cargo test -- --test-threads=1

# Ejecutar tests ignorados
cargo test -- --ignored
```

### Gestión de Dependencias
```bash
# Agregar dependencia
cargo add serde

# Agregar dependencia con features
cargo add serde --features derive

# Agregar dependencia de desarrollo
cargo add --dev criterion

# Agregar dependencia de build
cargo add --build cc

# Actualizar dependencias
cargo update

# Actualizar dependencia específica
cargo update serde

# Ver árbol de dependencias
cargo tree

# Verificar dependencias no utilizadas
cargo machete
```

---

## Herramientas de Desarrollo

### Formateo y Linting
```bash
# Formatear código
cargo fmt

# Verificar formato sin modificar
cargo fmt -- --check

# Ejecutar clippy (linter)
cargo clippy

# Clippy para todos los targets
cargo clippy --all-targets

# Clippy con warnings como errores
cargo clippy -- -D warnings

# Clippy con sugerencias
cargo clippy -- -W clippy::all
```

### Documentación
```bash
# Generar documentación
cargo doc

# Generar y abrir documentación
cargo doc --open

# Incluir dependencias privadas
cargo doc --document-private-items

# Generar documentación sin dependencias
cargo doc --no-deps

# Verificar enlaces en documentación
cargo doc --check
```

### Benchmarking y Profiling
```bash
# Ejecutar benchmarks
cargo bench

# Instalar herramientas de profiling
cargo install flamegraph

# Generar flamegraph
cargo flamegraph --bin mi_programa

# Instalar herramientas de análisis
cargo install cargo-audit
cargo install cargo-outdated
cargo install cargo-udeps

# Auditoría de seguridad
cargo audit

# Verificar dependencias desactualizadas
cargo outdated

# Encontrar dependencias no utilizadas
cargo udeps
```

---

## Publicación y Distribución

### Cargo Registry
```bash
# Login en crates.io
cargo login

# Publicar crate
cargo publish

# Publicar dry-run
cargo publish --dry-run

# Verificar antes de publicar
cargo package

# Ver contenido del paquete
cargo package --list

# Instalar desde crates.io
cargo install mi_crate

# Instalar desde Git
cargo install --git https://github.com/user/repo

# Instalar versión específica
cargo install mi_crate --version 1.0.0

# Desinstalar
cargo uninstall mi_crate
```

---

## Compilación Cruzada

### Targets Múltiples
```bash
# Listar targets disponibles
rustup target list

# Instalar target
rustup target add x86_64-unknown-linux-musl

# Compilar para target específico
cargo build --target x86_64-unknown-linux-musl

# Compilar para WebAssembly
rustup target add wasm32-unknown-unknown
cargo build --target wasm32-unknown-unknown

# Compilar para Windows desde Linux
rustup target add x86_64-pc-windows-gnu
cargo build --target x86_64-pc-windows-gnu

# Compilar para macOS desde Linux
rustup target add x86_64-apple-darwin
cargo build --target x86_64-apple-darwin
```

---

## Ejemplos de Uso Común

### Aplicación CLI Simple
```bash
# 1. Crear proyecto
cargo new mi_cli
cd mi_cli

# 2. Agregar dependencias para CLI
cargo add clap --features derive
cargo add serde --features derive
cargo add serde_json

# 3. Crear código fuente (src/main.rs)
cat > src/main.rs << 'EOF'
use clap::{Parser, Subcommand};
use serde::{Deserialize, Serialize};
use std::fs;

#[derive(Parser)]
#[command(name = "mi_cli")]
#[command(about = "Una CLI de ejemplo en Rust")]
struct Cli {
    #[command(subcommand)]
    command: Commands,
}

#[derive(Subcommand)]
enum Commands {
    /// Crear un nuevo archivo
    Create {
        /// Nombre del archivo
        name: String,
        /// Contenido del archivo
        #[arg(short, long)]
        content: Option<String>,
    },
    /// Listar archivos
    List,
}

#[derive(Serialize, Deserialize)]
struct Config {
    name: String,
    version: String,
}

fn main() {
    let cli = Cli::parse();

    match &cli.command {
        Commands::Create { name, content } => {
            let content = content.as_deref().unwrap_or("Contenido por defecto");
            fs::write(name, content).expect("Error escribiendo archivo");
            println!("Archivo '{}' creado exitosamente", name);
        }
        Commands::List => {
            let entries = fs::read_dir(".")
                .expect("Error leyendo directorio")
                .map(|res| res.map(|e| e.path().display().to_string()))
                .collect::<Result<Vec<_>, _>>()
                .expect("Error procesando entradas");
            
            for entry in entries {
                println!("{}", entry);
            }
        }
    }
}
EOF

# 4. Compilar y ejecutar
cargo build --release
./target/release/mi_cli create --name test.txt --content "Hola Rust"
./target/release/mi_cli list
```

### Servidor Web con Actix
```bash
# 1. Crear proyecto
cargo new mi_servidor
cd mi_servidor

# 2. Agregar dependencias
cargo add actix-web
cargo add serde --features derive
cargo add tokio --features full

# 3. Crear servidor (src/main.rs)
cat > src/main.rs << 'EOF'
use actix_web::{web, App, HttpResponse, HttpServer, Result, middleware::Logger};
use serde::{Deserialize, Serialize};

#[derive(Serialize, Deserialize)]
struct User {
    id: u32,
    name: String,
    email: String,
}

async fn get_users() -> Result<HttpResponse> {
    let users = vec![
        User {
            id: 1,
            name: "Juan".to_string(),
            email: "juan@example.com".to_string(),
        },
        User {
            id: 2,
            name: "María".to_string(),
            email: "maria@example.com".to_string(),
        },
    ];
    
    Ok(HttpResponse::Ok().json(users))
}

async fn create_user(user: web::Json<User>) -> Result<HttpResponse> {
    println!("Creando usuario: {}", user.name);
    Ok(HttpResponse::Created().json(&*user))
}

async fn health() -> Result<HttpResponse> {
    Ok(HttpResponse::Ok().json(serde_json::json!({
        "status": "ok",
        "timestamp": chrono::Utc::now().to_rfc3339()
    })))
}

#[actix_web::main]
async fn main() -> std::io::Result<()> {
    env_logger::init();
    
    println!("🚀 Iniciando servidor en http://localhost:8080");
    
    HttpServer::new(|| {
        App::new()
            .wrap(Logger::default())
            .route("/health", web::get().to(health))
            .route("/users", web::get().to(get_users))
            .route("/users", web::post().to(create_user))
    })
    .bind("127.0.0.1:8080")?
    .run()
    .await
}
EOF

# 4. Agregar dependencias adicionales
cargo add chrono --features serde
cargo add env_logger

# 5. Ejecutar servidor
cargo run
```

### Biblioteca Reutilizable
```bash
# 1. Crear biblioteca
cargo new mi_lib --lib
cd mi_lib

# 2. Implementar funcionalidad (src/lib.rs)
cat > src/lib.rs << 'EOF'
//! # Mi Biblioteca de Utilidades
//! 
//! Esta biblioteca proporciona utilidades comunes para desarrollo en Rust.

use std::collections::HashMap;

/// Estructura para manejar configuraciones
#[derive(Debug, Clone)]
pub struct Config {
    settings: HashMap<String, String>,
}

impl Config {
    /// Crear nueva configuración
    pub fn new() -> Self {
        Self {
            settings: HashMap::new(),
        }
    }
    
    /// Establecer valor de configuración
    pub fn set(&mut self, key: &str, value: &str) {
        self.settings.insert(key.to_string(), value.to_string());
    }
    
    /// Obtener valor de configuración
    pub fn get(&self, key: &str) -> Option<&String> {
        self.settings.get(key)
    }
    
    /// Obtener valor con default
    pub fn get_or_default(&self, key: &str, default: &str) -> String {
        self.settings.get(key).unwrap_or(&default.to_string()).clone()
    }
}

impl Default for Config {
    fn default() -> Self {
        Self::new()
    }
}

/// Función utilitaria para formatear texto
pub fn format_title(text: &str) -> String {
    format!("=== {} ===", text.to_uppercase())
}

/// Función para validar email
pub fn is_valid_email(email: &str) -> bool {
    email.contains('@') && email.contains('.')
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_config() {
        let mut config = Config::new();
        config.set("app_name", "Mi App");
        
        assert_eq!(config.get("app_name"), Some(&"Mi App".to_string()));
        assert_eq!(config.get("inexistente"), None);
        assert_eq!(config.get_or_default("inexistente", "default"), "default");
    }

    #[test]
    fn test_format_title() {
        assert_eq!(format_title("hello world"), "=== HELLO WORLD ===");
    }

    #[test]
    fn test_email_validation() {
        assert!(is_valid_email("test@example.com"));
        assert!(!is_valid_email("invalid-email"));
    }
}
EOF

# 3. Ejecutar tests
cargo test

# 4. Generar documentación
cargo doc --open

# 5. Preparar para publicación
cargo package
```

---

## Scripts de Utilidad

### Script de Desarrollo Rust
```bash
#!/bin/bash
# rust-dev.sh - Herramientas de desarrollo Rust

# Función para setup inicial
setup() {
    echo "🦀 Configurando entorno de desarrollo Rust..."
    
    # Verificar instalación de Rust
    if ! command -v rustc &> /dev/null; then
        echo "📦 Instalando Rust..."
        curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
        source ~/.cargo/env
    fi
    
    # Instalar componentes útiles
    echo "🔧 Instalando componentes..."
    rustup component add rustfmt
    rustup component add clippy
    rustup component add rust-src
    rustup component add rust-analyzer
    
    # Instalar herramientas útiles
    echo "⚙️  Instalando herramientas..."
    cargo install cargo-audit
    cargo install cargo-outdated
    cargo install cargo-udeps
    cargo install cargo-expand
    cargo install cargo-watch
    
    echo "✅ Setup completo"
}

# Función para desarrollo con auto-reload
dev_watch() {
    echo "👀 Iniciando desarrollo con auto-reload..."
    
    if ! command -v cargo-watch &> /dev/null; then
        echo "📦 Instalando cargo-watch..."
        cargo install cargo-watch
    fi
    
    # Ejecutar con watch
    cargo watch -x check -x test -x run
}

# Función para análisis completo
analyze() {
    echo "🔍 Ejecutando análisis completo..."
    
    # Verificar formato
    echo "🎨 Verificando formato..."
    cargo fmt -- --check
    
    # Ejecutar clippy
    echo "📎 Ejecutando clippy..."
    cargo clippy --all-targets -- -D warnings
    
    # Ejecutar tests
    echo "🧪 Ejecutando tests..."
    cargo test
    
    # Auditoría de seguridad
    echo "🔒 Auditoría de seguridad..."
    cargo audit
    
    # Verificar dependencias desactualizadas
    echo "📊 Verificando dependencias..."
    cargo outdated
    
    # Verificar dependencias no utilizadas
    echo "🗑️  Verificando dependencias no utilizadas..."
    cargo udeps
}

# Función para optimización
optimize() {
    echo "🚀 Optimizando build..."
    
    # Build optimizado
    cargo build --release
    
    # Verificar tamaño del binario
    if [ -f "target/release/$(basename $PWD)" ]; then
        echo "📏 Tamaño del binario:"
        ls -lh target/release/$(basename $PWD)
    fi
    
    # Sugerir optimizaciones adicionales
    echo "💡 Para optimizar más, considera agregar a Cargo.toml:"
    echo "[profile.release]"
    echo "lto = true"
    echo "codegen-units = 1"
    echo "panic = 'abort'"
}

# Función para cross-compilation
cross_compile() {
    echo "🔄 Compilación cruzada..."
    
    # Targets comunes
    TARGETS=(
        "x86_64-unknown-linux-musl"
        "x86_64-pc-windows-gnu"
        "x86_64-apple-darwin"
        "wasm32-unknown-unknown"
    )
    
    for target in "${TARGETS[@]}"; do
        echo "🎯 Compilando para $target..."
        rustup target add $target
        cargo build --release --target $target
        
        if [ $? -eq 0 ]; then
            echo "✅ $target: exitoso"
        else
            echo "❌ $target: falló"
        fi
    done
}

# Función para documentación
docs() {
    echo "📚 Generando documentación..."
    
    # Generar documentación
    cargo doc --document-private-items --open
    
    # Verificar enlaces
    cargo doc --check
    
    echo "✅ Documentación generada"
}

# Menú interactivo
echo "🦀 Herramientas de Desarrollo Rust"
echo "1. Setup inicial"
echo "2. Desarrollo con auto-reload"
echo "3. Análisis completo"
echo "4. Optimizar build"
echo "5. Compilación cruzada"
echo "6. Generar documentación"
echo "7. Benchmark"

read -p "Selecciona una opción: " option

case $option in
    1) setup ;;
    2) dev_watch ;;
    3) analyze ;;
    4) optimize ;;
    5) cross_compile ;;
    6) docs ;;
    7) 
        if [ -d "benches" ]; then
            cargo bench
        else
            echo "❌ No se encontraron benchmarks"
            echo "💡 Crea archivos en el directorio 'benches/'"
        fi
        ;;
    *) echo "Opción inválida" ;;
esac
```

### Script de CI/CD
```bash
#!/bin/bash
# ci-rust.sh - Script de CI/CD para proyectos Rust

set -e

echo "🚀 Iniciando pipeline de CI/CD para Rust..."

# 1. Verificar formato
echo "🎨 Verificando formato del código..."
cargo fmt -- --check

if [ $? -ne 0 ]; then
    echo "❌ Código no está formateado correctamente"
    echo "💡 Ejecuta: cargo fmt"
    exit 1
fi

# 2. Ejecutar clippy
echo "📎 Ejecutando clippy..."
cargo clippy --all-targets --all-features -- -D warnings

if [ $? -ne 0 ]; then
    echo "❌ Clippy encontró problemas"
    exit 1
fi

# 3. Ejecutar tests
echo "🧪 Ejecutando tests..."
cargo test --all-features

if [ $? -ne 0 ]; then
    echo "❌ Tests fallidos"
    exit 1
fi

# 4. Verificar documentación
echo "📚 Verificando documentación..."
cargo doc --all-features --no-deps

if [ $? -ne 0 ]; then
    echo "❌ Error generando documentación"
    exit 1
fi

# 5. Auditoría de seguridad
echo "🔒 Ejecutando auditoría de seguridad..."
cargo audit

if [ $? -ne 0 ]; then
    echo "⚠️  Problemas de seguridad encontrados"
    # No fallar por problemas de seguridad en CI, solo advertir
fi

# 6. Build optimizado
echo "🏗️  Compilando versión optimizada..."
cargo build --release --all-features

if [ $? -ne 0 ]; then
    echo "❌ Error en build de release"
    exit 1
fi

# 7. Generar artefactos
echo "📦 Generando artefactos..."
mkdir -p artifacts

# Copiar binarios
if [ -f "target/release/$(basename $PWD)" ]; then
    cp "target/release/$(basename $PWD)" artifacts/
fi

# Generar documentación
cargo doc --all-features --no-deps
cp -r target/doc artifacts/

# 8. Verificar tamaño del binario
if [ -f "target/release/$(basename $PWD)" ]; then
    BINARY_SIZE=$(stat -c%s "target/release/$(basename $PWD)")
    echo "📏 Tamaño del binario: $BINARY_SIZE bytes"
    
    # Advertir si el binario es muy grande (> 50MB)
    if [ $BINARY_SIZE -gt 52428800 ]; then
        echo "⚠️  Binario es muy grande (>50MB)"
    fi
fi

echo "✅ Pipeline completado exitosamente!"
```

### Script de Release
```bash
#!/bin/bash
# release-rust.sh - Script de release para proyectos Rust

VERSION=$1

if [ -z "$VERSION" ]; then
    echo "❌ Uso: $0 <version>"
    echo "   Ejemplo: $0 1.0.0"
    exit 1
fi

echo "🚀 Iniciando release v$VERSION..."

# 1. Verificar que no hay cambios pendientes
if ! git diff --quiet; then
    echo "❌ Hay cambios no confirmados"
    exit 1
fi

# 2. Ejecutar tests completos
echo "🧪 Ejecutando tests completos..."
cargo test --all-features

if [ $? -ne 0 ]; then
    echo "❌ Tests fallidos"
    exit 1
fi

# 3. Actualizar versión en Cargo.toml
echo "📝 Actualizando versión en Cargo.toml..."
sed -i "s/^version = .*/version = \"$VERSION\"/" Cargo.toml

# 4. Generar changelog
echo "📋 Generando changelog..."
if command -v git-cliff &> /dev/null; then
    git-cliff --tag v$VERSION > CHANGELOG.md
else
    echo "💡 Instala git-cliff para generar changelog automático"
fi

# 5. Crear commit de version
echo "📝 Creando commit de version..."
git add Cargo.toml CHANGELOG.md
git commit -m "chore: bump version to v$VERSION"

# 6. Crear tag
echo "🏷️  Creando tag..."
git tag -a "v$VERSION" -m "Release v$VERSION"

# 7. Build optimizado
echo "🏗️  Compilando versión de release..."
cargo build --release

# 8. Crear artefactos de release
echo "📦 Creando artefactos..."
mkdir -p release/v$VERSION

# Copiar binario
if [ -f "target/release/$(basename $PWD)" ]; then
    cp "target/release/$(basename $PWD)" "release/v$VERSION/"
fi

# Crear archivos comprimidos
tar -czf "release/v$VERSION/$(basename $PWD)-v$VERSION-linux-x86_64.tar.gz" \
    -C target/release $(basename $PWD)

# 9. Verificar que todo está listo para publicar
echo "🔍 Verificando release..."
cargo package --list

# 10. Preguntar si publicar
read -p "¿Publicar en crates.io? (y/N): " -n 1 -r
echo
if [[ $REPLY =~ ^[Yy]$ ]]; then
    echo "📤 Publicando en crates.io..."
    cargo publish
    
    echo "📤 Subiendo a GitHub..."
    git push origin main
    git push origin v$VERSION
    
    echo "✅ Release v$VERSION publicado exitosamente!"
else
    echo "📋 Release preparado localmente"
    echo "   Para publicar manualmente:"
    echo "   cargo publish"
    echo "   git push origin main"
    echo "   git push origin v$VERSION"
fi

echo "🎉 Release completado!"
```

---

## Configuraciones y Optimización

### Configuración de Cargo.toml Optimizada
```toml
[package]
name = "mi_app"
version = "0.1.0"
edition = "2021"
authors = ["Tu Nombre <tu@email.com>"]
description = "Descripción de la aplicación"
license = "MIT OR Apache-2.0"
repository = "https://github.com/usuario/mi_app"
homepage = "https://github.com/usuario/mi_app"
documentation = "https://docs.rs/mi_app"
readme = "README.md"
keywords = ["cli", "rust", "example"]
categories = ["command-line-utilities"]

[dependencies]
clap = { version = "4.0", features = ["derive"] }
serde = { version = "1.0", features = ["derive"] }
tokio = { version = "1.0", features = ["full"] }

[dev-dependencies]
criterion = "0.5"

[[bench]]
name = "mi_benchmark"
harness = false

[profile.release]
lto = true
codegen-units = 1
panic = "abort"
strip = true

[profile.dev]
debug = true
overflow-checks = true

[profile.test]
overflow-checks = true
```

### Configuración de Performance
```bash
# Variables de entorno para optimización
export RUSTFLAGS="-C target-cpu=native"
export CARGO_BUILD_JOBS=$(nproc)

# Configuración de linker más rápido
# En ~/.cargo/config.toml
[target.x86_64-unknown-linux-gnu]
linker = "clang"
rustflags = ["-C", "link-arg=-fuse-ld=lld"]

# Configuración para builds más rápidos
[build]
rustc-wrapper = "sccache"  # Requiere: cargo install sccache
```

Esta documentación cubre los comandos más importantes de Rust, desde instalación hasta optimización y publicación de proyectos.
