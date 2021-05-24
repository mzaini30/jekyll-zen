---
title: Yang Perlu Dilakukan Setelah Install Svelte Kit
category: svelte
image: https://cdn.coursehunter.net/course/svelte-3-proekt-movie-app-s-svelte-js-2020.jpg
layout: post
---

## Siapkan Icon

Iconnya format `.png`. Terus, diletakkan di `static/`. Contohnya aja `static/logo.png`.

Iconnya harus persegi ukurannya (lebar = tinggi). Misalnya aja ukurannya 300 x 300.

Lalu, di `src/app.html`, masukkan:

```html
<link rel="icon" href="/logo.png" />
```

## Buat `robots.txt`

Buat di `static/robots.txt` yang isinya:

```
# https://www.robotstxt.org/robotstxt.html
User-agent: *
Disallow:
```

## Sedikit Perbaikan di Svelte Kit

Ini gunanya untuk memperbaiki `URLSearchParams` saat build static.

Install replace:

```bash
pnpm i -D replace
```

Lalu, buat `ubahQuery.js` yang isinya:

```javascript
import replace from 'replace'

replace({
	regex: 'query: new URLSearchParams(.+),',
	replacement: 'query: new URLSearchParams(location.search),',
	paths: ['build'],
	recursive: true
})
```

Edit `package.json`:

```diff
"scripts": {
	"dev": "svelte-kit dev",
+	"build": "svelte-kit build && node ubahQuery.js",
	"preview": "svelte-kit preview"
},
```

## Jalankan Offline Mode

Install Workbox:

```bash
pnpm i -D workbox-cli
```

Buat `static/sw.js` yang nggak ada isinya.

Buat `static/registerSW.js` yang isinya:

```javascript
if('serviceWorker' in navigator) {
	window.addEventListener('load', () => {
		navigator.serviceWorker.register('/sw.js', { 
			scope: '/' 
		})
	})
}
```

Buat `static/manifest.json` yang isinya:

```json
{
	"name":"Zen",
	"short_name":"Zen",
	"start_url":"/",
	"display":"minimal-ui",
	"background_color":"#ffffff",
	"lang":"id",
	"scope":"/",
	"icons":[
		{
			"src":"/logo.png",
			"sizes":"892x892",
			"type":"image/png"
		}
	]
}
```

Tambahkan di `src/app.html`:

```html
<script src="/registerSW.js"></script>
<link rel="manifest" href="/manifest.json">
```

Buat `workbox-config.cjs` yang isinya:

```javascript
module.exports = {
	globDirectory: 'build/',
	globPatterns: [
		'**/*.*'
	],
	swDest: 'build/sw.js'
};
```

Ubah `package.json`:

```json
"scripts": {
	"dev": "svelte-kit dev",
	"build": "svelte-kit build && rm build/sw.js && workbox generateSW workbox-config.cjs",
	"preview": "svelte-kit preview"
},
```

## Siapkan Build Static

Install:

```bash
pnpm i -D @sveltejs/adapter-static@next
```

Edit `svelte.config.js`:

```diff
+import adapter from '@sveltejs/adapter-static'
import preprocess from 'svelte-preprocess'

/** @type {import('@sveltejs/kit').Config} */
const config = {
	kit: {
		// hydrate the <div id="svelte"> element in src/app.html
		target: '#svelte',
+		adapter: adapter()
	},
	preprocess: preprocess(),
};

export default config;
```

## Install SCSS

Install:

```bash
pnpm i -D sass svelte-preprocess
```

Edit `svelte.config.js`:

```diff
import adapter from '@sveltejs/adapter-static'
+import preprocess from 'svelte-preprocess'

/** @type {import('@sveltejs/kit').Config} */
const config = {
	kit: {
		// hydrate the <div id="svelte"> element in src/app.html
		target: '#svelte',
		adapter: adapter()
	},
+	preprocess: preprocess(),
};

export default config;
```