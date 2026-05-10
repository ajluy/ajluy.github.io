---
layout: page
title: About
permalink: /about/
---

<div class="about-section">
  <p class="section-label">Background</p>
  <p>I'm Allen, an undergraduate studying [Your Major] at [University]. I'm drawn to problems at the intersection of software, hardware, and data — and I like building things that are both technically rigorous and practically useful.</p>
  <p>Outside of coursework I spend time on self-directed projects ranging from embedded systems to data pipelines. I'm currently looking for opportunities in [area of interest].</p>
</div>

<div class="about-section">
  <p class="section-label">Skills</p>

  <div class="skills-group">
    <p class="skills-group__label">Software</p>
    <p class="skills-group__list">Python, JavaScript / TypeScript, C++, React, Node.js, SQL</p>
  </div>

  <div class="skills-group">
    <p class="skills-group__label">Hardware / EE</p>
    <p class="skills-group__list">KiCad, LTspice, FreeCAD, PCB layout, oscilloscope, soldering</p>
  </div>

  <div class="skills-group">
    <p class="skills-group__label">Business / Data</p>
    <p class="skills-group__list">Excel, Tableau, pandas, SQL, A/B testing, financial modeling</p>
  </div>

  <div class="skills-group">
    <p class="skills-group__label">Tools</p>
    <p class="skills-group__list">Git, Docker, Linux, VS Code, Figma</p>
  </div>
</div>

<div class="about-section">
  <p class="section-label">Interests</p>
  <p>Mechanical keyboards, long bike rides, cooking new things badly on the first attempt. I also read a lot of nonfiction — mostly history and science.</p>
</div>

<div class="about-section">
  <div class="about-social">
    {% if site.github_username %}
    <a class="social-link" href="https://github.com/{{ site.github_username }}" target="_blank" rel="noopener noreferrer">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
        <path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/>
      </svg>
      GitHub
    </a>
    {% endif %}
    {% if site.linkedin_username %}
    <a class="social-link" href="https://linkedin.com/in/{{ site.linkedin_username }}" target="_blank" rel="noopener noreferrer">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
        <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
      </svg>
      LinkedIn
    </a>
    {% endif %}
  </div>
</div>
