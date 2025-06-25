# 💎 Comandos Ruby

## Herramientas de Línea de Comandos

### ruby
**Descripción:** Intérprete de Ruby para ejecutar scripts y aplicaciones
**Sintaxis básica:**
```bash
ruby [opciones] script.rb [argumentos]
```

### gem
**Descripción:** Gestor de paquetes (gemas) de Ruby
**Sintaxis básica:**
```bash
gem [comando] [opciones] [argumentos]
```

### bundler
**Descripción:** Gestor de dependencias para proyectos Ruby
**Sintaxis básica:**
```bash
bundle [comando] [opciones]
```

### rake
**Descripción:** Herramienta de automatización y construcción para Ruby
**Sintaxis básica:**
```bash
rake [tarea] [opciones]
```

### rails
**Descripción:** Framework web para Ruby
**Sintaxis básica:**
```bash
rails [comando] [opciones] [argumentos]
```

---

## Gestión de Versiones Ruby

### rbenv
```bash
# Instalar rbenv
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/HEAD/bin/rbenv-installer | bash

# Listar versiones disponibles
rbenv install --list

# Instalar versión de Ruby
rbenv install 3.2.0

# Establecer versión global
rbenv global 3.2.0

# Establecer versión local para proyecto
rbenv local 3.1.0

# Ver versión actual
rbenv version

# Listar versiones instaladas
rbenv versions

# Actualizar rbenv
rbenv update
```

### RVM (Ruby Version Manager)
```bash
# Instalar RVM
curl -sSL https://get.rvm.io | bash -s stable

# Listar versiones disponibles
rvm list known

# Instalar Ruby
rvm install 3.2.0

# Usar versión específica
rvm use 3.2.0

# Establecer versión por defecto
rvm use 3.2.0 --default

# Crear gemset
rvm gemset create mi-proyecto

# Usar gemset
rvm use 3.2.0@mi-proyecto

# Listar gemsets
rvm gemset list
```

---

## Gestión de Gemas

### Comandos Básicos de Gem
```bash
# Instalar gema
gem install nombre_gema

# Instalar versión específica
gem install rails --version 7.0.0

# Instalar sin documentación (más rápido)
gem install rails --no-document

# Listar gemas instaladas
gem list

# Buscar gemas
gem search rails

# Ver información de gema
gem info rails

# Actualizar gema
gem update rails

# Actualizar todas las gemas
gem update

# Desinstalar gema
gem uninstall rails

# Limpiar gemas antiguas
gem cleanup
```

### Bundler - Gestión de Dependencias
```bash
# Instalar bundler
gem install bundler

# Crear Gemfile
bundle init

# Instalar dependencias del Gemfile
bundle install

# Instalar solo para producción
bundle install --without development test

# Actualizar gemas
bundle update

# Actualizar gema específica
bundle update rails

# Ejecutar comando con bundle
bundle exec comando

# Ver dependencias
bundle list

# Verificar Gemfile
bundle check

# Generar Gemfile.lock
bundle lock

# Limpiar gemas no utilizadas
bundle clean
```

---

## Ruby on Rails

### Crear y Configurar Proyectos
```bash
# Instalar Rails
gem install rails

# Crear nueva aplicación Rails
rails new mi_app

# Crear con base de datos específica
rails new mi_app --database=postgresql

# Crear API solamente
rails new mi_api --api

# Crear sin tests por defecto
rails new mi_app --skip-test

# Crear con Webpack
rails new mi_app --webpack=react

# Navegar al directorio
cd mi_app

# Instalar dependencias
bundle install
```

### Generadores Rails
```bash
# Generar controlador
rails generate controller Users index show create

# Generar modelo
rails generate model User name:string email:string age:integer

# Generar scaffold completo
rails generate scaffold Product name:string price:decimal description:text

# Generar migración
rails generate migration AddEmailToUsers email:string

# Generar mailer
rails generate mailer UserMailer welcome_email

# Generar job
rails generate job ProcessPayment

# Ver todos los generadores
rails generate --help

# Deshacer generación (rollback)
rails destroy controller Users
rails destroy model User
```

### Servidor y Consola
```bash
# Iniciar servidor de desarrollo
rails server
# o
rails s

# Iniciar en puerto específico
rails server -p 4000

# Iniciar en modo producción
rails server -e production

# Consola interactiva
rails console
# o
rails c

# Consola en sandbox (rollback al salir)
rails console --sandbox

# Consola en producción
rails console -e production
```

### Base de Datos
```bash
# Crear base de datos
rails db:create

# Ejecutar migraciones
rails db:migrate

# Rollback última migración
rails db:rollback

# Rollback múltiples migraciones
rails db:rollback STEP=3

# Rehacer migración
rails db:migrate:redo

# Ver estado de migraciones
rails db:migrate:status

# Sembrar base de datos
rails db:seed

# Resetear base de datos
rails db:reset

# Recrear base de datos desde cero
rails db:drop db:create db:migrate db:seed

# Generar esquema
rails db:schema:dump
```

