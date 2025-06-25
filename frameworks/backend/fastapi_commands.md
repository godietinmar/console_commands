# FastAPI Commands

FastAPI es un framework web moderno y de alto rendimiento para construir APIs con Python 3.7+ basado en hints de tipo estándar de Python.

## Instalación

### Instalar FastAPI
```bash
pip install fastapi
```

### Instalar con servidor ASGI
```bash
pip install "fastapi[all]"
# O específicamente
pip install fastapi uvicorn
```

### Instalar en entorno virtual
```bash
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate
pip install fastapi uvicorn
```

## Comandos de Desarrollo

### Ejecutar servidor de desarrollo
```bash
uvicorn main:app --reload
```

### Ejecutar en puerto específico
```bash
uvicorn main:app --reload --port 8080
```

### Ejecutar en host específico
```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### Ejecutar con log level específico
```bash
uvicorn main:app --reload --log-level debug
```

### Ejecutar con múltiples workers
```bash
uvicorn main:app --workers 4
```

### Ejecutar con Gunicorn + Uvicorn
```bash
pip install gunicorn
gunicorn main:app -w 4 -k uvicorn.workers.UvicornWorker
```

## Comandos de Proyecto

### Crear estructura básica
```bash
mkdir my-fastapi-app
cd my-fastapi-app
touch main.py requirements.txt
```

### Crear archivo requirements.txt típico
```bash
cat > requirements.txt << EOF
fastapi>=0.68.0,<0.69.0
uvicorn[standard]>=0.15.0,<0.16.0
python-multipart
python-jose[cryptography]
passlib[bcrypt]
python-decouple
SQLAlchemy
psycopg2-binary
alembic
EOF
```

### Instalar dependencias
```bash
pip install -r requirements.txt
```

## Comandos de Base de Datos con Alembic

### Instalar Alembic
```bash
pip install alembic
```

### Inicializar Alembic
```bash
alembic init alembic
```

### Crear migración
```bash
alembic revision -m "Create users table"
```

### Generar migración automática
```bash
alembic revision --autogenerate -m "Add user table"
```

### Aplicar migraciones
```bash
alembic upgrade head
```

### Revertir migración
```bash
alembic downgrade -1
```

### Ver historial de migraciones
```bash
alembic history
```

### Ver migración actual
```bash
alembic current
```

## Testing

### Instalar pytest y dependencias de testing
```bash
pip install pytest pytest-asyncio httpx
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
pytest tests/test_main.py
pytest -k "test_user"
```

### Ejecutar tests en modo verbose
```bash
pytest -v
```

### Ejecutar tests con output
```bash
pytest -s
```

## Comandos de Documentación

### Generar documentación automática
FastAPI genera automáticamente:
- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`
- OpenAPI JSON: `http://localhost:8000/openapi.json`

### Exportar esquema OpenAPI
```bash
python -c "
import json
from main import app
with open('openapi.json', 'w') as f:
    json.dump(app.openapi(), f, indent=2)
"
```

## Comandos de Desarrollo con Docker

### Crear Dockerfile
```bash
cat > Dockerfile << EOF
FROM python:3.9

WORKDIR /code

COPY ./requirements.txt /code/requirements.txt

RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

COPY ./app /code/app

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]
EOF
```

### Construir imagen Docker
```bash
docker build -t my-fastapi-app .
```

### Ejecutar contenedor
```bash
docker run -d --name fastapi-container -p 80:80 my-fastapi-app
```

### Docker Compose
```bash
cat > docker-compose.yml << EOF
version: '3.8'
services:
  web:
    build: .
    ports:
      - "8000:80"
    environment:
      - DATABASE_URL=postgresql://user:password@db:5432/mydb
    depends_on:
      - db
  db:
    image: postgres:13
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb
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

## Comandos de Seguridad

### Instalar dependencias de seguridad
```bash
pip install python-jose[cryptography] passlib[bcrypt] python-multipart
```

### Generar clave secreta
```bash
openssl rand -hex 32
```

### Crear hash de contraseña
```bash
python -c "
from passlib.context import CryptContext
pwd_context = CryptContext(schemes=['bcrypt'], deprecated='auto')
print(pwd_context.hash('mysecretpassword'))
"
```

## Comandos de Deployment

### Instalar para producción
```bash
pip install gunicorn uvicorn[standard]
```

### Ejecutar con Gunicorn
```bash
gunicorn main:app -w 4 -k uvicorn.workers.UvicornWorker --bind 0.0.0.0:8000
```

### Configurar variables de entorno
```bash
export ENVIRONMENT=production
export SECRET_KEY=your-secret-key
export DATABASE_URL=postgresql://user:pass@localhost/db
```

### Crear archivo .env
```bash
cat > .env << EOF
ENVIRONMENT=development
SECRET_KEY=your-secret-key-here
DATABASE_URL=sqlite:///./test.db
FIRST_SUPERUSER=admin@example.com
FIRST_SUPERUSER_PASSWORD=changethis
EOF
```

## Comandos de Optimización

### Instalar dependencias de performance
```bash
pip install uvloop httptools
```

### Ejecutar con optimizaciones
```bash
uvicorn main:app --loop uvloop --http httptools
```

### Profiling con cProfile
```bash
python -m cProfile -o profile.stats main.py
```

### Instalar herramientas de monitoring
```bash
pip install prometheus-fastapi-instrumentator
```

## Comandos de Utilidades

### Formatear código con Black
```bash
pip install black
black .
```

### Verificar tipos con mypy
```bash
pip install mypy
mypy app/
```

### Linting con flake8
```bash
pip install flake8
flake8 app/
```

### Ordenar imports con isort
```bash
pip install isort
isort .
```

### Pre-commit hooks
```bash
pip install pre-commit
pre-commit install
```

## Comandos de Base de Datos

### SQLAlchemy con PostgreSQL
```bash
pip install sqlalchemy psycopg2-binary
```

### SQLAlchemy con MySQL
```bash
pip install sqlalchemy pymysql
```

### SQLAlchemy con SQLite
```bash
pip install sqlalchemy
```

### MongoDB con Motor
```bash
pip install motor
```

### Redis
```bash
pip install redis aioredis
```

## Comandos de Middleware

### Instalar middleware de CORS
```bash
pip install python-multipart
```

### Middleware de compresión
```bash
pip install python-multipart
```

### Middleware de rate limiting
```bash
pip install slowapi
```

## Comandos de WebSockets

### Ejecutar con soporte WebSocket
```bash
pip install websockets
uvicorn main:app --reload
```

### Testing WebSockets
```bash
pip install websockets pytest-asyncio
```

## Comandos de Background Tasks

### Instalar Celery para tasks
```bash
pip install celery redis
```

### Ejecutar worker Celery
```bash
celery -A main.celery worker --loglevel=info
```

### Instalar APScheduler
```bash
pip install apscheduler
```
