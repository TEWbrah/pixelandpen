---
layout: default
title: Contact
permalink: /contact/
---

<div class="card" style="max-width:720px;margin:0 auto;">
  <h2>Contact Pixel &amp; Pen</h2>
  <p>Questions, tips, PR, or interview requests—drop us a line.</p>

  <form id="contact-form"
        action="https://formspree.io/f/xvgwzkzg"   <!-- 👈 REPLACE with your Formspree endpoint -->
        method="POST" novalidate>

    <!-- Email (reply-to) -->
    <label for="email">Your email</label>
    <input type="email" id="email" name="email" required
           placeholder="you@example.com"
           style="width:100%;padding:10px;border-radius:10px;border:1px solid var(--border);background:#0f1115;color:var(--text);margin-bottom:12px;">

    <!-- Subject -->
    <label for="subject">Subject</label>
    <input type="text" id="subject" name="subject" required
           placeholder="Subject"
           style="width:100%;padding:10px;border-radius:10px;border:1px solid var(--border);background:#0f1115;color:var(--text);margin-bottom:12px;">

    <!-- Message -->
    <label for="message">Message</label>
    <textarea id="message" name="message" rows="6" required
              placeholder="Write your message…"
              style="width:100%;padding:10px;border-radius:10px;border:1px solid var(--border);background:#0f1115;color:var(--text);margin-bottom:12px;"></textarea>

    <!-- (Optional) Tag to route/label messages -->
    <input type="hidden" name="_subject" value="Contact form: {{ site.title }}">
    <!-- Simple spam honeypot (humans won't fill this) -->
    <input type="text" name="_gotcha" style="display:none">

    <button type="submit"
            style="padding:10px 14px;border-radius:10px;border:1px solid var(--border);background:#151924;color:var(--text);cursor:pointer;">
      Send
    </button>

    <span id="form-status" style="margin-left:10px;color:var(--muted);"></span>
  </form>
</div>

<script>
  const form = document.getElementById('contact-form');
  const statusSpan = document.getElementById('form-status');

  form.addEventListener('submit', async (e) => {
    e.preventDefault();
    statusSpan.textContent = 'Sending…';

    // Basic client validation
    const email = document.getElementById('email').value.trim();
    const subject = document.getElementById('subject').value.trim();
    const message = document.getElementById('message').value.trim();
    if (!email || !subject || !message) {
      statusSpan.textContent = 'Please fill out all fields.';
      return;
    }

    try {
      const res = await fetch(form.action, {
        method: 'POST',
        headers: { 'Accept': 'application/json' },
        body: new FormData(form)
      });
      if (res.ok) {
        form.reset();
        statusSpan.textContent = 'Thanks! We got your message.';
      } else {
        statusSpan.textContent = 'Something went wrong. Try again in a moment.';
      }
    } catch {
      statusSpan.textContent = 'Network error. Please try again.';
    }
  });
</script>
