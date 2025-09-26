
---
layout: default
title: Home
---

<div id="search-box" style="margin: 12px 0 20px 0;">
  <input id="q" type="text" placeholder="Search articles…" style="width:100%; padding:10px; border-radius:10px; border:1px solid var(--border); background:#0f1115; color:var(--text);">
  <div style="margin-top:10px; display:flex; gap:10px; flex-wrap:wrap;">
    <input id="tag-input" type="text" placeholder="Filter by tag (e.g., review)" style="flex:1; min-width:220px; padding:8px; border-radius:10px; border:1px solid var(--border); background:#0f1115; color:var(--text);">
    <button id="clear-btn" style="padding:8px 12px; border-radius:10px; border:1px solid var(--border); background:#151924; color:var(--text); cursor:pointer;">Clear</button>
  </div>
</div>

<div id="results"></div>

# Latest Stories

<ul class="post-list">
{% for post in site.posts limit: 10 %}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <div class="post-meta">{{ post.date | date: "%b %d, %Y" }}</div>
  </li>
{% endfor %}
</ul>
