---
title: 张艾嘉
permalink: /sylvia-chang
---

<div class='d-flex flex-row flex-wrap'>
  {% assign pages = site.pages | where: 'singer', 'sylvia-chang' %}
  {% for page in pages %}
  <div class="col-12">
    <a href="{{ page.permalink }}">
      <span class="chinese-title-h2">{{ page.title }}</span>
    </a>
  </div>
  {% endfor %}
</div>
