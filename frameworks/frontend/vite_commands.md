# Vite Commands

Vite es una herramienta de build moderna que proporciona un servidor de desarrollo rápido y un bundler optimizado para producción.

## Instalación

### Crear proyecto con Vite
```bash
npm create vite@latest my-project
cd my-project
npm install
```

### Con template específico
```bash
npm create vite@latest my-react-app -- --template react
npm create vite@latest my-vue-app -- --template vue
npm create vite@latest my-svelte-app -- --template svelte
```

### Templates disponibles
```bash
# Vanilla JavaScript
npm create vite@latest my-app -- --template vanilla

# TypeScript
npm create vite@latest my-app -- --template vanilla-ts

# React
npm create vite@latest my-app -- --template react
npm create vite@latest my-app -- --template react-ts

# Vue
npm create vite@latest my-app -- --template vue
npm create vite@latest my-app -- --template vue-ts

# Svelte
npm create vite@latest my-app -- --template svelte
npm create vite@latest my-app -- --template svelte-ts

# Lit
npm create vite@latest my-app -- --template lit
npm create vite@latest my-app -- --template lit-ts

# Preact
npm create vite@latest my-app -- --template preact
npm create vite@latest my-app -- --template preact-ts
```

## Comandos de Desarrollo

### Ejecutar servidor de desarrollo
```bash
npm run dev
```

### Ejecutar en puerto específico
```bash
npm run dev -- --port 3001
```

### Ejecutar con host específico
```bash
npm run dev -- --host 0.0.0.0
```

### Ejecutar con HTTPS
```bash
npm run dev -- --https
```

### Ejecutar con configuración específica
```bash
npm run dev -- --config vite.config.dev.js
```

### Modo debug
```bash
npm run dev -- --debug
```

## Comandos de Build

### Construir para producción
```bash
npm run build
```

### Construir con modo específico
```bash
npm run build -- --mode production
npm run build -- --mode staging
```

### Construir con configuración específica
```bash
npm run build -- --config vite.config.prod.js
```

### Preview de build
```bash
npm run preview
```

### Preview en puerto específico
```bash
npm run preview -- --port 4173
```

## Optimización y Análisis

### Analizar bundle
```bash
npm run build -- --report
```

### Con rollup-plugin-visualizer
```bash
npm install --save-dev rollup-plugin-visualizer
```

### Configurar análisis en vite.config.js
```javascript
import { visualizer } from 'rollup-plugin-visualizer'

export default defineConfig({
  plugins: [
    visualizer({
      filename: 'dist/stats.html',
      open: true
    })
  ]
})
```

## Vite CLI Global

### Instalar Vite CLI globalmente
```bash
npm install -g vite
```

### Crear proyecto
```bash
vite create my-project
```

### Ejecutar desarrollo
```bash
vite
```

### Construir
```bash
vite build
```

### Preview
```bash
vite preview
```

### Optimizar dependencias
```bash
vite optimize
```

## Desarrollo con HMR

### Hot Module Replacement automático
HMR está habilitado por defecto

### Aceptar HMR en módulo específico
```javascript
if (import.meta.hot) {
  import.meta.hot.accept()
}
```

### HMR API
```javascript
if (import.meta.hot) {
  import.meta.hot.accept('./module.js', (newModule) => {
    // Actualizar módulo
  })
  
  import.meta.hot.dispose((data) => {
    // Limpiar recursos
  })
}
```

## Variables de Entorno

### Archivo .env
```bash
# .env
VITE_API_URL=https://api.example.com
VITE_APP_TITLE=My App
```

### Archivos de entorno específicos
```bash
.env                # cargado en todos los casos
.env.local          # cargado en todos los casos, ignorado por git
.env.[mode]         # solo cargado en modo específico
.env.[mode].local   # solo cargado en modo específico, ignorado por git
```

### Usar variables en código
```javascript
console.log(import.meta.env.VITE_API_URL)
console.log(import.meta.env.MODE)
console.log(import.meta.env.DEV)
console.log(import.meta.env.PROD)
```

## Plugins

### Instalar plugins oficiales
```bash
# React
npm install --save-dev @vitejs/plugin-react

# Vue
npm install --save-dev @vitejs/plugin-vue

# Svelte
npm install --save-dev @vitejs/plugin-svelte

# Legacy browser support
npm install --save-dev @vitejs/plugin-legacy
```

### Configurar plugins
```javascript
// vite.config.js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import { resolve } from 'path'

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': resolve(__dirname, 'src')
    }
  }
})
```

## CSS y Preprocessors

### CSS Modules
```css
/* styles.module.css */
.button {
  color: red;
}
```

### Sass/SCSS
```bash
npm install --save-dev sass
```

### Less
```bash
npm install --save-dev less
```

### Stylus
```bash
npm install --save-dev stylus
```

### PostCSS
```bash
npm install --save-dev postcss autoprefixer
```

### Tailwind CSS
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

## Assets y Static Files

