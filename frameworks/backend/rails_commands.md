# Ruby on Rails Commands

Ruby on Rails es un framework de desarrollo web escrito en Ruby que sigue el paradigma MVC (Model-View-Controller) y enfatiza la convención sobre la configuración.

## Instalación

### Instalar Ruby y Rails
```bash
# Instalar Ruby (con rbenv)
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/HEAD/bin/rbenv-installer | bash
rbenv install 3.2.0
rbenv global 3.2.0

# Instalar Rails
gem install rails
```

### Verificar instalación
```bash
ruby --version
rails --version
```

### Instalar versión específica de Rails
```bash
gem install rails -v 7.0.0
```

## Creación de Proyectos

### Crear nueva aplicación Rails
```bash
rails new myapp
```

### Crear aplicación con base de datos específica
```bash
rails new myapp --database=postgresql
rails new myapp --database=mysql
rails new myapp --database=sqlite3
```

### Crear aplicación API solamente
```bash
rails new myapp --api
```

### Crear aplicación sin test framework
```bash
rails new myapp --skip-test
```

### Crear aplicación con opciones específicas
```bash
rails new myapp --database=postgresql --css=bootstrap --javascript=esbuild
```

## Comandos de Desarrollo

### Ejecutar servidor de desarrollo
```bash
rails server
# o
rails s
```

### Ejecutar en puerto específico
```bash
rails server -p 4000
```

### Ejecutar en ambiente específico
```bash
rails server -e production
```

### Ejecutar servidor con binding específico
```bash
rails server -b 0.0.0.0
```

### Consola interactiva de Rails
```bash
rails console
# o
rails c
```

### Consola en ambiente específico
```bash
rails console production
```

## Generadores de Rails

### Generar modelo
```bash
rails generate model User name:string email:string
# o
rails g model User name:string email:string
```

### Generar controlador
```bash
rails generate controller Users index show create
```

### Generar scaffold completo
```bash
rails generate scaffold Post title:string content:text author:string
```

### Generar migración
```bash
rails generate migration AddAgeToUsers age:integer
```

### Generar vista
```bash
rails generate view Users index show
```

### Generar mailer
```bash
rails generate mailer UserMailer welcome_email
```

### Generar job
```bash
rails generate job EmailJob
```

### Generar initializer
```bash
rails generate initializer cors
```

## Comandos de Base de Datos

### Crear base de datos
```bash
rails db:create
```

### Ejecutar migraciones
```bash
rails db:migrate
```

### Revertir última migración
```bash
rails db:rollback
```

### Revertir múltiples migraciones
```bash
rails db:rollback STEP=3
```

### Migrar a versión específica
```bash
rails db:migrate VERSION=20230101000000
```

### Ver estado de migraciones
```bash
rails db:migrate:status
```

### Recrear base de datos
```bash
rails db:drop db:create db:migrate
```

### Poblar base de datos con seeds
```bash
rails db:seed
```

### Reset completo de base de datos
```bash
rails db:reset
```

### Setup inicial de base de datos
```bash
rails db:setup
```

## Comandos de Testing

### Ejecutar todos los tests
```bash
rails test
```

### Ejecutar tests específicos
```bash
rails test test/models/user_test.rb
```

### Ejecutar test específico por línea
```bash
rails test test/models/user_test.rb:10
```

### Ejecutar tests del sistema
```bash
rails test:system
```

### Ejecutar tests con coverage
```bash
# Agregar gem 'simplecov' al Gemfile
rails test
```

### Ejecutar tests con RSpec (si está instalado)
```bash
bundle exec rspec
```

## Comandos de Rutas

### Ver todas las rutas
```bash
rails routes
```

### Buscar rutas específicas
```bash
rails routes | grep users
```

### Ver rutas de un controlador específico
```bash
rails routes -c users
```

### Ver rutas con formato expandido
```bash
rails routes --expanded
```

## Comandos de Assets

