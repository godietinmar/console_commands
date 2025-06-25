# Flask Commands

Flask es un microframework web de Python que es ligero y flexible, diseñado para hacer que comenzar sea rápido y fácil, con la capacidad de escalar a aplicaciones complejas.

## Instalación

### Instalar Flask
```bash
pip install Flask
```

### Instalar en entorno virtual
```bash
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate
pip install Flask
```

### Instalar Flask con dependencias adicionales
```bash
pip install Flask[async]  # Para soporte async
pip install Flask[dotenv]  # Para soporte .env
```

## Comandos de Desarrollo

### Ejecutar aplicación Flask
```bash
flask run
```

### Ejecutar en modo debug
```bash
flask --debug run
```

### Ejecutar en puerto específico
```bash
flask run --port 8080
```

### Ejecutar en host específico
```bash
flask run --host 0.0.0.0
```

### Ejecutar con recarga automática
```bash
flask run --reload
```

### Configurar aplicación Flask
```bash
export FLASK_APP=app.py
export FLASK_ENV=development
flask run
```

### En Windows
```cmd
set FLASK_APP=app.py
set FLASK_ENV=development
flask run
```

### Con archivo .env
```bash
# Crear archivo .env
echo "FLASK_APP=app.py" > .env
echo "FLASK_DEBUG=True" >> .env
flask run
```

## Comandos de Shell

### Abrir shell interactivo de Flask
```bash
flask shell
```

### Ejecutar código en contexto de aplicación
```bash
flask shell
# Dentro del shell:
# >>> from app import db
# >>> db.create_all()
```

## Comandos de Base de Datos (Flask-SQLAlchemy)

### Instalar Flask-SQLAlchemy
```bash
pip install Flask-SQLAlchemy
```

### Instalar Flask-Migrate
```bash
pip install Flask-Migrate
```

### Inicializar migraciones
```bash
flask db init
```

### Crear migración
```bash
flask db migrate -m "Initial migration"
```

### Aplicar migraciones
```bash
flask db upgrade
```

### Revertir migración
```bash
flask db downgrade
```

### Ver historial de migraciones
```bash
flask db history
```

### Ver migración actual
```bash
flask db current
```

### Generar SQL de migración
```bash
flask db sql
```

### Crear base de datos
```bash
flask shell
>>> from app import db
>>> db.create_all()
```

## Comandos Personalizados

### Crear comando personalizado
```python
# En app.py
import click
from flask.cli import with_appcontext

@click.command()
@with_appcontext
def init_db():
    """Clear existing data and create new tables."""
    db.drop_all()
    db.create_all()
    click.echo('Initialized the database.')

app.cli.add_command(init_db)
```

### Ejecutar comando personalizado
```bash
flask init-db
```

### Crear comando con argumentos
```python
@click.command()
@click.argument('name')
@with_appcontext
def create_user(name):
    """Create a new user."""
    user = User(username=name)
    db.session.add(user)
    db.session.commit()
    click.echo(f'Created user {name}')

app.cli.add_command(create_user)
```

### Ejecutar comando con argumentos
```bash
flask create-user john
```

## Comandos de Testing

### Instalar pytest para Flask
```bash
pip install pytest pytest-flask
```

### Ejecutar tests
```bash
pytest
```

### Ejecutar tests con coverage
```bash
pip install pytest-cov
pytest --cov=app tests/
```

### Ejecutar tests específicos
```bash
pytest tests/test_app.py
```

### Ejecutar tests en modo verbose
```bash
pytest -v
```

### Ejecutar tests con output
```bash
pytest -s
```

## Comandos de Deployment

### Instalar Gunicorn
```bash
pip install gunicorn
```

### Ejecutar con Gunicorn
```bash
gunicorn -w 4 app:app
```

### Ejecutar Gunicorn en puerto específico
```bash
gunicorn -w 4 -b 0.0.0.0:8000 app:app
```

### Ejecutar con configuración
```bash
gunicorn -c gunicorn.conf.py app:app
```

### Instalar uWSGI
```bash
pip install uwsgi
```

### Ejecutar con uWSGI
```bash
uwsgi --http :8000 --module app:app
```

### Configurar variables de entorno para producción
```bash
export FLASK_ENV=production
export SECRET_KEY=your-secret-key
export DATABASE_URL=postgresql://user:pass@localhost/db
```

## Comandos de Flask Extensions

### Instalar Flask-Login
```bash
pip install Flask-Login
```

### Instalar Flask-WTF (formularios)
```bash
pip install Flask-WTF
```

### Instalar Flask-Mail
```bash
pip install Flask-Mail
```

### Instalar Flask-Admin
```bash
pip install Flask-Admin
```

### Instalar Flask-Security
```bash
pip install Flask-Security-Too
```

### Instalar Flask-JWT-Extended
```bash
pip install Flask-JWT-Extended
```

### Instalar Flask-CORS
```bash
pip install Flask-CORS
```

