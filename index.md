---
layout: home
title: Home
---

{% assign today = site.time | date: "%Y-%m-%d" %}
{% assign upcoming = site.events | where_exp: "event", "event.event_date >= today" | sort: "event_date" %}

{% if upcoming.size > 0 %}
<div class="upcoming-events-feature">
  <h2>Upcoming Events</h2>
  {% for event in upcoming limit:3 %}
  <article class="event-item featured">
    <h3><a href="{{ event.url | relative_url }}">{{ event.title }}</a></h3>
    <div class="event-meta">
      <time>{{ event.event_date | date: "%B %d, %Y" }}</time>
      {% if event.time %} · {{ event.time }}{% endif %}
      {% if event.venue %}<br>📍 {{ event.venue }}{% endif %}
      {% if event.sold_out %} <span class="event-badge sold-out">SOLD OUT</span>{% endif %}
      {% if event.ticket_url %}<br><a href="{{ event.ticket_url }}" target="_blank">🎟 Get Tickets</a>{% endif %}
    </div>
    <p>{{ event.excerpt | strip_html | truncatewords: 25 }}</p>
  </article>
  {% endfor %}
  <p><a href="{{ site.baseurl }}/events/">All events →</a></p>
</div>
{% endif %}

<div class="news-feature">
  <h2>NMTE News</h2>
  {% for post in site.posts limit:3 %}
  <article class="news-item">
    <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
    <time>{{ post.date | date: "%B %d, %Y" }}</time>
    <p>{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
  </article>
  {% endfor %}
  <p><a href="{{ site.baseurl }}/news/">View all news →</a></p>
</div>

<div class="home-cards">
  <a href="{{ site.baseurl }}/who-we-are/" class="card">
    <img src="{{ site.baseurl }}/assets/images/card-who.jpg" alt="Who We Are">
    <h3>Who We Are</h3>
    <p>The New Musical Theatre Exchange exists to bring together committed musical theatre writers.</p>
  </a>

  <a href="{{ site.baseurl }}/what-we-do/" class="card">
    <img src="{{ site.baseurl }}/assets/images/card-what.jpg" alt="What We Do">
    <h3>What We Do</h3>
    <p>Learn more about the NMTE.</p>
  </a>

  <a href="{{ site.baseurl }}/contact/" class="card">
    <img src="{{ site.baseurl }}/assets/images/card-contact.jpg" alt="Contact">
    <h3>Contact</h3>
    <p>Want to know more about NMTE meetings or membership?</p>
  </a>
</div>

<div style="text-align: center; margin-top: 3rem; padding-top: 2rem; border-top: 1px solid #333;">
  <img src="{{ '/assets/images/nmte-logo-gold.png' | relative_url }}" alt="New Musical Theatre Exchange" style="max-width: 300px; width: 100%; border: 2px solid #c4a843; border-radius: 10px; padding: 1.5rem; background: transparent;">
</div>