### Precompilar assets
```bash
rails assets:precompile
```

### Limpiar assets
```bash
rails assets:clean
```

### Limpiar todos los assets
```bash
rails assets:clobber
```

## Comandos de Bundler

### Instalar gems
```bash
bundle install
```

### Actualizar gems
```bash
bundle update
```

### Instalar gems sin grupos específicos
```bash
bundle install --without production
```

### Verificar dependencias
```bash
bundle check
```

### Mostrar gems instaladas
```bash
bundle list
```

### Ejecutar comando con bundle
```bash
bundle exec rails server
```

## Comandos de Deployment

### Precompilar para producción
```bash
RAILS_ENV=production rails assets:precompile
```

### Migrar en producción
```bash
RAILS_ENV=production rails db:migrate
```

### Crear secret key
```bash
rails secret
```

### Configurar variables de entorno
```bash
export RAILS_ENV=production
export SECRET_KEY_BASE=your-secret-key
```

## Comandos de Cache

### Limpiar cache
```bash
rails tmp:clear
```

### Limpiar cache de desarrollo
```bash
rails dev:cache
```

### Precargar aplicación
```bash
rails runner "Rails.application.eager_load!"
```

## Comandos de Logs

### Ver logs en tiempo real
```bash
tail -f log/development.log
```

### Limpiar logs
```bash
rails log:clear
```

### Rotar logs
```bash
rails log:rotate
```

## Comandos de Credentials

### Editar credentials
```bash
rails credentials:edit
```

### Ver credentials
```bash
rails credentials:show
```

### Editar credentials para ambiente específico
```bash
rails credentials:edit --environment production
```

## Comandos de Rake Tasks

### Ver todas las tasks disponibles
```bash
rails -T
# o
rake -T
```

### Ejecutar task específica
```bash
rails my_namespace:my_task
```

### Crear task personalizada
```bash
rails generate task my_namespace my_task
```

## Comandos de Instalación de Gems

### Agregar gem al Gemfile
```ruby
# En Gemfile
gem 'devise'
gem 'bootsnap', '>= 1.4.4', require: false
```

### Instalar y configurar Devise
```bash
bundle install
rails generate devise:install
rails generate devise User
```

### Instalar Bootstrap
```bash
bundle add bootstrap
```

### Instalar jQuery
```bash
yarn add jquery
```

## Comandos de Debugging

### Activar byebug en código
```ruby
# En el código
byebug
```

### Instalar pry para debugging
```bash
# Agregar al Gemfile
gem 'pry-rails'
bundle install
```

### Ver información de la aplicación
```bash
rails about
```

### Verificar configuración
```bash
rails runner "puts Rails.application.config.inspect"
```

## Comandos de Performance

### Benchmark de código
```bash
rails runner "
require 'benchmark'
puts Benchmark.measure { User.all.to_a }
"
```

### Profiling con rack-mini-profiler
```bash
# Agregar gem 'rack-mini-profiler' al Gemfile
bundle install
```

### Instalar bullet para N+1 queries
```bash
# Agregar gem 'bullet' al Gemfile
bundle install
```

## Comandos de API

### Generar token de API
```bash
rails runner "puts SecureRandom.hex(20)"
```

### Generar serializers
```bash
# Con gem 'active_model_serializers'
rails generate serializer User name email
```

### Testing de API con curl
```bash
curl -X GET http://localhost:3000/api/users \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-token"
```

## Comandos de Internacionalización

### Generar archivos de localización
```bash
# Crear config/locales/es.yml manualmente
```

### Extraer strings para traducir
```bash
# Con gem 'i18n-tasks'
i18n-tasks missing
i18n-tasks unused
```

## Comandos de Seguridad

### Verificar vulnerabilidades
```bash
bundle audit
```

### Actualizar base de datos de vulnerabilidades
```bash
bundle audit --update
```

### Escanear código con Brakeman
```bash
# Instalar brakeman
gem install brakeman
brakeman
```
