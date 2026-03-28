---
layout: page
title: Our Work
permalink: /our-work/
---

Original musicals developed through NMTE workshops, readings, and member collaboration.

<div class="musicals-grid">
{% assign musicals = site.musicals | sort: "title" %}
{% for musical in musicals %}
  <article class="musical-card">
    <a href="{{ musical.url | relative_url }}">
      {% if musical.image %}
        <img src="{{ site.baseurl }}{{ musical.image }}" alt="{{ musical.title | escape }}">
      {% else %}
        <div class="musical-placeholder">🎭</div>
      {% endif %}
      <div class="musical-card-content">
        <h3>{{ musical.title }}</h3>
        <div class="musical-card-meta">
          {{ musical.composer }}
          <span class="musical-status">
            {% if musical.status == "active" %}🟢 Active
            {% elsif musical.status == "in-development" %}🔵 In Development
            {% elsif musical.status == "completed" %}✅ Completed
            {% endif %}
          </span>
        </div>
        <p>{{ musical.content | strip_html | truncate: 120 }}</p>
      </div>
    </a>
  </article>
{% endfor %}
</div>

<style>
.musicals-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.musical-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
  transition: border-color 0.2s;
}

.musical-card:hover {
  border-color: #000;
}

.musical-card a {
  text-decoration: none;
  color: inherit;
}

.musical-card img {
  width: 100%;
  height: 180px;
  object-fit: cover;
}

.musical-placeholder {
  width: 100%;
  height: 180px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 4rem;
  background: #1a1a1a;
}

.musical-card-content {
  padding: 1rem;
}

.musical-card-content h3 {
  margin: 0 0 0.3rem 0;
  color: #000;
  font-size: 1.1rem;
}

.musical-card-meta {
  font-size: 0.85rem;
  color: #555;
  font-style: italic;
  margin-bottom: 0.5rem;
}

.musical-status {
  display: block;
  margin-top: 0.2rem;
  font-style: normal;
  font-size: 0.75rem;
}

.musical-card-content p {
  font-size: 0.9rem;
  color: #ccc;
  margin: 0;
}
</style>
