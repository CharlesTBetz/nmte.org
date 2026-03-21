---
layout: page
title: Blog
permalink: /blog/
---

In-depth interviews, commentary, and stories from the Twin Cities musical theatre community.

<div class="blog-grid">
{% assign posts = site.posts | where: "blog", true | sort: 'date' | reverse %}
{% for post in posts %}
  <article class="blog-item">
    <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
    <div class="blog-meta">
      <span class="date">{{ post.date | date: "%B %d, %Y" }}</span>
      {% if post.author %}
        <span class="author">by {{ post.author }}</span>
      {% endif %}
    </div>
    <div class="blog-excerpt">
      {{ post.excerpt | strip_html | truncate: 300 }}
    </div>
    <a href="{{ post.url | relative_url }}" class="read-more">Read more →</a>
  </article>
{% endfor %}

{% if site.posts.size == 0 %}
  <div class="coming-soon">
    <h3>Coming Soon</h3>
    <p>Our first blog post will be an interview with NMTE member Keith Benson about his collaborative musical <em>Anzhelina & Karina</em>. Check back soon!</p>
  </div>
{% endif %}
</div>

<style>
.blog-grid {
  display: grid;
  gap: 2rem;
  margin-top: 2rem;
}

.blog-item {
  padding: 1.5rem;
  border: 1px solid #e1e8ed;
  border-radius: 8px;
}

.blog-meta {
  display: flex;
  gap: 1rem;
  margin: 0.5rem 0;
  font-size: 0.9rem;
  color: #666;
}

.read-more {
  display: inline-block;
  margin-top: 1rem;
  color: #1a1a2e;
  font-weight: 500;
  text-decoration: none;
}

.read-more:hover {
  text-decoration: underline;
}

.coming-soon {
  text-align: center;
  padding: 3rem;
  color: #666;
}
</style>