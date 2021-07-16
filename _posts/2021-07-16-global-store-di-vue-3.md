---
layout: post
title: Global Store di Vue 3
image: https://vlebazaar.in/image/cache/data/img/MN-550x550w.jpg
category: vue
---

Download template Vue terlebih dahulu dengan perintah:

```bash
degit mzaini30/vue latihan-store-vue
```

Kemudian, masuk ke folder itu dan install dependencies.

Sekarang, untuk melist store, kita edit di `src/App.vue`:

```html
<template>
	<router-view></router-view>
	<ReloadPrompt/>
</template>

<script setup>
	import ReloadPrompt from './ReloadPrompt.vue'
	provide('counter', ref(0))
</script>
```

Di situ, aku provide counter dengan nilai ref 0.

Lalu, misalnya kita ingin menggunakan store tersebut, kita buat `src/pages/index.vue` berisi:

```html
<script setup="">
	document.title = 'Latihan Vue'
	const counter = inject('counter')
	import TambahCounter from './TambahCounter.vue'
</script>

<template>
	<p>{%raw%}{{counter}}{%endraw%}</p>
	<tambah-counter></tambah-counter>
</template>
```

Lalu, di `src/pages/TambahCounter.vue`:

```html
<script setup="">
	const counter = inject('counter')
</script>

<template>
	<button @click='counter++'>Tambah</button>
	<button @click='counter--'>Kurangi</button>
</template>
```

Hasilnya:

<iframe src='https://provide-inject-vue.vercel.app/'></iframe>
