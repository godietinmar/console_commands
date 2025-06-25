# Svelte Commands

Svelte es un framework de JavaScript que compila componentes en JavaScript vanilla eficiente, eliminando la necesidad de un virtual DOM.

## Instalación

### Crear aplicación Svelte con Vite
```bash
npm create svelte@latest my-app
cd my-app
npm install
```

### Crear aplicación con template específico
```bash
npm create svelte@latest my-app
# Opciones durante la creación:
# - Skeleton project, SvelteKit demo app, Library project
# - TypeScript, ESLint, Prettier, Playwright, Vitest
```

### Crear aplicación básica con degit
```bash
npx degit sveltejs/template my-app
cd my-app
npm install
```

### Con TypeScript
```bash
npx degit sveltejs/template my-app
cd my-app
node scripts/setupTypeScript.js
npm install
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

### Construir para producción
```bash
npm run build
```

### Preview de build
```bash
npm run preview
```

## SvelteKit Commands

### Crear aplicación SvelteKit
```bash
npm create svelte@latest my-app
cd my-app
npm install
```

### Ejecutar desarrollo
```bash
npm run dev
```

### Construir SvelteKit
```bash
npm run build
```

### Preview SvelteKit
```bash
npm run preview
```

### Sincronizar tipos
```bash
npm run sync
```

### Generar tipos
```bash
npm run check
```

## Comandos de Testing

### Instalar Jest
```bash
npm install --save-dev jest @testing-library/svelte @testing-library/jest-dom
```

### Instalar Vitest (recomendado)
```bash
npm install --save-dev vitest @testing-library/svelte jsdom
```

### Ejecutar tests
```bash
npm run test
```

### Ejecutar tests con coverage
```bash
npm run test -- --coverage
```

### Testing E2E con Playwright
```bash
npm install --save-dev @playwright/test
```

### Ejecutar tests E2E
```bash
npm run test:e2e
```

## Linting y Formateo

### Configurar ESLint
```bash
npm install --save-dev eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-plugin-svelte3
```

### Ejecutar ESLint
```bash
npm run lint
```

### Configurar Prettier
```bash
npm install --save-dev prettier prettier-plugin-svelte
```

### Formatear código
```bash
npm run format
```

## Svelte Components y Stores

### Crear store
```javascript
// stores.js
import { writable } from 'svelte/store';
export const count = writable(0);
```

### Usar store en componente
```svelte
<script>
  import { count } from './stores.js';
</script>

<button on:click={() => $count++}>
  Count: {$count}
</button>
```

### Stores derivados
```javascript
import { derived } from 'svelte/store';
export const doubled = derived(count, $count => $count * 2);
```

## Routing

### SvelteKit routing (file-based)
```bash
# Crear archivo en src/routes/about/+page.svelte
mkdir src/routes/about
touch src/routes/about/+page.svelte
```

### Page routing
```bash
# src/routes/+page.svelte -> /
# src/routes/about/+page.svelte -> /about
# src/routes/blog/[slug]/+page.svelte -> /blog/[slug]
```

### Svelte Routing (SPA)
```bash
npm install svelte-routing
```

### Page.js routing
```bash
npm install page
```

## UI Libraries

### Svelte Material UI
```bash
npm install @smui/button @smui/card @smui/textfield
```

### Carbon Components Svelte
```bash
npm install carbon-components-svelte
```

### Sveltestrap (Bootstrap)
```bash
npm install sveltestrap
```

### Smelte (Material Design)
```bash
npm install smelte
```

### Svelte UI
```bash
npm install @svelteuidev/core
```

## Animation

### Svelte transitions (built-in)
```svelte
<script>
  import { fade, slide, fly } from 'svelte/transition';
</script>

<div transition:fade>Content</div>
```

### Svelte animations
```svelte
<script>
  import { flip } from 'svelte/animate';
</script>
```

## Preprocessors

### PostCSS
```bash
npm install --save-dev postcss autoprefixer
```

### Sass/SCSS
```bash
npm install --save-dev sass
```

### Less
```bash
npm install --save-dev less
```

### TypeScript
```bash
npm install --save-dev typescript
```

## Deployment

### Construir para producción
```bash
npm run build
```

### Deploy estático
```bash
npm install -g serve
serve -s public
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

