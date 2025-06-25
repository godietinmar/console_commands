# Laravel Commands

Laravel es un framework de aplicaciones web con sintaxis expresiva y elegante. Proporciona una estructura sólida para el desarrollo rápido de aplicaciones web.

## Instalación

### Instalar Laravel via Composer
```bash
composer global require laravel/installer
```

### Verificar instalación
```bash
laravel --version
```

### Instalar Composer (si no está instalado)
```bash
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

## Creación de Proyectos

### Crear nueva aplicación Laravel
```bash
laravel new blog
```

### Crear aplicación con Composer
```bash
composer create-project laravel/laravel blog
```

### Crear aplicación con versión específica
```bash
composer create-project laravel/laravel blog "9.*"
```

### Crear aplicación con autenticación
```bash
laravel new blog --auth
```

### Crear aplicación con Jetstream
```bash
laravel new blog --jet
```

## Comandos Artisan Básicos

### Ver todos los comandos Artisan
```bash
php artisan list
```

### Ver ayuda de comando específico
```bash
php artisan help migrate
```

### Ejecutar servidor de desarrollo
```bash
php artisan serve
```

### Ejecutar en puerto específico
```bash
php artisan serve --port=8080
```

### Ejecutar en host específico
```bash
php artisan serve --host=0.0.0.0
```

## Comandos de Base de Datos

### Crear migración
```bash
php artisan make:migration create_users_table
```

### Crear migración con tabla
```bash
php artisan make:migration create_users_table --create=users
```

### Crear migración para modificar tabla
```bash
php artisan make:migration add_email_to_users_table --table=users
```

### Ejecutar migraciones
```bash
php artisan migrate
```

### Ejecutar migraciones en producción
```bash
php artisan migrate --force
```

### Revertir última migración
```bash
php artisan migrate:rollback
```

### Revertir múltiples migraciones
```bash
php artisan migrate:rollback --step=3
```

### Revertir todas las migraciones
```bash
php artisan migrate:reset
```

### Refrescar migraciones
```bash
php artisan migrate:refresh
```

### Refrescar y ejecutar seeders
```bash
php artisan migrate:refresh --seed
```

### Ver estado de migraciones
```bash
php artisan migrate:status
```

### Crear seeder
```bash
php artisan make:seeder UserSeeder
```

### Ejecutar seeders
```bash
php artisan db:seed
```

### Ejecutar seeder específico
```bash
php artisan db:seed --class=UserSeeder
```

## Comandos de Modelos y Controladores

### Crear modelo
```bash
php artisan make:model User
```

### Crear modelo con migración
```bash
php artisan make:model User -m
```

### Crear modelo con todo (migración, factory, seeder, controller)
```bash
php artisan make:model User -a
```

### Crear controlador
```bash
php artisan make:controller UserController
```

### Crear controlador de recursos
```bash
php artisan make:controller UserController --resource
```

### Crear controlador de API
```bash
php artisan make:controller UserController --api
```

### Crear controlador con modelo
```bash
php artisan make:controller UserController --model=User
```

## Comandos de Middleware

### Crear middleware
```bash
php artisan make:middleware CheckAge
```

### Registrar middleware globalmente
Se registra en `app/Http/Kernel.php`

### Registrar middleware para rutas
Se registra en `app/Http/Kernel.php` en el array `$routeMiddleware`

## Comandos de Requests

### Crear Form Request
```bash
php artisan make:request StoreUserRequest
```

### Crear Resource
```bash
php artisan make:resource UserResource
```

### Crear Resource Collection
```bash
php artisan make:resource UserCollection
```

## Comandos de Autenticación

### Instalar Laravel UI
```bash
composer require laravel/ui
```

### Crear scaffolding de autenticación
```bash
php artisan ui bootstrap --auth
php artisan ui vue --auth
php artisan ui react --auth
```

### Instalar Laravel Breeze
```bash
composer require laravel/breeze --dev
php artisan breeze:install
```

### Instalar Laravel Jetstream
```bash
composer require laravel/jetstream
php artisan jetstream:install livewire
```

### Instalar Laravel Sanctum
```bash
composer require laravel/sanctum
php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"
php artisan migrate
```

### Instalar Laravel Passport
```bash
composer require laravel/passport
php artisan migrate
php artisan passport:install
```

## Comandos de Jobs y Queues

### Crear Job
```bash
php artisan make:job ProcessPodcast
```

### Crear tabla de jobs
```bash
php artisan queue:table
php artisan migrate
```

### Ejecutar worker de queue
```bash
php artisan queue:work
```

### Ejecutar worker con timeout
```bash
php artisan queue:work --timeout=60
```

### Reiniciar workers
```bash
php artisan queue:restart
```

### Ver jobs fallidos
```bash
php artisan queue:failed
```

### Reintentar job fallido
```bash
php artisan queue:retry 1
```

### Limpiar jobs fallidos
```bash
php artisan queue:flush
```

## Comandos de Cache

### Limpiar cache de aplicación
```bash
php artisan cache:clear
```

### Limpiar cache de configuración
```bash
php artisan config:clear
```

### Limpiar cache de rutas
```bash
php artisan route:clear
```

### Limpiar cache de vistas
```bash
php artisan view:clear
```

### Cachear configuración
```bash
php artisan config:cache
```

### Cachear rutas
```bash
php artisan route:cache
```

### Cachear vistas
```bash
php artisan view:cache
```

### Crear tabla de cache
```bash
php artisan cache:table
php artisan migrate
```

## Comandos de Eventos

### Crear evento
```bash
php artisan make:event OrderShipped
```

### Crear listener
```bash
php artisan make:listener SendShipmentNotification
```

### Crear listener con evento
```bash
php artisan make:listener SendShipmentNotification --event=OrderShipped
```

### Generar listeners para eventos
```bash
php artisan event:generate
```

## Comandos de Notificaciones

### Crear notificación
```bash
php artisan make:notification InvoicePaid
```

### Crear tabla de notificaciones
```bash
php artisan notifications:table
php artisan migrate
```

## Comandos de Mail

### Crear mailable
```bash
php artisan make:mail OrderShipped
```

### Crear mailable con markdown
```bash
php artisan make:mail OrderShipped --markdown=emails.orders.shipped
```

## Comandos de Políticas

### Crear policy
```bash
php artisan make:policy PostPolicy
```

### Crear policy con modelo
```bash
php artisan make:policy PostPolicy --model=Post
```

## Comandos de Comandos Personalizados

### Crear comando Artisan personalizado
```bash
php artisan make:command SendEmails
```

### Ejecutar comando personalizado
```bash
php artisan email:send
```

## Comandos de Storage

### Crear enlace simbólico para storage
```bash
php artisan storage:link
```

## Comandos de Rutas

### Ver todas las rutas
```bash
php artisan route:list
```

### Ver rutas con filtro
```bash
php artisan route:list --name=user
```

### Ver rutas de un middleware
```bash
php artisan route:list --middleware=auth
```

## Comandos de Tinker

### Abrir shell interactivo
```bash
php artisan tinker
```

### Ejecutar código en Tinker
```bash
# Dentro de tinker
User::all();
User::create(['name' => 'John', 'email' => 'john@example.com']);
```

## Comandos de Testing

### Crear test
```bash
php artisan make:test UserTest
```

### Crear test unitario
```bash
php artisan make:test UserTest --unit
```

### Ejecutar tests
```bash
php artisan test
```

### Ejecutar tests con coverage
```bash
php artisan test --coverage
```

### Ejecutar test específico
```bash
php artisan test tests/Feature/UserTest.php
```

## Comandos de Optimización

### Optimizar aplicación para producción
```bash
composer install --optimize-autoloader --no-dev
php artisan config:cache
php artisan route:cache
php artisan view:cache
```

### Limpiar todas las cachés
```bash
php artisan optimize:clear
```

### Optimizar para desarrollo
```bash
php artisan optimize
```

## Comandos de Mantenimiento

### Poner aplicación en modo mantenimiento
```bash
php artisan down
```

### Poner en mantenimiento con mensaje personalizado
```bash
php artisan down --message="Upgrading Database"
```

### Sacar de modo mantenimiento
```bash
php artisan up
```

### Modo mantenimiento con secreto
```bash
php artisan down --secret="1630542a-246b-4b66-afa1-dd72a4c43515"
```

## Comandos de Vendor

### Publicar assets de vendor
```bash
php artisan vendor:publish
```

### Publicar assets específicos
```bash
php artisan vendor:publish --provider="Spatie\Permission\PermissionServiceProvider"
```

### Publicar tags específicos
```bash
php artisan vendor:publish --tag=laravel-assets
```

## Comandos de Scheduled Tasks

### Ejecutar scheduler
```bash
php artisan schedule:run
```

### Ver tareas programadas
```bash
php artisan schedule:list
```

### Ejecutar tarea específica
```bash
php artisan schedule:test
```

## Comandos de Horizon (Laravel Horizon)

### Instalar Horizon
```bash
composer require laravel/horizon
php artisan horizon:install
```

### Ejecutar Horizon
```bash
php artisan horizon
```

### Pausar Horizon
```bash
php artisan horizon:pause
```

### Continuar Horizon
```bash
php artisan horizon:continue
```

### Terminar Horizon
```bash
php artisan horizon:terminate
```

## Comandos de Telescope (Laravel Telescope)

### Instalar Telescope
```bash
composer require laravel/telescope
php artisan telescope:install
php artisan migrate
```

### Publicar assets de Telescope
```bash
php artisan telescope:publish
```
