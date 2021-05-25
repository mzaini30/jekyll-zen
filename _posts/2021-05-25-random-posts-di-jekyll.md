---
layout: post
title: Random Posts di Jekyll
image: https://i1.wp.com/blog.hostdime.com.co/wp-content/uploads/jekyll-logo.jpg?resize=362%2C252
category: jekyll
---

```liquid
{% raw %}{% assign n = site.posts | size %}
{% assign posts = site.posts | sample: n %}
{% for x in posts %}
	{{ x.title }}
{% endfor %}{% endraw %}
```