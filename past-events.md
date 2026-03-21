---
layout: page
title: Past Events
permalink: /past-events/
---

{% assign today = site.time | date: "%Y%m%d" | plus: 0 %}
{% assign sorted_events = site.events | sort: "event_date" | reverse %}
{% assign current_year = nil %}
{% assign has_past = false %}

{% for event in sorted_events %}
  {% assign event_d = event.event_date | date: "%Y%m%d" | plus: 0 %}
  {% if event_d < today %}
    {% assign has_past = true %}
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
  {% endif %}
{% endfor %}

{% unless has_past %}
No past events yet — we're just getting started!
{% endunless %}
