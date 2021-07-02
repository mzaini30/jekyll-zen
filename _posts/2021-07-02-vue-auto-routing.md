---
layout: post
title: Cara Supaya Vue Auto Routing Seperti Nuxt
image: https://bhuh12.gitee.io/vue-router-tab/demo/img/logo.png
category: vue
---

## Instalasi

```bash
npm init @vitejs/app coba-vue
```

Terus pilih Vue

## Pasang Auto Routing

### Install

```bash
pnpm i -D vue-router@4 npm-run-all vue-route-generator chokidar
```

### Setting `package.json` pada Bagian `scripts`

```json
{
  "version": "0.0.0",
  "scripts": {
    "dev": "run-p dev:*",
    "dev:vite": "vite",
    "dev:routify": "node watch-routify.js",
    "build": "node routify.js && vite build",
    "serve": "vite preview"
  },
  "dependencies": {
    "vue": "^3.0.5"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^1.2.3",
    "@vue/compiler-sfc": "^3.0.5",
    "npm-run-all": "^4.1.5",
    "vite": "^2.3.8",
    "vue-route-generator": "^1.0.0",
    "vue-router": "4"
  }
}
```

### Buat File `routify.js`

```javascript
const fs = require('fs')
const { generateRoutes } = require('vue-route-generator')

const code = generateRoutes({
  pages: './src/pages'
})

fs.writeFileSync('./src/routes.js', code)
```

### Buat File `watch-routify.js`

```javascript
const fs = require('fs')
const { generateRoutes } = require('vue-route-generator')
const chokidar = require('chokidar');

const perintah = () => fs.writeFileSync('./src/routes.js', generateRoutes({
  pages: './src/pages'
}))

const watcher = chokidar.watch('./src/pages')
watcher.on('add', () => perintah())
watcher.on('unlink', () => perintah())
```

### Setting `vite.config.js`

```javascript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import path from 'path'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, '/src'),
    }
  }
})
```

### Setting `src/main.js`

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import {createRouter, createWebHistory} from 'vue-router'
import routes from './routes'

const router = createRouter({
	routes,
	history: createWebHistory()
})

createApp(App).use(router).mount('#app')
```

### Setting `src/App.vue`

```html
<template>
  <router-view></router-view>
</template>
```

### Buat File `src/pages/index.vue`

## Jalankan

```bash
npm run dev
```