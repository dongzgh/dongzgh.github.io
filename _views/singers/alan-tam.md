---
title: 谭咏麟
permalink: /alan-tam
---

<div class='d-flex flex-row flex-wrap'>
  {% assign pages = site.pages | where: 'singer', 'alan-tam' %}
  {% for page in pages %}
  <div class="col-12">
    <a href="{{ page.permalink }}">
      <span class="chinese-title-h2">{{ page.title }}</span>
    </a>
  </div>
  {% endfor %}
</div>
