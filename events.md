---
layout: page
title: Events
permalink: /events/
---

{% assign today = site.time | date: "%Y%m%d" | plus: 0 %}
{% assign sorted_events = site.posts | where_exp: "post", "post.tags contains 'event'" | sort: "event_date" %}
{% assign has_upcoming = false %}

{% for event in sorted_events %}
  {% assign event_d = event.event_date | date: "%Y%m%d" | plus: 0 %}
  {% if event_d >= today %}
    {% unless has_upcoming %}
## Upcoming Events
    {% endunless %}
    {% assign has_upcoming = true %}

<article class="event-item">
  <h3><a href="{{ event.url | relative_url }}">{{ event.title }}</a></h3>
  <div class="event-meta">
    <time>{{ event.event_date | date: "%B %d, %Y" }}</time>
    {% if event.time %} · {{ event.time }}{% endif %}
    {% if event.venue %}<br>📍 {{ event.venue }}{% endif %}
    {% if event.sold_out %} <span class="event-badge sold-out">SOLD OUT</span>{% endif %}
    {% if event.ticket_url %}<br><a href="{{ event.ticket_url }}" target="_blank">🎟 Get Tickets</a>{% endif %}
  </div>
  <p>{{ event.excerpt | strip_html | truncatewords: 30 }}</p>
</article>
  {% endif %}
{% endfor %}

{% unless has_upcoming %}
## Next Meeting

The NMTE meets the **third Sunday of most months** at the <a href="https://www.google.com/maps/place/710+Raymond+Ave,+St+Paul,+MN" target="_blank">Playwrights' Center, 710 Raymond Ave, St. Paul</a>. [Contact us](/about/contact/) for details.
{% endunless %}

---

## Recent Events

{% assign past_events = site.posts | where: "event", true | sort: "event_date" | reverse %}
{% assign recent_count = 0 %}

{% for event in past_events %}
  {% assign event_d = event.event_date | date: "%Y%m%d" | plus: 0 %}
  {% if event_d < today and recent_count < 6 %}
    {% assign recent_count = recent_count | plus: 1 %}

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

---

[View all past events →]({{ site.baseurl }}/past-events/)
