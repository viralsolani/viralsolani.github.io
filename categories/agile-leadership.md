---
layout: default
title: "Category: Agile Leadership"
permalink: /categories/agile-leadership/
---

<h2>Posts in Agile Leadership</h2>

<ul>
  {% for post in site.categories["Agile Leadership"] %}
    <li><a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date: "%b %d, %Y" }})</li>
  {% endfor %}
</ul>
