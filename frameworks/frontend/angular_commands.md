# Angular Commands

Angular es una plataforma y framework para construir aplicaciones de una sola página usando HTML y TypeScript. Angular está escrito en TypeScript.

## Instalación

### Instalar Angular CLI globalmente
```bash
npm install -g @angular/cli
```

### Verificar instalación
```bash
ng version
```

### Actualizar Angular CLI
```bash
npm update -g @angular/cli
```

## Creación de Proyectos

### Crear nueva aplicación
```bash
ng new my-app
cd my-app
```

### Crear aplicación con routing
```bash
ng new my-app --routing
```

### Crear aplicación con estilo específico
```bash
ng new my-app --style=scss
ng new my-app --style=sass
ng new my-app --style=less
ng new my-app --style=stylus
```

### Crear aplicación sin tests
```bash
ng new my-app --skip-tests
```

### Crear aplicación con configuración mínima
```bash
ng new my-app --minimal
```

## Comandos de Desarrollo

### Ejecutar servidor de desarrollo
```bash
ng serve
```

### Ejecutar en puerto específico
```bash
ng serve --port 4201
```

### Ejecutar con host específico
```bash
ng serve --host 0.0.0.0
```

### Ejecutar con SSL
```bash
ng serve --ssl
```

### Ejecutar con hot module replacement
```bash
ng serve --hmr
```

### Construir aplicación
```bash
ng build
```

### Construir para producción
```bash
ng build --prod
# o en versiones recientes
ng build --configuration production
```

## Generadores de Angular

### Generar componente
```bash
ng generate component my-component
# o
ng g c my-component
```

### Generar componente sin archivos de test
```bash
ng g c my-component --skip-tests
```

### Generar servicio
```bash
ng generate service my-service
# o
ng g s my-service
```

### Generar módulo
```bash
ng generate module my-module
# o
ng g m my-module
```

### Generar directiva
```bash
ng generate directive my-directive
# o
ng g d my-directive
```

### Generar pipe
```bash
ng generate pipe my-pipe
# o
ng g p my-pipe
```

### Generar guard
```bash
ng generate guard my-guard
# o
ng g g my-guard
```

### Generar interceptor
```bash
ng generate interceptor my-interceptor
```

### Generar resolver
```bash
ng generate resolver my-resolver
```

### Generar clase
```bash
ng generate class my-class
# o
ng g cl my-class
```

### Generar interface
```bash
ng generate interface my-interface
# o
ng g i my-interface
```

### Generar enum
```bash
ng generate enum my-enum
# o
ng g e my-enum
```

## Comandos de Testing

### Ejecutar tests unitarios
```bash
ng test
```

### Ejecutar tests en modo CI
```bash
ng test --watch=false --browsers=ChromeHeadless
```

### Ejecutar tests con coverage
```bash
ng test --code-coverage
```

### Ejecutar tests E2E
```bash
ng e2e
```

### Generar configuración de test específica
```bash
ng generate config karma
```

## Comandos de Linting

### Ejecutar linting
```bash
ng lint
```

### Fix automático de linting
```bash
ng lint --fix
```

## Comandos de Librerías

### Generar librería
```bash
ng generate library my-lib
```

### Construir librería
```bash
ng build my-lib
```

### Publicar librería
```bash
cd dist/my-lib
npm publish
```

### Generar aplicación demo para librería
```bash
ng generate application my-lib-demo
```

## Angular Material

### Instalar Angular Material
```bash
ng add @angular/material
```

### Generar componentes de Material
```bash
ng generate @angular/material:navigation my-nav
ng generate @angular/material:dashboard my-dashboard
ng generate @angular/material:table my-table
ng generate @angular/material:tree my-tree
ng generate @angular/material:drag-drop my-drag-drop
```

## PWA Commands

### Agregar PWA support
```bash
ng add @angular/pwa
```

### Construir PWA
```bash
ng build --prod
```

### Servir PWA localmente
```bash
npm install -g http-server
http-server -p 8080 -c-1 dist/my-app
```

## Angular Universal (SSR)

### Agregar Universal
```bash
ng add @nguniversal/express-engine
```

### Construir para SSR
```bash
npm run build:ssr
```

### Servir SSR
```bash
npm run serve:ssr
```

### Pre-render estático
```bash
npm run prerender
```

## Comandos de Actualización

### Verificar actualizaciones disponibles
```bash
ng update
```

### Actualizar Angular Core
```bash
ng update @angular/core @angular/cli
```

