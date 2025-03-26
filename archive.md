---
layout: page
title: Archive
permalink: https://lagamma-arianna.github.io/root-logs/archive/
---

## 📂 Blog Archive

<ul>
  {% for post in site.posts %}
    <li>
      <strong>{{ post.date | date: "%d %b %Y" }}</strong> —
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>


