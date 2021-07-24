---
title: Piano
permalink: /piano
tags: [music, instrument]
image: /assets/img/pages/piano.jpg
spellcheck: off
---

<div class='d-flex flex-row flex-wrap'>
  {% assign pages  = site.pages | where: 'parent', 'piano' %}
  {% for page in pages %}
  <div class="col-3">
    <a href="{{ page.permalink }}">
      <img class="gallery-item-image" src="{{ page.image }}"/>
    </a>
  </div>
  {% endfor %}
</div>
