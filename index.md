---
layout: home
gallery: 
  - books
  - blogs
topics:
  - geometry
  - ai
---

<!-- <div class='d-flex flex-row flex-wrap'>
  {% for item in page.gallery %}
  <div class="col-4 gallery-item">
    <a href="/{{ item }}">
      <img class="gallery-item-image" src="/assets/img/views/{{ item }}.jpg" alt="{{ item }}"/>
      <div class="gallery-item-overlay">
        <div class="gallery-item-title">{{ item | upcase }}</div>
      </div>
    </a>
  </div>
  {% endfor %}
</div> -->

<div class='d-flex flex-row flex-wrap'>  
  {% for topic in page.topics %}
  <div class="col-12 topic-item">
    <span class="topic-item-title">{{ topic }}</span>
  </div>
  {% assign pages = site.pages | where_exp: "page", "page.tags contains topic" %}
  {% for page in pages %}
  <div class="col-12">
    <a href="{{ page.permalink }}">
      <span>{{ page.title }}</span>
    </a>
  </div>
  {% endfor %}
  {% endfor %}  
</div>
