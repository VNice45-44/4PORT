<template>
  <q-page class="page landing">
    <div class="topbar">
      <router-link to="/" class="brand-link">
        <svg width="28" height="28" viewBox="0 0 48 48">
          <circle cx="24" cy="24" r="20" fill="none" stroke="var(--accent)" stroke-width="4" />
          <circle cx="24" cy="24" r="6" fill="var(--accent)" />
        </svg>
        <span>KS</span>
      </router-link>
      <nav class="desktop-nav">
        <router-link to="/about">Method</router-link>
      </nav>
      <button type="button" class="theme-toggle" @click="toggleTheme">Theme</button>
    </div>

    <section class="hero">
      <div class="hero-content">
        <div class="eyebrow">Kilifi // Software Intelligence</div>
        <h1>Systems that stay nominal</h1>
        <p class="tagline">
          High-performance web applications and technical consultancy built for continuity.
        </p>
      </div>
    </section>

    <section class="case-study">
      <div class="case-study-inner">
        <h2>System Integrity: Real Impact</h2>
        <div class="case-study-grid">
          <div class="case-study-text">
            <h3>From Chaos to Operational Clarity</h3>
            <p>
              We've helped construction firms visualize project timelines and resource allocation,
              solar companies manage installation networks across regions, ride-hailing operators
              track fleet performance, and resort owners streamline bookings and maintenance. The
              common thread: systems that were either broken or invisible.
            </p>
            <div class="engineering-challenge">
              <div class="challenge-item">
                <div class="challenge-label">The Problem</div>
                <p>
                  Critical business data scattered across spreadsheets, databases, and paperwork. No
                  visibility. No speed. No control.
                </p>
              </div>
              <div class="challenge-item">
                <div class="challenge-label">What We Build</div>
                <p>
                  Lightweight, fast interfaces that let you see and manage your entire operation at
                  a glance. Real-time updates, clear decision-making, operational confidence.
                </p>
              </div>
            </div>
            <p class="case-conclusion">
              We clean up, stabilize, and scale the systems that run your business.
            </p>
          </div>
          <div class="case-study-visual">
            <div class="visual-placeholder">
              <svg width="100%" height="100%" viewBox="0 0 300 300">
                <circle
                  cx="150"
                  cy="150"
                  r="80"
                  fill="none"
                  stroke="rgba(51, 172, 81, 0.3)"
                  stroke-width="2"
                />
                <circle
                  cx="150"
                  cy="150"
                  r="60"
                  fill="none"
                  stroke="rgba(51, 172, 81, 0.5)"
                  stroke-width="2"
                />
                <circle
                  cx="150"
                  cy="150"
                  r="40"
                  fill="none"
                  stroke="var(--accent)"
                  stroke-width="2"
                />
                <circle cx="150" cy="150" r="10" fill="var(--accent)" />
                <text x="150" y="260" text-anchor="middle" font-size="12" fill="var(--text-muted)">
                  Data Layers
                </text>
              </svg>
            </div>
          </div>
        </div>
      </div>
    </section>

    <div class="service-grid q-mt-xl">
      <div class="kanu-card" v-for="s in services" :key="s.title">
        <div class="text-h6 text-green q-mb-md">// 0{{ s.id }}</div>
        <h3>{{ s.title }}</h3>
        <p class="sub">{{ s.desc }}</p>
      </div>
    </div>

    <footer class="footer">
      <div class="footer-grid">
        <div class="footer-col">
          <h4>Kanu Systems</h4>
          <p>Delivering from Kilifi.</p>
          <p class="meta">Location: 1.2921° S, 36.8219° E</p>
        </div>
        <div class="footer-col">
          <h4>Explore</h4>
          <router-link to="/about">Methodology</router-link>
          <router-link to="/map" class="footer-map-link">System Map</router-link>
        </div>
        <div class="footer-col">
          <h4>Channel</h4>
          <p>ops@kanusystems.com</p>
        </div>
      </div>
      <div class="subtle-sign">© 2026 KANU_SYSTEMS. STATUS: ALL_SYSTEMS_NOMINAL</div>
    </footer>
  </q-page>
</template>

<script setup>
const toggleTheme = () => {
  const isSoft = document.body.classList.toggle('theme-soft')
  document.body.classList.toggle('theme-dark', !isSoft)
  document.body.classList.toggle('body--dark', !isSoft)
  document.body.classList.toggle('body--light', isSoft)
  document.body.style.setProperty('--q-dark-page', isSoft ? '#faf8f6' : '#07110a')
}

const services = [
  {
    id: 1,
    title: 'Web Architecture',
    desc: 'Interfaces for complex data and high-load environments.',
  },
  {
    id: 2,
    title: 'App Development',
    desc: 'Custom engines with maintainability as the first priority.',
  },
  {
    id: 3,
    title: 'Data Viz',
    desc: 'Transforming geographical and systemic data into actionables.',
  },
  {
    id: 4,
    title: 'Consultancy',
    desc: 'Technical strategy to bridge the gap between business and code.',
  },
]
</script>
