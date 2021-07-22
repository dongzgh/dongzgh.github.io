---
title: Music
permalink: /views/music
---

## Chinese Songs

<div class='d-flex flex-row flex-wrap'>
  {% assign pages1 = site.pages | where: 'tags', 'music' %}
  {% assign pages2 = pages1 | where: 'tags', 'song' %}
  {% assign pages3 = pages2 | where: 'tags', 'Chinese' %}
  {% assign groups = pages3 | group_by: 'singer' %}
  {% for group in groups %}
  <div class="col-3">
    <a href="{{ '/' | append: group.items[0].singer }}">
      <img class="gallery-item-image"
        src="{{ '/assets/img/singers/' | append: group.items[0].singer | append: '.jpg' }}" />
      <div class="gallery-item-overlay">
        <div class="gallery-item-title">{{ group.items[0].singer | replace: '-', ' ' }}</div>
      </div>
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
