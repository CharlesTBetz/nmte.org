---
layout: page
title: Updates
permalink: /updates/
---

Events, member news, and announcements — all in one place.

<div class="tab-bar">
  <button class="tab active" data-filter="all">All</button>
  <button class="tab" data-filter="event">Events</button>
  <button class="tab" data-filter="news">News</button>
  <button class="tab" data-filter="media">Media</button>
  <button class="tab" data-filter="blog">Blog</button>
</div>

<div class="updates-list">
{% assign all_posts = site.posts | sort: 'date' | reverse %}
{% for post in all_posts %}
  <article class="update-item" data-tags="{{ post.tags | join: ' ' }}">
    <div class="update-type-badges">
      {% for tag in post.tags %}
        {% if tag == "event" %}<span class="badge badge-event">🎭 Event</span>{% endif %}
        {% if tag == "news" %}<span class="badge badge-news">📰 News</span>{% endif %}
        {% if tag == "media" %}<span class="badge badge-media">🎬 Media</span>{% endif %}
        {% if tag == "blog" %}<span class="badge badge-blog">✍️ Blog</span>{% endif %}
      {% endfor %}
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

<script>
document.addEventListener('DOMContentLoaded', function() {
  var tabs = document.querySelectorAll('.tab');
  var items = document.querySelectorAll('.update-item');

  tabs.forEach(function(tab) {
    tab.addEventListener('click', function() {
      // Update active tab
      tabs.forEach(function(t) { t.classList.remove('active'); });
      tab.classList.add('active');

      var filter = tab.getAttribute('data-filter');

      items.forEach(function(item) {
        if (filter === 'all') {
          item.style.display = '';
        } else {
          var tags = item.getAttribute('data-tags') || '';
          item.style.display = tags.indexOf(filter) !== -1 ? '' : 'none';
        }
      });
    });
  });
});
</script>

<style>
.tab-bar {
  display: flex;
  gap: 0;
  margin: 1.5rem 0;
  border-bottom: 2px solid #333;
}

.tab {
  background: none;
  border: none;
  color: #999;
  font-size: 1rem;
  padding: 0.6rem 1.2rem;
  cursor: pointer;
  border-bottom: 2px solid transparent;
  margin-bottom: -2px;
  font-family: inherit;
  transition: color 0.2s, border-color 0.2s;
}

.tab:hover {
  color: #e0e0e0;
}

.tab.active {
  color: #F0C14B;
  border-bottom-color: #F0C14B;
}

.updates-list {
  margin-top: 1rem;
}

.update-item {
  padding: 1.5rem 0;
  border-bottom: 1px solid #333;
}

.update-item:last-child {
  border-bottom: none;
}

.update-type-badges {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 0.5rem;
}

.badge {
  font-size: 0.75rem;
  padding: 0.15rem 0.5rem;
  border-radius: 3px;
  opacity: 0.85;
}

.badge-event { background: rgba(240, 193, 75, 0.2); color: #F0C14B; }
.badge-news { background: rgba(100, 180, 255, 0.2); color: #64b4ff; }
.badge-media { background: rgba(180, 100, 255, 0.2); color: #b464ff; }
.badge-blog { background: rgba(100, 220, 100, 0.2); color: #64dc64; }

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