### Deploy SvelteKit a Vercel
```bash
npm install -D @sveltejs/adapter-vercel
```

### Deploy SvelteKit a Netlify
```bash
npm install -D @sveltejs/adapter-netlify
```

### Deploy SvelteKit a Node.js
```bash
npm install -D @sveltejs/adapter-node
```

## SvelteKit Adapters

### Adapter estático
```bash
npm install -D @sveltejs/adapter-static
```

### Adapter de Node.js
```bash
npm install -D @sveltejs/adapter-node
```

### Adapter de Cloudflare Pages
```bash
npm install -D @sveltejs/adapter-cloudflare-workers
```

### Adapter de AWS Lambda
```bash
npm install -D @sveltejs/adapter-aws
```

## Mobile Development

### Capacitor
```bash
npm install @capacitor/core @capacitor/cli
npx cap init
```

### Tauri (desktop)
```bash
npm install -D @tauri-apps/cli
```

### Cordova
```bash
npm install -g cordova
cordova create myapp
```

## State Management

### Svelte stores (built-in)
```javascript
import { writable, readable, derived } from 'svelte/store';
```

### Overmind
```bash
npm install overmind
```

### Zustand
```bash
npm install zustand
```

## Development Tools

### Svelte DevTools
Extensión del navegador

### Svelte Language Server
```bash
npm install -g svelte-language-server
```

### Svelte VSCode Extension
Instalar desde VSCode Marketplace

## Bundle Analysis

### Rollup Bundle Analyzer
```bash
npm install --save-dev rollup-plugin-analyzer
```

### Vite Bundle Analyzer
```bash
npm install --save-dev rollup-plugin-visualizer
```

## Performance

### Svelte compiler optimizations
Incluido por defecto

### Code splitting
```javascript
// Lazy loading de componentes
const LazyComponent = () => import('./LazyComponent.svelte');
```

### Tree shaking
Automático con bundlers modernos

## Svelte Native (Mobile)

### Instalar Svelte Native
```bash
npm install -g @nativescript/cli
tns create myApp --svelte
```

### Ejecutar en emulador
```bash
tns run android
tns run ios
```

## Electron (Desktop)

### Electron con Svelte
```bash
npm install --save-dev electron
```

### Electron Builder
```bash
npm install --save-dev electron-builder
```

## Debugging

### Chrome DevTools
Usar source maps para debugging

### Svelte DevTools
Extensión específica para Svelte

### VSCode debugging
```json
{
  "type": "chrome",
  "request": "launch",
  "name": "Launch Chrome against localhost",
  "url": "http://localhost:5000",
  "webRoot": "${workspaceFolder}"
}
```

## Scripts de Package.json

### Scripts típicos para Svelte
```json
{
  "scripts": {
    "dev": "vite dev",
    "build": "vite build",
    "preview": "vite preview",
    "test": "vitest",
    "check": "svelte-kit sync && svelte-check --tsconfig ./tsconfig.json",
    "check:watch": "svelte-kit sync && svelte-check --tsconfig ./tsconfig.json --watch",
    "lint": "prettier --plugin-search-dir . --check .",
    "format": "prettier --plugin-search-dir . --write ."
  }
}
```

### Scripts para Svelte clásico
```json
{
  "scripts": {
    "build": "rollup -c",
    "dev": "rollup -c -w",
    "start": "sirv public --no-clear",
    "check": "svelte-check --tsconfig ./tsconfig.json"
  }
}
```

## Storybook

### Instalar Storybook para Svelte
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

## Optimización

### Svelte compiler optimizations
```javascript
// svelte.config.js
export default {
  compilerOptions: {
    dev: false,
    css: false,
    hydratable: true,
    legacy: false
  }
};
```

### Bundle optimization
```javascript
// vite.config.js
export default {
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['svelte']
        }
      }
    }
  }
};
```

## Migración

### De React a Svelte
Reescribir componentes usando sintaxis Svelte

### De Vue a Svelte
Adaptar templates y lógica de componentes

### Actualizar Svelte
```bash
npm update svelte
```

### Migrar a SvelteKit
```bash
npx svelte-migrate routes
```
