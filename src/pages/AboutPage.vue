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
      <h2>System Specifications</h2>
      <div class="specs-grid">
        <div class="spec-item">
          <div class="spec-label">Runtime</div>
          <div class="spec-value">Modern tooling</div>
          <p class="spec-desc">High-speed reactivity</p>
        </div>
        <div class="spec-item">
          <div class="spec-label">Visualization</div>
          <div class="spec-value">Mathematical models</div>
          <p class="spec-desc">Data-driven graphics</p>
        </div>
        <div class="spec-item">
          <div class="spec-label">Components</div>
          <div class="spec-value">UI/UX</div>
          <p class="spec-desc">Enterprise-grade dev</p>
        </div>
        <div class="spec-item">
          <div class="spec-label">Data Format</div>
          <div class="spec-value">GeoJSON / TopoJSON</div>
          <p class="spec-desc">Optimized geographical data</p>
        </div>
      </div>
    </section>

    <footer class="footer">
      <div class="footer-grid">
        <div class="footer-col">
          <h4>Kanu Systems</h4>
          <p>Delivering high-performance code from Nairobi.</p>
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
  const width = 500,
    height = 400
  const nodes = [
    { id: 'CORE', r: 40, color: '#33ac51' },
    { id: 'Data', r: 20 },
    { id: 'Logic', r: 20 },
    { id: 'UI', r: 20 },
    { id: 'Ops', r: 20 },
  ]
  const links = nodes.slice(1).map((n) => ({ source: 'CORE', target: n.id }))

  const svg = d3
    .select('#aboutViz')
    .append('svg')
    .attr('viewBox', `0 0 ${width} ${height}`)
    .style('overflow', 'visible')

  const link = svg
    .append('g')
    .selectAll('line')
    .data(links)
    .enter()
    .append('line')
    .attr('stroke', 'rgba(51, 172, 81, 0.2)')
    .attr('stroke-width', 2)

  const node = svg.append('g').selectAll('g').data(nodes).enter().append('g')

  node
    .append('circle')
    .attr('class', (d) => `node-${d.id}`)
    .attr('r', (d) => d.r)
    .attr('fill', (d) => d.color || 'rgba(255,255,255,0.05)')
    .attr('stroke', '#33ac51')
    .attr('stroke-width', 2)

  node
    .append('text')
    .text((d) => d.id)
    .attr('text-anchor', 'middle')
    .attr('dy', 5)
    .attr('fill', '#fff')
    .attr('font-size', '10px')
    .style('pointer-events', 'none')

  // Pulse effect for core
  const pulse = () => {
    svg
      .select('.node-CORE')
      .transition()
      .duration(1000)
      .attr('r', 45)
      .attr('stroke-opacity', 0.3)
      .transition()
      .duration(1000)
      .attr('r', 40)
      .attr('stroke-opacity', 1)
      .on('end', pulse)
  }

  d3.forceSimulation(nodes)
    .force(
      'link',
      d3
        .forceLink(links)
        .id((d) => d.id)
        .distance(120),
    )
    .force('charge', d3.forceManyBody().strength(-300))
    .force('center', d3.forceCenter(width / 2, height / 2))
    .on('tick', () => {
      link
        .attr('x1', (d) => d.source.x)
        .attr('y1', (d) => d.source.y)
        .attr('x2', (d) => d.target.x)
        .attr('y2', (d) => d.target.y)
      node.attr('transform', (d) => `translate(${d.x},${d.y})`)
    })
    .restart()

  pulse()
})
</script>
