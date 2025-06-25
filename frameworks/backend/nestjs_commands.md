# NestJS Commands

NestJS es un framework de Node.js para construir aplicaciones del lado del servidor eficientes y escalables. Está construido con TypeScript y combina elementos de OOP, FP y FRP.

## Instalación

### Instalar NestJS CLI globalmente
```bash
npm install -g @nestjs/cli
```

### Verificar instalación
```bash
nest --version
```

### Actualizar NestJS CLI
```bash
npm update -g @nestjs/cli
```

## Creación de Proyectos

### Crear nueva aplicación
```bash
nest new my-app
```

### Crear aplicación con npm
```bash
nest new my-app --package-manager npm
```

### Crear aplicación con yarn
```bash
nest new my-app --package-manager yarn
```

### Crear aplicación con pnpm
```bash
nest new my-app --package-manager pnpm
```

### Crear aplicación sin git
```bash
nest new my-app --skip-git
```

## Comandos de Desarrollo

### Ejecutar en modo desarrollo
```bash
npm run start:dev
```

### Ejecutar en modo debug
```bash
npm run start:debug
```

### Ejecutar en modo producción
```bash
npm run start:prod
```

### Ejecutar con watch mode
```bash
nest start --watch
```

### Ejecutar con debug mode
```bash
nest start --debug
```

## Generadores de NestJS

### Generar módulo
```bash
nest generate module users
# o
nest g module users
```

### Generar controlador
```bash
nest generate controller users
nest g controller users --no-spec  # Sin archivos de test
```

### Generar servicio
```bash
nest generate service users
nest g service users --no-spec
```

### Generar provider
```bash
nest generate provider users
```

### Generar guard
```bash
nest generate guard auth
```

### Generar interceptor
```bash
nest generate interceptor logging
```

### Generar middleware
```bash
nest generate middleware logger
```

### Generar pipe
```bash
nest generate pipe validation
```

### Generar filter
```bash
nest generate filter http-exception
```

### Generar decorator
```bash
nest generate decorator roles
```

### Generar gateway (WebSocket)
```bash
nest generate gateway chat
```

### Generar resolver (GraphQL)
```bash
nest generate resolver users
```

### Generar biblioteca
```bash
nest generate library my-lib
```

### Generar sub-aplicación
```bash
nest generate sub-app my-sub-app
```

### Generar recurso completo (CRUD)
```bash
nest generate resource users
```

## Comandos de Construcción

### Construir aplicación
```bash
npm run build
```

### Construir con webpack
```bash
nest build --webpack
```

### Construir aplicación específica
```bash
nest build my-app
```

### Construir con watch mode
```bash
nest build --watch
```

## Comandos de Testing

### Ejecutar tests unitarios
```bash
npm run test
```

### Ejecutar tests en watch mode
```bash
npm run test:watch
```

### Ejecutar tests e2e
```bash
npm run test:e2e
```

### Ejecutar tests con coverage
```bash
npm run test:cov
```

### Ejecutar tests específicos
```bash
npm run test -- users.service.spec.ts
```

### Ejecutar tests con debug
```bash
npm run test:debug
```

## Comandos de Información

### Ver información del proyecto
```bash
nest info
```

### Listar todos los comandos
```bash
nest --help
```

### Ver información de comando específico
```bash
nest generate --help
```

## Comandos de Base de Datos

### Instalar TypeORM
```bash
npm install @nestjs/typeorm typeorm mysql2
```

### Instalar Prisma
```bash
npm install @nestjs/prisma prisma
npx prisma init
```

### Instalar Mongoose
```bash
npm install @nestjs/mongoose mongoose
```

### Ejecutar migraciones TypeORM
```bash
npm run typeorm migration:run
```

### Crear migración TypeORM
```bash
npm run typeorm migration:create -- -n CreateUserTable
```

### Generar migración TypeORM
```bash
npm run typeorm migration:generate -- -n UserTable
```

### Revertir migración TypeORM
```bash
npm run typeorm migration:revert
```

### Prisma generate
```bash
npx prisma generate
```

### Prisma migrate
```bash
npx prisma migrate dev
```

### Prisma studio
```bash
npx prisma studio
```

## Comandos de Microservicios

### Generar aplicación de microservicio
```bash
nest new my-microservice
```

### Instalar transporte de microservicios
```bash
npm install @nestjs/microservices
```

### Instalar Redis para microservicios
```bash
npm install redis
```

