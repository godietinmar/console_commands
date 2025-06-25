# 🐘 Comandos PHP

## Herramientas de Línea de Comandos

### php
**Descripción:** Intérprete de PHP para ejecutar scripts y aplicaciones
**Sintaxis básica:**
```bash
php [opciones] script.php [argumentos]
```

### composer
**Descripción:** Gestor de dependencias para PHP
**Sintaxis básica:**
```bash
composer [comando] [opciones] [argumentos]
```

### artisan
**Descripción:** Herramienta de línea de comandos de Laravel
**Sintaxis básica:**
```bash
php artisan [comando] [opciones] [argumentos]
```

### phpunit
**Descripción:** Framework de testing para PHP
**Sintaxis básica:**
```bash
phpunit [opciones] [directorio|archivo]
```

---

## Comandos Básicos PHP

### Ejecutar PHP
```bash
# Ejecutar script PHP
php script.php

# Ejecutar código PHP directamente
php -r "echo 'Hola Mundo';"

# Ejecutar con servidor web integrado
php -S localhost:8000

# Ejecutar en puerto específico con directorio
php -S localhost:8080 -t public/

# Verificar sintaxis
php -l script.php

# Ver información de PHP
php -i

# Ver versión
php -v

# Ver módulos cargados
php -m

# Ejecutar interactivo
php -a
```

### Configuración PHP
```bash
# Ver configuración actual
php --ini

# Ver directiva específica
php -r "echo ini_get('memory_limit');"

# Ejecutar con configuración personalizada
php -d memory_limit=512M script.php

# Ejecutar con archivo php.ini específico
php -c /ruta/a/php.ini script.php

# Ver todas las configuraciones
php -r "phpinfo();" | grep -i memory

# Validar archivo de configuración
php --syntax-check /etc/php/7.4/apache2/php.ini
```

---

## Composer - Gestión de Dependencias

### Instalación y Configuración
```bash
# Instalar Composer globalmente (Linux/Mac)
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer

# Verificar instalación
composer --version

# Actualizar Composer
composer self-update

# Crear proyecto nuevo
composer create-project laravel/laravel mi-proyecto

# Inicializar composer.json
composer init
```

### Gestión de Paquetes
```bash
# Instalar dependencias
composer install

# Instalar solo dependencias de producción
composer install --no-dev

# Agregar paquete
composer require monolog/monolog

# Agregar paquete de desarrollo
composer require --dev phpunit/phpunit

# Agregar versión específica
composer require "monolog/monolog:^2.0"

# Actualizar dependencias
composer update

# Actualizar paquete específico
composer update monolog/monolog

# Remover paquete
composer remove monolog/monolog

# Mostrar paquetes instalados
composer show

# Buscar paquetes
composer search monolog

# Ver información de paquete
composer info monolog/monolog
```

### Autoload y Optimización
```bash
# Generar autoload
composer dump-autoload

# Optimizar autoload para producción
composer dump-autoload --optimize

# Validar composer.json
composer validate

# Ver árbol de dependencias
composer depends monolog/monolog

# Ver dependencias inversas
composer prohibits symfony/symfony

# Limpiar cache
composer clear-cache

# Verificar problemas de seguridad
composer audit
```

---

## Laravel Framework

### Crear y Configurar Proyecto
```bash
# Instalar Laravel via Composer
composer global require laravel/installer

# Crear proyecto Laravel
laravel new mi-app
# o
composer create-project --prefer-dist laravel/laravel mi-app

# Navegar al proyecto
cd mi-app

# Configurar permisos
chmod -R 775 storage bootstrap/cache

# Generar clave de aplicación
php artisan key:generate

# Configurar base de datos (.env)
# Editar archivo .env con credenciales de DB
```

### Comandos Artisan
```bash
# Ver todos los comandos disponibles
php artisan list

# Ayuda de comando específico
php artisan help make:controller

# Limpiar cache
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan view:clear

# Optimizar para producción
php artisan config:cache
php artisan route:cache
php artisan view:cache
php artisan optimize

# Información de rutas
php artisan route:list

# Iniciar servidor de desarrollo
php artisan serve

# Servidor en puerto específico
php artisan serve --port=8080

# Servidor en host específico
php artisan serve --host=0.0.0.0 --port=8000
```

