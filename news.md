---
layout: page
title: News
permalink: /news/
---

# News & Updates

Stay up to date with NMTE member achievements, new demo recordings, industry news, and community updates.

<div class="news-grid">
{% assign sorted_news = site.news | sort: 'date' | reverse %}
{% for item in sorted_news %}
  <article class="news-item">
    <h2><a href="{{ item.url | relative_url }}">{{ item.title }}</a></h2>
    <div class="news-meta">
      <span class="date">{{ item.date | date: "%B %d, %Y" }}</span>
      {% if item.type %}
        <span class="type">{{ item.type }}</span>
      {% endif %}
    </div>
    <div class="news-excerpt">
      {{ item.excerpt | strip_html | truncate: 200 }}
    </div>
    {% if item.youtube_url %}
      <div class="video-embed">
        <iframe width="560" height="315" src="{{ item.youtube_url | replace: 'youtu.be/', 'www.youtube.com/embed/' | replace: 'watch?v=', 'embed/' }}" frameborder="0" allowfullscreen></iframe>
      </div>
    {% endif %}
  </article>
{% endfor %}
</div>

<style>
.news-grid {
  display: grid;
  gap: 2rem;
  margin-top: 2rem;
}

.news-item {
  padding: 1.5rem;
  border: 1px solid #e1e8ed;
  border-radius: 8px;
}

.news-meta {
  display: flex;
  gap: 1rem;
  margin: 0.5rem 0;
  font-size: 0.9rem;
  color: #666;
}

.type {
  background: #f0f4f8;
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  font-weight: 500;
}

.video-embed {
  margin-top: 1rem;
}

.video-embed iframe {
  max-width: 100%;
  height: auto;
  aspect-ratio: 16/9;
}
</style>