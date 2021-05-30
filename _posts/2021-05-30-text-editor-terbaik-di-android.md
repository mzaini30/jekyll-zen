---
layout: post
title: Text Editor Terbaik untuk Android
image: https://ggia.berkeley.edu/assets/general/GGIA-ExpressiveWriting.jpg
category: android
---

Coding di Android adalah tantangan tersendiri. Soalnya kan kalau di laptop itu enak, ada 10 jari. Kalau pakai HP, cuma bisa pakai dua jempol. Capek sih. Tapi kadang kita perlu ngedit kode di HP. Misalnya aja kita lagi jalan dan nggak bawa laptop, lalu tiba-tiba ditelpon sama klien untuk memperbaiki error yang muncul di website yang kita buat, ya akhirnya mau nggak mau sih pakai HP aja ngeditnya. Itu kalau kodenya nggak terlalu ribet sih. Kalau terlalu ribet ya bingung juga kita. Hehe.

Nah sekarang, bagusnya pakai text editor apa ni untuk di HP? Kalau cari yang bagus sih, nggak ada habisnya karena ya masing-masing mengatakan bahwa text editor pilihannya adalah yang terbaik. Tapi, jika aku ditanya: Apakah text editor terbaik menurutmu? Mungkin aku akan menjawab **micro**!

Seperti inilah tampilan micro:

![Tampilan micro editor](https://i.ibb.co/D8z6mbm/Screenshot-2021-05-30-10-31-44-35-84d3000e3f4017145260f7618db1d683.png)

Ini tampilan micro saat membuka file HTML:

![File HTML di micro](https://i.ibb.co/CQMm46K/Screenshot-2021-05-30-10-34-27-41-84d3000e3f4017145260f7618db1d683.png)

Ini tampilan saat membuka file JavaScript:

![micro membuka file JavaScript](https://i.ibb.co/sCzgChG/Screenshot-2021-05-30-10-38-23-68-84d3000e3f4017145260f7618db1d683.png)

Sintaks highlightingnya sudah otomatis menyesuaikan dengan ekstensi file. Jadinya lebih nyaman saat kita coding.

## Mulai Menggunakan

Untuk menginstall micro, kita ketikkan perintah ini di Termux:

```bash
pkg install micro
```

Untuk membuka file `index.js` di micro, kita cukup jalankan perintah:

```bash
micro index.js
```

Lalu, saat pertama kali menggunakan micro, dia nggak wrapping teks. Jadi, kita pencet Ctrl e, lalu ketikkan perintah:

```bash
set softwrap on
```

Lalu pencet Enter.

Untuk keluar dari editor, pencet Ctrl q

Untuk menyimpan file, pencet Ctrl s

Untuk duplicate line, pencet Ctrl d

Untuk undo, pencet Ctrl z

Untuk redo, pencet Ctrl y

Jadi, cocok banget ya buat coding di HP. Pakai micro, lalu dikombinasikan dengan [tmux](/meningkatkan-produktivitas-dengan-splitting-terminal/).