### Generadores Laravel
```bash
# Generar controlador
php artisan make:controller UserController

# Controlador con recursos
php artisan make:controller UserController --resource

# Controlador de API
php artisan make:controller Api/UserController --api

# Generar modelo
php artisan make:model User

# Modelo con migración
php artisan make:model User -m

# Modelo con controlador y migración
php artisan make:model User -mcr

# Generar migración
php artisan make:migration create_users_table

# Generar seeder
php artisan make:seeder UserSeeder

# Generar factory
php artisan make:factory UserFactory

# Generar middleware
php artisan make:middleware CheckAge

# Generar request
php artisan make:request StoreUserRequest

# Generar job
php artisan make:job ProcessPayment

# Generar event
php artisan make:event UserRegistered

# Generar listener
php artisan make:listener SendWelcomeEmail

# Generar mail
php artisan make:mail WelcomeEmail

# Generar notification
php artisan make:notification InvoicePaid

# Generar command personalizado
php artisan make:command SendEmails
```

### Base de Datos - Migraciones
```bash
# Ejecutar migraciones
php artisan migrate

# Ejecutar migraciones en producción
php artisan migrate --force

# Rollback última migración
php artisan migrate:rollback

# Rollback múltiples migraciones
php artisan migrate:rollback --step=3

# Resetear todas las migraciones
php artisan migrate:reset

# Refrescar migraciones (reset + migrate)
php artisan migrate:refresh

# Refrescar con seeders
php artisan migrate:refresh --seed

# Ver estado de migraciones
php artisan migrate:status

# Crear base de datos
php artisan db:create

# Sembrar base de datos
php artisan db:seed

# Ejecutar seeder específico
php artisan db:seed --class=UserSeeder
```

### Testing Laravel
```bash
# Ejecutar tests
php artisan test

# Ejecutar PHPUnit directamente
./vendor/bin/phpunit

# Ejecutar tests específicos
php artisan test --filter UserTest

# Ejecutar tests con cobertura
php artisan test --coverage

# Crear test
php artisan make:test UserTest

# Crear test unitario
php artisan make:test UserTest --unit

# Ejecutar tests en paralelo
php artisan test --parallel
```

---

## Symfony Framework

### Crear Proyecto Symfony
```bash
# Instalar Symfony CLI
curl -sS https://get.symfony.com/cli/installer | bash

# Crear aplicación web completa
symfony new mi-app --full

# Crear microservicio/API
symfony new mi-api

# Navegar al proyecto
cd mi-app

# Iniciar servidor de desarrollo
symfony serve

# Servidor en segundo plano
symfony serve -d

# Parar servidor
symfony server:stop
```

### Console Commands Symfony
```bash
# Ver comandos disponibles
php bin/console list

# Limpiar cache
php bin/console cache:clear

# Calentar cache
php bin/console cache:warmup

# Ver rutas
php bin/console debug:router

# Información de servicios
php bin/console debug:container

# Crear controlador
php bin/console make:controller UserController

# Crear entidad
php bin/console make:entity User

# Crear migración
php bin/console make:migration

# Ejecutar migraciones
php bin/console doctrine:migrations:migrate

# Crear formulario
php bin/console make:form UserType

# Crear command personalizado
php bin/console make:command app:send-emails
```

---

## Testing con PHPUnit

### Comandos Básicos
```bash
# Instalar PHPUnit
composer require --dev phpunit/phpunit

# Ejecutar todos los tests
./vendor/bin/phpunit

# Ejecutar test específico
./vendor/bin/phpunit tests/UserTest.php

# Ejecutar con cobertura HTML
./vendor/bin/phpunit --coverage-html coverage/

# Ejecutar con filtro
./vendor/bin/phpunit --filter testUserCanLogin

# Ejecutar grupo específico
./vendor/bin/phpunit --group unit

# Generar archivo de configuración
./vendor/bin/phpunit --generate-configuration

# Ejecutar en modo verbose
./vendor/bin/phpunit --verbose
```

---

## CodeSniffer y Herramientas de Calidad

