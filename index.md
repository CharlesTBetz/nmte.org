---
layout: home
title: Home
---

<!-- Hero Banner: Manual hero flag takes priority, then auto-select -->
{% assign today = site.time | date: "%Y%m%d" | plus: 0 %}
{% assign all_events = site.posts | where: "event", true | sort: "event_date" | reverse %}
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
            <img src="{{ site.baseurl }}{{ image | strip }}" alt="{{ hero_event.title }}">
          </div>
        {% endfor %}
        <!-- Navigation removed - auto-advance only -->
      </div>
    {% elsif hero_event.promo_image %}
      <img src="{{ site.baseurl }}{{ hero_event.promo_image }}" alt="{{ hero_event.title }}">
    {% else %}
      <img src="{{ site.baseurl }}/assets/media/crooners-cabaret-2026/dunsmore-room-performance.jpg" alt="NMTE Event">
    {% endif %}
    <div class="hero-overlay">
      <h2>{{ hero_event.title }}</h2>
      <p>{{ hero_event.excerpt | strip_html | truncatewords: 15 }}</p>
      <span class="hero-tagline">Music and words — storytelling with music</span>
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
<div class="featured-cards-row">
  {% assign event_candidates = site.posts | where: "event", true | sort: "event_date" | reverse %}
  {% assign shown_events = 0 %}
  
  <!-- Two recent events (excluding hero) -->
  {% for event in event_candidates %}
    {% if event != hero_event and shown_events < 2 %}
      <article class="feature-card">
        <a href="{{ event.url | relative_url }}">
          {% if event.promo_image %}
            <img src="{{ site.baseurl }}{{ event.promo_image }}" alt="{{ event.title }}">
          {% endif %}
          <div class="feature-content">
            <h3>{{ event.title }}</h3>
            <div class="feature-meta">
              {{ event.event_date | date: "%B %d, %Y" }}
              {% if event.venue %} · {{ event.venue }}{% endif %}
              {% if event.sold_out %} · <strong>SOLD OUT</strong>{% endif %}
            </div>
          </div>
        </a>
      </article>
      {% assign shown_events = shown_events | plus: 1 %}
    {% endif %}
  {% endfor %}
  
  <!-- One recent non-event news item -->
  {% for post in site.posts %}
    {% unless post.event %}
      <article class="feature-card">
        <a href="{{ post.url | relative_url }}">
          {% if post.youtube_url %}
            <div class="video-thumbnail">
              <img src="https://img.youtube.com/vi/{{ post.youtube_url | split: '/' | last | replace: 'watch?v=', '' }}/mqdefault.jpg" alt="Video thumbnail">
              <div class="play-button">▶</div>
            </div>
          {% elsif post.promo_image %}
            <img src="{{ site.baseurl }}{{ post.promo_image }}" alt="{{ post.title }}">
          {% endif %}
          <div class="feature-content">
            <h3>{{ post.title }}</h3>
            <div class="feature-meta">
              {{ post.date | date: "%B %d, %Y" }}
              {% if post.category %} · {{ post.category }}{% endif %}
              {% if post.composer %} · {{ post.composer }}{% endif %}
            </div>
          </div>
        </a>
      </article>
      {% break %}
    {% endunless %}
  {% endfor %}
</div>

<!-- CTA Banner -->
<div class="cta-banner">
  <h2>Interested in NMTE?</h2>
  <p>Learn about our mission, meet our members, and discover how to get involved.</p>
  <a href="{{ site.baseurl }}/about/" class="cta-button">About Us</a>
</div>

<!-- Force rebuild Sat Mar 21 11:29:30 CDT 2026 -->
