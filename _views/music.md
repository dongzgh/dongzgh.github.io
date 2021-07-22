---
title: Music
permalink: /views/music
---

## Songs

<div class='d-flex flex-row flex-wrap'>
  {% assign pages1  = site.pages | where: 'tags', 'music' %}
  {% assign pages2 = pages1 | where: 'tags', 'song' %}
  {% for page in pages2 %}
  <div class="col-3">
    <a href="{{ page.permalink }}">
      <img class="gallery-item-image" src="{{ page.image }}"/>
    </a>
  </div>
  {% endfor %}
</div>

## Instruments

<div class='d-flex flex-row flex-wrap'>
  {% assign pages1  = site.pages | where: 'tags', 'music' %}
  {% assign pages2 = pages1 | where: 'tags', 'instrument' %}
  {% for page in pages2 %}
  <div class="col-3">
    <a href="{{ page.permalink }}">
      <img class="gallery-item-image" src="{{ page.image }}"/>
    </a>
  </div>
  {% endfor %}
</div>

## Theories

<div class='d-flex flex-row flex-wrap'>
  {% assign pages1  = site.pages | where: 'tags', 'music' %}
  {% assign pages2 = pages1 | where: 'tags', 'theory' %}
  {% for page in pages2 %}
  <div class="col-3">
    <a href="{{ page.permalink }}">
      <img class="gallery-item-image" src="{{ page.image }}"/>
    </a>
  </div>
  {% endfor %}
</div>