### Instalar Flask-RESTful
```bash
pip install Flask-RESTful
```

### Instalar Flask-Caching
```bash
pip install Flask-Caching
```

## Comandos de Configuración

### Crear archivo de configuración
```python
# config.py
import os

class Config:
    SECRET_KEY = os.environ.get('SECRET_KEY') or 'dev-secret-key'
    SQLALCHEMY_DATABASE_URI = os.environ.get('DATABASE_URL') or 'sqlite:///app.db'
    SQLALCHEMY_TRACK_MODIFICATIONS = False
```

### Usar configuración desde archivo
```python
# app.py
from flask import Flask
from config import Config

app = Flask(__name__)
app.config.from_object(Config)
```

### Configurar desde variables de entorno
```bash
export SECRET_KEY=your-secret-key
export DATABASE_URL=postgresql://user:pass@localhost/db
export MAIL_SERVER=smtp.gmail.com
export MAIL_PORT=587
```

## Comandos de Logging

### Configurar logging básico
```python
import logging
from logging.handlers import RotatingFileHandler

if not app.debug:
    file_handler = RotatingFileHandler('logs/app.log', maxBytes=10240, backupCount=10)
    file_handler.setFormatter(logging.Formatter(
        '%(asctime)s %(levelname)s: %(message)s [in %(pathname)s:%(lineno)d]'))
    file_handler.setLevel(logging.INFO)
    app.logger.addHandler(file_handler)
    app.logger.setLevel(logging.INFO)
```

### Ver logs en tiempo real
```bash
tail -f logs/app.log
```

## Comandos de Docker

### Crear Dockerfile para Flask
```bash
cat > Dockerfile << EOF
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY . .

CMD ["flask", "run", "--host=0.0.0.0"]
EOF
```

### Construir imagen Docker
```bash
docker build -t flask-app .
```

### Ejecutar contenedor
```bash
docker run -p 5000:5000 flask-app
```

### Docker Compose para Flask
```bash
cat > docker-compose.yml << EOF
version: '3.8'
services:
  web:
    build: .
    ports:
      - "5000:5000"
    environment:
      - FLASK_ENV=development
    volumes:
      - .:/app
  db:
    image: postgres:13
    environment:
      POSTGRES_DB: flaskapp
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
    volumes:
      - postgres_data:/var/lib/postgresql/data/
volumes:
  postgres_data:
EOF
```

### Ejecutar con Docker Compose
```bash
docker-compose up -d
```

## Comandos de Utilidades

### Crear requirements.txt
```bash
pip freeze > requirements.txt
```

### Instalar desde requirements.txt
```bash
pip install -r requirements.txt
```

### Formatear código con Black
```bash
pip install black
black .
```

### Linting con flake8
```bash
pip install flake8
flake8 app.py
```

### Verificar tipos con mypy
```bash
pip install mypy
mypy app.py
```

### Ordenar imports con isort
```bash
pip install isort
isort .
```

## Comandos de Seguridad

### Generar clave secreta
```bash
python -c "import secrets; print(secrets.token_hex(16))"
```

### Hashear contraseña
```bash
python -c "
from werkzeug.security import generate_password_hash
print(generate_password_hash('password'))
"
```

### Verificar contraseña
```bash
python -c "
from werkzeug.security import check_password_hash
hash = 'your-hash-here'
print(check_password_hash(hash, 'password'))
"
```

## Comandos de Performance

### Instalar Flask-Compress
```bash
pip install Flask-Compress
```

### Profiling con Flask-Profiler
```bash
pip install flask-profiler
```

### Monitoring con Flask-MonitoringDashboard
```bash
pip install flask-monitoringdashboard
```

## Comandos de APIs

### Instalar Marshmallow para serialización
```bash
pip install marshmallow flask-marshmallow
```

### Instalar Flasgger para Swagger
```bash
pip install flasgger
```

### Instalar Flask-Limiter para rate limiting
```bash
pip install Flask-Limiter
```

## Comandos de Background Tasks

### Instalar Celery
```bash
pip install celery redis
```

### Ejecutar worker Celery
```bash
celery -A app.celery worker --loglevel=info
```

### Instalar RQ (Redis Queue)
```bash
pip install rq
```

### Ejecutar worker RQ
```bash
rq worker
```

## Comandos de WebSockets

### Instalar Flask-SocketIO
```bash
pip install flask-socketio
```

### Ejecutar con SocketIO
```bash
python app.py
```

## Comandos de Internacionalización

### Instalar Flask-Babel
```bash
pip install Flask-Babel
```

### Extraer strings para traducir
```bash
pybabel extract -F babel.cfg -k _l -o messages.pot .
```

### Crear traducción
```bash
pybabel init -i messages.pot -d app/translations -l es
```

### Actualizar traducciones
```bash
pybabel update -i messages.pot -d app/translations
```

### Compilar traducciones
```bash
pybabel compile -d app/translations
```
