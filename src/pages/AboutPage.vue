<template>
  <q-page class="page about">
    <div class="topbar">
      <router-link to="/" class="brand-link"><span>Kanu Systems</span></router-link>
      <nav class="desktop-nav">
        <router-link to="/about">Method</router-link>
        <router-link to="/map">Live Map</router-link>
      </nav>
    </div>

    <div class="hero grid-2">
      <div class="hero-body">
        <div class="eyebrow">Our Philosophy</div>
        <h1>Code is a living environment.</h1>
        <p>
          We treat software as an ecosystem. When one part changes, the whole must adapt. Our work
          focuses on visibility—ensuring you can see how your data flows before it fails.
        </p>
      </div>
      <div class="viz-container">
        <div id="aboutViz" class="kanu-card"></div>
      </div>
    </div>

    <section class="protocol-section">
      <h2>The Kanu Protocol</h2>
      <p class="section-intro">Our methodology for building resilient systems.</p>
      <div class="protocol-grid">
        <div class="protocol-card">
          <div class="phase-number">01</div>
          <h3>Stress-Testing Requirements</h3>
          <p>
            We look for where the logic breaks before we write a single line of code. Understanding
            edge cases defines the foundation.
          </p>
        </div>
        <div class="protocol-card">
          <div class="phase-number">02</div>
          <h3>Modular Architecture</h3>
          <p>
            Building systems as independent, communicating nodes. Each component handles one
            responsibility, enforcing clarity and resilience.
          </p>
        </div>
        <div class="protocol-card">
          <div class="phase-number">03</div>
          <h3>Observability</h3>
          <p>
            Integrating real-time feedback loops so the system remains operational. Visibility into
            system state is non-negotiable.
          </p>
        </div>
      </div>
    </section>

    <section class="edge-section">
      <div class="edge-content">
        <div class="edge-text">
          <h2>Designed for the Edge</h2>
          <p>
            Software fails when it hits the field. Low bandwidth, changing requirements, offline
            needs—these aren't edge cases, they're requirements.
          </p>
          <p>
            At Kanu Systems, resilience is a core feature, not an afterthought. We build systems
            that continue to work when conditions change.
          </p>
          <ul class="edge-features">
            <li>Optimized for variable network conditions</li>
            <li>Graceful degradation under load</li>
            <li>Adaptive interfaces for changing contexts</li>
            <li>Real-time synchronization and conflict resolution</li>
          </ul>
        </div>
      </div>
    </section>

    <section class="specs-section">
      <h2>System Capabilities</h2>
      <div class="specs-grid">
        <div class="spec-item">
          <div class="spec-label">Resilience</div>
          <div class="spec-value">Built to adapt</div>
          <p class="spec-desc">Enduring systems that shift without breaking.</p>
        </div>
        <div class="spec-item">
          <div class="spec-label">Insight</div>
          <div class="spec-value">Clear system view</div>
          <p class="spec-desc">Actionable visibility into running behavior.</p>
        </div>
        <div class="spec-item">
          <div class="spec-label">Interfaces</div>
          <div class="spec-value">Purposeful touchpoints</div>
          <p class="spec-desc">Operational dashboards that stay intuitive.</p>
        </div>
        <div class="spec-item">
          <div class="spec-label">Structure</div>
          <div class="spec-value">Organized systems</div>
          <p class="spec-desc">Clean, predictable delivery of complex data.</p>
        </div>
      </div>
    </section>

    <footer class="footer">
      <div class="footer-grid">
        <div class="footer-col">
          <h4>Kanu Systems</h4>
          <p>Delivering high-performance code from Kilifi.</p>
          <p class="meta">Location: 1.2921° S, 36.8219° E</p>
        </div>
        <div class="footer-col">
          <h4>Protocol</h4>
          <router-link to="/about">Philosophy</router-link>
          <router-link to="/map">Data Systems</router-link>
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
import { onMounted } from 'vue'
import * as d3 from 'd3'

