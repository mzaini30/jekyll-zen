---
layout: post
title: Meningkatkan Produktivitas dengan Splitting Terminal
image: https://www.northeastohioparent.com/wp-content/uploads/2019/06/bigstock-Hacker-Using-Laptop-With-Binar-257453926.jpg
category: linux
---

Bagi seorang developer, apapun divisinya, yang namanya Terminal adalah tools yang paling sering digunakan. Dengan Terminal itulah kita bisa melakukan tugas yang sangat sederhana seperti ping Google hingga tugas yang lumayan berat seperti testing image Docker di VPS via SSH.

Nah, maka ketika kita tau cara untuk mengelola Terminal dengan lebih baik, pekerjaan kita bisa lebih efisien. Salah satu teknik mengelola terminal adalah dengan menggunakan teknik splitting Terminal seperti ini:

![Contoh splitting Terminal di Termux](https://i.ibb.co/TcLBPkH/Screenshot-2021-05-28-05-52-47-02-84d3000e3f4017145260f7618db1d683.png)

Jadi, kita menggunakan aplikasi tmux untuk bisa membelah Terminal.

Untuk instalasi, kalau kamu pakai Termux, perintahnya adalah:

```bash
pkg install tmux
```

Kalau pakai Linux, perintahnya adalah:

```bash
sudo apt install tmux
```

Lalu, untuk menjalankannya, bisa mengetikkan perintah:

```bash
tmux
```

Kalau aku sih, dibuat otomatis aja dengan cara menambahkan perintah tmux di Bashrc (Linux: ~/.bashrc, Termux: /data/data/com.termux/files/usr/etc/bash.bashrc).

Nah sekarang, kalau kita buka Terminal atau Termux, tmux akan dijalankan otomatis. Sekarang, kita coba main splitting-splitting.

Untuk splitting vertikal (dibelah jadi sisi kiri dan sisi kanan), caranya adalah pencet Ctrl b, terus dilepas, terus pencet %

Untuk splitting horizontal (dibelah jadi sisi atas dan sisi bawah), caranya adalah pencet Ctrl b, terus dilepas, terus pencet "

Untuk menghapus sisi yang aktif, pencet Ctrl d

Untuk fokus ke salah satu sisi sehingga jadi full, pencet Ctrl b, terus dilepas, terus pencet z

Untuk lepas dari fokus, pencet Ctrl b, terus dilepas, terus pencet z

Untuk mode scroll, pencet Ctrl b, terus dilepas, terus pencet [

Untuk lepas dari mode scroll, pencet Esc

Untuk berpindah ke sisi kanan (cursor dari sisi kiri, ke sisi kanan), pencet Ctrl b, terus dilepas, terus pencet panah kanan. Begitu pula untuk ke sisi atas, bawah, dan kiri.

Untuk memperbesar sisi aktif ke kanan, pencet Ctrl b, terus dilepas, terus pencet Ctrl bersamaan dengan panah kanan, jangan dilepas, tahan terus Ctrl sambil pencet panah kanan berkali-kali untuk memperbesar sesuai dengan lebar yang diinginkan.

Selamat mencoba~

Kalau nggak dicoba, pusing sendiri biasanya. Kalau dicoba terus, ntar hapal sendiri.