### Testing
```bash
# Ejecutar todos los tests
rails test

# Ejecutar tests específicos
rails test test/models/user_test.rb

# Ejecutar test específico
rails test test/models/user_test.rb:test_should_not_save_user_without_name

# Ejecutar tests del sistema
rails test:system

# Ejecutar tests de integración
rails test:integration

# Ejecutar tests de modelos
rails test:models

# Ejecutar tests de controladores
rails test:controllers
```

---

## Rake - Tareas de Automatización

### Comandos Básicos
```bash
# Listar tareas disponibles
rake --tasks
# o
rake -T

# Ejecutar tarea específica
rake db:migrate

# Ejecutar múltiples tareas
rake db:drop db:create db:migrate db:seed

# Ver información detallada de tarea
rake --describe db:migrate

# Ejecutar tarea con argumentos
rake mi_tarea[arg1,arg2]
```

### Tareas Personalizadas
```bash
# Crear archivo de tareas (lib/tasks/mi_tarea.rake)
cat > lib/tasks/mi_tarea.rake << 'EOF'
namespace :mi_app do
  desc "Importar datos desde CSV"
  task :import_csv => :environment do
    # Código de la tarea
    puts "Importando datos..."
  end
  
  desc "Limpiar archivos temporales"
  task :cleanup do
    puts "Limpiando archivos temporales..."
    system("rm -rf tmp/cache/*")
  end
end
EOF

# Ejecutar tareas personalizadas
rake mi_app:import_csv
rake mi_app:cleanup
```

---

## IRB (Interactive Ruby)

### Comandos Básicos
```bash
# Iniciar IRB
irb

# Cargar archivo en IRB
irb -r ./mi_archivo.rb

# IRB con preload
irb -I lib -r mi_gem

# Comandos dentro de IRB
help         # Ayuda
exit         # Salir
quit         # Salir
hist         # Historial de comandos
```

---

## Ejemplos de Uso Común

### Aplicación Rails Completa
```bash
# 1. Crear nueva aplicación
rails new blog --database=postgresql
cd blog

# 2. Configurar base de datos (config/database.yml)
# Editar configuración de PostgreSQL

# 3. Crear base de datos
rails db:create

# 4. Generar scaffold para posts
rails generate scaffold Post title:string content:text author:string published:boolean

# 5. Ejecutar migración
rails db:migrate

# 6. Agregar datos de prueba (db/seeds.rb)
cat >> db/seeds.rb << 'EOF'
Post.create([
  {
    title: "Mi primer post",
    content: "Este es el contenido de mi primer post.",
    author: "Autor",
    published: true
  },
  {
    title: "Segundo post",
    content: "Contenido del segundo post.",
    author: "Otro Autor",
    published: false
  }
])
EOF

# 7. Sembrar base de datos
rails db:seed

# 8. Iniciar servidor
rails server

# 9. Navegar a http://localhost:3000/posts
```

### API REST con Rails
```bash
# 1. Crear aplicación API
rails new mi_api --api --database=postgresql
cd mi_api

# 2. Agregar gemas al Gemfile
cat >> Gemfile << 'EOF'
gem 'jwt'
gem 'bcrypt'
gem 'rack-cors'
EOF

# 3. Instalar dependencias
bundle install

# 4. Generar modelo User
rails generate model User name:string email:string password_digest:string

# 5. Generar controlador API
rails generate controller Api::V1::Users --skip-routes

# 6. Configurar rutas (config/routes.rb)
cat > config/routes.rb << 'EOF'
Rails.application.routes.draw do
  namespace :api do
    namespace :v1 do
      resources :users, only: [:index, :show, :create, :update, :destroy]
      post '/login', to: 'auth#login'
    end
  end
end
EOF

# 7. Ejecutar migraciones
rails db:migrate

# 8. Iniciar servidor
rails server -p 3001
```

### Script Ruby Standalone
```bash
# 1. Crear script
cat > mi_script.rb << 'EOF'
#!/usr/bin/env ruby

require 'optparse'
require 'json'
require 'net/http'

options = {}
OptionParser.new do |opts|
  opts.banner = "Uso: #{$0} [opciones]"
  
  opts.on("-u", "--url URL", "URL a consultar") do |url|
    options[:url] = url
  end
  
  opts.on("-o", "--output FILE", "Archivo de salida") do |file|
    options[:output] = file
  end
  
  opts.on("-h", "--help", "Mostrar ayuda") do
    puts opts
    exit
  end
end.parse!

if options[:url]
  uri = URI(options[:url])
  response = Net::HTTP.get_response(uri)
  
  result = {
    status: response.code,
    headers: response.to_hash,
    body: response.body
  }
  
  if options[:output]
    File.write(options[:output], JSON.pretty_generate(result))
    puts "Resultado guardado en #{options[:output]}"
  else
    puts JSON.pretty_generate(result)
  end
else
  puts "Error: URL requerida"
  exit 1
end
EOF

# 2. Hacer ejecutable
chmod +x mi_script.rb

# 3. Ejecutar
ruby mi_script.rb --url https://api.github.com/users/octocat --output resultado.json
```

