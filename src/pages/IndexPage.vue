<template>
  <q-page class="page landing">
    <div class="topbar">
      <router-link to="/" class="brand-link">
        <img class="brand-mark" src="/lion-logo.svg" alt="" />
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
        <h2>Systems that stay nominal</h2>
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
              We've helped firms visualize project timelines and resource allocation, manage
              installation networks across regions, run ride-hailing platforms to track fleet
              performance, and several more. The common thread: systems that were either broken or
              invisible.
            </p>
            <div class="engineering-challenge">
              <button
                v-for="(layer, index) in dataLayers"
                :key="layer.label"
                type="button"
                class="challenge-item layer-card"
                :class="{ active: index === activeLayerIndex }"
                @click="activeLayerIndex = index"
                @mouseenter="activeLayerIndex = index"
              >
                <div class="challenge-label">The Problem</div>
                <h4>{{ layer.label }}</h4>
                <p>{{ layer.copy }}</p>
              </button>
            </div>
            <div class="layer-build">
              <div class="challenge-label">What We Build</div>
              <p>
                Lightweight interfaces that connect scattered inputs into a clear operational view:
                real-time updates, confident decisions, and systems your team can actually steer.
              </p>
            </div>
            <p class="case-conclusion">
              We clean, stabilize, and scale systems that run your business.
            </p>
          </div>
          <div class="case-study-visual">
            <div class="visual-placeholder layer-viz">
              <svg
                width="100%"
                height="100%"
                viewBox="0 0 340 320"
                aria-label="Interactive data layer visualization"
              >
                <circle
                  v-for="(layer, index) in dataLayers"
                  :key="layer.label"
                  cx="170"
                  cy="138"
                  :r="layer.radius"
                  fill="none"
                  :stroke="index === activeLayerIndex ? layer.color : 'var(--border-strong)'"
                  :stroke-width="index === activeLayerIndex ? 5 : 2"
                  :opacity="index === activeLayerIndex ? 1 : 0.32"
                  class="layer-ring"
                />
                <g v-for="(node, index) in layerNodes" :key="node.label" class="layer-node">
                  <line
                    x1="170"
                    y1="138"
                    :x2="node.x"
                    :y2="node.y"
                    :stroke="index === activeLayerIndex ? dataLayers[index].color : 'var(--border)'"
                    :stroke-width="index === activeLayerIndex ? 2 : 1"
                  />
                  <circle
                    :cx="node.x"
                    :cy="node.y"
                    :r="index === activeLayerIndex ? 14 : 8"
                    :fill="index === activeLayerIndex ? dataLayers[index].color : 'var(--card-bg)'"
                    :stroke="dataLayers[index].color"
                    stroke-width="2"
                  />
                </g>
                <circle
                  cx="170"
                  cy="138"
                  r="18"
                  fill="var(--card-bg)"
                  stroke="var(--accent)"
                  stroke-width="3"
                />
                <circle cx="170" cy="138" r="5" fill="var(--accent)" />
                <text x="170" y="266" text-anchor="middle" font-size="13" fill="var(--text)">
                  {{ activeLayer.label }}
                </text>
                <text x="170" y="286" text-anchor="middle" font-size="11" fill="var(--text-muted)">
                  {{ activeLayer.signal }}
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
import { computed, ref } from 'vue'

const toggleTheme = () => {
  const isSoft = document.body.classList.toggle('theme-soft')
  document.body.classList.toggle('theme-dark', !isSoft)
  document.body.classList.toggle('body--dark', !isSoft)
  document.body.classList.toggle('body--light', isSoft)
  document.body.style.setProperty('--q-dark-page', isSoft ? '#faf8f6' : '#07110a')
}

const activeLayerIndex = ref(0)

const dataLayers = [
  {
    label: 'Collection',
    copy: 'Spreadsheets, field notes, bookings, and device signals start in different places.',
    signal: 'Capture the signal',
    radius: 96,
    color: '#33ac51',
  },
  {
    label: 'Structure',
    copy: 'Records need shared meaning before teams can compare, search, and trust them.',
    signal: 'Normalize the model',
    radius: 74,
    color: '#68e0ff',
  },
  {
    label: 'Workflow',
    copy: 'Approvals, assignments, alerts, and exceptions become repeatable operating logic.',
    signal: 'Move work forward',
    radius: 52,
    color: '#f2c037',
  },
  {
    label: 'Visibility',
    copy: 'Dashboards and maps turn live operations into decisions people can act on quickly.',
    signal: 'See the system',
    radius: 30,
    color: '#40a86b',
  },
]

const layerNodes = [
  { label: 'Collection', x: 84, y: 76 },
  { label: 'Structure', x: 260, y: 78 },
  { label: 'Workflow', x: 274, y: 205 },
  { label: 'Visibility', x: 74, y: 210 },
]

const activeLayer = computed(() => dataLayers[activeLayerIndex.value])

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
