---
layout: post
title: "Lua: Import from Parent Directory (Relative PATH)"
category: lua
image: https://i1.wp.com/techmoran.com/wp-content/uploads/2017/08/parcel-scam-shutterstock-291281267.jpg?fit=768%2C576&ssl=1
---

Misalnya kita memiliki dua file Lua:

- app.lua
- data.lua

Kita bisa mengimport data.lua di app.lua dengan sintaks seperti ini:

```lua
local data = require 'data'

print(data)
```

Atau, misalnya kita memiliki file serperti ini:

- app.lua
- config/data.lua

Kita bisa import config/data.lua di app.lua dengan kode seperti ini:

```lua
local data = require 'config.data'

print(data)
```

Lalu, bagaimana jika yang mau kita import itu di parent folder? Misalnya aja dengan struktur seperti ini:

- aplikasi/app.lua
- data.lua

Kita coba import seperti ini:

```lua
local data = require '../data'

print(data)
```

Apa yang terjadi?

Hasilnya malah error:

```
lua: app.lua:1: module '../data' not found:
        no field package.preload['../data']
        no file './///data.lua'
        no file '/usr/local/share/lua/5.1////data.lua'
        no file '/usr/local/share/lua/5.1////data/init.lua'
        no file '/usr/local/lib/lua/5.1////data.lua'
        no file '/usr/local/lib/lua/5.1////data/init.lua'
        no file '/usr/share/lua/5.1////data.lua'
        no file '/usr/share/lua/5.1////data/init.lua'
        no file './///data.so'
        no file '/usr/local/lib/lua/5.1////data.so'
        no file '/usr/lib/x86_64-linux-gnu/lua/5.1////data.so'
        no file '/usr/lib/lua/5.1////data.so'
        no file '/usr/local/lib/lua/5.1/loadall.so'
        no file './.so'
        no file '/usr/local/lib/lua/5.1/.so'
        no file '/usr/lib/x86_64-linux-gnu/lua/5.1/.so'
        no file '/usr/lib/lua/5.1/.so'
        no file '/usr/local/lib/lua/5.1/loadall.so'
stack traceback:
        [C]: in function 'require'
        app.lua:1: in main chunk
        [C]: ?
```

Wow! Kok bisa ya? Berarti Lua nggak mendukung relative path import dong...

Eits tunggu dulu, bisa diatasi..

Sekarang, kita cek dulu PATHnya dengan perintah:

```lua
print(package.path)
```

Hasilnya:

```
./?.lua;/usr/local/share/lua/5.1/?.lua;/usr/local/share/lua/5.1/?/init.lua;/usr/local/lib/lua/5.1/?.lua;/usr/local/lib/lua/5.1/?/init.lua;/usr/share/lua/5.1/?.lua;/usr/share/lua/5.1/?/init.lua
```

Kalau kita rapikan, akan seperti ini:

```
./?.lua;
/usr/local/share/lua/5.1/?.lua;
/usr/local/share/lua/5.1/?/init.lua;
/usr/local/lib/lua/5.1/?.lua;
/usr/local/lib/lua/5.1/?/init.lua;
/usr/share/lua/5.1/?.lua;
/usr/share/lua/5.1/?/init.lua
```

Perhatikan pada bagian `./?.lua;` Itu artinya, ketika kita menjalankan perintah:

```lua
local data = require 'data'
```

Pertama kali akan menjalankan:

```
./data.lua
```

Kalau nggak ada, dia akan cek di PATH lainnya:

```
/usr/local/share/lua/5.1/data.lua;
/usr/local/share/lua/5.1/data/init.lua;
/usr/local/lib/lua/5.1/data.lua;
/usr/local/lib/lua/5.1/data/init.lua;
/usr/share/lua/5.1/data.lua;
/usr/share/lua/5.1/data/init.lua
```

Misal kita lihat di kode yang tadi:

```lua
local data = require '../data'
```

Itu kan, artinya sama aja dengan:

```lua
local data = require 'data'
```

Aslinya memang, nggak bisa kita import dari parentnya. Nah, solusinya adalah memasukkan `../?.lua` ke dalam list PATH. Oke, kita mulai.

## Mulai Coding

Kita buat folder. 

Di dalam folder itu, kita jalankan:

```bash
luarocks write_rockspec
```

Maka, akan terbuat file `nyoba-lua-dev-1.rockspec` yang isinya:

```lua
package = "nyoba-lua"
version = "dev-1"
source = {
   url = "*** please add URL for source tarball, zip or repository here ***"
}
description = {
   homepage = "*** please enter a project homepage ***",
   license = "*** please specify a license ***"
}
build = {
   type = "builtin",
   modules = {}
}
```

Lalu, kita tambahkan kode berikut di paling bawahnya:

```lua
dependencies = {
	'f-strings'
}
```

Lalu, kita jalankan:

```bash
sudo luarocks install --only-deps nyoba-lua-dev-1.rockspec
```

Maka, secara otomatis, f-strings terinstall jika belum diinstall.

Sekarang, kita buat file data.lua yang isinya:

```lua
return 'hello world'
```

Kemudian, buat file aplikasi/app.lua yang isinya:

```lua
local f = require 'F'
package.path = f'{package.path};../?.lua'

local data = require 'data'

print(data)
```

Hasilnya:

```
hello world
```

Sip. Berhasil.