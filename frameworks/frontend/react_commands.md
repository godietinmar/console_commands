# React Commands

React es una biblioteca de JavaScript para construir interfaces de usuario, especialmente aplicaciones web de una sola página donde necesitas un manejo rápido e interactivo de datos.

## Instalación

### Crear nueva aplicación React
```bash
npx create-react-app my-app
cd my-app
```

### Crear aplicación con TypeScript
```bash
npx create-react-app my-app --template typescript
```

### Crear aplicación con template específico
```bash
npx create-react-app my-app --template redux
npx create-react-app my-app --template redux-typescript
```

### Instalar React en proyecto existente
```bash
npm install react react-dom
npm install --save-dev @types/react @types/react-dom  # Para TypeScript
```

## Comandos de Desarrollo

### Iniciar servidor de desarrollo
```bash
npm start
```

### Ejecutar en puerto específico
```bash
PORT=3001 npm start
```

### Ejecutar con HTTPS
```bash
HTTPS=true npm start
```

### Construir para producción
```bash
npm run build
```

### Ejecutar tests
```bash
npm test
```

### Ejecutar tests sin watch mode
```bash
CI=true npm test
```

### Ejecutar tests con coverage
```bash
npm test -- --coverage
```

### Eject (exponer configuración)
```bash
npm run eject
```

## Comandos con Vite (alternativa moderna)

### Crear proyecto React con Vite
```bash
npm create vite@latest my-react-app -- --template react
cd my-react-app
npm install
```

### Con TypeScript
```bash
npm create vite@latest my-react-app -- --template react-ts
```

### Ejecutar desarrollo con Vite
```bash
npm run dev
```

### Construir con Vite
```bash
npm run build
```

### Preview de build
```bash
npm run preview
```

## Herramientas de Desarrollo

### Instalar React Developer Tools (extensión del navegador)
Disponible para Chrome y Firefox

### Instalar Storybook
```bash
npx storybook@latest init
```

### Ejecutar Storybook
```bash
npm run storybook
```

### Construir Storybook
```bash
npm run build-storybook
```

## Librerías Populares de React

### React Router (enrutamiento)
```bash
npm install react-router-dom
npm install --save-dev @types/react-router-dom  # Para TypeScript
```

### Redux (gestión de estado)
```bash
npm install @reduxjs/toolkit react-redux
npm install --save-dev @types/react-redux  # Para TypeScript
```

### Material-UI (componentes UI)
```bash
npm install @mui/material @emotion/react @emotion/styled
```

### Styled Components
```bash
npm install styled-components
npm install --save-dev @types/styled-components  # Para TypeScript
```

### Formik (formularios)
```bash
npm install formik yup
```

### React Hook Form
```bash
npm install react-hook-form
```

### Axios (cliente HTTP)
```bash
npm install axios
```

### React Query (gestión de estado del servidor)
```bash
npm install @tanstack/react-query
```

### Zustand (gestión de estado)
```bash
npm install zustand
```

## Testing

### Instalar Testing Library adicional
```bash
npm install --save-dev @testing-library/user-event
npm install --save-dev @testing-library/jest-dom
```

### Instalar Enzyme (alternativa)
```bash
npm install --save-dev enzyme @wojtekmaj/enzyme-adapter-react-17
```

### Ejecutar tests específicos
```bash
npm test -- --testNamePattern="MyComponent"
```

### Ejecutar tests de un archivo
```bash
npm test -- MyComponent.test.js
```

## Linting y Formateo

### Instalar ESLint
```bash
npm install --save-dev eslint eslint-plugin-react
npx eslint --init
```

### Ejecutar ESLint
```bash
npx eslint src/
```

### Instalar Prettier
```bash
npm install --save-dev prettier
```

### Formatear código
```bash
npx prettier --write src/
```

### Instalar Husky para pre-commit hooks
```bash
npm install --save-dev husky lint-staged
npx husky install
```

## Deployment

### Construir para producción
```bash
npm run build
```

### Servir build localmente
```bash
npm install -g serve
serve -s build
```

### Deploy a Netlify
```bash
npm install -g netlify-cli
netlify deploy --prod --dir=build
```

### Deploy a Vercel
```bash
npm install -g vercel
vercel --prod
```

### Deploy a GitHub Pages
```bash
npm install --save-dev gh-pages
```

### Agregar script de deploy
```json
{
  "scripts": {
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build"
  }
}
```

## Optimización

### Analizar bundle
```bash
npm install --save-dev webpack-bundle-analyzer
npm run build
npx webpack-bundle-analyzer build/static/js/*.js
```

### Con Vite Bundle Analyzer
```bash
npm install --save-dev rollup-plugin-visualizer
```

### Code splitting automático
React ya incluye code splitting con `React.lazy()`

### Memoización
Usar `React.memo()`, `useMemo()`, `useCallback()`

## React Native (móvil)

### Instalar React Native CLI
```bash
npm install -g @react-native-community/cli
```

### Crear proyecto React Native
```bash
npx react-native init MyApp
```

### Ejecutar en iOS
```bash
npx react-native run-ios
```

### Ejecutar en Android
```bash
npx react-native run-android
```

### Con Expo
```bash
npm install -g @expo/cli
npx create-expo-app MyApp
cd MyApp
npx expo start
```

## Next.js (React con SSR)

### Crear aplicación Next.js
```bash
npx create-next-app@latest my-app
cd my-app
```

### Con TypeScript
```bash
npx create-next-app@latest my-app --typescript
```

### Ejecutar desarrollo
```bash
npm run dev
```

### Construir para producción
```bash
npm run build
```

### Iniciar en producción
```bash
npm start
```

## Herramientas de Build Alternativas

### Parcel
```bash
npm install -g parcel-bundler
parcel index.html
```

### Webpack (manual)
```bash
npm install --save-dev webpack webpack-cli webpack-dev-server
```

### Rollup
```bash
npm install --save-dev rollup
```

## Debugging

### React DevTools Profiler
Usar la pestaña "Profiler" en React DevTools

### Source maps en desarrollo
Habilitado por defecto en Create React App

### Debug en VSCode
Configurar `.vscode/launch.json` para debugging

## Comandos Útiles de Package.json

### Scripts típicos para React
```json
{
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "lint": "eslint src/",
    "lint:fix": "eslint src/ --fix",
    "format": "prettier --write src/"
  }
}
```

## Actualización de Dependencias

### Verificar dependencias desactualizadas
```bash
npm outdated
```

### Actualizar React
```bash
npm update react react-dom
```

### Actualizar Create React App
```bash
npm install react-scripts@latest
```

## Micro-frontends

### Module Federation (Webpack 5)
```bash
npm install --save-dev @module-federation/webpack
```

### Single-SPA
```bash
npm install single-spa
```
