---
layout: page
title: Updates
permalink: /updates/
---

# Updates

Events, member news, and announcements — all in one place.

<div class="updates-list">
{% assign all_posts = site.posts | sort: 'date' | reverse %}
{% for post in all_posts %}
  <article class="update-item">
    <div class="update-type-badge">
      {% if post.event %}🎭 Event{% else %}📰 News{% endif %}
    </div>
    <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
    <div class="update-meta">
      {{ post.date | date: "%B %d, %Y" }}
      {% if post.venue %} · {{ post.venue }}{% endif %}
      {% if post.category %} · {{ post.category }}{% endif %}
      {% if post.composer %} · {{ post.composer }}{% endif %}
      {% if post.sold_out %} · <strong>SOLD OUT</strong>{% endif %}
    </div>
    <div class="update-excerpt">
      {{ post.excerpt | strip_html | truncate: 200 }}
    </div>
  </article>
{% endfor %}
</div>

<style>
.updates-list {
  margin-top: 2rem;
}

.update-item {
  padding: 1.5rem 0;
  border-bottom: 1px solid #333;
}

.update-item:last-child {
  border-bottom: none;
}

.update-type-badge {
  font-size: 0.8rem;
  margin-bottom: 0.5rem;
  opacity: 0.8;
}

.update-item h2 {
  margin: 0 0 0.5rem 0;
  font-size: 1.3rem;
}

.update-item h2 a {
  text-decoration: none;
  color: #F0C14B;
}

.update-item h2 a:hover {
  text-decoration: underline;
}

.update-meta {
  font-size: 0.9rem;
  color: white;
  font-style: italic;
  margin-bottom: 0.5rem;
}

.update-excerpt {
  color: #e0e0e0;
}
</style>