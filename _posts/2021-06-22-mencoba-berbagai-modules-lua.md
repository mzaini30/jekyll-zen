---
layout: post
title: Mencoba Berbagai Modules Lua
category: lua
image: https://unctad.org/sites/default/files/inline-images/Creative-Economy-IP-CCIs-2-800x450px_0.jpg
---

Lua adalah bahasa pemrograman yang kecil, sederhana, dan cepat. Kalau kamu baru mendengar apa itu Lua, mungkin kamu bisa membaca artikelku sebelumnya tentang [pengantar Lua](/yuk-berkenalan-dengan-bahasa-pemrograman-lua/). Kalau sudah, ayo kita mulai.

Jadi, kita akan mencoba berbagai modules Lua yang terdapat di situs Luarocks. Oh iya, sebelumnya, install dulu Lua dan Luarocks. Lalu, kita buat dulu file rockspec (mirip dengan package.json di Node JS) dengan perintah:

```bash
luarocks write_rockspec
```

Kalau di laptopku, akan terbuat file `nyoba-lua-dev-1.rockspec`

Terus, kalau kita ingin menambah modules, kita edit di file rockspec itu dengan kode seperti ini:

```lua
dependencies = {
	'module1',
	'module2',
	'module3'
}
```

Lalu, kita install dengan 

```bash
sudo luarocks install --only-deps nyoba-lua-dev-1.rockspec
```

## f-strings

Ini module favoritku nih. Contoh cara menggunakannya:

```lua
local f = require 'F'
local nama = 'Zen'

print(f'Hello {nama}')
```

Hasilnya:

```
Hello Zen
```

## dump

Kalau dump ini fungsinya seperti JSON.parse() kalau di JavaScript.

Contoh kodenya:

```lua
local dump = require 'dump'

local data = {
	{
		nama = 'Zen',
		kelas = 1
	},
	{
		nama = 'Maryam',
		kelas = 2
	}
}

print(dump(data))
```

Hasilnya:

```
{
    [1] = {
        kelas = 1,
        nama = "Zen"
    },
    [2] = {
        kelas = 2,
        nama = "Maryam"
    }
}
```

## md5

Ini untuk encrypt satu arah (yang fitur encrypt decryptnya aku belum nyoba sih. Masih gagal tadi). Contohnya:

```lua
local md5 = require 'md5'
local f = require 'F'

local teks = {
	'Zen',
	'Halo semuanyaaa...',
	'Teks ketiga'
}

print('~~~~~ MD5 SUMHEXA: ~~~~~\n')

for n = 1, #teks do
	print(f[[{teks[n]}
{md5.sumhexa(teks[n])}
]])
end

print('~~~~~ MD5 SUM: ~~~~~\n')

for n = 1, #teks do
	print(f[[{teks[n]}
{md5.sum(teks[n])}
]])
end
```

Hasilnya:

```
~~~~~ MD5 SUMHEXA: ~~~~~

Zen
e566cc5f20887adf2bad47f5389ba59a

Halo semuanyaaa...
8094bbc9df3e9348c940fb2da87e567a

Teks ketiga
c648ef54883fb8ee08a1084d94e270f6

~~~~~ MD5 SUM: ~~~~~

Zen
 zG8

Halo semuanyaaa...
>H-~Vz

Teks ketiga
M
```

## ansicolors

Ini untuk menambahkan warna pada kode Lua kita. Contohnya:

```lua
local colors = require 'ansicolors'

print(colors('%{red}Seluruh kota%{reset}'))
print(colors('%{dim underline}Merupakan tempat bermain yang asyik%{reset}'))
print(colors('%{magentabg reverse}Oh senangnyaaa... aku senang sekali...%{reset}'))
```

Hasilnya:

![Kode Lua dengan warna](https://i.ibb.co/HpKRCyv/image.png)

## argparse

Untuk menampilkan --help dalam menggunakan aplikasi. Contohnya:

```lua
local argparse = require "argparse"

local parser = argparse("lua argumen.lua", "Contoh...")

parser:argument("input", "Input file.")

parser:option("-o --output", "Output file.", "a.out")
parser:option("-I --include", "Include locations."):count("*")

local args = parser:parse()
```

Contoh cara menjalankan:

```bash
lua argumen.lua --help
```

Hasilnya:

```
Usage: lua argumen.lua [-h] [-o <output>] [-I <include>] <input>

Contoh...

Arguments:
   input                 Input file.

Options:
   -h, --help            Show this help message and exit.
         -o <output>,    Output file. (default: a.out)
   --output <output>
          -I <include>,  Include locations.
   --include <include>
```