# Next.js Commands

Next.js es un framework de React que proporciona renderizado del lado del servidor, generación de sitios estáticos, y muchas otras características listas para producción.

## Instalación

### Crear nueva aplicación Next.js
```bash
npx create-next-app@latest my-app
cd my-app
```

### Con TypeScript
```bash
npx create-next-app@latest my-app --typescript
```

### Con template específico
```bash
npx create-next-app@latest my-app --example with-tailwindcss
npx create-next-app@latest my-app --example blog-starter
```

### Crear aplicación con opciones interactivas
```bash
npx create-next-app@latest
# Responder preguntas sobre TypeScript, ESLint, Tailwind CSS, etc.
```

## Comandos de Desarrollo

### Ejecutar servidor de desarrollo
```bash
npm run dev
```

### Ejecutar en puerto específico
```bash
npm run dev -- -p 3001
```

### Ejecutar con hostname específico
```bash
npm run dev -- -H 0.0.0.0
```

### Construir para producción
```bash
npm run build
```

### Iniciar en modo producción
```bash
npm run start
```

### Análisis de bundle
```bash
ANALYZE=true npm run build
```

## Comandos de Routing

### Routing basado en archivos (automático)
```bash
# pages/index.js -> /
# pages/about.js -> /about
# pages/blog/[slug].js -> /blog/:slug
# pages/api/users.js -> /api/users
```

### App Router (Next.js 13+)
```bash
# app/page.js -> /
# app/about/page.js -> /about
# app/blog/[slug]/page.js -> /blog/:slug
```

## Comandos de API Routes

### Crear API route
```bash
# pages/api/hello.js o app/api/hello/route.js
```

### Middleware
```bash
# middleware.js en la raíz del proyecto
```

## Pre-rendering y Data Fetching

### Static Site Generation (SSG)
```javascript
// getStaticProps en pages
export async function getStaticProps() {
  return { props: {} }
}
```

### Server-Side Rendering (SSR)
```javascript
// getServerSideProps en pages
export async function getServerSideProps() {
  return { props: {} }
}
```

### Incremental Static Regeneration (ISR)
```javascript
export async function getStaticProps() {
  return {
    props: {},
    revalidate: 60 // segundos
  }
}
```

## Comandos de Styling

### CSS Modules (incluido)
```css
/* styles/Home.module.css */
.container { }
```

### Styled Components
```bash
npm install styled-components
npm install --save-dev babel-plugin-styled-components
```

### Emotion
```bash
npm install @emotion/react @emotion/styled
```

### Tailwind CSS
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

### Sass/SCSS
```bash
npm install sass
```

## Image Optimization

### Next.js Image component (incluido)
```javascript
import Image from 'next/image'
```

### Configurar dominios de imágenes
```javascript
// next.config.js
module.exports = {
  images: {
    domains: ['example.com']
  }
}
```

## Comandos de Testing

### Jest y Testing Library
```bash
npm install --save-dev jest jest-environment-jsdom @testing-library/react @testing-library/jest-dom
```

### Ejecutar tests
```bash
npm run test
```

### Cypress para E2E
```bash
npm install --save-dev cypress
```

### Playwright
```bash
npm install --save-dev @playwright/test
```

## Deployment

### Deploy a Vercel (recomendado)
```bash
npm install -g vercel
vercel
```

### Deploy estático
```bash
npm run build
npm run export  # Para Next.js < 13
```

### Con output export (Next.js 13+)
```javascript
// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  output: 'export'
}
```

### Deploy a Netlify
```bash
npm run build
# Subir carpeta .next a Netlify
```

### Docker
```bash
# Dockerfile incluido en create-next-app
docker build -t my-next-app .
docker run -p 3000:3000 my-next-app
```

## Performance Optimization

### Bundle Analyzer
```bash
npm install @next/bundle-analyzer
```

### Configurar en next.config.js
```javascript
const withBundleAnalyzer = require('@next/bundle-analyzer')({
  enabled: process.env.ANALYZE === 'true'
})

module.exports = withBundleAnalyzer({})
```

### Lazy loading
```javascript
import dynamic from 'next/dynamic'

const DynamicComponent = dynamic(() => import('../components/MyComponent'))
```

## PWA Support

### Instalar next-pwa
```bash
npm install next-pwa
```

### Configurar PWA
```javascript
const withPWA = require('next-pwa')({
  dest: 'public'
})

module.exports = withPWA({})
```

