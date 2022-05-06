---
title: Renju
permalink: /renju
tags: [gaming, chess]
image: /assets/img/pages/renju.jpg
spellcheck: off
---

<div class='d-flex flex-row flex-wrap'>
  {% assign pages  = site.pages | where: 'parent', 'renju' %}
  {% for page in pages %}
  <div class="col-3">
    <a href="{{ page.permalink }}">
      <img class="gallery-item-image" src="{{ page.image }}"/>
    </a>
  </div>
  {% endfor %}
</div>
