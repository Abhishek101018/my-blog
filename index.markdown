---
layout: default
title: Home
---

<h2>📬 Recent Posts</h2>

<ul>
  {% for post in site.posts %}
    <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
