---
layout: page
title: Submit Content
permalink: /submit/
---

Have news, an event, or media to share? Use this form to submit content for the NMTE website. All submissions are reviewed before publishing.

<form id="content-form" action="https://formspree.io/f/PLACEHOLDER" method="POST" enctype="multipart/form-data">

  <div class="form-group">
    <label for="name">Your Name *</label>
    <input type="text" id="name" name="name" required>
  </div>

  <div class="form-group">
    <label for="email">Your Email *</label>
    <input type="email" id="email" name="email" required>
  </div>

  <div class="form-group">
    <label for="title">Title / Headline *</label>
    <input type="text" id="title" name="title" required placeholder="e.g. 'Member Show at Crooners' or 'New Video Release'">
  </div>

  <div class="form-group">
    <label>Content Type (select all that apply) *</label>
    <div class="checkbox-group">
      <label class="checkbox-label"><input type="checkbox" name="tags" value="event"> 🎭 Event</label>
      <label class="checkbox-label"><input type="checkbox" name="tags" value="news"> 📰 News</label>
      <label class="checkbox-label"><input type="checkbox" name="tags" value="media"> 🎬 Media</label>
    </div>
  </div>

  <div class="form-group" id="event-fields" style="display:none;">
    <label for="event_date">Event Date</label>
    <input type="date" id="event_date" name="event_date">
    <label for="event_time">Time</label>
    <input type="text" id="event_time" name="event_time" placeholder="e.g. 7:00 PM">
    <label for="venue">Venue</label>
    <input type="text" id="venue" name="venue" placeholder="e.g. Crooners Supper Club">
    <label for="ticket_url">Ticket Link (if applicable)</label>
    <input type="url" id="ticket_url" name="ticket_url">
  </div>

  <div class="form-group">
    <label for="story">Story / Description *</label>
    <textarea id="story" name="story" rows="8" required placeholder="Write up the details. Who, what, when, where, why it matters."></textarea>
  </div>

  <div class="form-group">
    <label for="links">Links (YouTube, website, social media, etc.)</label>
    <textarea id="links" name="links" rows="3" placeholder="One per line"></textarea>
  </div>

  <div class="form-group">
    <label for="image">Image (optional — we'll follow up if we need one)</label>
    <input type="file" id="image" name="image" accept="image/*">
  </div>

  <button type="submit" class="cta-button">Submit for Review</button>
</form>

<script>
// Show/hide event fields based on checkbox
document.addEventListener('DOMContentLoaded', function() {
  var eventCheck = document.querySelector('input[value="event"]');
  var eventFields = document.getElementById('event-fields');
  eventCheck.addEventListener('change', function() {
    eventFields.style.display = this.checked ? 'block' : 'none';
  });
});
</script>

<style>
.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.4rem;
  font-weight: bold;
  color: #e8e8e8;
}

.form-group input[type="text"],
.form-group input[type="email"],
.form-group input[type="url"],
.form-group input[type="date"],
.form-group textarea {
  width: 100%;
  padding: 0.6rem;
  background: #222;
  border: 1px solid #444;
  color: #e8e8e8;
  border-radius: 4px;
  font-family: inherit;
  font-size: 1rem;
  margin-bottom: 0.5rem;
}

.form-group input:focus,
.form-group textarea:focus {
  border-color: #c4a843;
  outline: none;
}

.form-group input[type="file"] {
  color: #e8e8e8;
}

.checkbox-group {
  display: flex;
  gap: 1.5rem;
  margin-top: 0.3rem;
}

.checkbox-label {
  font-weight: normal !important;
  color: #e8e8e8 !important;
  cursor: pointer;
}

.checkbox-label input {
  margin-right: 0.3rem;
}

#event-fields {
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  background: rgba(240, 193, 75, 0.05);
}

button.cta-button {
  cursor: pointer;
  font-size: 1.1rem;
  padding: 0.8rem 2rem;
}
</style>
