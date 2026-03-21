---
layout: page
title: Past Events
permalink: /past-events/
---

{% assign today = site.time | date: "%Y-%m-%d" %}
{% assign past = site.events | where_exp: "event", "event.event_date | date: '%Y-%m-%d' < today" | sort: "event_date" | reverse %}

{% assign current_year = nil %}
{% for event in past %}
  {% assign event_year = event.event_date | date: "%Y" %}
  {% if event_year != current_year %}
    {% assign current_year = event_year %}
## {{ current_year }}
  {% endif %}

<article class="event-item">
  <h3><a href="{{ event.url | relative_url }}">{{ event.title }}</a></h3>
  <div class="event-meta">
    <time>{{ event.event_date | date: "%B %d, %Y" }}</time>
    {% if event.venue %} · {{ event.venue }}{% endif %}
    {% if event.sold_out %} <span class="event-badge sold-out">SOLD OUT</span>{% endif %}
  </div>
  <p>{{ event.excerpt | strip_html | truncatewords: 30 }}</p>
</article>
{% endfor %}

{% if past.size == 0 %}
No past events yet — we're just getting started!
{% endif %}
