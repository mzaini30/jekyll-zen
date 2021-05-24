---
title: Latihan SCSS dengan SvelteKit
category: svelte
image: https://i.ibb.co/2ZjSx7M/image.png
layout: post
---

SCSS adalah preprocessor CSS. Jadi, kita bisa lebih mudah dalam mengolah CSS.

Misalnya aja, kalau dengan SCSS:

```scss
.container {
	p {
		margin-top: 10px;
	}
}
```

Maka, akan menjadi seperti ini ketika diolah menjadi CSS:

```css
.container p {
	margin-top: 10px;
}
```

Atau, dengan kode SCSS seperti ini:

```scss
.tombol {
	background: blue;
	&:hover {
		background: red;
	}
}
```

Akan menghasilkan:

```css
.tombol {
	background: blue;
}

.tombol:hover {
	background: red;
}
```

Keren kan? Jadi, kita nggak perlu menuliskan sintaks CSS yang sama berkali-kali.

Nah, sekarang kita coba menggunakan SCSS dengan SvelteKit.

Kenapa menggunakan SvelteKit? Karena untuk bisa menguasai frontend, kita perlu berkenalan dengan framework JavaScript. Lalu, di antara framework JS lainnya, SvelteKit ini adalah framework JavaScript yang paling mudah karena kita hanya perlu pengetahuan dasar HTML, CSS, dan JS, kemudian ditambahkan sedikit kode Svelte kalau kita membutuhkannya. Oke, langsung kita mulai aja.

Pertama, buat dulu project SvelteKit dengan perintah:

```bash
npm init svelte@next latihan-scss
```

Kemudian, akan muncul beberapa pertanyaan:

```
? Which Svelte app template? › - Use arrow-keys. Return to submit.
    SvelteKit demo app
❯   Skeleton project
```

Yang itu, pilih Skeleton project.

```
? Use TypeScript? › No / Yes
```

Yang itu, pilih No.

```
? Add ESLint for code linting? › No / Yes
```

Yang itu, pilih No.

```
? Add Prettier for code formatting? › No / Yes
```

Yang itu (Prettier), pilih No.

Nah, sekarang kita akan install dependencies yang diperlukan dengan pnpm. Kalau belum ada pnpm, install dengan:

```bash
npm i -g pnpm
```

Sekarang, kita masuk ke projectnya, terus install semua yang dibutuhkan:

```bash
cd latihan-scss/
pnpm i
subl . -a
```

Oh iya, penjelasan dikit ya...

`cd latihan-scss/` itu berarti kita masuk ke folder latihan-scss. Lalu, `pnpm i` berarti kita install semua dependencies yang diperlukan. `subl . -a` itu berarti buka project tersebut di Sublime.

Buka `src/app.html` lalu hapus `<link rel="icon" href="/favicon.ico" />`

Lalu, kita install SCSS dengan perintah:

```bash
pnpm i -D sass svelte-preprocess
```

Lalu, edit `svelte.config.js`:

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
+    preprocess: preprocess(),
};

export default config;
```

Kemudian, kita jalankan development SvelteKit:

```bash
npm run dev -- --open
```

Nah, sekarang, kita edit `src/routes/index.svelte`

Karena di situ, udah ada teks bawaan dari Svelte, kita pakai itu aja ya...

```html
<h1>Welcome to SvelteKit</h1>
<p>
	Visit 
	<a href="https://kit.svelte.dev">kit.svelte.dev</a> 
	to read the documentation
</p>
```

Sekarang, untuk menggunakan SCSS, kita hanya perlu menuliskan `<style lang='scss'></style>` di situ:

```html
<h1>Welcome to SvelteKit</h1>
<p>
	Visit 
	<a href="https://kit.svelte.dev">kit.svelte.dev</a> 
	to read the documentation
</p>

<style lang="scss">
	
</style>
```

Nah, baru deh kita coba eksperimen dengan SCSS:

```html
<h1>Welcome to SvelteKit</h1>
<p>
	Visit 
	<a href="https://kit.svelte.dev">kit.svelte.dev</a> 
	to read the documentation
</p>

<style lang="scss">
	* {
		text-align: center;
	}
	h1 {
		padding-top: 30px;
		font-family: Cambria;
		font-size: 40px;
	}
	p {
		font-family: Candara;
		font-size: 20px;
		a {
			color: green !important;
			text-decoration: none !important;
		}
	}
</style>
```

Jadinya seperti ini:

![Hasil Jadinya](https://i.ibb.co/2ZjSx7M/image.png)

Sekarang, kita tambahkan title:

```html
<h1>Welcome to SvelteKit</h1>
<p>
	Visit 
	<a href="https://kit.svelte.dev">kit.svelte.dev</a> 
	to read the documentation
</p>

<style lang="scss">
	* {
		text-align: center;
	}
	h1 {
		padding-top: 30px;
		font-family: Cambria;
		font-size: 40px;
	}
	p {
		font-family: Candara;
		font-size: 20px;
		a {
			color: green !important;
			text-decoration: none !important;
		}
	}
</style>

<svelte:head>
	<title>Latihan SCSS</title>
</svelte:head>
```

Kalau sudah, kita build dengan adapter static.

Matikan dulu proses development tadi dengan Ctrl c

Kemudian, kita install adapter static:

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
+        adapter: adapter()
    },
    preprocess: preprocess(),
};

export default config;
```

Kita build dengan:

```bash
npm run build
```

Maka, akan terbentuk folder `build/` yang merupakan hasil buildnya.