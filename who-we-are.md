---
layout: page
title: Who We Are
permalink: /who-we-are/
---

## Members

<div class="member-gallery">
{% for member in site.data.members %}
  {% if member.photo and member.photo != "" %}
    {% assign photo_src = site.baseurl | append: "/assets/images/members/" | append: member.photo %}
  {% else %}
    {% assign photo_src = site.baseurl | append: "/assets/images/members/placeholder.svg" %}
  {% endif %}
  <div class="member-tile">
    <a href="{{ member.pwc_url }}" target="_blank" rel="noopener">
      <img src="{{ photo_src }}" alt="{{ member.name }}">
      <span class="member-name">{{ member.name }}{% if member.board %} <span class="board-mark">*</span>{% endif %}</span>
    </a>
  </div>
{% endfor %}
</div>

<p class="members-note">* Board member &nbsp;·&nbsp; <em>Names link to <a href="https://pwcenter.org/member-directory/" target="_blank">Playwrights' Center</a> profiles.</em></p>

---

## About NMTE

The **New Musical Theatre Exchange** is a nonprofit 501(c) bringing together committed librettists, lyricists, and composers of musical theatre in the Twin Cities and surrounding region. We workshop new musicals, find collaborators, share resources, and support efforts to get members' work produced.

Founded in 2012, we believe new musicals can — and should — be developed outside of New York City. The Twin Cities and surrounding region has a wealth of talent, a thriving theater community, and audiences hungry for original work.

We meet on the **third Sunday of most months** at the <a href="https://www.google.com/maps/place/710+Raymond+Ave,+St+Paul,+MN" target="_blank">Playwrights' Center, 710 Raymond Ave, St. Paul</a>.

<div class="home-cards" style="margin-top: 2rem;">
  <a href="{{ site.baseurl }}/what-we-do/" class="card">
    <h3>What We Do</h3>
    <p>Monthly workshops, staged readings, cabaret showcases, and partnerships with organizations like Nautilus Music-Theater.</p>
  </a>

  <a href="{{ site.baseurl }}/get-involved/" class="card">
    <h3>Get Involved</h3>
    <p>Learn about our membership process and how to join our community of musical theater creators.</p>
  </a>

  <a href="{{ site.baseurl }}/contact/" class="card">
    <h3>Contact</h3>
    <p>Get in touch with us about meetings, membership, or general questions about NMTE.</p>
  </a>
</div>

<img src="{{ site.baseurl }}/assets/images/banner-actors.png" alt="NMTE members" style="width:100%; border-radius:8px; margin-top: 2rem;">

<style>
.member-gallery {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 1.25rem;
  margin: 1.5rem 0 0.5rem;
}
.member-tile a {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-decoration: none;
  color: inherit;
}
.member-tile img {
  width: 100%;
  aspect-ratio: 1/1;
  object-fit: cover;
  border-radius: 6px;
  border: none !important;
  box-shadow: none !important;
}
.member-tile:hover img {
  opacity: 0.85;
}
.member-name {
  display: block;
  text-align: center;
  font-size: 0.85rem;
  margin-top: 0.4rem;
  line-height: 1.3;
}
.board-mark {
  color: #c4a843;
}
.members-note {
  font-size: 0.8rem;
  color: #777;
  margin-top: 0.75rem;
}
@media (max-width: 768px) {
  .member-gallery { grid-template-columns: repeat(4, 1fr); }
}
@media (max-width: 480px) {
  .member-gallery { grid-template-columns: repeat(3, 1fr); }
}
</style>
