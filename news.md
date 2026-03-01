---
layout: page
title: News
permalink: /news/
---

<div class="news-list">
{% for post in site.posts %}
  <article class="news-item">
    <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
    <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time>
    <p>{{ post.excerpt | strip_html | truncatewords: 50 }}</p>
  </article>
{% endfor %}
</div>

{% if site.posts.size == 0 %}
<p>No news yet — check back soon!</p>
{% endif %}
