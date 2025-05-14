---
layout: default
title: "Category: GitLab"
permalink: /categories/gitlab/
---

<h2>Posts in GitLab</h2>

<ul>
  {% for post in site.categories.gitlab %}
    <li><a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date: "%b %d, %Y" }})</li>
  {% endfor %}
</ul>