## Internationalization (i18n)

### Configurar i18n (Next.js incluye soporte)
```javascript
// next.config.js
module.exports = {
  i18n: {
    locales: ['en', 'es', 'fr'],
    defaultLocale: 'en'
  }
}
```

### next-i18next
```bash
npm install next-i18next react-i18next i18next
```

## Authentication

### NextAuth.js
```bash
npm install next-auth
```

### Configurar providers
```javascript
// pages/api/auth/[...nextauth].js
import NextAuth from 'next-auth'
import GoogleProvider from 'next-auth/providers/google'

export default NextAuth({
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_ID,
      clientSecret: process.env.GOOGLE_SECRET
    })
  ]
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

### PostgreSQL
```bash
npm install pg
npm install --save-dev @types/pg
```

## State Management

### SWR (recomendado para Next.js)
```bash
npm install swr
```

### React Query
```bash
npm install @tanstack/react-query
```

### Redux Toolkit
```bash
npm install @reduxjs/toolkit react-redux
```

### Zustand
```bash
npm install zustand
```

## Environment Variables

### Variables de entorno locales
```bash
# .env.local
NEXT_PUBLIC_API_URL=https://api.example.com
DATABASE_URL=postgres://...
```

### Variables públicas
```bash
# Variables que empiezan con NEXT_PUBLIC_ son públicas
NEXT_PUBLIC_ANALYTICS_ID=12345
```

## Middleware

### Crear middleware
```javascript
// middleware.js
import { NextResponse } from 'next/server'

export function middleware(request) {
  return NextResponse.redirect(new URL('/login', request.url))
}

export const config = {
  matcher: '/protected/:path*'
}
```

## Edge Runtime

### Usar Edge Runtime
```javascript
export const config = {
  runtime: 'edge'
}
```

### Edge API Routes
```javascript
// app/api/edge/route.js
export const runtime = 'edge'

export async function GET() {
  return new Response('Hello from Edge!')
}
```

## Server Components (Next.js 13+)

### Usar Server Components
```javascript
// app/page.js (Server Component por defecto)
async function getData() {
  const res = await fetch('https://api.example.com/data')
  return res.json()
}

export default async function Page() {
  const data = await getData()
  return <main>{data.title}</main>
}
```

### Client Components
```javascript
'use client'

import { useState } from 'react'

export default function Counter() {
  const [count, setCount] = useState(0)
  return <button onClick={() => setCount(count + 1)}>{count}</button>
}
```

## Streaming

### Loading UI
```javascript
// app/loading.js
export default function Loading() {
  return <div>Loading...</div>
}
```

### Suspense boundaries
```javascript
import { Suspense } from 'react'

export default function Page() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <SlowComponent />
    </Suspense>
  )
}
```

## Error Handling

### Error boundaries
```javascript
// app/error.js
'use client'

export default function Error({ error, reset }) {
  return (
    <div>
      <h2>Something went wrong!</h2>
      <button onClick={() => reset()}>Try again</button>
    </div>
  )
}
```

### Not found pages
```javascript
// app/not-found.js
export default function NotFound() {
  return <div>404 - Page Not Found</div>
}
```

## Debugging

### Debug mode
```bash
NODE_OPTIONS='--inspect' npm run dev
```

### Next.js DevTools
Extensión del navegador disponible

### Performance profiling
```bash
npm run build -- --profile
```

## Custom Server

### Crear servidor personalizado
```javascript
// server.js
const { createServer } = require('http')
const { parse } = require('url')
const next = require('next')

const dev = process.env.NODE_ENV !== 'production'
const app = next({ dev })
const handle = app.getRequestHandler()
```

### Express.js custom server
```bash
npm install express
```

## Scripts de Package.json

### Scripts típicos para Next.js
```json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "export": "next export"
  }
}
```

## Configuration

### next.config.js básico
```javascript
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  swcMinify: true,
  images: {
    domains: ['example.com']
  },
  experimental: {
    appDir: true
  }
}

module.exports = nextConfig
```

## Migration

### Migrar a App Router
```bash
npx @next/codemod new-link .
npx @next/codemod next-image-to-legacy-image .
```

### Actualizar Next.js
```bash
npm install next@latest react@latest react-dom@latest
```

### Codemods disponibles
```bash
npx @next/codemod --help
```