---

## Scripts de Utilidad

### Script de Setup de Proyecto Rails
```bash
#!/bin/bash
# setup_rails.sh - Script de configuración para proyectos Rails

PROJECT_NAME=$1

if [ -z "$PROJECT_NAME" ]; then
    echo "❌ Uso: $0 <nombre_proyecto>"
    exit 1
fi

echo "🚀 Creando proyecto Rails: $PROJECT_NAME"

# 1. Crear aplicación Rails
rails new $PROJECT_NAME --database=postgresql --skip-test
cd $PROJECT_NAME

# 2. Agregar gemas comunes al Gemfile
cat >> Gemfile << 'EOF'

# Autenticación
gem 'devise'

# Autorización
gem 'cancancan'

# API
gem 'jbuilder'

# Environment variables
gem 'dotenv-rails'

# Testing
group :development, :test do
  gem 'rspec-rails'
  gem 'factory_bot_rails'
  gem 'faker'
end

# Development
group :development do
  gem 'annotate'
  gem 'better_errors'
  gem 'binding_of_caller'
end
EOF

# 3. Instalar dependencias
echo "📦 Instalando dependencias..."
bundle install

# 4. Configurar base de datos
echo "🗄️  Configurando base de datos..."
rails db:create

# 5. Instalar Devise
echo "🔐 Configurando autenticación..."
rails generate devise:install
rails generate devise User

# 6. Configurar RSpec
echo "🧪 Configurando tests..."
rails generate rspec:install

# 7. Ejecutar migraciones
rails db:migrate

# 8. Crear archivo .env
cat > .env.example << 'EOF'
DATABASE_URL=postgresql://usuario:password@localhost/database_name
SECRET_KEY_BASE=tu_clave_secreta_aqui
EOF

cp .env.example .env

# 9. Configurar Git
git init
git add .
git commit -m "Initial commit"

echo "✅ Proyecto $PROJECT_NAME configurado exitosamente!"
echo "🌐 Para iniciar: cd $PROJECT_NAME && rails server"
```

### Script de Deploy
```bash
#!/bin/bash
# deploy.sh - Script de despliegue para aplicaciones Rails

APP_NAME="mi-rails-app"
DEPLOY_USER="deploy"
DEPLOY_HOST="servidor.com"
DEPLOY_PATH="/var/www/$APP_NAME"

echo "🚀 Desplegando $APP_NAME..."

# 1. Ejecutar tests localmente
echo "🧪 Ejecutando tests..."
bundle exec rspec

if [ $? -ne 0 ]; then
    echo "❌ Tests fallidos, cancelando deploy"
    exit 1
fi

# 2. Precompilar assets
echo "🎨 Precompilando assets..."
RAILS_ENV=production bundle exec rails assets:precompile

# 3. Crear paquete de deploy
echo "📦 Creando paquete..."
tar -czf deploy.tar.gz \
    --exclude='.git' \
    --exclude='node_modules' \
    --exclude='tmp' \
    --exclude='log' \
    --exclude='*.log' \
    .

# 4. Subir y desplegar en servidor
echo "📤 Subiendo al servidor..."
scp deploy.tar.gz $DEPLOY_USER@$DEPLOY_HOST:/tmp/

echo "🔧 Desplegando en servidor..."
ssh $DEPLOY_USER@$DEPLOY_HOST << EOF
    cd $DEPLOY_PATH
    
    # Backup de versión actual
    if [ -d "current" ]; then
        cp -r current backup-\$(date +%Y%m%d-%H%M%S)
    fi
    
    # Extraer nueva versión
    rm -rf new_release
    mkdir new_release
    cd new_release
    tar -xzf /tmp/deploy.tar.gz
    
    # Instalar dependencias
    bundle install --deployment --without development test
    
    # Ejecutar migraciones
    RAILS_ENV=production bundle exec rails db:migrate
    
    # Cambiar a nueva versión
    cd ..
    rm -rf current
    mv new_release current
    
    # Reiniciar servicios
    sudo systemctl restart $APP_NAME
    sudo systemctl reload nginx
    
    # Limpiar archivos temporales
    rm /tmp/deploy.tar.gz
EOF

# 5. Verificar deploy
echo "🔍 Verificando deploy..."
HTTP_STATUS=$(curl -s -o /dev/null -w "%{http_code}" https://$DEPLOY_HOST)

if [ $HTTP_STATUS -eq 200 ]; then
    echo "✅ Deploy exitoso!"
    echo "🌐 Aplicación disponible en: https://$DEPLOY_HOST"
else
    echo "❌ Error en deploy (HTTP $HTTP_STATUS)"
fi

# Limpiar archivos locales
rm -f deploy.tar.gz
rm -rf public/assets
```