### Instalar NATS para microservicios
```bash
npm install nats
```

### Instalar RabbitMQ para microservicios
```bash
npm install amqplib amqp-connection-manager
```

## Comandos de GraphQL

### Instalar GraphQL
```bash
npm install @nestjs/graphql @nestjs/apollo graphql apollo-server-express
```

### Generar esquema GraphQL
```bash
npm run generate:graphql
```

### Instalar herramientas de GraphQL
```bash
npm install @nestjs/graphql graphql-tools graphql
```

## Comandos de Swagger/OpenAPI

### Instalar Swagger
```bash
npm install @nestjs/swagger swagger-ui-express
```

### Generar documentación
```bash
# La documentación se genera automáticamente en /api
```

## Comandos de Autenticación

### Instalar Passport
```bash
npm install @nestjs/passport passport passport-local
npm install @types/passport-local --save-dev
```

### Instalar JWT
```bash
npm install @nestjs/jwt passport-jwt
npm install @types/passport-jwt --save-dev
```

### Instalar bcrypt
```bash
npm install bcrypt
npm install @types/bcrypt --save-dev
```

## Comandos de Validación

### Instalar class-validator
```bash
npm install class-validator class-transformer
```

### Instalar Joi
```bash
npm install joi
npm install @types/joi --save-dev
```

## Comandos de Configuración

### Instalar módulo de configuración
```bash
npm install @nestjs/config
```

### Instalar dotenv
```bash
npm install dotenv
```

### Validar configuración con Joi
```bash
npm install joi
```

## Comandos de Logging

### Usar logger integrado
```bash
# NestJS incluye un logger por defecto
```

### Instalar Winston
```bash
npm install winston nest-winston
```

### Instalar Pino
```bash
npm install pino nestjs-pino pino-pretty
```

## Comandos de Cache

### Instalar cache manager
```bash
npm install cache-manager
npm install @types/cache-manager --save-dev
```

### Instalar Redis para cache
```bash
npm install cache-manager-redis-store redis
```

## Comandos de Scheduling

### Instalar cron jobs
```bash
npm install @nestjs/schedule
```

### Instalar node-cron
```bash
npm install node-cron
npm install @types/node-cron --save-dev
```

## Comandos de File Upload

### Instalar multer
```bash
npm install @nestjs/platform-express multer
npm install @types/multer --save-dev
```

### Instalar sharp para procesamiento de imágenes
```bash
npm install sharp
```

## Comandos de WebSockets

### Instalar WebSocket
```bash
npm install @nestjs/websockets @nestjs/platform-socket.io
```

### Instalar Socket.io
```bash
npm install socket.io
```

## Comandos de Server-Sent Events

### Instalar SSE
```bash
# SSE está incluido en NestJS core
```

## Comandos de Deployment

### Instalar PM2
```bash
npm install -g pm2
```

### Ejecutar con PM2
```bash
pm2 start dist/main.js --name "my-app"
```

### Crear archivo de ecosistema PM2
```bash
pm2 ecosystem
```

### Instalar herramientas de Docker
```bash
# Crear Dockerfile
cat > Dockerfile << EOF
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY dist ./dist
CMD ["node", "dist/main"]
EOF
```

## Comandos de Monitoreo

### Instalar Prometheus
```bash
npm install @willsoto/nestjs-prometheus prom-client
```

### Instalar health check
```bash
npm install @nestjs/terminus
```

### Instalar métricas
```bash
npm install @nestjs/metrics
```

## Comandos de Utilidades

### Formatear código con Prettier
```bash
npm run format
```

### Linting con ESLint
```bash
npm run lint
```

### Fix de linting
```bash
npm run lint:fix
```

### Pre-commit hooks
```bash
npm install husky lint-staged --save-dev
```

## Scripts de Package.json

```json
{
  "scripts": {
    "prebuild": "rimraf dist",
    "build": "nest build",
    "format": "prettier --write \"src/**/*.ts\" \"test/**/*.ts\"",
    "start": "nest start",
    "start:dev": "nest start --watch",
    "start:debug": "nest start --debug --watch",
    "start:prod": "node dist/main",
    "lint": "eslint \"{src,apps,libs,test}/**/*.ts\" --fix",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:cov": "jest --coverage",
    "test:debug": "node --inspect-brk -r tsconfig-paths/register -r ts-node/register node_modules/.bin/jest --runInBand",
    "test:e2e": "jest --config ./test/jest-e2e.json"
  }
}
```
