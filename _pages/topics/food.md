---
layout: page
title: Food
permalink: /topics/food
created_lists:
  - image: /assets/img/food/badacaixi.png
    title: 八大菜系
    link: /topics/food/badacaixi
---

<!-- markdownlint-disable MD033 -->

## Saved Lists

<div class='d-flex flex-row flex-wrap'>
  {% for item in page.created_lists %}
    <div class="col-md-4">
      <a href="{{ item.link }}">
        <img class="gallery-item-image" src="{{ item.image }}" height="150px"/>
      </a>
      <div class="gallery-item-title">{{ item.title }}</div>
    </div>
  {% endfor %}
</div>

