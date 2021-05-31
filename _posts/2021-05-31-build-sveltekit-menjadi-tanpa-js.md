---
layout: post
title: Build SvelteKit Menjadi Tanpa JS Sama Sekali
image: https://carpetcleanertn.com/wp-content/uploads/2019/01/Dogs-Shocked-Look.jpg
category: svelte
---

Yang namanya framework JavaScript, sudah lumrah sih jika pada akhirnya akan menghasilkan JavaScript. Tapi, bagaimana jika tidak menghasilkan JavaScript sama sekali?

Hal inilah yang ditawarkan oleh SvelteKit. Kita bisa menikmati kenyamanan developing menggunakan SvelteKit saat dev, tapi bisa kita build menjadi pure HTML dan CSS.

Oke, langsung kita coba aja...

Pertama, kita download dulu SvelteKit dengan perintah:

```bash
npm init svelte@next main-statis
```

Kemudian, kita menuju folder main-statis dan install dependencies yang diperlukan:

```bash
cd main-statis
pnpm i
```

Oh iya, aku menggunakan pnpm supaya bisa install dependencies dari cache. Kalau kamu belum punya pnpm, install dengan:

```bash
npm i -g pnpm
```

Kalau sudah, jalankan dengan:

```bash
npm run dev -- --open
```

Maka, akan terbuka localhost:3000 dengan tampilan seperti berikut ini:

![SvelteKit starter](https://i.ibb.co/tJxXBRS/image.png)

Terlalu simpel ya. Kita modif dikit deh... (nama filenya: src/routes/index.svelte)

```html
<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<svelte:head>
	<title>Hello World</title>
</svelte:head>

<style>
	h1,
	p {
		text-align: center;
		font-family: Candara;
	}
	h1 {
		color: red;
	}
	p {
		color: green;
	}
	p a {
		color: magenta !important;
	}
</style>
```

Hasilnya:

![SvelteKit starter habis dimodif dikit stylenya](https://i.ibb.co/SNSbWz2/image.png)

Lumayan.

Nah, sekarang kita akan build ke static dengan menghilangkan JS di outputnya.

Sekarang, matikan dulu proses dev tadi dengan Ctrl c

Terus, install adapter static dengan:

```bash
pnpm i -D @sveltejs/adapter-static@next
```

Lalu, edit `svelte.config.js` menjadi seperti ini:

```diff
+ import adapter from '@sveltejs/adapter-static'

/** @type {import('@sveltejs/kit').Config} */
const config = {
	kit: {
		// hydrate the <div id="svelte"> element in src/app.html
		target: '#svelte',
+		adapter: adapter(),
+		hydrate: false,
+		router: false
	}
};

export default config;
```

Kemudian, jalankan:

```bash
npm run build
```

Hasilnya di `build/index.html`:

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8" />
		<link rel="icon" href="/favicon.png" />
		<meta name="viewport" content="width=device-width, initial-scale=1" />
		<title>Hello World</title>

		

		<link rel="stylesheet" href="/./_app/assets/start-a8cd1609.css">
		<link rel="stylesheet" href="/./_app/assets/pages/index.svelte-9fb7a9ef.css">

		
	</head>
	<body>
		<div id="svelte">


<h1 class="svelte-7juoyx">Welcome to SvelteKit</h1>
<p class="svelte-7juoyx">Visit <a href="https://kit.svelte.dev" class="svelte-7juoyx">kit.svelte.dev</a> to read the documentation</p>





	
</div>
	</body>
</html>
```

Wow! Nggak menghasilkan JavaScript sama sekali! Keren kan ya... Jadi, kita bisa menikmati kenyamanan development dengan fitur HMR (Hot Module Replacement) di SvelteKit dan outputnya tidak menghasilkan JavaScript sama sekali. Ini bagus banget buat yang main aplikasi mobile dengan teknik webview, atau buat yang lagi develop template untuk blognya, maupun untuk yang pengen nggak ada JavaScript di website statisnya.

Lalu, bagaimana jika kita ingin menambahkan JavaScript? Kita bisa menggunakan Alpine JS.

> Catatan: Saat kembali ke mode dev, setting router dan hydrate menjadi true di `svelte.config.js`. Atau, bisa juga dengan mematikannya menggunakan teknik comment:

```javascript
import adapter from '@sveltejs/adapter-static'

/** @type {import('@sveltejs/kit').Config} */
const config = {
	kit: {
		// hydrate the <div id="svelte"> element in src/app.html
		target: '#svelte',
		adapter: adapter(),
		// hydrate: false,
		// router: false
	}
};

export default config;
```