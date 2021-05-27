---
layout: post
title: Mudahnya Desain Website dengan Windi dan SvelteKit
image: https://miro.medium.com/max/1024/1*ybIU8NfYytBbrrldiwU87g.png
category: svelte
---

Sebelum memulai artikel ini, pastikan dulu kamu sudah memiliki pnpm dan degit supaya mudah mengikuti artikel ini. Kalau belum punya, install dulu dengan perintah:

```bash
npm i -g pnpm
pnpm i -g degit
```

Kalau sudah ada, kita bisa mulai artikelnya...

Bagi seorang web designer, memilih tools yang tepat akan memudahkan kita dalam menyelesaikan pekerjaan kita dengan lebih cepat. Nah, di sini kita akan menggunakan dua tools yaitu Windi dan SvelteKit. Apa sih perbedaannya dibandingkan tools-tools lainnya?

Pertama, kita ke Windi. Windi adalah tools untuk generate CSS Tailwind. Nah, mengapa nggak langsung pakai Tailwind aja? Kalau menurutku sih, Tailwind itu lambat. Tailwind JIT (Just In Time) yang konsepnya sama kayak Windi aja juga menurutku sama aja dengan Tailwind tanpa JIT. Sama-sama lambat sih. Makanya, aku milih Windi.

Jadi, kode-kodenya Tailwind dan Windi itu sama aja. Cuma, Windi itu generate class CSSnya lebih cepat.

Ya, karena aku pakai laptop jadul aja sih. Jadinya, perbedaan kecepatan sedikit aja, kerasanya beda banget di laptopku.

## Fitur-Fitur Windi

Kemudian, ada beberapa keunggulan di Windi yang setauku belum ada di Tailwind JIT seperti:

### Bisa Desktop First

Kalau di desain menggunakan Tailwind, kita hanya bisa Mobile First seperti ini:

```html
<p class='text-red-500 md:text-purple-500'>Hello World</p>
```

Pada contoh di atas, secara default, teks akan berwarna merah. Jika, pada tampilan desktop ke atas, teks akan berwarna ungu.

Kalau di Windi, kita bisa aja desain tampilan desktopnya terlebih dahulu:

```html
<p class='text-purple-500 <md:text-red-500'>Hello World</p>
```

Arti dari kode di atas adalah secara default, teks berwarna ungu. Jika, pada tampilan _di bawah_ tampilan desktop, teks akan berwarna merah.

Bahkan, kita bisa membuat style khusus untuk tampilan desktop aja, nggak untuk tampilan di atasnya maupun tampilan di bawahnya:

```html
<p class='text-red-500 @md:text-purple-500'>Hello World</p>
```

Arti dari kode di atas: secara default, teks berwarna merah. Ketika pada tampilan desktop (nggak di bawahnya maupun di atasnya), teks berwarna ungu.

### Bisa Grouping Variant

Contohnya:

```html
<div class="bg-white dark:hover:(bg-gray-800 font-medium text-white)"/>
```

Jadi, pada contoh di atas, kita bisa grouping variant dark dan hover yang berisi `bg-gray-800 font-medium text-white`.

### Bisa Kasih `!important`

Jadi ya cuma menambahkan `!` di awal class. Contoh:

```html
<div class="text-red-400 !text-green-300">Green</div>
```

Jadi, kira-kira tuh hasilnya seperti ini:

```css
.text-red-400 {
	color: red;
}

.\!text-green-300 {
	color: green !important;
}
```

### Bisa Membaca CSS Variable

Caranya adalah menambahkan tanda `$` di dalam class Windi.

Contohnya aja, kita mau membaca CSS Variable berikut ini:

```css
:root {
	--warna: green;
}
```

Nah, jadi, kita akan menerapkan warna hijau itu ke tulisan Hello World. Maka, kode HTMLnya akan seperti ini:

```html
<p class='text-$warna'>Hello World</p>
```

### Bisa Menambahkan Alias

Contoh kodenya di config:

```typescript
// windi.config.ts
export default {
  alias: {
    hstack: 'flex items-center',
    // ...
  },
}
```

Kemudian, untuk cara memanggilnya:

```html
<div class="*hstack">
  ...
</div>
```

Dia pakai `*` untuk memanggilnya.

Kemudian, masih ada lagi fitur-fitur Windi lainnya yang belum kusebutkan di sini karena aku belum ada explor lebih jauh lagi. Misalnya aja seperti Attributify. Jadi, dengan Attributify, kita nggak perlu menuliskan kode di dalam attribute class lagi, melainkan menjadi attribute tersendiri seperti ini:

```html
<p
	text='red-500'
	bg='green-700'
	dark='text-light-500'
>
	Hello World
</p>
```

Cuma, entah kenapa, menurutku lebih enak ya kalau langsung dituliskan semuanya di dalam class. Lebih enak dipandang dan mudah untuk copy paste. Hehe.

```html
<p class='text-red-500 bg-green-700 dark:text-light-500'>Hello World</p>
```

Kemudian, ada juga Windi Lang:

