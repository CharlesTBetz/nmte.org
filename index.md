---
layout: default
title: Home
---

<!-- Hero Banner: Manual hero flag takes priority, then auto-select -->
{% assign today = site.time | date: "%Y%m%d" | plus: 0 %}
{% assign all_events = site.posts | where_exp: "post", "post.tags contains 'event'" | sort: "event_date" | reverse %}
{% assign hero_event = nil %}

<!-- First check for manually flagged hero -->
{% for event in all_events %}
  {% if event.hero and hero_event == nil %}
    {% assign hero_event = event %}
    {% break %}
  {% endif %}
{% endfor %}

<!-- If no manual hero, try upcoming events -->
{% if hero_event == nil %}
  {% for event in all_events %}
    {% assign event_d = event.event_date | date: "%Y%m%d" | plus: 0 %}
    {% if event_d >= today and hero_event == nil %}
      {% assign hero_event = event %}
      {% break %}
    {% endif %}
  {% endfor %}
{% endif %}

<!-- If no upcoming, use most recent -->
{% if hero_event == nil %}
  {% for event in all_events %}
    {% assign event_d = event.event_date | date: "%Y%m%d" | plus: 0 %}
    {% if event_d < today and hero_event == nil %}
      {% assign hero_event = event %}
      {% break %}
    {% endif %}
  {% endfor %}
{% endif %}

{% if hero_event %}
<div class="hero-banner">
  <a href="{{ hero_event.url | relative_url }}">
    {% if hero_event.hero_carousel %}
      {% assign carousel_images = hero_event.hero_carousel | split: ',' %}
      <div class="hero-carousel">
        {% for image in carousel_images %}
          <div class="hero-slide {% if forloop.first %}active{% endif %}">
            <img src="{{ site.baseurl }}{{ image | strip }}" alt="{{ hero_event.title | escape }}">
          </div>
        {% endfor %}
        <!-- Navigation removed - auto-advance only -->
      </div>
    {% elsif hero_event.promo_image %}
      <img src="{{ site.baseurl }}{{ hero_event.promo_image }}" alt="{{ hero_event.title | escape }}">
    {% else %}
      <img src="{{ site.baseurl }}/assets/media/crooners-cabaret-2026/dunsmore-room-performance.jpg" alt="NMTE Event">
    {% endif %}
    <div class="hero-overlay">
      <h2>{% if hero_event.hero_title %}{{ hero_event.hero_title }}{% else %}{{ hero_event.title }}{% endif %}</h2>
    </div>
  </a>
</div>

<script>
const heroCarousel = {
  currentSlide: 0,
  slides: document.querySelectorAll('.hero-slide'),
  
  init() {
    if (this.slides.length > 1) {
      setInterval(() => this.next(), 5000); // Auto-advance every 5 seconds
    }
  },
  
  showSlide(n) {
    this.slides.forEach(slide => slide.classList.remove('active'));
    this.currentSlide = (n + this.slides.length) % this.slides.length;
    this.slides[this.currentSlide].classList.add('active');
  },
  
  next() {
    this.showSlide(this.currentSlide + 1);
  }
};

// Initialize carousel when page loads
document.addEventListener('DOMContentLoaded', () => {
  heroCarousel.init();
});
</script>
{% endif %}

<!-- Three-card featured row -->
<!-- Featured cards: pinned (featured: true) first, then most recent eligible, max 3 -->
<!-- Posts with featured: false are excluded. Omitting featured = eligible by recency. -->
<!-- Hero post is excluded to avoid duplication. -->
<div class="featured-cards-row">
  {% assign card_count = 0 %}

  <!-- Pass 1: Pinned posts (featured: true) -->
  {% for post in site.posts %}
    {% if card_count >= 3 %}{% break %}{% endif %}
    {% if post.featured == true and post != hero_event %}
      <article class="feature-card">
        <a href="{{ post.url | relative_url }}">
          {% if post.youtube_url %}
            <div class="video-thumbnail">
              <img src="https://img.youtube.com/vi/{{ post.youtube_url | split: '/' | last | replace: 'watch?v=', '' }}/mqdefault.jpg" alt="Video thumbnail">
              <div class="play-button">▶</div>
            </div>
          {% elsif post.promo_image %}
            <img src="{{ site.baseurl }}{{ post.promo_image }}" alt="{{ post.title | escape }}">
          {% endif %}
          <div class="feature-content">
            <h3>{{ post.title }}</h3>
            <div class="feature-meta">
              {{ post.date | date: "%B %d, %Y" }}
              {% if post.venue %} · {{ post.venue }}{% endif %}
              {% if post.composer %} · {{ post.composer }}{% endif %}
              {% if post.sold_out %} · <strong>SOLD OUT</strong>{% endif %}
            </div>
          </div>
        </a>
      </article>
      {% assign card_count = card_count | plus: 1 %}
    {% endif %}
  {% endfor %}

  <!-- Pass 2: Fill remaining slots with most recent eligible posts -->
  {% for post in site.posts %}
    {% if card_count >= 3 %}{% break %}{% endif %}
    {% if post != hero_event and post.featured != true and post.featured != false %}
      <article class="feature-card">
        <a href="{{ post.url | relative_url }}">
          {% if post.youtube_url %}
            <div class="video-thumbnail">
              <img src="https://img.youtube.com/vi/{{ post.youtube_url | split: '/' | last | replace: 'watch?v=', '' }}/mqdefault.jpg" alt="Video thumbnail">
              <div class="play-button">▶</div>
            </div>
          {% elsif post.promo_image %}
            <img src="{{ site.baseurl }}{{ post.promo_image }}" alt="{{ post.title | escape }}">
          {% endif %}
          <div class="feature-content">
            <h3>{{ post.title }}</h3>
            <div class="feature-meta">
              {{ post.date | date: "%B %d, %Y" }}
              {% if post.venue %} · {{ post.venue }}{% endif %}
              {% if post.composer %} · {{ post.composer }}{% endif %}
              {% if post.sold_out %} · <strong>SOLD OUT</strong>{% endif %}
            </div>
          </div>
        </a>
      </article>
      {% assign card_count = card_count | plus: 1 %}
    {% endif %}
  {% endfor %}
</div>

<hr class="section-rule">

<!-- CTA Banner -->
<div class="cta-banner">
  <h2>Interested in NMTE?</h2>
  <p>Learn about our mission, meet our members, and discover how to get involved.</p>
  <a href="{{ site.baseurl }}/about/" class="cta-button">About Us</a>
  <div class="social-links">
    <a href="https://www.facebook.com/NewMusicalTheatreExchange/" target="_blank">Facebook</a>
  </div>
</div>

<!-- Force rebuild Sat Mar 21 11:29:30 CDT 2026 -->
