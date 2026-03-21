---
layout: default
title: My Blog
---

Welcome to my blog! Here's my posts.

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) — {{ post.date | date: "%b %-d, %Y" }}
{% endfor %}