### Importar assets
```javascript
import logoUrl from './logo.svg'
import './style.css'
```

### Assets como URL
```javascript
import logoUrl from './logo.svg?url'
```

### Assets como string
```javascript
import logoSvg from './logo.svg?raw'
```

### Assets en carpeta public
```html
<!-- Accesible como /icon.png -->
<img src="/icon.png" alt="Icon" />
```

## TypeScript

### Crear proyecto con TypeScript
```bash
npm create vite@latest my-app -- --template vanilla-ts
```

### Configurar TypeScript
```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true
  },
  "include": ["src"]
}
```

## Testing

### Vitest (recomendado)
```bash
npm install --save-dev vitest
```

### Configurar Vitest
```javascript
// vite.config.js
export default defineConfig({
  test: {
    globals: true,
    environment: 'jsdom'
  }
})
```

### Ejecutar tests
```bash
npm run test
```

### Testing con coverage
```bash
npm install --save-dev @vitest/coverage-c8
npm run test -- --coverage
```

## Server-Side Rendering

### Vite SSR
```bash
# Estructura para SSR
src/
  entry-client.js
  entry-server.js
  main.js
```

### Build SSR
```bash
vite build
vite build --ssr src/entry-server.js
```

## Multi-Page Applications

### Configurar múltiples entry points
```javascript
// vite.config.js
export default defineConfig({
  build: {
    rollupOptions: {
      input: {
        main: resolve(__dirname, 'index.html'),
        nested: resolve(__dirname, 'nested/index.html')
      }
    }
  }
})
```

## Library Mode

### Construir como librería
```javascript
// vite.config.js
export default defineConfig({
  build: {
    lib: {
      entry: resolve(__dirname, 'lib/main.js'),
      name: 'MyLib',
      fileName: 'my-lib'
    },
    rollupOptions: {
      external: ['vue'],
      output: {
        globals: {
          vue: 'Vue'
        }
      }
    }
  }
})
```

## Proxy y CORS

### Configurar proxy
```javascript
// vite.config.js
export default defineConfig({
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:3001',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, '')
      }
    }
  }
})
```

### CORS headers
```javascript
export default defineConfig({
  server: {
    cors: true,
    headers: {
      'Access-Control-Allow-Origin': '*'
    }
  }
})
```

## Performance

### Pre-bundling de dependencias
```javascript
export default defineConfig({
  optimizeDeps: {
    include: ['lodash'],
    exclude: ['heavy-lib']
  }
})
```

### Code splitting
```javascript
// Dinámico
const module = await import('./module.js')

// Manual chunks
export default defineConfig({
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom'],
          utils: ['lodash']
        }
      }
    }
  }
})
```

## Docker

### Dockerfile para Vite
```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=0 /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### Docker multi-stage para desarrollo
```dockerfile
FROM node:18-alpine as dev
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
EXPOSE 5173
CMD ["npm", "run", "dev", "--", "--host"]
```

## Deployment

### Netlify
```bash
npm run build
# Subir carpeta dist/
```

### Vercel
```bash
npm install -g vercel
vercel
```

### GitHub Pages
```bash
npm install --save-dev gh-pages
```

### Build y deploy script
```json
{
  "scripts": {
    "deploy": "npm run build && gh-pages -d dist"
  }
}
```

### Configurar base path
```javascript
// vite.config.js
export default defineConfig({
  base: '/my-repo-name/'
})
```

## Scripts de Package.json

### Scripts típicos para Vite
```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "test": "vitest",
    "test:ui": "vitest --ui",
    "lint": "eslint . --ext js,jsx,ts,tsx",
    "format": "prettier --write ."
  }
}
```

## Debugging

### Source maps
```javascript
export default defineConfig({
  build: {
    sourcemap: true
  }
})
```

### Debug en VSCode
```json
{
  "type": "chrome",
  "request": "launch",
  "name": "Launch Chrome",
  "url": "http://localhost:5173",
  "webRoot": "${workspaceFolder}"
}
```

## Configuración Avanzada

### Vite config completo
```javascript
import { defineConfig, loadEnv } from 'vite'
import react from '@vitejs/plugin-react'
import { resolve } from 'path'

export default defineConfig(({ command, mode }) => {
  const env = loadEnv(mode, process.cwd(), '')
  
  return {
    plugins: [react()],
    define: {
      __APP_VERSION__: JSON.stringify(process.env.npm_package_version)
    },
    resolve: {
      alias: {
        '@': resolve(__dirname, 'src'),
        '~': resolve(__dirname, 'src')
      }
    },
    server: {
      port: 3000,
      open: true,
      cors: true
    },
    build: {
      outDir: 'dist',
      assetsDir: 'assets',
      sourcemap: command === 'serve',
      minify: 'terser',
      rollupOptions: {
        output: {
          chunkFileNames: 'js/[name]-[hash].js',
          entryFileNames: 'js/[name]-[hash].js',
          assetFileNames: 'assets/[name]-[hash].[ext]'
        }
      }
    }
  }
})
```
