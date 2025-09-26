---
title: Blogs
permalink: /blogs
categories: 
  - how-to
  - what-is
  - review
  - curated
---

{% for category in page.categories %}
{% assign pages = site.pages | where: 'medium', 'blog' | where: 'category', category %}
{% if pages.size > 0 %}
<h2>{{ category | upcase }}</h2>
<div class='d-flex flex-row flex-wrap'>
  {% for page in pages %}
  <div class="col-12">
    <a href="{{ page.permalink }}">
      <span>{{ page.title }}</span>
    </a>
  </div>
  {% endfor %}
</div>
{% endif %}
{% endfor %}
