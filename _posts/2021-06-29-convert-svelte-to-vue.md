---
layout: post
title: Convert Svelte to Vue
category: vue
image: https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Vue.js_Logo_2.svg/694px-Vue.js_Logo_2.svg.png
---

## Introduction/Basics

### Svelte

```html
<h1>Hello world!</h1>
```

### Vue

```html
<template>
	<h1>Hello world!</h1>
</template>
```

## Introduction/Adding Data

### Svelte

```html
<script>
	let name = 'world';
</script>

<h1>Hello {name.toUpperCase()}!</h1>
```

### Vue

```html
<script setup>
	import {ref} from 'vue'
	const name = ref('world')
</script>

<template>
	<h1>Hello {{name.toUpperCase()}}!</h1>
</template>
```

## Introduction/Dynamic Attributes

### Svelte

```html
<script>
	let src = 'https://svelte.dev/tutorial/image.gif';
	let name = 'Rick Astley';
</script>

<img {src} alt="{name} dances.">
```

### Vue

```html
<script setup>
	import {ref} from 'vue'

	const src = ref('https://svelte.dev/tutorial/image.gif')
	const name = ref('Rick Astley')
</script>

<template>
	<img :src="src" :alt="name + ' dances'">
</template>
```