---
layout: default
title: "Category: DevOps"
permalink: /categories/devops/
---

<h2>Posts in DevOps</h2>

<ul>
  {% for post in site.categories.devops %}
    <li><a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date: "%b %d, %Y" }})</li>
  {% endfor %}
</ul>
