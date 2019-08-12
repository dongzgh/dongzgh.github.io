---
layout: page
title: Food
permalink: /topics/food
saved_lists:
  - image: /assets/img/food/amanda-fast.png
    title: Amanda Fast
    link: https://www.youtube.com/watch?v=NhTYlMBsTtY&index=1&list=PLXpt3FUcUvXoVKyOpdUI67Qv6v3cdFefn
  - image: /assets/img/food/amanda-fast.png
    title: 八大菜系
    link: /topics/food/badacaixi
---

<!-- markdownlint-disable MD033 -->

## Saved Lists

<div class='d-flex flex-row flex-wrap'>
  {% for item in page.saved_lists %}
    <div class="col-md-4">
      <a href="{{ item.link }}">
        <img class="gallery-item-image" src="{{ item.image }}" height="100px"/>
      </a>
      <div class="gallery-item-title">{{ item.title }}</div>
    </div>
  {% endfor %}
</div>