### PHP CodeSniffer
```bash
# Instalar PHP CodeSniffer
composer require --dev squizlabs/php_codesniffer

# Verificar estándares de código
./vendor/bin/phpcs src/

# Usar estándar específico
./vendor/bin/phpcs --standard=PSR12 src/

# Corregir automáticamente
./vendor/bin/phpcbf src/

# Generar reporte XML
./vendor/bin/phpcs --report=xml src/ > report.xml
```

### PHP-CS-Fixer
```bash
# Instalar PHP-CS-Fixer
composer require --dev friendsofphp/php-cs-fixer

# Corregir archivos
./vendor/bin/php-cs-fixer fix src/

# Dry run (solo mostrar cambios)
./vendor/bin/php-cs-fixer fix src/ --dry-run --diff

# Usar configuración específica
./vendor/bin/php-cs-fixer fix src/ --config=.php-cs-fixer.php
```

### PHPStan - Análisis Estático
```bash
# Instalar PHPStan
composer require --dev phpstan/phpstan

# Analizar código
./vendor/bin/phpstan analyse src

# Nivel específico de análisis (0-9)
./vendor/bin/phpstan analyse src --level=5

# Generar archivo de configuración
./vendor/bin/phpstan analyse src --generate-baseline
```

---

## Ejemplos de Uso Común

### API REST con Laravel
```bash
# 1. Crear proyecto Laravel
composer create-project laravel/laravel mi-api
cd mi-api

# 2. Configurar base de datos (.env)
cat >> .env << 'EOF'
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=mi_api
DB_USERNAME=usuario
DB_PASSWORD=password
EOF

# 3. Crear modelo con migración
php artisan make:model Product -m

# 4. Editar migración (database/migrations/xxxx_create_products_table.php)
# Agregar campos: name, description, price, etc.

# 5. Ejecutar migración
php artisan migrate

# 6. Crear controlador API
php artisan make:controller Api/ProductController --api

# 7. Definir rutas API (routes/api.php)
cat >> routes/api.php << 'EOF'
Route::apiResource('products', App\Http\Controllers\Api\ProductController::class);
EOF

# 8. Crear seeder
php artisan make:seeder ProductSeeder

# 9. Ejecutar seeder
php artisan db:seed --class=ProductSeeder

# 10. Iniciar servidor
php artisan serve
```

### Aplicación Web con Symfony
```bash
# 1. Crear proyecto Symfony
symfony new mi-web-app --full
cd mi-web-app

# 2. Configurar base de datos (.env.local)
cat > .env.local << 'EOF'
DATABASE_URL="mysql://usuario:password@127.0.0.1:3306/mi_web_app"
EOF

# 3. Crear base de datos
php bin/console doctrine:database:create

# 4. Crear entidad
php bin/console make:entity Product

# 5. Crear migración
php bin/console make:migration

# 6. Ejecutar migración
php bin/console doctrine:migrations:migrate

# 7. Crear controlador
php bin/console make:controller ProductController

# 8. Crear formulario
php bin/console make:form ProductType

# 9. Instalar Webpack Encore para assets
composer require symfony/webpack-encore-bundle
npm install

# 10. Compilar assets
npm run dev

# 11. Iniciar servidor
symfony serve
```

### Script PHP Personalizado
```bash
# 1. Crear script con dependencias
cat > mi_script.php << 'EOF'
<?php
require_once 'vendor/autoload.php';

use GuzzleHttp\Client;
use Monolog\Logger;
use Monolog\Handler\StreamHandler;

// Configurar logger
$logger = new Logger('mi_script');
$logger->pushHandler(new StreamHandler('app.log', Logger::INFO));

// Configurar cliente HTTP
$client = new Client();

// Función principal
function procesarDatos($url, $logger) {
    try {
        $logger->info("Procesando URL: $url");
        
        $response = $client->request('GET', $url);
        $data = json_decode($response->getBody(), true);
        
        $logger->info("Datos procesados exitosamente");
        return $data;
        
    } catch (Exception $e) {
        $logger->error("Error procesando datos: " . $e->getMessage());
        throw $e;
    }
}

// Ejecutar si es llamado directamente
if (basename(__FILE__) == basename($_SERVER["SCRIPT_NAME"])) {
    $url = $argv[1] ?? 'https://api.github.com/users/octocat';
    $datos = procesarDatos($url, $logger);
    echo json_encode($datos, JSON_PRETTY_PRINT);
}
EOF

# 2. Crear composer.json
cat > composer.json << 'EOF'
{
    "require": {
        "guzzlehttp/guzzle": "^7.0",
        "monolog/monolog": "^2.0"
    }
}
EOF

# 3. Instalar dependencias
composer install

# 4. Ejecutar script
php mi_script.php https://api.github.com/users/octocat
```

