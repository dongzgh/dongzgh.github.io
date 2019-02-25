---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
hobbies:
  - image: /assets/img/topics/photo.jpg
    link: /topics/photo
  - image: /assets/img/topics/video.jpg
    link: /topics/video
  - image: /assets/img/topics/origami.jpg
    link: /topics/origami
  - image: /assets/img/topics/art.jpg
    link: /topics/art
  - image: /assets/img/topics/music.jpg
    link: /topics/music
  - image: /assets/img/topics/car.jpg
    link: /topics/car
  - image: /assets/img/topics/read.jpg
    link: /topics/read
  - image: /assets/img/topics/travel.jpg
    link: /topics/travel
  - image: /assets/img/topics/fitness.jpg
    link: /topics/fitness
  - image: /assets/img/topics/hike.jpg
    link: /topics/hike
  - image: /assets/img/topics/dive.jpg
    link: /topics/dive
  - image: /assets/img/topics/food.jpg
    link: /topics/food  
---

<!-- markdownlint-disable MD033 -->

<div class='d-flex flex-row flex-wrap'>
  {% for item in page.hobbies %}
    <div class="col-4">
      <a href="{{ item.link }}">
        <img class="gallery-item-image" src="{{ item.image }}"/>
      </a>
    </div>
  {% endfor %}
</div>
