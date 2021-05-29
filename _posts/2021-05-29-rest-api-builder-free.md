---
layout: post
title: 'Excalibur: REST API Builder 100% Free (Powered by Nasihosting)'
image: https://pm1.narvii.com/6869/6d032598525b257dfa362c773d44c44b558da555r1-1024-768v2_hq.jpg
category: php
---

Sebagai programmer frontend, pengennya sih main di frontend aja, nggak perlu ngurusin backend juga. Makanya, akhirnya aku buat tools bernama Excalibur yang bisa membuat kita generate REST API secara otomatis.

Excalibur ini kisahnya aku ambil dari Noble Phantasmnya Arthuria Saber dari anime Fate Series. Nah, Noble Phantasm yang bernama Excalibur ini adalah Noble Phantasm yang terkuat jika dibandingkan dengan yang lainnya.

## Menggunakan Excalibur

Oke, kita langsung aja buat skenarionya. Kisahnya, kita akan buat website buku tamu nikahan yang membutuhkan field _nama_ dan _alamat_. Jadi, kita buka dulu excalibur.nasihosting.com

Begini tampilannya:

![Excalibur](https://i.ibb.co/5j4XQps/excalibur.png)

Sekarang, klik bagian `Tambah Database`:

![Isi di Excalibur](https://i.ibb.co/rHfGqzS/image.png)

Di form, kita masukkan **nama, alamat**

Lalu, pencet Enter.

![Hasilnya](https://i.ibb.co/7WDdds7/image.png)

Hasilnya, kita mendapatkan ID **78203471258347b1c3753a4c60106619** dan keterangan kolom: **id, nama, alamat**

Nah, bagian itu kita catat dulu ya...

Sekarang, kita klik Olah SQL.

Masukkan ID tadi di ID Database lalu pencet Enter.

Kemudian, di form yang besar, kita masukkan SQL yang kita inginkan. Contohnya aja:

```sql
tambah
insert into [db] (nama, alamat) values ([nama], [alamat])

ambil
select * from [db] order by id desc

hapus-nama
delete [db] where nama = [nama]
```

Lalu, klik Update.

![Habis input SQL di Excalibur](https://i.ibb.co/XSdSkc7/image.png)

## Masuk ke Bagian Frontend

Kemudian, untuk mengolah APInya seperti ini:

### Tambah Data

```javascript
import axios from 'axios'
import qs from 'qs'

const bukuTamu = '78203471258347b1c3753a4c60106619'
const sql = 'https://excalibur.nasihosting.com/sql.php'

async function tambah(){
	const data = await axios.post(sql, qs.stringify({
		id: bukuTamu,
		kunci: 'tambah',
		nama: 'Maryam',
		alamat: 'Samarinda'
	}))
	if (data) {
		console.log('Data sudah ditambahkan')
	}
}
tambah()
```

### Ambil Data

```javascript
import axios from 'axios'
import qs from 'qs'

const bukuTamu = '78203471258347b1c3753a4c60106619'
const sql = 'https://excalibur.nasihosting.com/sql.php'

async function ambil(){
	let data = await axios.post(sql, qs.stringify({
		id: bukuTamu,
		kunci: 'ambil'
	}))
	data = data.data
	console.log(data)
}
ambil()
```

### Hapus Data

```javascript
import axios from 'axios'
import qs from 'qs'

const bukuTamu = '78203471258347b1c3753a4c60106619'
const sql = 'https://excalibur.nasihosting.com/sql.php'

async function hapus(){
	const data = await axios.post(sql, qs.stringify({
		id: bukuTamu,
		kunci: 'hapus',
		nama: 'Zen'
	}))
	if (data) {
		console.log('Data sudah dihapus')
	}
}
hapus()
```