```css
@apply font-bold text-lg; /* generate utilities .font-bold .text-lg */

.button {
  @apply px-4 py-2 bg-blue-400 text-white hover:bg-blue-500;
}

.button-red: px-4 py-2 bg-red-500 text-gray-100; /* more simple one line version */

/* generate all different colors */
@for color in colors {
  @apply bg-${color};
}

/* support nested css and variables */
@var borderWidth = 1rem;
.button {
  &:hover {
    border: ${borderWidth + 4px} outset blue;
    background: rbga(${theme('blue.400').toRGB().join(', ')}, var(--button-opacity));
  }
}

/* what about setup config only works in this scope */
@config local {
  colors: {
    ...
  }
}

/* directly interact with JavaScript */
@js {
  import { eval, rgba, get, set } from 'windi/lang';

  const a = get('width');
  set('width', eval('4px'));
  const width = eval('3px');
  export function add(a, b) {
    return a + b;
  }
}

.hello {
  width: ${add(1,2)}rem;
}
```

Satu kata untuk itu: _Wow!_ Keren aja sih ya, Windi bisa eksplor CSS lebih dalam lagi sehingga bisa membuatnya menjadi bahasa tersendiri. Cuma ya aku belum eksplor sampai ke situ sih. Jadi, belum bisa kubahas kali ini. Mungkin nanti aja sih kalau mood.

Sekarang kita bahas SvelteKit.

## Keunggulan SvelteKit

Jadi, SvelteKit itu frameworknya Svelte. Svelte adalah framework JavaScript yang simpel. Kenapa kok bisa dibilang simpel? Ya karena Svelte itu seperti kamu menulis HTML CSS JS biasa aja. Gitu. Beda dengan React yang learning curvenya lumayan. Kalau Svelte, kamu cukup baca tutorialnya aja 30 menit, langsung paham dan bisa langsung buat website.

Kalau SvelteKit, dia melengkapi Svelte dengan tambahan fitur seperti routing, build ke berbagai layanan (Vercel, Netlify, Begin, dll), SSR (Server Site Rendering), dan berbagai fitur lainnya. Oh iya, SvelteKit menerapkan konsep HMR (Hot Module Replacement). Di sini **titik tekannya**. Dengan HMR, ketika mendesain website, kita nggak perlu reload-reload lagi, baik manual maupun otomatis, tetapi ketika kita mengedit kode Svelte, hasilnya akan otomatis muncul di browser **tanpa reload**. Nah. Keren. Itu yang kita perlukan.

## Langsung Praktek Aja Ya Biar Nggak Bingung~

Sekarang, kita langsung praktek. Pertama, download dulu template SvelteKit yang sudah kuolah (udah ada Windi di situ):

```bash
degit mzaini30/svelte latihan-svelte-windi
```

Sekarang, kita masuk ke foldernya dan install semua dependencies yang diperlukan:

```bash
cd latihan-svelte-windi
pnpm i
```

Lalu, kita masukkan ke Sublime Text:

```bash
subl . -a
```

Sekarang, kita jalankan mode dev:

```bash
npm run dev -- --open
```

Maka, secara otomatis, akan terbuka website Svelte kita di browser. Di situ kan masih kosong. Nah, sekarang kita coba isi.

Jadi, kita buka `src/routes/index.svelte`

Sekarang, kita buat judulnya dulu:

```html
<svelte:head>
	<title>Latihan Svelte Windi</title>
</svelte:head>
```

Kemudian, kita coba buat tombol dengan class-class Windi sehingga file index tadi menjadi:

```html
<svelte:head>
	<title>Latihan Svelte Windi</title>
</svelte:head>

<div class="p-10">
	<a href="/" class="pt-3 pb-2 px-6 bg-green-300 border border-3 font-bold border-green-500 rounded-4xl text-green-700">Ke Beranda</a>
</div>
```

Hehe. Kaget dengan kodenya yang panjang ya? Tapi, dengan class yang panjang itu, semuanya jadi jelas kok itu link kita apain aja:

| Class | Maksudnya |
|---|---|
| p-10 | padding 10 * 0.25 rem |
| pt-3 | padding top 3 * 0.25 rem |
| pb-2 | padding bottom 2 * 0.25 rem |
| px-6 | padding left & right 6 * 0.25 rem |
| bg-green-300 | background color green palet ke 300 |
| border | border |
| border-3 | border line height 3 * 0.25 |
| font-bold | font weight bold |
| border-green-300 | border color green palet ke 300 |
| rounded-4xl | border radius ukuran 4 xl |
| text-green-700 | color green palet ke 700 |

Nah, jadinya kan sangat deskriptif banget ya dengan apa yang kita lakukan pada setiap elemen HTML.

Hasilnya seperti ini:

![Hasil Windi](https://i.ibb.co/Sn9v7xD/image.png)

Sekarang kita akan coba buat jika dalam mode desktop (jadi, yang kode tadi itu kita anggap untuk mode mobile):

```html
<svelte:head>
	<title>Latihan Svelte Windi</title>
</svelte:head>

<div class="p-10">
	<a href="/" class="
		pt-3 pb-2 px-6 bg-green-300 border border-3 font-bold border-green-500 rounded-4xl text-green-700
		md:(border-red-500 text-red-700 bg-red-300 rounded-none)
	">Ke Beranda</a>
</div>
```

Jadi, untuk mode desktop, kita desain tombolnya berwarna merah dan nggak ada roundednya. Kodenya adalah di dalam `md:()`.

Hasilnya untuk mode desktop:

![Hasil Windi tampilan desktop](https://i.ibb.co/wQtqfpg/image.png)

Mudah aja kan ya?

Kemudian, untuk generate project Svelte tadi menjadi HTML biasa, cukup dengan perintah:

```bash
npm run build
```

Hasil buildnya ada di folder `build/`