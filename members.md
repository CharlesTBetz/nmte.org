---
layout: page
title: Members
permalink: /members/
---

<div class="members-grid">
{% for member in site.data.members %}
  <div class="member-card">
    {% if member.image %}
    <img src="/assets/images/{{ member.image }}" alt="{{ member.name }}">
    {% endif %}
    <h3>{{ member.name }}</h3>
    {% if member.shows %}
    <ul class="member-shows">
      {% for show in member.shows %}
      <li>
        <strong>{{ show.title }}</strong><br>
        <span class="show-credits">{{ show.credits }}</span>
      </li>
      {% endfor %}
    </ul>
    {% endif %}
  </div>
{% endfor %}
</div>
