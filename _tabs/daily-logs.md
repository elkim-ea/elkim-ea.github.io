---
title: Daily Logs
icon: fas fa-book
order: 2
layout: page
---

## 📘 Daily Logs

This page contains all my study notes, certification preparation logs,
and troubleshooting records.

---

{% assign posts = site.posts %}
{% for post in posts %}
  <div class="card-wrapper">
    <article class="card">
      <h3>
        <a href="{{ post.url }}">{{ post.title }}</a>
      </h3>
      <p>{{ post.excerpt | strip_html | truncate: 120 }}</p>
      <span class="post-meta">{{ post.date | date: "%b %d, %Y" }}</span>
    </article>
  </div>
{% endfor %}
