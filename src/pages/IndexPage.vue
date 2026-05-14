<template>
  <q-page class="page landing">
    <div class="topbar">
      <router-link to="/" class="brand-link">
        <svg width="28" height="28" viewBox="0 0 48 48">
          <circle cx="24" cy="24" r="20" fill="none" stroke="#33ac51" stroke-width="4" />
          <circle cx="24" cy="24" r="6" fill="#33ac51" />
        </svg>
        <span>Kanu Systems</span>
      </router-link>
      <nav class="desktop-nav">
        <router-link to="/about">Method</router-link>
        <router-link to="/map">Live Map</router-link>
      </nav>
    </div>

    <section class="hero">
      <div class="hero-content">
        <div class="eyebrow">Kilifi // Software Intelligence</div>
        <h1>Systems that stay nominal.</h1>
        <p class="tagline">
          High-performance web applications and technical consultancy built for continuity.
        </p>
      </div>
    </section>

    <section class="case-study">
      <div class="case-study-inner">
        <h2>System Integrity: A Case Study</h2>
        <div class="case-study-grid">
          <div class="case-study-text">
            <h3>Visualizing Administrative Complexity</h3>
            <p>
              We took a raw, 15MB GeoJSON file containing Kenya's administrative data—messy,
              unoptimized, and prone to rendering failure—and transformed it into a lightweight,
              interactive operational tool.
            </p>
            <div class="engineering-challenge">
              <div class="challenge-item">
                <div class="challenge-label">Engineering Challenge</div>
                <p>
                  Optimize geographical data for web performance without losing detail. Scale
                  complex geometries to maintain responsiveness.
                </p>
              </div>
              <div class="challenge-item">
                <div class="challenge-label">Solution</div>
                <p>
                  Custom metadata schema, TopoJSON compression, and D3.js-driven rendering. The
                  result: submillisecond interactions on complex datasets.
                </p>
              </div>
            </div>
            <p class="case-conclusion">
              We transform raw geographical data into lightweight, interactive operational tools.
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
                <circle cx="150" cy="150" r="40" fill="none" stroke="#33ac51" stroke-width="2" />
                <circle cx="150" cy="150" r="10" fill="#33ac51" />
                <text
                  x="150"
                  y="260"
                  text-anchor="middle"
                  font-size="12"
                  fill="rgba(255,255,255,0.5)"
                >
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
          <p>Delivering field-ready code from Nairobi.</p>
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
