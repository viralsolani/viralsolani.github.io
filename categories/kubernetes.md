---
layout: default
title: "Category: Kubernetes"
permalink: /categories/kubernetes/
---

<h2>Posts in Kubernetes</h2>

<ul>
  {% for post in site.categories.Kubernetes %}
    <li><a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date: "%b %d, %Y" }})</li>
  {% endfor %}
</ul>
