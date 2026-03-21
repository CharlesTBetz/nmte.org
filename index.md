---
layout: home
title: Home
---

<div class="hero-banner">
  <a href="{{ site.baseurl }}/events/2026-02-23-new-works-cabaret-crooners/">
    <img src="{{ site.baseurl }}/assets/media/crooners-cabaret-2026/dunsmore-room-performance.jpg" alt="NMTE New Works Cabaret at Crooners — Sold Out">
    <div class="hero-overlay">
      <h2>New Works Cabaret at Crooners — Sold Out!</h2>
      <p>NMTE packed the Dunsmore Jazz Room with original musical theater</p>
    </div>
  </a>
</div>

<div class="image-grid">
  <a href="{{ site.baseurl }}/events/2026-02-23-new-works-cabaret-crooners/" class="grid-card">
    <img src="{{ site.baseurl }}/assets/media/crooners-cabaret-2026/cabaret-02.jpg" alt="Performance at Crooners">
    <div class="grid-caption">Crooners Cabaret Performances</div>
  </a>
  <a href="{{ site.baseurl }}/events/2026-03-16-rough-cuts-nautilus/" class="grid-card">
    <img src="{{ site.baseurl }}/assets/media/rough-cuts-2026-03/performance.jpg" alt="Rough Cuts at Nautilus">
    <div class="grid-caption">Rough Cuts at Nautilus — March 2026</div>
  </a>
  <a href="{{ site.baseurl }}/events/2023-10-23-teslas-mistress-reading/" class="grid-card">
    <img src="{{ site.baseurl }}/assets/media/teslas-mistress-2023/promo-flyer.png" alt="Tesla's Mistress">
    <div class="grid-caption">Tesla's Mistress — Staged Reading</div>
  </a>
</div>

<div class="home-intro">
  <p>The <strong>New Musical Theatre Exchange</strong> brings together committed composers, lyricists, and librettists in the Twin Cities to workshop new musicals, find collaborators, and get original work produced. We meet monthly and present public showcases of work in development.</p>
  <p><a href="{{ site.baseurl }}/about/">Learn more about us →</a></p>
</div>

{% assign today = site.time | date: "%Y%m%d" | plus: 0 %}
{% assign sorted_events = site.events | sort: "event_date" %}
{% assign has_upcoming = false %}

{% for event in sorted_events %}
  {% assign event_d = event.event_date | date: "%Y%m%d" | plus: 0 %}
  {% if event_d >= today %}
    {% unless has_upcoming %}
<div class="upcoming-events-feature">
  <h2>Upcoming Events</h2>
    {% endunless %}
    {% assign has_upcoming = true %}
  <article class="event-item featured">
    <h3><a href="{{ event.url | relative_url }}">{{ event.title }}</a></h3>
    <div class="event-meta">
      <time>{{ event.event_date | date: "%B %d, %Y" }}</time>
      {% if event.time %} · {{ event.time }}{% endif %}
      {% if event.venue %}<br>📍 {{ event.venue }}{% endif %}
      {% if event.sold_out %} <span class="event-badge sold-out">SOLD OUT</span>{% endif %}
    </div>
    <p>{{ event.excerpt | strip_html | truncatewords: 25 }}</p>
  </article>
  {% endif %}
{% endfor %}
{% if has_upcoming %}
  <p><a href="{{ site.baseurl }}/news-and-events/">All news & events →</a></p>
</div>
{% endif %}

