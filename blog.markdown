---
layout: page
title: Blog
permalink: /blog
---

{%- if site.posts.size > 0 -%}
  <p class="rss-subscribe">Subscribe to this blog's <a href="{{ "/feed.xml" | relative_url }}">RSS feed</a>.</p>
  <ul class="post-list">
    {%- for post in site.posts -%}
    <li>
      {%- assign date_format = site.minima.date_format | default: "%Y-%m-%d" -%}
      <p><span class="post-meta">
        {{ post.date | date: date_format }}
        —
        <a class="post-link" href="{{ post.url | relative_url }}"> {{ post.title | escape }} </a>
      </span></p>
    </li>
    {%- endfor -%}
  </ul>
{%- endif -%}

