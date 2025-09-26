
---
layout: default
title: Home
---

# Latest Stories

<ul class="post-list">
{% for post in site.posts limit: 10 %}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <div class="post-meta">{{ post.date | date: "%b %d, %Y" }}</div>
  </li>
{% endfor %}
</ul>
