# Django Commands

Django es un framework de desarrollo web de alto nivel escrito en Python que fomenta el desarrollo rápido y el diseño limpio y pragmático.

## Instalación

### Instalar Django
```bash
pip install django
```

### Instalar versión específica
```bash
pip install django==4.2
```

### Instalar en entorno virtual
```bash
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate
pip install django
```

## Creación de Proyectos

### Crear nuevo proyecto
```bash
django-admin startproject myproject
```

### Crear proyecto en directorio actual
```bash
django-admin startproject myproject .
```

### Crear aplicación dentro del proyecto
```bash
cd myproject
python manage.py startapp myapp
```

## Comandos de Desarrollo

### Ejecutar servidor de desarrollo
```bash
python manage.py runserver
```

### Ejecutar en puerto específico
```bash
python manage.py runserver 8080
```

### Ejecutar en IP específica
```bash
python manage.py runserver 0.0.0.0:8000
```

### Ejecutar servidor con SSL
```bash
python manage.py runserver_plus --cert-file cert.pem --key-file key.pem
```

## Comandos de Base de Datos

### Crear migraciones
```bash
python manage.py makemigrations
```

### Aplicar migraciones
```bash
python manage.py migrate
```

### Crear migración específica para una app
```bash
python manage.py makemigrations myapp
```

### Mostrar migraciones
```bash
python manage.py showmigrations
```

### Crear migración vacía
```bash
python manage.py makemigrations --empty myapp
```

### Revertir migración
```bash
python manage.py migrate myapp 0001
```

### Generar SQL de migración
```bash
python manage.py sqlmigrate myapp 0001
```

## Comandos de Administración

### Crear superusuario
```bash
python manage.py createsuperuser
```

### Cambiar contraseña de usuario
```bash
python manage.py changepassword username
```

### Recopilar archivos estáticos
```bash
python manage.py collectstatic
```

### Limpiar cache
```bash
python manage.py clear_cache
```

## Comandos de Shell

### Abrir shell interactivo de Django
```bash
python manage.py shell
```

### Abrir shell con IPython
```bash
pip install ipython
python manage.py shell
```

### Ejecutar script Python con contexto Django
```bash
python manage.py shell < script.py
```

## Testing

### Ejecutar todos los tests
```bash
python manage.py test
```

### Ejecutar tests de una app específica
```bash
python manage.py test myapp
```

### Ejecutar test específico
```bash
python manage.py test myapp.tests.MyTestCase
```

### Ejecutar tests con coverage
```bash
pip install coverage
coverage run --source='.' manage.py test
coverage report
coverage html
```

### Ejecutar tests en paralelo
```bash
python manage.py test --parallel
```

## Comandos de Inspección

### Verificar configuración
```bash
python manage.py check
```

### Verificar deployment
```bash
python manage.py check --deploy
```

### Mostrar configuración
```bash
python manage.py diffsettings
```

### Mostrar URLs
```bash
python manage.py show_urls
```

### Inspeccionar base de datos
```bash
python manage.py inspectdb
```

### Mostrar estructura de modelos
```bash
python manage.py graph_models -a -o models.png
```

## Comandos de Fixtures

### Crear fixture
```bash
python manage.py dumpdata myapp.MyModel > fixture.json
```

### Cargar fixture
```bash
python manage.py loaddata fixture.json
```

### Crear fixture con formato específico
```bash
python manage.py dumpdata --format=yaml myapp > fixture.yaml
```

## Comandos de Internacionalización

### Crear archivos de traducción
```bash
python manage.py makemessages -l es
```

### Compilar traducciones
```bash
python manage.py compilemessages
```

### Crear traducciones para JavaScript
```bash
python manage.py makemessages -d djangojs -l es
```

## Comandos Personalizados

### Crear comando personalizado
```bash
mkdir -p myapp/management/commands
touch myapp/management/__init__.py
touch myapp/management/commands/__init__.py
```

### Ejecutar comando personalizado
```bash
python manage.py mycommand
```

## Deployment

### Instalar servidor WSGI
```bash
pip install gunicorn
gunicorn myproject.wsgi:application
```

### Ejecutar con Gunicorn
```bash
gunicorn --bind 0.0.0.0:8000 myproject.wsgi:application
```

### Configurar variables de entorno
```bash
export DJANGO_SETTINGS_MODULE=myproject.settings.production
export SECRET_KEY=your-secret-key
export DEBUG=False
```

### Instalar servidor de archivos estáticos
```bash
pip install whitenoise
```

## Utilidades de Desarrollo

### Instalar Django Debug Toolbar
```bash
pip install django-debug-toolbar
```

### Instalar Django Extensions
```bash
pip install django-extensions
```

### Instalar Django REST Framework
```bash
pip install djangorestframework
```

### Crear requirements.txt
```bash
pip freeze > requirements.txt
```

### Instalar desde requirements.txt
```bash
pip install -r requirements.txt
```

## Comandos de Cache

### Crear tabla de cache
```bash
python manage.py createcachetable
```

### Limpiar cache
```bash
python manage.py clear_cache
```

## Comandos de Sesiones

### Limpiar sesiones expiradas
```bash
python manage.py clearsessions
```

### Crear tabla de sesiones
```bash
python manage.py migrate sessions
```
