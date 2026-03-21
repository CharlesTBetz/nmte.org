---
layout: home
title: Home
---

<!-- Hero Banner: Manual hero flag takes priority, then auto-select -->
{% assign today = site.time | date: "%Y%m%d" | plus: 0 %}
{% assign sorted_events = site.events | sort: "event_date" | reverse %}
{% assign hero_event = nil %}

<!-- First check for manually flagged hero -->
{% for event in sorted_events %}
  {% if event.hero and hero_event == nil %}
    {% assign hero_event = event %}
    {% break %}
  {% endif %}
{% endfor %}

<!-- If no manual hero, try upcoming events -->
{% if hero_event == nil %}
  {% for event in sorted_events %}
    {% assign event_d = event.event_date | date: "%Y%m%d" | plus: 0 %}
    {% if event_d >= today and hero_event == nil %}
      {% assign hero_event = event %}
      {% break %}
    {% endif %}
  {% endfor %}
{% endif %}

<!-- If no upcoming, use most recent -->
{% if hero_event == nil %}
  {% for event in sorted_events %}
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
        <div class="carousel-nav">
          <button class="carousel-btn prev" onclick="heroCarousel.prev()">‹</button>
          <button class="carousel-btn next" onclick="heroCarousel.next()">›</button>
        </div>
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
  },
  
  prev() {
    this.showSlide(this.currentSlide - 1);
  }
};

// Initialize carousel when page loads
document.addEventListener('DOMContentLoaded', () => {
  heroCarousel.init();
});
</script>
{% endif %}

<!-- Dual Featured Blocks -->
<div class="featured-blocks">
  <!-- Featured Event (excluding hero) -->
  <div class="featured-event">
    {% assign featured_event = nil %}
    {% assign event_candidates = site.events | sort: "event_date" | reverse %}
    
    <!-- First try manually featured events -->
    {% for event in event_candidates %}
      {% if event.featured and event != hero_event %}
        {% assign featured_event = event %}
        {% break %}
      {% endif %}
    {% endfor %}
    
    <!-- If no featured flag, use recent (excluding hero) -->
    {% if featured_event == nil %}
      {% for event in event_candidates %}
        {% if event != hero_event %}
          {% assign featured_event = event %}
          {% break %}
        {% endif %}
      {% endfor %}
    {% endif %}
    
    {% if featured_event %}
      <article class="feature-card">
        <a href="{{ featured_event.url | relative_url }}">
          {% if featured_event.promo_image %}
            <img src="{{ site.baseurl }}{{ featured_event.promo_image }}" alt="{{ featured_event.title }}">
          {% endif %}
          <div class="feature-content">
            <h3>{{ featured_event.title }}</h3>
            <div class="feature-meta">
              {{ featured_event.event_date | date: "%B %d, %Y" }}
              {% if featured_event.venue %} · {{ featured_event.venue }}{% endif %}
            </div>
          </div>
        </a>
      </article>
    {% endif %}
  </div>
  
  <!-- Featured News/Blog -->
  <div class="featured-news">
    {% assign featured_news = nil %}
    
    <!-- First try manually featured news -->
    {% for item in site.news %}
      {% if item.featured %}
        {% assign featured_news = item %}
        {% break %}
      {% endif %}
    {% endfor %}
    
    <!-- If no featured news, try recent news -->
    {% if featured_news == nil and site.news.size > 0 %}
      {% assign featured_news = site.news | sort: 'date' | reverse | first %}
    {% endif %}
    
    <!-- If no news, try featured blog posts -->
    {% if featured_news == nil %}
      {% for post in site.posts %}
        {% if post.featured %}
          {% assign featured_news = post %}
          {% break %}
        {% endif %}
      {% endfor %}
    {% endif %}
    
    <!-- If no featured blog, use most recent post -->
    {% if featured_news == nil and site.posts.size > 0 %}
      {% assign featured_news = site.posts | first %}
    {% endif %}
    
    {% if featured_news %}
      <article class="feature-card">
        <a href="{{ featured_news.url | relative_url }}">
          {% if featured_news.youtube_url %}
            <div class="video-thumbnail">
              <img src="https://img.youtube.com/vi/{{ featured_news.youtube_url | split: '/' | last | replace: 'watch?v=', '' }}/mqdefault.jpg" alt="Video thumbnail">
              <div class="play-button">▶</div>
            </div>
          {% elsif featured_news.image %}
            <img src="{{ site.baseurl }}/{{ featured_news.image }}" alt="{{ featured_news.title }}">
          {% endif %}
          <div class="feature-content">
            <h3>{{ featured_news.title }}</h3>
            <div class="feature-meta">
              {{ featured_news.date | date: "%B %d, %Y" }}
              {% if featured_news.type %} · {{ featured_news.type }}{% endif %}
            </div>
          </div>
        </a>
      </article>
    {% endif %}
  </div>
</div>

<!-- CTA Banner -->
<div class="cta-banner">
  <h2>Interested in NMTE?</h2>
  <p>Learn about our mission, meet our members, and discover how to get involved.</p>
  <a href="{{ site.baseurl }}/about/" class="cta-button">About Us</a>
</div>

<!-- Force rebuild Sat Mar 21 11:29:30 CDT 2026 -->
