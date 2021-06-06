---
layout: post
title: Menyesuaikan Hasil SvelteKit untuk assets Android Studio
image: https://www1-lw.xda-cdn.com/files/2016/04/Android-Studio.jpg
category: svelte
---

```javascript
import replace from 'replace'

replace({
	regex: '/\./(.+)#',
	replacement: '/./$1/index.html',
	paths: ['build'],
	recursive: true,
	include: '*.html,*.css'
})

replace({
	regex: '/\./',
	replacement: 'file:///android_asset/build/',
	paths: ['build'],
	recursive: true,
	include: '*.html,*.css'
})```
