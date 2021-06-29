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
	<h1>Hello {%raw%}{{name.toUpperCase()}}{%endraw%}!</h1>
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

## Introduction/Styling

### Svelte

```html
<p>This is a paragraph.</p>

<style>
	p {
		color: purple;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
</style>
```

### Vue

```html
<template>
	<p>This is a paragraph.</p>
</template>

<style scoped>
	p {
		color: purple;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
</style>
```

## Introduction/Nested Component

### Svelte

App.svelte

```html
<script>
	import Nested from './Nested.svelte';
</script>

<p>This is a paragraph.</p>
<Nested/>

<style>
	p {
		color: purple;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
</style>
```

Nested.svelte

```html
<p>This is another paragraph.</p>
```

### Vue

App.vue

```html
<script setup>
	import Nested from './Nested.vue';
</script>

<template>
	<p>This is a paragraph.</p>
	<Nested/>
</template>

<style scoped>
	p {
		color: purple;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
</style>
```

Nested.vue

```html
<template>
	<p>This is another paragraph.</p>
</template>
```

## Introduction/HTML Tag

### Svelte

```html
<script>
	let string = `this string contains some <strong>HTML!!!</strong>`;
</script>

<p>{@html string}</p>
```

### Vue

```html
<script setup>
	import {ref} from 'vue'

	const string = ref(`this string contains some <strong>HTML!!!</strong>`);
</script>

<template>
	<p v-html='string'></p>
</template>
```

## Reactivity/Assignments

### Svelte

```html
<script>
	let count = 0;

	function handleClick() {
		count += 1;
	}
</script>

<button on:click={handleClick}>
	Clicked {count} {count === 1 ? 'time' : 'times'}
</button>
```

### Vue

```html
<script setup>
	import {ref} from 'vue'
	const count = ref(0);

	function handleClick() {
		count.value += 1;
	}
</script>

<template>
	<button @click='handleClick'>
		Clicked {%raw%}{{count}}{%endraw%} {%raw%}{{count === 1 ? 'time' : 'times'}}{%endraw%}
	</button>
</template>
```

## Reactivity/Declarations

### Svelte

```html
<script>
	let count = 0;
	$: doubled = count * 2;

	function handleClick() {
		count += 1;
	}
</script>

<button on:click={handleClick}>
	Clicked {count} {count === 1 ? 'time' : 'times'}
</button>

<p>{count} doubled is {doubled}</p>
```

### Vue

```html
<script setup>
	import {computed, ref} from 'vue'
	const count = ref(0);
	const doubled = computed(() => count.value * 2)

	function handleClick() {
		count.value += 1;
	}
</script>

<template>
	<button @click='handleClick'>
		Clicked {%raw%}{{count}}{%endraw%} {%raw%}{{count === 1 ? 'time' : 'times'}}{%endraw%}
	</button>

	<p>{%raw%}{{count}}{%endraw%} doubled is {%raw%}{{doubled}}{%endraw%}</p>
</template>
```

## Reactivity/Statements

### Svelte

```html
<script>
	let count = 0;

	$: if (count >= 10) {
		alert(`count is dangerously high!`);
		count = 9;
	}

	function handleClick() {
		count += 1;
	}
</script>

<button on:click={handleClick}>
	Clicked {count} {count === 1 ? 'time' : 'times'}
</button>
```

### Vue

```html
<script setup>
	import {ref, watch} from 'vue'
	const count = ref(0);

	const cek = () => {
		if (count.value >= 10) {
			alert(`count is dangerously high!`);
			count.value = 9;
		}
	}
	watch(count, cek)

	function handleClick() {
		count.value += 1;
	}
</script>

<template>
	<button @click='handleClick'>
		Clicked {%raw%}{{count}}{%endraw%} {%raw%}{{count === 1 ? 'time' : 'times'}}{%endraw%}
	</button>
</template>
```

## Reactivity/Updating Arrays and Objects

### Svelte

```html
<script>
	let numbers = [1, 2, 3, 4];

	function addNumber() {
		numbers = [...numbers, numbers.length + 1];
	}

	$: sum = numbers.reduce((t, n) => t + n, 0);
</script>

<p>{numbers.join(' + ')} = {sum}</p>

<button on:click={addNumber}>
	Add a number
</button>
```

### Vue

```html
<script setup>
	import {ref, computed} from 'vue'
	const numbers = ref([1, 2, 3, 4]);

	function addNumber() {
		numbers.value = [...numbers.value, numbers.value.length + 1];
	}

	const sum = computed(() => numbers.value.reduce((t, n) => t + n, 0))
</script>

<template>
	<p>{%raw%}{{numbers.join(' + ')}}{%endraw%} = {%raw%}{{sum}}{%endraw%}</p>

	<button @click='addNumber'>
		Add a number
	</button>
</template>
```

## Props/Declaring Props

### Svelte

App.svelte

```html
<script>
	import Nested from './Nested.svelte';
</script>

<Nested answer={42}/>
```

Nested.svelte

```html
<script>
	export let answer;
</script>

<p>The answer is {answer}</p>
```

### Vue

App.vue

```html
<script setup>
	import Nested from './Nested.vue';
</script>

<template>
	<Nested answer='42'/>
</template>
```

Nested.vue

```html
<script setup>
	import {defineProps} from 'vue'
	defineProps(['answer'])
</script>

<template>
	<p>The answer is {%raw%}{{answer}}{%endraw%}</p>
</template>
```

## Props/Default Props

### Svelte

App.svelte

```html
<script>
	import Nested from './Nested.svelte';
</script>

<Nested answer={42}/>
<Nested/>
```

Nested.svelte

```html
<script>
	export let answer = 'a mystery';
</script>

<p>The answer is {answer}</p>
```

### Vue

App.vue

```html
<script setup>
	import Nested from './Nested.vue';
</script>

<template>
	<Nested answer='42'/>
	<Nested/>
</template>
```

Nested.vue

```html
<script setup>
	import {defineProps} from 'vue'
	defineProps({
		answer: {
			default: 'a mistery'
		}
	})
</script>

<template>
	<p>The answer is {%raw%}{{answer}}{%endraw%}</p>
</template>
```

## Special Elements/<svelte:head>

### Svelte

```html
<svelte:head>
	<link rel="stylesheet" href="https://svelte.dev/tutorial/dark-theme.css">
</svelte:head>

<h1>Hello world!</h1>
```

### Vue

```html
<template>
	<teleport to='head'>
		<link rel="stylesheet" href="https://svelte.dev/tutorial/dark-theme.css">
	</teleport>

	<h1>Hello world!</h1>
</template>
```