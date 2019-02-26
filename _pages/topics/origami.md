---
layout: page
title: Origami
permalink: /topics/origami
created_lists:
  - image: /assets/img/origami/awesome-origami.png
    title: Awesome Origami
    link: https://www.youtube.com/watch?v=RntZNBrfrQo&list=PLu43en8_KcyI92DMQCgLPOkRsUvaenO9n
---

## Created Lists

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