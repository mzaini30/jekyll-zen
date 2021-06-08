---
layout: post
title: 3 Bentuk Hasil Build SvelteKit untuk 3 Kebutuhan Berbeda
image: https://blog-assets.pinshape.com/blog/wp-content/uploads/2015/11/02123159/flexsolid_p_grande.jpg
category: svelte
---

SvelteKit adalah Svelte yang ditambahkan dengan beberapa lib. Ya bisa dibilang seperti Next JS kalau di React. Keunggulan dari SvelteKit salah satunya adalah adanya adapter. Adapter itu akan mengatur kita buildnya ke mana; bisa ke node, static, vercel, netlify, begin, dll.

Cara menggunakannya pun gampang. Jadi, kita menggunakan sintaks Svelte pada umumnya. Contohnya aja isi file `index.svelte`:

```html
<p>Masukkan Nama:</p>
<input type="text" bind:value={nama}>
<p>Hai {nama}</p>
<p><a href="/{nama}">Klik untuk menuju ke {nama}</a></p>

<script>
	let nama = 'kucing'
</script>
```

Akan menghasilkan:

![Hasil jadi index.svelte](https://i.ibb.co/R9fSW4q/image.png)

Kemudian, untuk file `[nama].svelte`:

```html
<script>
	import {page} from '$app/stores'
</script>

<h1>Hai {$page.params.nama}</h1>
```

![Hasil jadi nama.svelte](https://i.ibb.co/rkfYHwT/image.png)

Simpel banget kan ya?

Nah, sekarang kita akan melihat 3 bentuk hasil build untuk 3 kebutuhan yang berbeda. Apa aja itu?

1. Frontend website pada environment Node JS
2. Frontend website pada environment _selain_ Node JS
3. Aplikasi Android webview

Oke, langsung aja kita bahas.

## 1. Frontend website pada environment Node JS

Kalau untuk frontend website pada environment Node JS, baik itu berupa server Node JS maupun serverless function menggunakan layanan seperti Vercel, Netlify, dan Begin, caranya cukup mudah. Yaitu cukup menggunakan adapter-adapter yang sudah disediakan. Cara menggunakannya sudah ada di docsnya SvelteKit pada bagian adapters. 

Misalnya aja, kita ingin deploy ke Vercel, contoh script pada `svelte.config.js` seperti ini:

```javascript
import adapterVercel from '@sveltejs/adapter-vercel'

/** @type {import('@sveltejs/kit').Config} */
const config = {
	kit: {
		// hydrate the <div id="svelte"> element in src/app.html
		target: '#svelte',
		adapter: adapterVercel()
	}
};

export default config;
```

Jadi, kita tinggal upload project kita ke Vercel dan atur perintah build ke `npm run build` atau bisa aja menggunakan defaultnya (karena sama aja perintahnya). Kemudian, akan jalan deh SvelteKit kita dengan mode SSR di Vercel.

## 2. Frontend website pada environment _selain_ Node JS

Kalau untuk selain Node JS, kita build dengan adapter static dan menghidupkan mode SPA:

```javascript
import adapterStatic from '@sveltejs/adapter-static'

/** @type {import('@sveltejs/kit').Config} */
const config = {
	kit: {
		// hydrate the <div id="svelte"> element in src/app.html
		target: '#svelte',
		adapter: adapterStatic({
			fallback: 'index.html'
		})
	}
};

export default config;
```

Mengapa kita perlu menghidupkan mode SPA? Soalnya, dengan menghidupkan mode SPA, kita bisa menggunakan dynamic routing seperti `[nama].svelte`

## 3. Aplikasi Android webview

Kalau untuk webview pada Android, kita pakai adapter static dengan mematikan JavaScriptnya Svelte. Jadi, kita pakai JavaScript biasa:

```javascript
import adapterStatic from '@sveltejs/adapter-static'

/** @type {import('@sveltejs/kit').Config} */
const config = {
	kit: {
		// hydrate the <div id="svelte"> element in src/app.html
		target: '#svelte',
		adapter: adapterStatic(),
		appDir: 'svelte',
		router: false,
		hydrate: false
	}
};

export default config;
```

Nah, kita matikan router dan hydrate untuk mematikan keseluruhan JavaScriptnya Svelte. Lalu, untuk appDir, kita buat nama foldernya dengan nama svelte. Kalau defaultnya kan nama foldernya itu `_app`. Kalau di Android Studio, nama-nama folder berawalan underscore akan diabaikan.

Jadi, untuk JavaScriptnya, kita gunakan Alpine JS.

Misalnya aja kita pakai kode Svelte yang tadi:

```html
<p>Masukkan Nama:</p>
<input type="text" bind:value={nama}>
<p>Hai {nama}</p>
<p><a href="/{nama}">Klik untuk menuju ke {nama}</a></p>

<script>
	let nama = 'kucing'
</script>
```

Maka, kalau dalam bentuk Alpine JS, akan menjadi:

```html
<div class="" x-data='init()'>
	<p>Masukkan Nama:</p>
	<input type="text" x-model='nama'>
	<p>Hai <span x-text='nama'></span></p>
	<p><a x-bind:href="'/' + nama">Klik untuk menuju ke <span x-text='nama'></span></a></p>
</div>

<div class="">
	<script>
		function init(){
			return {
				nama: 'kucing'
			}
		}
	</script>
</div>
```

Untuk tag script, kita perlu bungkus dengan sebuah div supaya nggak disangka scriptnya Svelte oleh Svelte.