### Actualizar Angular Material
```bash
ng update @angular/material
```

### Actualizar todas las dependencias
```bash
ng update --all
```

## Comandos de Configuración

### Generar archivo de configuración
```bash
ng generate config
```

### Ver configuración de webpack
```bash
ng eject  # Deprecado en versiones recientes
```

### Configurar proxy para desarrollo
```bash
ng serve --proxy-config proxy.conf.json
```

## Internacionalización (i18n)

### Agregar soporte i18n
```bash
ng add @angular/localize
```

### Extraer mensajes para traducir
```bash
ng extract-i18n
```

### Construir para idioma específico
```bash
ng build --localize
```

### Servir con idioma específico
```bash
ng serve --configuration=es
```

## Angular DevKit

### Instalar Schematics
```bash
npm install -g @angular-devkit/schematics-cli
```

### Crear schematic personalizado
```bash
schematics blank --name=my-schematic
```

### Ejecutar schematic
```bash
ng generate my-schematic:my-rule
```

## Deployment

### Construir para producción
```bash
ng build --prod --base-href="/my-app/"
```

### Deploy a GitHub Pages
```bash
ng add angular-cli-ghpages
ng deploy --base-href="/repository-name/"
```

### Deploy a Firebase Hosting
```bash
ng add @angular/fire
ng deploy
```

### Deploy a Netlify
```bash
npm run build
# Subir carpeta dist/ a Netlify
```

## Angular Flex Layout

### Instalar Flex Layout
```bash
ng add @angular/flex-layout
```

## Angular CDK

### Instalar CDK
```bash
ng add @angular/cdk
```

### Generar componentes CDK
```bash
ng generate @angular/cdk:table my-table
ng generate @angular/cdk:tree my-tree
ng generate @angular/cdk:drag-drop my-drag-drop
```

## Estado con NgRx

### Instalar NgRx
```bash
ng add @ngrx/store
ng add @ngrx/effects
ng add @ngrx/store-devtools
```

### Generar store
```bash
ng generate @ngrx/schematics:store State --root --module app.module.ts
```

### Generar feature
```bash
ng generate @ngrx/schematics:feature my-feature --module app.module.ts
```

### Generar effect
```bash
ng generate @ngrx/schematics:effect my-effect --module app.module.ts
```

## Ionic (Móvil)

### Instalar Ionic CLI
```bash
npm install -g @ionic/cli
```

### Crear aplicación Ionic con Angular
```bash
ionic start my-app tabs --type=angular
```

### Ejecutar en navegador
```bash
ionic serve
```

### Construir para móvil
```bash
ionic capacitor build ios
ionic capacitor build android
```

## Electron (Desktop)

### Instalar Electron
```bash
ng add ngx-electron
```

### Ejecutar aplicación Electron
```bash
npm run electron
```

### Construir aplicación Electron
```bash
npm run electron:pack
```

## Comandos de Análisis

### Analizar bundle
```bash
ng build --stats-json
npx webpack-bundle-analyzer dist/my-app/stats.json
```

### Source map explorer
```bash
npm install -g source-map-explorer
ng build --source-map
source-map-explorer dist/my-app/*.js
```

## Comandos de Workspace

### Crear workspace con múltiples proyectos
```bash
ng new my-workspace --create-application=false
cd my-workspace
```

### Agregar aplicación al workspace
```bash
ng generate application my-app
```

### Agregar librería al workspace
```bash
ng generate library my-lib
```

### Ejecutar comando en proyecto específico
```bash
ng serve my-app
ng build my-lib
```

## Scripts de Package.json

### Scripts típicos para Angular
```json
{
  "scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "ng e2e"
  }
}
```

## Debugging

### Debugging en VSCode
```json
{
  "type": "chrome",
  "request": "launch",
  "name": "Launch Chrome against localhost",
  "url": "http://localhost:4200",
  "webRoot": "${workspaceFolder}"
}
```

### Angular DevTools
Extensión del navegador para debugging

### Augury (deprecado)
```bash
# Usar Angular DevTools en su lugar
```

## Comandos de Performance

### Lazy loading de módulos
```bash
ng generate module feature --route feature --module app.module
```

### Service Workers
```bash
ng add @angular/pwa
```

### Preloading strategies
Configurar en el routing module

## Comandos de Migración

### Migrar de AngularJS
```bash
ng add @angular/upgrade
```

### Actualizar de versión mayor
```bash
ng update @angular/core @angular/cli --next
```
