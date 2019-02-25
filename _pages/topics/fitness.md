---
layout: page
title: Fitness
permalink: /topics/fitness
created_lists:
  - image: /assets/img/fitness/awesome-zumba.png
    title: Awesome Zumba
    link: https://www.youtube.com/watch?v=YtVgIeiX2zM&list=PLu43en8_KcyLDOdjXT-6tcMRRNrLvTKN6
---

<div class='d-flex flex-row flex-wrap'>
  {% for item in page.created_lists %}
    <div class="col-md-4">
      <a href="{{ item.link }}">
        <img class="gallery-item-image" src="{{ item.image }}"/>
      </a>
      <div class="gallery-item-title">{{ item.title }}</div>
    </div>
  {% endfor %}
</div>