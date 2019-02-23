---
layout: page
title: Food
permalink: /topics/food
saved_amanda:
  - image: /assets/img/food/amanda-fast.png
    title: Amanda Fast
    link: https://www.youtube.com/watch?v=NhTYlMBsTtY&index=1&list=PLXpt3FUcUvXoVKyOpdUI67Qv6v3cdFefn
  - image: /assets/img/food/amanda-bakery.png
    title: Amanda Bakery
    link: https://www.youtube.com/watch?v=Caopoyr53TY&list=PLXpt3FUcUvXot1wRlnftWaGwy1KuX5BsS
  - image: /assets/img/food/amanda-snacks.png
    title: Amanda Snacks
    link: https://www.youtube.com/watch?v=sZFxo1Pc3-8&list=PLXpt3FUcUvXp7XqQ0ww81a18-1ICzaIML
---

<!-- markdownlint-disable MD033 -->

## Saved from Amanda

<div class='d-flex flex-row flex-wrap'>
  {% for item in page.saved_amanda %}
    <div class="col-md-4">
      <a href="{{ item.link }}">
        <img class="gallery-item-image" src="{{ item.image }}"/>
      </a>
      <div class="gallery-item-title">{{ item.title }}</div>
    </div>
  {% endfor %}
</div>