---

## Scripts de Utilidad

### Script de Desarrollo Laravel
```bash
#!/bin/bash
# laravel-dev.sh - Herramientas de desarrollo Laravel

# Función para setup inicial
setup() {
    echo "🚀 Configurando proyecto Laravel..."
    
    # Instalar dependencias
    composer install
    
    # Copiar archivo de configuración
    if [ ! -f .env ]; then
        cp .env.example .env
        echo "📝 Archivo .env creado - configura tu base de datos"
    fi
    
    # Generar clave de aplicación
    php artisan key:generate
    
    # Configurar permisos
    chmod -R 775 storage bootstrap/cache
    
    # Crear base de datos si no existe
    php artisan migrate --seed
    
    echo "✅ Setup completo"
}

# Función para desarrollo con hot reload
dev_server() {
    echo "🔥 Iniciando servidor con hot reload..."
    
    # Limpiar cache
    php artisan cache:clear
    php artisan config:clear
    php artisan route:clear
    php artisan view:clear
    
    # Iniciar servidor
    php artisan serve &
    SERVER_PID=$!
    
    # Monitorear cambios
    echo "👀 Monitoreando cambios en archivos..."
    
    trap "kill $SERVER_PID" EXIT
    
    while inotifywait -r -e modify app/ resources/ routes/; do
        echo "🔄 Cambios detectados, limpiando cache..."
        php artisan cache:clear
        php artisan config:clear
        php artisan route:clear
        php artisan view:clear
    done
}

# Función para ejecutar tests
run_tests() {
    echo "🧪 Ejecutando tests..."
    
    # Configurar base de datos de testing
    php artisan migrate --env=testing
    
    # Ejecutar tests
    php artisan test --coverage
    
    # Ejecutar análisis estático si está disponible
    if [ -f "./vendor/bin/phpstan" ]; then
        echo "🔍 Ejecutando análisis estático..."
        ./vendor/bin/phpstan analyse
    fi
    
    # Verificar estándares de código
    if [ -f "./vendor/bin/phpcs" ]; then
        echo "🎨 Verificando estándares de código..."
        ./vendor/bin/phpcs app/
    fi
}

# Función para optimizar para producción
optimize_production() {
    echo "🚀 Optimizando para producción..."
    
    # Instalar dependencias de producción
    composer install --no-dev --optimize-autoloader
    
    # Optimizar configuraciones
    php artisan config:cache
    php artisan route:cache
    php artisan view:cache
    php artisan optimize
    
    # Compilar assets si existe npm
    if command -v npm &> /dev/null; then
        npm run production
    fi
    
    echo "✅ Optimización completa"
}

# Menú interactivo
echo "🛠️  Herramientas de Desarrollo Laravel"
echo "1. Setup inicial"
echo "2. Servidor de desarrollo"
echo "3. Ejecutar tests"
echo "4. Optimizar para producción"
echo "5. Limpiar todo el cache"
echo "6. Generar documentación API"

read -p "Selecciona una opción: " option

case $option in
    1) setup ;;
    2) dev_server ;;
    3) run_tests ;;
    4) optimize_production ;;
    5) 
        php artisan cache:clear
        php artisan config:clear
        php artisan route:clear
        php artisan view:clear
        composer dump-autoload
        echo "✅ Cache limpiado"
        ;;
    6)
        if [ -f "./vendor/bin/apidoc" ]; then
            ./vendor/bin/apidoc generate
            echo "📚 Documentación generada"
        else
            echo "❌ apidoc no instalado"
        fi
        ;;
    *) echo "Opción inválida" ;;
esac
```

