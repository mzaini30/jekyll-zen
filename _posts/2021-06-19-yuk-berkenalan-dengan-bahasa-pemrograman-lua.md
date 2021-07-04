---
layout: post
title: Yuk Berkenalan dengan Bahasa Pemrograman Lua
category: lua
image: https://develop.spacemacs.org/layers/+lang/lua/img/lua.gif
---

Bahasa pemrograman Lua adalah bahasa pemrograman yang sintaksnya sederhana, bahasa scripting, interpreternya ukurannya kecil, dan cepat. Bahasa pemrograman ini dibuat pada tahun 1993 (lebih tua 2 tahun dibandingkan JavaScript) oleh Roberto Ierusalimschy, Luiz Henrique de Figueiredo, dan Waldemar Celes yang merupakan anggota dari the Computer Graphics Technology Group (Tecgraf) di the Pontifical Catholic University of Rio de Janeiro, in Brazil.

Contoh dari betapa sederhananya sintaks Lua adalah seperti ini:

```lua
print("Hello World")
```

Yang akan menghasilkan Hello World.

Atau, kita coba dengan operasi matematika sederhana:

```lua
local f = require("F")

io.write("Masukkan angka pertama: ")
local pertama = io.read()
pertama = tonumber(pertama)

io.write("Masukkan angka kedua: ")
local kedua = io.read()
kedua = tonumber(kedua)

print(f("{pertama} + {kedua} = {pertama + kedua}"))
```

Hasilnya:

```
Masukkan angka pertama: 1
Masukkan angka kedua: 2
1 + 2 = 3
```
