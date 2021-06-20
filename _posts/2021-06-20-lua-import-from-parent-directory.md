---
layout: post
title: "Lua: Import from Parent Directory"
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

