---
title: let dan const pada JavaScript
category: javascript
image: https://www.ateamsoftsolutions.com/wp-content/uploads/2019/07/javascript-logo.jpg
layout: post
---

JavaScript pada awalnya hanya mengenal `var` untuk mendeklarasikan varibel. Contohnya seperti di bawah ini:

```javascript
var nama = 'Zen'
console.log('Halo ' + nama) // Hasil: 'Halo Zen'
```

Namun, seiring perkembangan JavaScript, mulai dari standar di tahun 2015, JavaScript mulai mengenal `let` dan `const` untuk mendeklarasikan variabel. Nah, mengapa tidak menggunakan `var` aja? Ternyata, menggunakan `var` dan tidak menggunakan `var` sama aja. Misalnya, kita mengubah value dari variabel `nama` tadi:

```javascript
var nama = 'Zen'
var nama = 'Alysia'
console.log('Halo ' + nama) // Hasil: 'Halo Alysia'
```

Ada yang aneh? Nah, kita kembali ke teori tadi, bahwasanya `var` digunakan untuk deklarasi variabel. Disebut deklarasi adalah bahwa kita tidak bisa menggunakan `var` kembali. Tapi, di contoh di atas bisa. Harusnya kan seperti ini:

```javascript
var nama = 'Zen'
nama = 'Alysia'
console.log('Halo ' + nama) // Hasil: 'Halo Alysia'
```

Jadi, harusnya `var` itu disebut sekali aja. Makanya, hadirlah `let` dan `const` untuk menggantinya.

## Perbedaan Antara `let` dan `const`

`let` digunakan untuk mendeklarasikan variabel yang bisa diubah nilainya. Sedangkan `const` digunakan untuk mendeklarasikan variabel yang nggak bisa diubah nilainya.

Misalnya:

```javascript
let nama = 'Zen'
nama = 'Alysia'
console.log('Halo ' + nama)
```

Kalau kita menggunakan `const`, nggak bisa kita mengubah nilai dari `nama`:

```javascript
const nama = 'Zen'
nama = 'Alysia' // error
console.log('Halo ' + nama)
```

Jadi, nilai dari `nama` nggak bisa diubah. Dia tetap `Zen` nilainya.

Lalu, walaupun `let` bisa untuk mengubah variabel, dia nggak bisa digunakan untuk mendeklarasikan variabel yang sama dua kali:

```javascript
let nama = 'Zen'
let nama = 'Alysia' // error
console.log('Halo ' + nama)
```

## Apakah Kita Wajib Menggunakan `let` dan `const`?

Mungkin kamu berpikir apakah perlu menggunakan `let` maupun `const` sedangkan tanpa menggunakannya pun bisa:

```javascript
nama = 'Zen'
nama = 'Alysia'
console.log('Halo ' + nama)
```

Nah, kalau kita menggunakan framework JavaScript seperti Svelte, penggunaan `let` dan `const` itu wajib. Aku belum tau sih alasannya karena belum pernah mengetesnya.