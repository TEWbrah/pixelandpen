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

<script>
(async function(){
  const res = await fetch('{{ "/search.json" | relative_url }}');
  const data = await res.json();

  const q = document.getElementById('q');
  const t = document.getElementById('tag-input');
  const clearBtn = document.getElementById('clear-btn');
  const out = document.getElementById('results');

  function render(list){
    if(!list.length){ out.innerHTML = "<div class='card'><p>No matching articles.</p></div>"; return; }
    out.innerHTML = `
      <div class="card">
        <ul class="post-list">
          ${list.map(p => `
            <li>
              <a href="${p.url}">${p.title}</a>
              <div class="post-meta">${p.date}${(p.tags && p.tags.length) ? " • " + p.tags.join(", ") : ""}</div>
              ${p.excerpt ? `<div style="color:var(--muted); font-size:14px;">${p.excerpt}</div>` : ""}
            </li>
          `).join("")}
        </ul>
      </div>`;
  }

  function search(){
    const qv = (q.value || "").toLowerCase();
    const tv = (t.value || "").toLowerCase();

    const filtered = data.filter(p => {
      const hay = (p.title + " " + (p.content || "")).toLowerCase();
      const textMatch = !qv || hay.includes(qv);
      const tagMatch  = !tv || (Array.isArray(p.tags) && p.tags.some(tag => (tag||"").toLowerCase().includes(tv)));
      return textMatch && tagMatch;
    });

    render(filtered.slice(0, 50));
  }

  q.addEventListener('input', search);
  t.addEventListener('input', search);
  clearBtn.addEventListener('click', () => { q.value=""; t.value=""; search(); });

  render(data);
})();
</script>
