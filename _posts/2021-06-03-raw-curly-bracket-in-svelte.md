---
layout: post
title: Raw Curly Bracket in Svelte
image: https://res.cloudinary.com/practicaldev/image/fetch/s--Nl8wxs2q--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jfeadvedmdtc7pbd9lhj.png
category: svelte
---

Misalnya aja kita iseng-iseng ingin menjalankan Alpine JS di SvelteKit. Kita buat dah kodenya seperti ini:

```html
<div class="" x-data='{nama: "Zen"}'>
	<div class="" x-text='"Hello " + nama'></div>
</div>
```

Harusnya kan muncul `Hello Zen`. Tapi, kok hasilnya malah seperti ini:

_Error di browser_:

```
500
Failed to fetch dynamically imported module: http://localhost:3000/src/routes/index.svelte

TypeError: Failed to fetch dynamically imported module: http://localhost:3000/src/routes/index.svelte
```

_Error di Terminal_:

```
08.53.07 [vite] Internal server error: Expected }
  Plugin: vite-plugin-svelte
  File: /home/zen/aplikasi-android/tes/app/src/main/assets/src/routes/index.svelte
  1: <div class="" x-data='{nama: "Zen"}'>
                                ^
  2:   <div class="" x-text='"Hello " + nama'></div>
  3: </div>
```

Ternyata, kalau di Svelte itu, curly bracket merupakan cara menjalankan kode JS maupun kode Svelte di dalam markup. Misalnya aja seperti `{#if condition}{/if}` dan `{each data as x}{/each}`.

Maka, kita harus raw atau mematikan kodenya supaya nggak dianggap seperti sintaks JS maupun sintaks Svelte. Maka, di dalam curly bracket, kita buat seperti ini:

```html
<div class="" x-data={``}></div>
```

Nah, secara otomatis, semua di dalam tanda petik itu dianggap sebagai string dan nggak dirender dengan Svelte.

Hasil HTMLnya:

```html
<div class="" x-data=""></div>
```

Maka, sekarang, kita ubah lagi kode yang sebelumnya error menjadi seperti ini:

```html
<div class="" x-data={`{nama: "Zen"}`}>
	<div class="" x-text='"Hello " + nama'></div>
</div>
```

Hasilnya:

```html
<div class="" x-data="{nama: &quot;Zen&quot;}"><div class="" x-text="&quot;Hello &quot; + nama"></div></div>
```

Kode Alpine JSnya dirender oleh browser sehingga menjadi:

```
Hello Zen
```