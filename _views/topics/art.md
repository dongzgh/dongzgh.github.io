---
title: Art
permalink: /views/art
---

<div class='d-flex flex-row flex-wrap'>
  {% assign filtered_items = site.pages | where: 'tags', 'art' %}
  {% for item in filtered_items %}
  <div class="col-3">
    <a href="{{ item.permalink }}">
      <img class="gallery-item-image" src="{{ item.image }}"/>
    </a>
  </div>
  {% endfor %}
</div>
