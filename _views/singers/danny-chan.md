---
title: 陈百强
permalink: /danny-chan
---

<div class='d-flex flex-row flex-wrap'>
  {% assign pages = site.pages | where: 'singer', 'danny-chan' %}
  {% for page in pages %}
  <div class="col-12">
    <a href="{{ page.permalink }}">
      <span class="chinese-title-h3">{{ page.title }}</span>
    </a>
  </div>
  {% endfor %}
</div>
