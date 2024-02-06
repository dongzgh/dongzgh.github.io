---
title: Blogs
permalink: /views/blogs
---

## How To

<div class='d-flex flex-row flex-wrap'>
  {% assign filtered_items = site.pages | where: 'medium', 'blog' | where: 'category', 'how-to' %}
  {% for item in filtered_items %}
  <div class="col-12">
    <a href="{{ item.permalink }}">
      <span>{{ item.title }}</span>
    </a>
  </div>
  {% endfor %}
</div>