### Script de Deploy PHP
```bash
#!/bin/bash
# deploy-php.sh - Script de despliegue para aplicaciones PHP

APP_NAME="mi-app-php"
DEPLOY_USER="deploy"
DEPLOY_HOST="servidor.com"
DEPLOY_PATH="/var/www/$APP_NAME"
BACKUP_PATH="/var/backups/$APP_NAME"

echo "🚀 Desplegando aplicación PHP: $APP_NAME"

# 1. Ejecutar tests localmente
echo "🧪 Ejecutando tests..."
if [ -f "./vendor/bin/phpunit" ]; then
    ./vendor/bin/phpunit
    
    if [ $? -ne 0 ]; then
        echo "❌ Tests fallidos, cancelando deploy"
        exit 1
    fi
fi

# 2. Optimizar aplicación
echo "⚙️  Optimizando aplicación..."
composer install --no-dev --optimize-autoloader

# 3. Crear paquete de deploy
echo "📦 Creando paquete..."
tar -czf deploy.tar.gz \
    --exclude='.git' \
    --exclude='node_modules' \
    --exclude='tests' \
    --exclude='*.log' \
    --exclude='.env' \
    .

# 4. Subir y desplegar
echo "📤 Desplegando en servidor..."
scp deploy.tar.gz $DEPLOY_USER@$DEPLOY_HOST:/tmp/

ssh $DEPLOY_USER@$DEPLOY_HOST << EOF
    # Crear backup
    if [ -d "$DEPLOY_PATH" ]; then
        echo "💾 Creando backup..."
        sudo cp -r $DEPLOY_PATH $BACKUP_PATH/backup-\$(date +%Y%m%d-%H%M%S)
    fi
    
    # Crear directorio temporal
    sudo rm -rf /tmp/new_release
    sudo mkdir /tmp/new_release
    cd /tmp/new_release
    
    # Extraer nueva versión
    sudo tar -xzf /tmp/deploy.tar.gz
    
    # Copiar configuración de producción
    if [ -f "$DEPLOY_PATH/.env" ]; then
        sudo cp $DEPLOY_PATH/.env .env
    fi
    
    # Instalar dependencias de producción
    sudo composer install --no-dev --optimize-autoloader
    
    # Ejecutar migraciones si es Laravel
    if [ -f "artisan" ]; then
        sudo php artisan migrate --force
        sudo php artisan config:cache
        sudo php artisan route:cache
        sudo php artisan view:cache
        sudo php artisan optimize
    fi
    
    # Configurar permisos
    sudo chown -R www-data:www-data .
    sudo chmod -R 755 .
    
    if [ -d "storage" ]; then
        sudo chmod -R 775 storage bootstrap/cache
    fi
    
    # Mover a producción
    sudo rm -rf $DEPLOY_PATH.old
    if [ -d "$DEPLOY_PATH" ]; then
        sudo mv $DEPLOY_PATH $DEPLOY_PATH.old
    fi
    sudo mv /tmp/new_release $DEPLOY_PATH
    
    # Reiniciar servicios
    sudo systemctl reload php7.4-fpm
    sudo systemctl reload nginx
    
    # Limpiar archivos temporales
    sudo rm /tmp/deploy.tar.gz
EOF

# 5. Verificar deploy
echo "🔍 Verificando deploy..."
sleep 5

HTTP_STATUS=$(curl -s -o /dev/null -w "%{http_code}" https://$DEPLOY_HOST)

if [ $HTTP_STATUS -eq 200 ]; then
    echo "✅ Deploy exitoso!"
    echo "🌐 Aplicación disponible en: https://$DEPLOY_HOST"
else
    echo "❌ Error en deploy (HTTP $HTTP_STATUS)"
    echo "🔄 Revirtiendo cambios..."
    
    ssh $DEPLOY_USER@$DEPLOY_HOST << EOF
        if [ -d "$DEPLOY_PATH.old" ]; then
            sudo rm -rf $DEPLOY_PATH
            sudo mv $DEPLOY_PATH.old $DEPLOY_PATH
            sudo systemctl reload php7.4-fpm
            sudo systemctl reload nginx
        fi
EOF
fi

# Limpiar archivos locales
rm -f deploy.tar.gz

# Restaurar dependencias de desarrollo
composer install
```

