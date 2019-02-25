---
layout: page
title: Video
permalink: /topics/video
created_lists:
  - image: /assets/img/videos/red-wanted.png
    title: 红色通缉
    link: https://www.youtube.com/watch?v=fYDeFzMwPU8&list=PLu43en8_KcyIYpb0BVWSb_7sxavmZQqdZ
  - image: /assets/img/videos/deep-diving.png
    title: 深潜
    link: https://www.youtube.com/watch?v=Xxw3JPvBp8g&list=PLinO3Bage4ckq2f45clCiPP5B2xh55nhz
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