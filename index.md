---
layout: home
items:
  - music
  - origami
  - food
  - paint
  - car
  - diving
  - fitness  
  - hiking  
  - photography
  - reading
  - traveling
  - video
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