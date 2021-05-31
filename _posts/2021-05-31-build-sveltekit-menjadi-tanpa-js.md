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