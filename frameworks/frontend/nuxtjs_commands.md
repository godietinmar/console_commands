# Nuxt.js Commands

Nuxt.js es un framework de Vue.js que proporciona renderizado del lado del servidor, generación de sitios estáticos, y una arquitectura modular para aplicaciones Vue.js.

## Instalación

### Crear nueva aplicación Nuxt 3
```bash
npx nuxi@latest init my-app
cd my-app
npm install
```

### Crear con template específico
```bash
npx nuxi@latest init my-app --template ui
```

### Crear aplicación Nuxt 2 (Legacy)
```bash
npx create-nuxt-app my-app
```

## Comandos de Desarrollo

### Ejecutar servidor de desarrollo
```bash
npm run dev
```

### Ejecutar con puerto específico
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

### Generar sitio estático
```bash
npm run generate
```

### Preview de producción
```bash
npm run preview
```

## Comandos de Nuxi (Nuxt 3 CLI)

### Crear nuevo proyecto
```bash
npx nuxi init my-project
```

### Agregar dependencia
```bash
npx nuxi add component MyButton
npx nuxi add page about
npx nuxi add layout default
```

### Construir aplicación
```bash
npx nuxi build
```

### Limpiar cache
```bash
npx nuxi cleanup
```

### Analizar aplicación
```bash
npx nuxi analyze
```

### Información del proyecto
```bash
npx nuxi info
```

### Actualizar dependencias
```bash
npx nuxi upgrade
```

## File-based Routing

### Páginas automáticas
```bash
# pages/index.vue -> /
# pages/about.vue -> /about
# pages/users/[id].vue -> /users/:id
# pages/blog/[...slug].vue -> /blog/:slug*
```

### Crear páginas dinámicas
```bash
mkdir pages/blog
touch pages/blog/[slug].vue
```

### Nested routes
```bash
mkdir pages/users
touch pages/users.vue
touch pages/users/index.vue
touch pages/users/profile.vue
```

## Layouts

### Crear layout
```bash
mkdir layouts
touch layouts/default.vue
```

### Layout personalizado
```bash
touch layouts/admin.vue
```

### Usar layout en página
```vue
<template>
  <div>Content</div>
</template>

<script setup>
definePageMeta({
  layout: 'admin'
})
</script>
```

## Components

### Crear componente
```bash
mkdir components
touch components/MyButton.vue
```

### Auto-import de componentes
Los componentes en `components/` se importan automáticamente

### Componentes anidados
```bash
mkdir components/ui
touch components/ui/Button.vue
# Se usa como <UiButton />
```

## Plugins

### Crear plugin
```bash
mkdir plugins
touch plugins/my-plugin.js
```

### Plugin client-side
```javascript
// plugins/client-plugin.client.js
export default defineNuxtPlugin(() => {
  // Solo se ejecuta en el cliente
})
```

### Plugin server-side
```javascript
// plugins/server-plugin.server.js
export default defineNuxtPlugin(() => {
  // Solo se ejecuta en el servidor
})
```

## Middleware

### Crear middleware
```bash
mkdir middleware
touch middleware/auth.js
```

### Middleware global
```javascript
// middleware/auth.global.js
export default defineNuxtRouteMiddleware((to, from) => {
  // Se ejecuta en todas las rutas
})
```

### Usar middleware en página
```vue
<script setup>
definePageMeta({
  middleware: 'auth'
})
</script>
```

## Modules

### Instalar módulos oficiales
```bash
npm install @nuxtjs/tailwindcss
npm install @pinia/nuxt
npm install @nuxtjs/color-mode
```

### Configurar módulos
```javascript
// nuxt.config.ts
export default defineNuxtConfig({
  modules: [
    '@nuxtjs/tailwindcss',
    '@pinia/nuxt',
    '@nuxtjs/color-mode'
  ]
})
```

### Crear módulo personalizado
```bash
mkdir modules
touch modules/my-module.ts
```

## State Management

### Pinia (recomendado)
```bash
npm install @pinia/nuxt pinia
```

### Crear store
```javascript
// stores/counter.js
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  const increment = () => count.value++
  return { count, increment }
})
```

### Vuex (Nuxt 2)
```bash
mkdir store
touch store/index.js
```

## Server API

### Crear API route
```bash
mkdir server/api
touch server/api/users.get.ts
```

### API con parámetros
```bash
touch server/api/users/[id].get.ts
```

### Middleware de servidor
```bash
mkdir server/middleware
touch server/middleware/cors.ts
```

## Composables

### Crear composable
```bash
mkdir composables
touch composables/useAuth.js
```

### Auto-import de composables
```javascript
// composables/useCounter.js
export const useCounter = () => {
  const count = ref(0)
  const increment = () => count.value++
  return { count, increment }
}
```

## Styling

### CSS/SCSS
```bash
npm install sass
```

### Tailwind CSS
```bash
npm install @nuxtjs/tailwindcss
npx tailwindcss init
```

### Windicss
```bash
npm install nuxt-windicss
```

### UnoCSS
```bash
npm install @unocss/nuxt
```

## Content Management

