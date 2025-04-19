---
layout: page
title: "Blogs"
permalink: /blogs/
---

# 📝 My Blog Posts

Welcome to my blog collection! 🚀

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }})
{% endfor %}