onMounted(() => {
  const width = 540,
    height = 420
  const data = {
    name: 'CORE',
    children: [
      { name: 'Data', children: [{ name: 'Reports' }, { name: 'Signals' }] },
      { name: 'Logic', children: [{ name: 'Flows' }, { name: 'Rules' }] },
      { name: 'UI', children: [{ name: 'Field' }, { name: 'Control' }] },
      { name: 'Ops', children: [{ name: 'Monitor' }, { name: 'Sync' }] },
    ],
  }

  const svg = d3
    .select('#aboutViz')
    .append('svg')
    .attr('viewBox', `0 0 ${width} ${height}`)
    .attr('width', '100%')
    .attr('height', '100%')
    .style('overflow', 'visible')

  const defs = svg.append('defs')
  const gradient = defs
    .append('linearGradient')
    .attr('id', 'linkGradient')
    .attr('x1', '0%')
    .attr('y1', '0%')
    .attr('x2', '100%')
    .attr('y2', '0%')

  gradient
    .append('stop')
    .attr('offset', '0%')
    .attr('stop-color', '#33ac51')
    .attr('stop-opacity', 0.28)

  gradient
    .append('stop')
    .attr('offset', '100%')
    .attr('stop-color', '#68e0ff')
    .attr('stop-opacity', 0.75)

  defs
    .append('filter')
    .attr('id', 'nodeGlow')
    .append('feDropShadow')
    .attr('dx', 0)
    .attr('dy', 0)
    .attr('stdDeviation', 4)
    .attr('flood-color', '#33ac51')
    .attr('flood-opacity', 0.25)

  const root = d3.hierarchy(data)
  d3
    .tree()
    .size([height - 100, width - 160])
    .separation((a, b) => (a.parent === b.parent ? 1.4 : 2))(root)

  const g = svg.append('g').attr('transform', 'translate(80,50)')

  g.selectAll('path')
    .data(root.links())
    .join('path')
    .attr('fill', 'none')
    .attr('stroke', 'url(#linkGradient)')
    .attr('stroke-width', 2)
    .attr(
      'd',
      d3
        .linkHorizontal()
        .x((d) => d.y)
        .y((d) => d.x),
    )
    .attr('stroke-dasharray', function () {
      const len = this.getTotalLength()
      return `${len} ${len}`
    })
    .attr('stroke-dashoffset', function () {
      return this.getTotalLength()
    })
    .transition()
    .duration(1200)
    .attr('stroke-dashoffset', 0)

  const node = g
    .selectAll('g')
    .data(root.descendants())
    .join('g')
    .attr('transform', (d) => `translate(${d.y},${d.x})`)
    .style('opacity', 0)

  node
    .transition()
    .delay((d, i) => i * 120)
    .duration(600)
    .style('opacity', 1)

  node
    .append('circle')
    .attr('r', (d) => (d.depth === 0 ? 28 : 16))
    .attr('fill', (d) => (d.depth === 0 ? 'rgba(51,172,81,0.16)' : 'rgba(255,255,255,0.16)'))
    .attr('stroke', (d) => (d.depth === 0 ? '#68e0ff' : '#33ac51'))
    .attr('stroke-width', (d) => (d.depth === 0 ? 3.2 : 1.5))
    .attr('filter', 'url(#nodeGlow)')

  node
    .append('text')
    .text((d) => d.data.name)
    .attr('dy', 5)
    .attr('x', (d) => (d.depth === 0 ? 0 : 22))
    .attr('text-anchor', (d) => (d.depth === 0 ? 'middle' : 'start'))
    .attr('fill', '#fff')
    .attr('font-size', (d) => (d.depth === 0 ? '0.95rem' : '0.8rem'))
    .style('pointer-events', 'none')

  const pulse = () => {
    svg
      .select('circle')
      .transition()
      .duration(1000)
      .attr('r', 32)
      .attr('stroke-opacity', 0.4)
      .transition()
      .duration(1000)
      .attr('r', 28)
      .attr('stroke-opacity', 1)
      .on('end', pulse)
  }

  pulse()
})
</script>
