---
layout: post
title: "Welcome to Pixel & Pen"
date: 2025-09-26
tags: [news, site-update]
---
layout: default
---

<div class="container onecol">
  <article class="card">
    <h1>{{ page.title }}</h1>
    <div class="post-meta">
      {{ page.date | date: "%b %d, %Y" }}
      {% if page.tags and page.tags.size > 0 %} • {{ page.tags | join: ", " }}{% endif %}
    </div>
    <div class="post-body">
      {{ content }}
    </div>
  </article>
</div>
