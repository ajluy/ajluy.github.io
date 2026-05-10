---
layout: home
---
<div class="home-intro">
  <h1 class="home-intro__name">Allen Jeremy Uy</h1>
  <p class="home-intro__bio">Student at the University of Notre Dame studying Computer Engineering. I work on projects spanning software, hardware, and data — from embedded systems to buissness analytics.</p>
  <div class="home-intro__links">
    {% if site.github_username %}
    <a class="home-intro__link" href="https://github.com/{{ site.github_username }}" target="_blank" rel="noopener noreferrer">GitHub</a>
    {% endif %}
    {% if site.linkedin_username %}
    <a class="home-intro__link" href="https://linkedin.com/in/{{ site.linkedin_username }}" target="_blank" rel="noopener noreferrer">LinkedIn</a>
    {% endif %}
  </div>
</div>