### Nuxt Content
```bash
npm install @nuxt/content
```

### Crear contenido
```bash
mkdir content
touch content/index.md
touch content/blog/my-post.md
```

### Usar contenido
```vue
<template>
  <ContentDoc />
</template>
```

## Image Optimization

### Nuxt Image
```bash
npm install @nuxt/image
```

### Usar componente Image
```vue
<template>
  <NuxtImg src="/image.jpg" alt="Image" />
</template>
```

## SEO y Meta

### Meta tags dinámicos
```vue
<script setup>
useSeoMeta({
  title: 'My Page',
  description: 'My page description'
})
</script>
```

### Open Graph
```vue
<script setup>
useHead({
  meta: [
    { property: 'og:title', content: 'My Page' },
    { property: 'og:description', content: 'Description' }
  ]
})
</script>
```

## Testing

### Vitest
```bash
npm install --save-dev vitest @vue/test-utils happy-dom
```

### Playwright
```bash
npm install --save-dev @playwright/test
```

### Ejecutar tests
```bash
npm run test
```

## Deployment

### Static hosting
```bash
npm run generate
```

### Server deployment
```bash
npm run build
```

### Deploy a Vercel
```bash
npm install -g vercel
vercel
```

### Deploy a Netlify
```bash
npm install -g netlify-cli
netlify deploy --prod --dir=dist
```

### Deploy a CloudFlare Pages
```bash
npm run generate
# Subir carpeta dist/ a CloudFlare Pages
```

### Docker
```bash
# Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]
```

## PWA

### Instalar PWA module
```bash
npm install @nuxtjs/pwa
```

### Configurar PWA
```javascript
// nuxt.config.ts
export default defineNuxtConfig({
  modules: ['@nuxtjs/pwa'],
  pwa: {
    manifest: {
      name: 'My App',
      short_name: 'MyApp'
    }
  }
})
```

## Internationalization

### Nuxt i18n
```bash
npm install @nuxtjs/i18n
```

### Configurar idiomas
```javascript
// nuxt.config.ts
export default defineNuxtConfig({
  modules: ['@nuxtjs/i18n'],
  i18n: {
    locales: ['en', 'es', 'fr'],
    defaultLocale: 'en'
  }
})
```

## Performance

### Analizar bundle
```bash
npm run build -- --analyze
```

### Lazy loading
```vue
<template>
  <LazyMyComponent />
</template>
```

### Preloading
```vue
<script setup>
await preloadComponents('MyComponent')
</script>
```

## DevTools

### Nuxt DevTools
```bash
npm install --save-dev @nuxt/devtools
```

### Vue DevTools
Extensión del navegador

## Environment Variables

### Variables de entorno
```bash
# .env
NUXT_SECRET_KEY=secret
NUXT_PUBLIC_API_BASE=https://api.example.com
```

### Runtime config
```javascript
// nuxt.config.ts
export default defineNuxtConfig({
  runtimeConfig: {
    secretKey: process.env.NUXT_SECRET_KEY,
    public: {
      apiBase: process.env.NUXT_PUBLIC_API_BASE
    }
  }
})
```

## Database Integration

### Prisma
```bash
npm install prisma @prisma/client
npx prisma init
```

### MongoDB
```bash
npm install mongodb
```

### Supabase
```bash
npm install @nuxtjs/supabase
```

## Authentication

### Nuxt Auth
```bash
npm install @sidebase/nuxt-auth
```

### NextAuth.js
```bash
npm install next-auth @auth/core
```

## Error Handling

### Error page
```bash
touch error.vue
```

### Custom error page
```vue
<template>
  <div>
    <h1>{{ error.statusCode }}</h1>
    <p>{{ error.statusMessage }}</p>
    <button @click="handleError">Go back</button>
  </div>
</template>

<script setup>
const props = defineProps(['error'])

const handleError = () => clearError({ redirect: '/' })
</script>
```

## Scripts de Package.json

### Scripts típicos para Nuxt 3
```json
{
  "scripts": {
    "build": "nuxt build",
    "dev": "nuxt dev",
    "generate": "nuxt generate",
    "preview": "nuxt preview",
    "postinstall": "nuxt prepare"
  }
}
```

### Scripts para Nuxt 2
```json
{
  "scripts": {
    "dev": "nuxt",
    "build": "nuxt build",
    "start": "nuxt start",
    "generate": "nuxt generate"
  }
}
```

## Configuration

### nuxt.config.ts básico
```typescript
export default defineNuxtConfig({
  devtools: { enabled: true },
  css: ['~/assets/css/main.css'],
  modules: [
    '@nuxtjs/tailwindcss',
    '@pinia/nuxt'
  ],
  runtimeConfig: {
    public: {
      apiBase: '/api'
    }
  }
})
```

## Migration

### Migrar de Nuxt 2 a Nuxt 3
```bash
npx nuxi upgrade --force
```

### Migration helper
```bash
npx @nuxt/bridge
```

## Debugging

### Debug mode
```bash
npm run dev -- --debug
```

### Server logs
```bash
npm run dev -- --verbose
```
