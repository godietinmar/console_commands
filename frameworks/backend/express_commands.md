# Express.js Commands

Express.js es un framework web minimalista y flexible para Node.js que proporciona un conjunto robusto de características para aplicaciones web y móviles.

## Instalación

### Instalar Express globalmente
```bash
npm install -g express-generator
```

### Crear nueva aplicación Express
```bash
express myapp
cd myapp
npm install
```

### Instalar Express en proyecto existente
```bash
npm install express --save
```

### Instalar Express con TypeScript
```bash
npm install express @types/express --save
npm install typescript ts-node @types/node --save-dev
```

## Comandos de Desarrollo

### Iniciar servidor de desarrollo
```bash
npm start
```

### Iniciar con nodemon (auto-reload)
```bash
npm install -g nodemon
nodemon app.js
```

### Iniciar en modo debug
```bash
DEBUG=myapp:* npm start
```

### Iniciar en puerto específico
```bash
PORT=8080 npm start
```

## Generadores de Express

### Generar aplicación básica
```bash
express --view=pug myapp
```

### Generar con motor de plantillas específico
```bash
express --view=ejs myapp
express --view=hbs myapp
express --view=hogan myapp
```

### Generar con CSS preprocessor
```bash
express --css=sass myapp
express --css=less myapp
express --css=stylus myapp
```

### Generar estructura completa
```bash
express --view=ejs --css=sass --git myapp
```

## Middlewares Comunes

### Instalar middleware de logging
```bash
npm install morgan --save
```

### Instalar middleware de parsing
```bash
npm install body-parser --save
npm install cookie-parser --save
```

### Instalar middleware de seguridad
```bash
npm install helmet --save
npm install cors --save
```

### Instalar middleware de sesiones
```bash
npm install express-session --save
```

### Instalar middleware de archivos estáticos
```bash
npm install serve-static --save
```

## Testing

### Instalar herramientas de testing
```bash
npm install --save-dev mocha chai supertest
```

### Ejecutar tests
```bash
npm test
```

### Ejecutar tests con coverage
```bash
npm install --save-dev nyc
npm run test:coverage
```

## Deployment

### Instalar PM2 para producción
```bash
npm install -g pm2
pm2 start app.js
pm2 status
pm2 restart app
pm2 stop app
pm2 delete app
```

### Configurar variables de entorno
```bash
export NODE_ENV=production
export PORT=3000
```

### Crear archivo ecosystem para PM2
```bash
pm2 ecosystem
```

## Utilidades de Desarrollo

### Instalar ESLint
```bash
npm install --save-dev eslint
npx eslint --init
```

### Instalar Prettier
```bash
npm install --save-dev prettier
```

### Instalar herramientas de desarrollo
```bash
npm install --save-dev concurrently
npm install --save-dev cross-env
```

## Comandos de Package.json

### Scripts típicos para Express
```json
{
  "scripts": {
    "start": "node ./bin/www",
    "dev": "nodemon ./bin/www",
    "test": "mocha test/**/*.js",
    "lint": "eslint .",
    "format": "prettier --write ."
  }
}
```

## Comandos de Base de Datos

### Instalar drivers de base de datos
```bash
# MongoDB
npm install mongoose --save

# MySQL
npm install mysql2 --save

# PostgreSQL
npm install pg --save

# SQLite
npm install sqlite3 --save
```

## Optimización

### Instalar compression middleware
```bash
npm install compression --save
```

### Instalar rate limiting
```bash
npm install express-rate-limit --save
```

### Analizar bundle
```bash
npm install --save-dev webpack-bundle-analyzer
```
