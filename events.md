---
layout: page
title: Events
permalink: /events/
---

{% assign today = site.time | date: "%Y-%m-%d" %}
{% assign upcoming = site.events | where_exp: "event", "event.event_date >= today" | sort: "event_date" %}
{% assign has_upcoming = false %}

{% for event in upcoming %}
{% assign has_upcoming = true %}
<article class="event-item">
  <h2><a href="{{ event.url | relative_url }}">{{ event.title }}</a></h2>
  <div class="event-meta">
    <time>{{ event.event_date | date: "%B %d, %Y" }}</time>
    {% if event.time %} · {{ event.time }}{% endif %}
    {% if event.venue %}<br>📍 {{ event.venue }}{% endif %}
    {% if event.sold_out %} <span class="event-badge sold-out">SOLD OUT</span>{% endif %}
  </div>
  <p>{{ event.excerpt | strip_html | truncatewords: 30 }}</p>
</article>
{% endfor %}

{% unless has_upcoming %}
## Monthly Workshop

The NMTE meets the **third Sunday of most months** at the <a href="https://www.google.com/maps/place/710+Raymond+Ave,+St+Paul,+MN" target="_blank">Playwrights' Center, 710 Raymond Ave, St. Paul</a>. Members share songs, scenes, and lyrics for feedback and development.

[Contact us]({{ site.baseurl }}/contact/) for details on the next meeting.
{% endunless %}

---

Looking for earlier events? [View past events →]({{ site.baseurl }}/past-events/)
