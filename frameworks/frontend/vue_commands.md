# Vue.js Commands

Vue.js es un framework progresivo de JavaScript para construir interfaces de usuario. Está diseñado para ser adoptado incrementalmente.

## Instalación

### Instalar Vue CLI globalmente
```bash
npm install -g @vue/cli
```

### Verificar instalación
```bash
vue --version
```

### Crear nueva aplicación Vue
```bash
vue create my-project
cd my-project
```

### Crear proyecto con configuración manual
```bash
vue create my-project --preset manual
```

### Crear proyecto con Vite (Recomendado)
```bash
npm create vue@latest my-project
cd my-project
npm install
```

## Comandos de Desarrollo

### Ejecutar servidor de desarrollo
```bash
npm run serve  # Con Vue CLI
npm run dev    # Con Vite
```

### Ejecutar en puerto específico
```bash
npm run serve -- --port 8081
```

### Construir para producción
```bash
npm run build
```

### Ejecutar linting
```bash
npm run lint
```

### Fix automático de linting
```bash
npm run lint -- --fix
```

## Vue CLI Commands

### Ver configuración de webpack
```bash
vue inspect
```

### Ver configuración específica
```bash
vue inspect --mode production
```

### Agregar plugin
```bash
vue add <plugin-name>
```

### Agregar router
```bash
vue add router
```

### Agregar Vuex
```bash
vue add vuex
```

### Agregar TypeScript
```bash
vue add typescript
```

### Agregar PWA
```bash
vue add pwa
```

## Comandos con Vite

### Crear proyecto Vue 3 con Vite
```bash
npm create vue@latest my-vue-app
```

### Opciones disponibles durante creación
- TypeScript
- JSX
- Vue Router
- Pinia (gestión de estado)
- Vitest (testing)
- ESLint
- Prettier

### Ejecutar desarrollo
```bash
npm run dev
```

### Construir
```bash
npm run build
```

### Preview de build
```bash
npm run preview
```

## Herramientas de Desarrollo

### Vue DevTools
Extensión del navegador para debugging

### Vetur (VSCode Extension)
```bash
# Instalar desde VSCode Marketplace
```

### Volar (VSCode Extension para Vue 3)
```bash
# Instalar desde VSCode Marketplace
# Mejor soporte para Composition API
```

## Vue 3 Composition API

### Crear componente con setup script
```vue
<script setup lang="ts">
import { ref, computed } from 'vue'

const count = ref(0)
const doubled = computed(() => count.value * 2)
</script>
```

### Usar Composition API en opciones
```vue
<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  setup() {
    const count = ref(0)
    return { count }
  }
})
</script>
```

## Gestión de Estado

### Instalar Pinia (Vue 3)
```bash
npm install pinia
```

### Instalar Vuex (Vue 2/3)
```bash
npm install vuex@next  # Para Vue 3
npm install vuex       # Para Vue 2
```

## Enrutamiento

### Instalar Vue Router
```bash
npm install vue-router@4  # Para Vue 3
npm install vue-router    # Para Vue 2
```

### Generar rutas automáticamente
```bash
# Con vue-cli
vue add router
```

## Testing

### Instalar Vue Test Utils
```bash
npm install --save-dev @vue/test-utils
```

### Para Vue 3
```bash
npm install --save-dev @vue/test-utils@next
```

### Instalar Jest
```bash
npm install --save-dev jest vue-jest babel-jest
```

### Instalar Vitest (recomendado para Vite)
```bash
npm install --save-dev vitest @vue/test-utils jsdom
```

### Ejecutar tests
```bash
npm run test
# o
npm run test:unit
```

### Testing E2E con Cypress
```bash
vue add e2e-cypress
```

### Ejecutar tests E2E
```bash
npm run test:e2e
```

## UI Libraries

### Vuetify (Material Design)
```bash
vue add vuetify
```

### Element Plus
```bash
npm install element-plus
```

### Ant Design Vue
```bash
npm install ant-design-vue
```

### Quasar
```bash
npm install -g @quasar/cli
quasar create my-project
```

### PrimeVue
```bash
npm install primevue primeicons
```

