---
layout: post
title: Cara Edit CSS Tanpa Reload dan Tanpa Framework JS
image: https://cdn.shopify.com/s/files/1/0698/1729/products/RMA-002A-sfw_fe2f44a9-24ed-42bf-8d74-8a64f9f28894_grande.gif?v=1518750667
category: css
---

Sebagai developer frontend, tentu seringkali berkutat dengan framework JavaScript yang menawarkan pengalaman development yang menyenangkan seperti sintaks-sintaks JavaScript yang reactive dan styling yang mudah dengan Tailwind serta tentunya adalah halaman website yang berubah tanpa sama sekali reload.

Tapi, bagaimana jika kita bisa melakukannya tanpa menggunakan framework JavaScript?

Trik ini sebenarnya sudah cukup lama aku gunakan tapi mulai jarang aku gunakan karena udah asyik bermain dengan SvelteKit. Tapi, tentu nggak ada salahnya jika kita coba kembali, apalagi jika kita hanya membuat website yang ringan-ringan aja.

Pertama, kita membutuhkan **Firefox**. Kalau browser lain, nggak bisa.

Nah, sekarang kita buat deh file `index.html` yang isinya:

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>

	<link rel="stylesheet" href="style.css">

</head>
<body>
	
	<div class="container">
		<h1>Hello World</h1>
		<p>My name is Zen</p>
	</div>

</body>
</html>
```

Kemudian, buat `style.css` yang isinya:

```css
hello
```

Intinya sih, diisi asal aja ya file CSSnya.

Sekarang, kita buka `index.html` di Firefox dengan cara double klik atau klik kanan, open with, Firefox.

Hasilnya seperti ini:

![Tampilan sementara](https://i.ibb.co/6tXTSVS/image.png)

Kemudian, kita aktifkan Style Editor dengan memencet Shift f7

![Setelah muncul Style Editor](https://i.ibb.co/grZp7pg/image.png)

Sekarang, kita bisa ubah stylenya sesuka hati.

![Setelah diberi style](https://i.ibb.co/cLmM9PL/image.png)

Ini style yang aku gunakan:

```css
*,
*:before,
*:after {
  margin: 0;
  padding: 0;
  font-family: Candara, sans-serif;
}

.container {
  padding: 20px;
}

h1 {
  color: blue;
}

p {
  color: green;
}
```

Kalau sudah, kita tinggal Ctrl s untuk menyimpannya (atau pencet tulisan Save).