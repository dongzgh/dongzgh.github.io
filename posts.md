---
layout: page
title: Posts
permalink: /posts/
order: 2
---

{%- if site.posts.size > 0 -%}
<ul class="post-list">
  {%- for post in site.posts -%}
  {% if post.tags contains "personal" %}
  {% continue %}
  {%- endif -%}
  <li>
    {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
    <span class="post-meta">{{ post.date | date: date_format }}</span>
    <h2>
      <a class="post-link" href="{{ post.url | relative_url }}">
        {{ post.title | escape }}
      </a>
    </h2>
    {%- if site.show_excerpts -%}
    {{ post.excerpt }}
    {%- endif -%}
  </li>
  {%- endfor -%}
</ul>
{%- endif -%}
