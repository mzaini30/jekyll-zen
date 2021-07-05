---
layout: post
title: Self Closing JSX di Sublime Text Editor
image: https://soshace-12d3e.kxcdn.com/wp-content/uploads/2019/10/JSX-vs-HTML-inside.jpg
category: sublime
---

## Masalahnya

Kalau kita Emmet di JSX, dengan `<input` harusnya jadi `<input type='text'/>`, tapi jadinya malah `<input type='text'>`

## Caranya

Ctrl Shift p

Pilih `Emmet Settings`

Masukkan kode berikut:

```json
"config": {
	"jsx": {
		"options": {
			"output.selfClosingStyle": "xml"
		}
	}
}
```