### Script de Backup Base de Datos
```bash
#!/bin/bash
# backup-db.sh - Script de backup para aplicaciones PHP con base de datos

# Configuración
APP_NAME="mi-app"
BACKUP_DIR="/var/backups/$APP_NAME"
DATE=$(date +%Y%m%d_%H%M%S)

# Función para backup MySQL
backup_mysql() {
    local host=$1
    local user=$2
    local password=$3
    local database=$4
    
    echo "🗄️  Creando backup de MySQL..."
    
    mysqldump -h$host -u$user -p$password \
        --single-transaction \
        --routines \
        --triggers \
        $database > "$BACKUP_DIR/mysql_${database}_${DATE}.sql"
    
    if [ $? -eq 0 ]; then
        gzip "$BACKUP_DIR/mysql_${database}_${DATE}.sql"
        echo "✅ Backup MySQL completado"
    else
        echo "❌ Error en backup MySQL"
        return 1
    fi
}

# Función para backup PostgreSQL
backup_postgresql() {
    local host=$1
    local user=$2
    local database=$3
    
    echo "🐘 Creando backup de PostgreSQL..."
    
    PGPASSWORD=$4 pg_dump -h$host -U$user -d$database \
        --clean --create > "$BACKUP_DIR/postgres_${database}_${DATE}.sql"
    
    if [ $? -eq 0 ]; then
        gzip "$BACKUP_DIR/postgres_${database}_${DATE}.sql"
        echo "✅ Backup PostgreSQL completado"
    else
        echo "❌ Error en backup PostgreSQL"
        return 1
    fi
}

# Función para backup de archivos
backup_files() {
    local source_dir=$1
    
    echo "📁 Creando backup de archivos..."
    
    tar -czf "$BACKUP_DIR/files_${DATE}.tar.gz" \
        --exclude='vendor' \
        --exclude='node_modules' \
        --exclude='*.log' \
        -C $(dirname $source_dir) $(basename $source_dir)
    
    if [ $? -eq 0 ]; then
        echo "✅ Backup de archivos completado"
    else
        echo "❌ Error en backup de archivos"
        return 1
    fi
}

# Función para limpiar backups antiguos
cleanup_old_backups() {
    local days=${1:-7}
    
    echo "🧹 Limpiando backups antiguos (más de $days días)..."
    find $BACKUP_DIR -name "*.sql.gz" -mtime +$days -delete
    find $BACKUP_DIR -name "*.tar.gz" -mtime +$days -delete
    echo "✅ Limpieza completada"
}

# Crear directorio de backup
mkdir -p $BACKUP_DIR

# Leer configuración de .env si existe
if [ -f ".env" ]; then
    source .env
    
    # Detectar tipo de base de datos
    if [[ $DB_CONNECTION == "mysql" ]]; then
        backup_mysql $DB_HOST $DB_USERNAME $DB_PASSWORD $DB_DATABASE
    elif [[ $DB_CONNECTION == "pgsql" ]]; then
        backup_postgresql $DB_HOST $DB_USERNAME $DB_DATABASE $DB_PASSWORD
    fi
fi

# Backup de archivos
backup_files $(pwd)

# Limpiar backups antiguos
cleanup_old_backups 7

echo "🎉 Proceso de backup completado"
echo "📁 Backups almacenados en: $BACKUP_DIR"
```

---

## Configuraciones y Optimización

### Configuración PHP para Producción
```bash
# php.ini optimizado para producción
expose_php = Off
display_errors = Off
log_errors = On
error_log = /var/log/php_errors.log
memory_limit = 256M
max_execution_time = 30
max_input_time = 60
upload_max_filesize = 10M
post_max_size = 10M
session.gc_maxlifetime = 1440
opcache.enable = 1
opcache.memory_consumption = 128
opcache.interned_strings_buffer = 8
opcache.max_accelerated_files = 4000
opcache.revalidate_freq = 2
```

### Optimización con OPcache
```bash
# Verificar estado de OPcache
php -r "echo opcache_get_status()['opcache_enabled'] ? 'Enabled' : 'Disabled';"

# Ver estadísticas de OPcache
php -r "print_r(opcache_get_status());"

# Limpiar cache de OPcache
php -r "opcache_reset();"

# Script para verificar performance
php -r "
$start = microtime(true);
for(\$i = 0; \$i < 100000; \$i++) {
    \$test = 'Hello World ' . \$i;
}
echo 'Tiempo: ' . (microtime(true) - \$start) . ' segundos';
"
```

Esta documentación cubre los comandos más importantes de PHP, desde desarrollo básico hasta optimización y despliegue en producción.
