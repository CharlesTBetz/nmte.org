---
layout: home
title: Home
---

<div class="news-feature">
  <h2>NMTE News</h2>
  {% for post in site.posts limit:3 %}
  <article class="news-item">
    <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
    <time>{{ post.date | date: "%B %d, %Y" }}</time>
    <p>{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
  </article>
  {% endfor %}
  <p><a href="/news/">View all news →</a></p>
</div>

<div class="home-cards">
  <a href="/who-we-are/" class="card">
    <img src="/assets/images/card-who.jpg" alt="Who We Are">
    <h3>Who We Are</h3>
    <p>The New Musical Theatre Exchange exists to bring together committed musical theatre writers.</p>
  </a>

  <a href="/what-we-do/" class="card">
    <img src="/assets/images/card-what.jpg" alt="What We Do">
    <h3>What We Do</h3>
    <p>Learn more about the NMTE.</p>
  </a>

  <a href="/members/" class="card">
    <h3>Members</h3>
    <p>Learn more about NMTE members.</p>
  </a>

  <a href="/contact/" class="card">
    <img src="/assets/images/card-contact.jpg" alt="Contact">
    <h3>Contact</h3>
    <p>Want to know more about NMTE meetings or membership?</p>
  </a>
</div>
