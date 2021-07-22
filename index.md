---
layout: home
items:
  - music
  - culinary
  - reading  
  - outdoor
  - business
  - living
---

<div class='d-flex flex-row flex-wrap'>
  {% for item in page.items %}
  <div class="col-4">
    <a href="{{ '/views/' | append: item }}">
      <img class="gallery-item-image" src="{{ '/assets/img/topics/' | append: item | append: '.jpg' }}"/>
      <div class="gallery-item-overlay">
        <div class="gallery-item-title">{{ item | upcase }}</div>
      </div>
    </a>
  </div>
  {% endfor %}
</div>
