---
layout: page
title: Food
permalink: /topics/food
saved_lists:
  - image: /assets/img/food/amanda-fast.png
    title: Amanda Fast
    link: https://www.youtube.com/watch?v=NhTYlMBsTtY&index=1&list=PLXpt3FUcUvXoVKyOpdUI67Qv6v3cdFefn
  - image: /assets/img/food/amanda-bakery.png
    title: Amanda Bakery
    link: https://www.youtube.com/watch?v=Caopoyr53TY&list=PLXpt3FUcUvXot1wRlnftWaGwy1KuX5BsS
  - image: /assets/img/food/amanda-snacks.png
    title: Amanda Snacks
    link: https://www.youtube.com/watch?v=sZFxo1Pc3-8&list=PLXpt3FUcUvXp7XqQ0ww81a18-1ICzaIML
  - image: /assets/img/food/amanda-desserts.png
    title: Amanda Desserts
    link: https://www.youtube.com/watch?v=UtYKBYapYkM&list=PLXpt3FUcUvXpJOI5o_V98KqvV9oaIe1tO
  - image: /assets/img/food/amanda-chinese-cuisine.png
    title: Amanda Chinese Cuisine
    link: https://www.youtube.com/watch?v=0MUDs97FGGM&list=PLXpt3FUcUvXq_kp-uc_lz_UcNmxhRrbyH
  - image: /assets/img/food/amanda-asian-cuisine.png
    title: Amanda Asian Cuisine
    link: https://www.youtube.com/watch?v=BFtA-pAaW0g&list=PLXpt3FUcUvXpIMxDRv-cslqos8p4vFxLT
  - image: /assets/img/food/amanda-european-cuisine.png
    title: Amanda European Cuisine
    link: https://www.youtube.com/watch?v=yDlsuWoXmbQ&list=PLXpt3FUcUvXpmCoCKYCfy6bH8-NNb8mus
  - image: /assets/img/food/catskitchen-season-1.png
    title: Cat's Kitchen Season 1
    link: https://www.youtube.com/watch?v=4vT-BfQGnYg&list=PL2LpQH-oKNWI4VFvnYSgYzn9LejQaTAIA
  - image: /assets/img/food/catskitchen-season-2.png
    title: Cat's Kitchen Season 2
    link: https://www.youtube.com/watch?v=eZFgq_DeKwM&list=PL2LpQH-oKNWJYfB1M1eEZk58qmWxpdnr_
  - image: /assets/img/food/catskitchen-rices.png
    title: Cat's Kitchen Rices
    link: https://www.youtube.com/watch?v=ok1rq7wRcKU&list=PL2LpQH-oKNWJucPq1yD0J5nQA_Y7-VEqJ
  - image: /assets/img/food/catskitchen-noodles.png
    title: Cat's Kitchen Noodles
    link: https://www.youtube.com/watch?v=_5KuZlR4CcQ&list=PL2LpQH-oKNWJVVIQKrA9DePK5V74Fa7vs
  - image: /assets/img/food/catskitchen-hotpots.png
    title: Cat's Kitchen Hotpots
    link: https://www.youtube.com/watch?v=-dDtkS_vFPg&list=PL2LpQH-oKNWJV4CLyoJx3enIaDClgWi2n
  - image: /assets/img/food/catskitchen-vegetables.png
    title: Cat's Kitchen Vegetables
    link: https://www.youtube.com/watch?v=GDEtiwWQg1c&list=PL2LpQH-oKNWIiczZdaS6gzYljdVa-528t
  - image: /assets/img/food/catskitchen-desserts.png
    title: Cat's Kitchen Desserts
    link: https://www.youtube.com/watch?v=HrFr_PF0V0I&list=PL2LpQH-oKNWL3XNY01dVO0jZGDsI22wpe 
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

