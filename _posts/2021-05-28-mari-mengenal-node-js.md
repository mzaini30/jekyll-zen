---
layout: post
title: Mari Mengenal Node JS
category: javascript
image: https://aventislearning.com/wp-content/uploads/2020/06/Node.js.png
---

Node JS singkatnya adalah tools supaya kita bisa menjalankan JavaScript di luar lingkungan browser. 

Itu sih.

Misalnya aja, untuk menampilkan Hello World, kita biasanya menjalankan seperti ini di Console browser:

```javascript
console.log('Hello World')
```

Maka, kita pun bisa juga menjalankannya _di luar browser_ menggunakan Node JS.

Keren kan?

Untuk menginstall Node JS, kalau di Termux, perintahnya adalah `pkg install nodejs`. Sedangkan kalau di Linux, perintahnya adalah `sudo apt install nodejs`.

Untuk menjalankan `index.js` dengan Node JS, perintahnya cukup dengan `node index.js`

Simpel banget kan?

Nah, coba deh setelah berhasil menginstall Node JS, kita buat `index.js` yang berisi:

```javascript
console.log('Hello World')
```

Lalu, kita jalankan dengan `node index.js`:

![Hasilnya script Node JS yang kita jalankan tadi](https://i.ibb.co/GCBWyQS/image.png)

Nah sekarang berarti kita sudah siap coding dengan JavaScript **di manapun!**

Sekarang, kita coba buat kode JavaScript yang lebih panjang dikit di `jika.js`:

```javascript
const nilai = 80
const nilaiYangDiharapkan = 100

function tulis(teks){
	console.log(teks)
}

if (nilai < nilaiYangDiharapkan) {
	tulis('Nggak papa deh. Nanti usaha lagi...')
} else {
	tulis('Mantap.....')
}
```

Kemudian, kita jalankan dengan `node jika.js`:

![Hasilnya dengan kode JavaScript yang agak panjang dikit](https://i.ibb.co/xL3jRdN/image.png)

Nah, sekarang kita coba menggunakan kode dari eksternal menggunakan bantuan NPM (Node Package Manager).

Oh iya, walaupun versi officialnya menggunakan npm untuk export import module JavaScript, aku lebih menyarankan menggunakan pnpm karena pnpm mendukung fitur caching. Jadi, jika kita pernah mendownload modul tertentu, kita nggak perlu mendownloadnya lagi jika menggunakan pnpm.

Untuk menginstall pnpm, jalankan perintah berikut:

```bash
npm i -g pnpm
```

Sekarang, kita coba menggunakan modul JavaScript yang sudah ada.

Nah, di folder latihan kita tadi, jalankan perintah:

```bash
npm init -y
```

Secara otomatis, akan terbuat file `package.json` yang isinya:

```json
{
  "name": "node-js",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

Setelah jadi file `package.json`, langsung aja kita buat file `.gitignore` yang berisi:

```
node_modules
```

Jadi, kalau nanti kita upload ke Github, dia akan mengabaikan folder node_modules.

Sekarang, kita tambahkan `"type": "module"` di situ sehingga menjadi:

```json
{
  "name": "node-js",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "type": "module"
}
```

Mengapa kita menggunakan type module? Ya karena lebih enak aja sih dilihat untuk sintaks export/importnya. Jadi, perbedaannya itu seperti ini:

**Common JS (cjs)**

_Import_

```javascript
const nama = require('nama')
```

_Named Export_

```javascript
module.exports = {tools}
```

_Default Export_

```javascript
function perintahnya(){
	console.log('Hello World')
}
module.exports = perintahnya
```

**Module JS (cjs)**

_Import_

```javascript
import nama from 'nama'
```

_Named Export_

```javascript
export const tools = 123
```

_Default Export_

```javascript
function perintahnya(){
	console.log('Hello World')
}
export default perintahnya
```

Sekarang, kita coba import module dari NPM.

Kita akan menggunakan module `is-even` untuk mengecek apakah suatu bilangan itu genap.

Masih di folder kita tadi, yang sudah ada file `package.json`, 

Kemudian, jalankan perintah:

```bash
pnpm i -D is-even
```

Lalu, kita buat file `genapKah.js` yang isinya:

```javascript
import genapKah from 'is-even'

console.log(`genap kah 34? ${genapKah(34)}`)
console.log(`genap kah 99? ${genapKah(99)}`)
```

Cara menjalankannya:

```bash
node genapKah.js
```

Hasilnya:

![Cek genap kah](https://i.ibb.co/Ytb4kWK/image.png)

Mudah kan coding dengan JavaScript?