### Script de Desarrollo
```bash
#!/bin/bash
# dev.sh - Script para entorno de desarrollo Rails

# Función para setup inicial
setup() {
    echo "🔧 Configurando entorno de desarrollo..."
    
    # Verificar Ruby
    if ! command -v ruby &> /dev/null; then
        echo "❌ Ruby no está instalado"
        exit 1
    fi
    
    # Verificar Bundler
    if ! command -v bundle &> /dev/null; then
        gem install bundler
    fi
    
    # Instalar dependencias
    bundle install
    
    # Configurar base de datos
    rails db:create db:migrate db:seed
    
    echo "✅ Setup completo"
}

# Función para desarrollo con recarga automática
dev_server() {
    echo "🚀 Iniciando servidor de desarrollo..."
    
    # Iniciar servicios en paralelo
    rails server &
    SERVER_PID=$!
    
    # Monitorear cambios en archivos
    echo "👀 Monitoreando cambios..."
    
    trap "kill $SERVER_PID" EXIT
    
    while inotifywait -r -e modify app/ config/ lib/; do
        echo "🔄 Archivos modificados, reiniciando servidor..."
        kill $SERVER_PID
        rails server &
        SERVER_PID=$!
    done
}

# Función para ejecutar tests con watch
test_watch() {
    echo "🧪 Ejecutando tests con monitoreo..."
    
    # Test inicial
    bundle exec rspec
    
    # Monitorear cambios
    while inotifywait -r -e modify app/ spec/; do
        echo "🔄 Ejecutando tests..."
        bundle exec rspec --fail-fast
    done
}

# Función para linting y formateo
lint() {
    echo "🎨 Ejecutando linters..."
    
    # RuboCop
    if command -v rubocop &> /dev/null; then
        rubocop -A
    else
        echo "Installing RuboCop..."
        gem install rubocop
        rubocop -A
    fi
    
    # Brakeman (security)
    if command -v brakeman &> /dev/null; then
        brakeman
    else
        echo "Installing Brakeman..."
        gem install brakeman
        brakeman
    fi
}

# Menú interactivo
echo "🛠️  Herramientas de Desarrollo Rails"
echo "1. Setup inicial"
echo "2. Servidor de desarrollo"
echo "3. Tests con monitoreo"
echo "4. Linting y formateo"
echo "5. Consola Rails"
echo "6. Generar documentación"

read -p "Selecciona una opción: " option

case $option in
    1) setup ;;
    2) dev_server ;;
    3) test_watch ;;
    4) lint ;;
    5) rails console ;;
    6) 
        echo "📚 Generando documentación..."
        yard doc
        echo "Documentación disponible en doc/"
        ;;
    *) echo "Opción inválida" ;;
esac
```

---

## Configuraciones y Optimización

### Configuración para Producción
```bash
# Variables de entorno
export RAILS_ENV=production
export RACK_ENV=production
export SECRET_KEY_BASE="clave_secreta_larga_y_segura"

# Precompilación de assets
RAILS_ENV=production rails assets:precompile

# Configuración de servidor (Puma)
# config/puma.rb
workers ENV.fetch("WEB_CONCURRENCY") { 2 }
threads_count = ENV.fetch("RAILS_MAX_THREADS") { 5 }
threads threads_count, threads_count

port ENV.fetch("PORT") { 3000 }
environment ENV.fetch("RAILS_ENV") { "development" }

# Habilitar clustering en producción
if ENV.fetch("RAILS_ENV") == "production"
  preload_app!
end
```

### Performance y Monitoreo
```bash
# Instalar herramientas de profiling
gem install ruby-prof
gem install memory_profiler
gem install stackprof

# Benchmark de código Ruby
ruby -rbenchmark -e "
  include Benchmark
  bm do |x|
    x.report('Method 1:') { 1000.times { 'hello world'.upcase } }
    x.report('Method 2:') { 1000.times { 'HELLO WORLD'.downcase.upcase } }
  end
"

# Análisis de memoria
ruby -rmemory_profiler -e "
  MemoryProfiler.report do
    1000.times { 'hello world'.upcase }
  end.pretty_print
"
```

Esta documentación cubre los comandos más importantes de Ruby y Rails, desde desarrollo básico hasta despliegue en producción.