### Naive UI
```bash
npm install naive-ui
```

## Herramientas de Build

### Vite (recomendado)
```bash
npm create vue@latest my-project
```

### Webpack (con Vue CLI)
```bash
vue create my-project
```

### Configurar Vite manualmente
```bash
npm install --save-dev vite @vitejs/plugin-vue
```

## Styling

### CSS Modules
```vue
<style module>
.red {
  color: red;
}
</style>
```

### Scoped CSS
```vue
<style scoped>
.example {
  color: red;
}
</style>
```

### Instalar Sass/SCSS
```bash
npm install --save-dev sass
```

### Instalar Less
```bash
npm install --save-dev less
```

### Instalar Stylus
```bash
npm install --save-dev stylus
```

## Deployment

### Build para producción
```bash
npm run build
```

### Servir archivos estáticos
```bash
npm install -g serve
serve -s dist
```

### Deploy a Netlify
```bash
npm install -g netlify-cli
netlify deploy --prod --dir=dist
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

## Server-Side Rendering

### Nuxt.js (SSR/SSG para Vue)
```bash
npx nuxi@latest init my-nuxt-app
cd my-nuxt-app
npm install
```

### Ejecutar Nuxt en desarrollo
```bash
npm run dev
```

### Construir Nuxt
```bash
npm run build
```

### Generar sitio estático con Nuxt
```bash
npm run generate
```

## Mobile Development

### Quasar (multiplataforma)
```bash
npm install -g @quasar/cli
quasar create my-app
```

### Capacitor
```bash
npm install @capacitor/core @capacitor/cli
npx cap init
```

### NativeScript-Vue
```bash
npm install -g @nativescript/cli
tns create my-app --vue
```

## Optimización

### Analizar bundle
```bash
npm run build -- --report
```

### Con webpack-bundle-analyzer
```bash
npm install --save-dev webpack-bundle-analyzer
```

### Lazy loading de rutas
```javascript
const Home = () => import('./views/Home.vue')
```

### Tree shaking automático
Incluido en Vite y webpack por defecto

## Debugging

### Vue DevTools
- Extensión del navegador
- Standalone app: `npm install -g @vue/devtools`

### Debug en VSCode
```json
{
  "type": "chrome",
  "request": "launch",
  "name": "vuejs: chrome",
  "url": "http://localhost:8080",
  "webRoot": "${workspaceFolder}/src",
  "sourceMapPathOverrides": {
    "webpack:///src/*": "${webRoot}/*"
  }
}
```

## Linting y Formateo

### ESLint para Vue
```bash
npm install --save-dev eslint @vue/eslint-config-typescript
```

### Prettier
```bash
npm install --save-dev prettier @vue/eslint-config-prettier
```

### Configuración ESLint
```javascript
module.exports = {
  extends: [
    '@vue/typescript/recommended',
    '@vue/prettier',
    '@vue/prettier/@typescript-eslint'
  ]
}
```

## TypeScript

### Crear proyecto con TypeScript
```bash
vue create my-project --preset typescript
```

### Agregar TypeScript a proyecto existente
```bash
vue add typescript
```

### Definir componente con TypeScript
```vue
<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'MyComponent',
  props: {
    message: {
      type: String,
      required: true
    }
  }
})
</script>
```

## Scripts de Package.json

### Scripts típicos para Vue
```json
{
  "scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "test:unit": "vue-cli-service test:unit",
    "test:e2e": "vue-cli-service test:e2e",
    "lint": "vue-cli-service lint"
  }
}
```

### Scripts con Vite
```json
{
  "scripts": {
    "dev": "vite",
    "build": "vue-tsc --noEmit && vite build",
    "preview": "vite preview",
    "test": "vitest",
    "lint": "eslint . --ext .vue,.js,.jsx,.cjs,.mjs,.ts,.tsx,.cts,.mts --fix"
  }
}
```

## Actualización

### Actualizar Vue CLI
```bash
npm update -g @vue/cli
```

### Actualizar dependencias del proyecto
```bash
vue upgrade
```

### Migrar de Vue 2 a Vue 3
```bash
vue add vue-next
```
