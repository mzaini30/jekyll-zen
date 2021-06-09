---
layout: post
title: Redirect di SvelteKit
image: https://www.7riversalliance.org/wp-content/uploads/2015/05/location-location-location.png
category: svelte
---

```html
<script>
	import {goto} from '$app/navigation'
	import {browser} from '$app/env'
	if (browser) {
		goto('/dashboard')
	}
</script>
```