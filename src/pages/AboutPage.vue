<template>
  <q-page class="page about">
    <div class="topbar">
      <router-link to="/" class="brand-link"><span>KS</span></router-link>
      <nav class="desktop-nav">
        <router-link to="/about">Method</router-link>
      </nav>
      <button type="button" class="theme-toggle" @click="toggleTheme">Theme</button>
    </div>

    <div class="hero grid-2">
      <div class="hero-body">
        <div class="eyebrow">Philosophy</div>
        <h1>Code is a living environment</h1>
        <p>
          We treat software like an ecosystem. When one part changes, the whole must adapt. Our work
          focuses on visibility. We ensure you can see how your data flows.
        </p>
      </div>
      <div class="viz-container">
        <div id="aboutViz" class="kanu-card d3-panel"></div>
      </div>
    </div>

    <section class="protocol-section">
      <h2>The KS Protocol</h2>
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

    <section class="systems-section">
      <div class="section-heading">
        <div>
          <div class="eyebrow">Custom Systems Lab</div>
          <h2>How we make complex operations legible</h2>
        </div>
        <p class="section-intro">
          We design the logic, data movement, and feedback loops as one product surface.
        </p>
      </div>
      <div class="systems-grid">
        <div class="viz-card wide">
          <div class="viz-copy">
            <span>Delivery Flow</span>
            <h3>From field signal to decision</h3>
          </div>
          <div id="deliveryFlowViz" class="mini-viz"></div>
        </div>
        <div class="viz-card">
          <div class="viz-copy">
            <span>Engineering Bias</span>
            <h3>Balanced for resilience</h3>
          </div>
          <div id="capabilityRadarViz" class="mini-viz"></div>
        </div>
        <div class="viz-card">
          <div class="viz-copy">
            <span>Runtime Health</span>
            <h3>Observe, adapt, recover</h3>
          </div>
          <div id="opsPulseViz" class="mini-viz"></div>
        </div>
      </div>
    </section>

    <section class="edge-section">
      <div class="edge-content">
        <div class="edge-text">
          <h2>Edge Case Design</h2>
          <p>
            Software fails when it hits the field. Low bandwidth, changing requirements, offline
            needs—these aren't edge cases, they're requirements.
          </p>
          <p>
            At KS, resilience is a core feature, not an afterthought. We build systems that continue
            to work when conditions change.
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
          <p>Delivering from Kilifi.</p>
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
import { onBeforeUnmount, onMounted } from 'vue'
import * as d3 from 'd3'

const timers = []

const themeColor = (name, fallback) =>
  getComputedStyle(document.body).getPropertyValue(name).trim() || fallback

const alphaColor = (color, opacity) => {
  const parsed = d3.color(color)
  if (!parsed) return color
  parsed.opacity = opacity
  return parsed.formatRgb()
}

const setupSvg = (selector, width, height) => {
  d3.select(selector).selectAll('*').remove()

  return d3
    .select(selector)
    .append('svg')
    .attr('viewBox', `0 0 ${width} ${height}`)
    .attr('width', '100%')
    .attr('height', '100%')
    .attr('role', 'img')
}

const drawArchitectureTree = () => {
  const width = 900
  const height = 560
  const accent = themeColor('--accent', '#33ac51')
  const accentSoft = themeColor('--accent-soft', '#68e0ff')
  const text = themeColor('--text', '#eef2f4')
  const muted = themeColor('--text-muted', 'rgba(238, 242, 244, 0.72)')

  const data = {
    name: 'SYSTEM',
    children: [
      {
        name: 'Data Layer',
        children: [
          {
            name: 'Collection',
            children: [{ name: 'Sensors' }, { name: 'Input' }, { name: 'API' }],
          },
          { name: 'Storage', children: [{ name: 'Cache' }, { name: 'Persist' }] },
          { name: 'Access', children: [{ name: 'Query' }, { name: 'Index' }] },
        ],
      },
      {
        name: 'Logic Layer',
        children: [
          {
            name: 'Processing',
            children: [{ name: 'Transform' }, { name: 'Validate' }, { name: 'Compute' }],
          },
          { name: 'Rules', children: [{ name: 'Business' }, { name: 'State' }] },
          { name: 'Workflow', children: [{ name: 'Sequence' }, { name: 'Branch' }] },
        ],
      },
      {
        name: 'Visibility',
        children: [
          {
            name: 'Interface',
            children: [{ name: 'Display' }, { name: 'Interact' }, { name: 'Feedback' }],
          },
          { name: 'Analytics', children: [{ name: 'Metrics' }, { name: 'Trace' }] },
          { name: 'Control', children: [{ name: 'Admin' }, { name: 'Config' }] },
        ],
      },
      {
        name: 'Operations',
        children: [
          { name: 'Monitoring', children: [{ name: 'Health' }, { name: 'Performance' }] },
          { name: 'Sync', children: [{ name: 'Reconcile' }, { name: 'Replicate' }] },
          { name: 'Recovery', children: [{ name: 'Backup' }, { name: 'Restore' }] },
        ],
      },
    ],
  }

  const svg = setupSvg('#aboutViz', width, height).style('overflow', 'visible')

  const defs = svg.append('defs')
  const gradient = defs
    .append('linearGradient')
    .attr('id', 'linkGradient')
    .attr('x1', '0%')
    .attr('y1', '0%')
    .attr('x2', '100%')
    .attr('y2', '0%')

  gradient.append('stop').attr('offset', '0%').attr('stop-color', accent).attr('stop-opacity', 0.28)

  gradient
    .append('stop')
    .attr('offset', '100%')
    .attr('stop-color', accentSoft)
    .attr('stop-opacity', 0.75)

  defs
    .append('filter')
    .attr('id', 'nodeGlow')
    .append('feDropShadow')
    .attr('dx', 0)
    .attr('dy', 0)
    .attr('stdDeviation', 4)
    .attr('flood-color', accent)
    .attr('flood-opacity', 0.25)

  const root = d3.hierarchy(data)
  d3
    .tree()
    .size([height - 120, width - 200])
    .separation((a, b) => (a.parent === b.parent ? 1.2 : 2.2))(root)

  const g = svg.append('g').attr('transform', 'translate(100,60)')

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
    .attr('r', (d) => {
      if (d.depth === 0) return 24
      if (d.depth === 1) return 18
      return 12
    })
    .attr('fill', (d) => {
      if (d.depth === 0) return alphaColor(accent, 0.16)
      if (d.depth === 1) return alphaColor(accentSoft, 0.12)
      return 'rgba(255,255,255,0.08)'
    })
    .attr('stroke', (d) => {
      if (d.depth === 0) return accentSoft
      if (d.depth === 1) return accent
      return muted
    })
    .attr('stroke-width', (d) => {
      if (d.depth === 0) return 3.2
      if (d.depth === 1) return 2
      return 1
    })
    .attr('filter', 'url(#nodeGlow)')

  node
    .append('text')
    .text((d) => d.data.name)
    .attr('dy', 4)
    .attr('x', (d) => {
      if (d.depth === 0) return 0
      if (d.depth === 1) return 24
      return 16
    })
    .attr('text-anchor', (d) => (d.depth === 0 ? 'middle' : 'start'))
    .attr('fill', text)
    .attr('font-size', (d) => {
      if (d.depth === 0) return '0.95rem'
      if (d.depth === 1) return '0.75rem'
      return '0.65rem'
    })
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
}

const drawDeliveryFlow = () => {
  const width = 860
  const height = 300
  const accent = themeColor('--accent', '#33ac51')
  const accentSoft = themeColor('--accent-soft', '#68e0ff')
  const text = themeColor('--text', '#eef2f4')
  const muted = themeColor('--text-muted', 'rgba(238, 242, 244, 0.72)')
  const svg = setupSvg('#deliveryFlowViz', width, height)

  const lanes = [
    { label: 'Field Inputs', x: 80, y: 74 },
    { label: 'Validation', x: 260, y: 168 },
    { label: 'Workflow Engine', x: 450, y: 86 },
    { label: 'Decision UI', x: 630, y: 170 },
    { label: 'Ops Feedback', x: 780, y: 92 },
  ]

  const line = d3
    .line()
    .curve(d3.curveCatmullRom.alpha(0.7))
    .x((d) => d.x)
    .y((d) => d.y)

  const path = svg
    .append('path')
    .datum(lanes)
    .attr('d', line)
    .attr('fill', 'none')
    .attr('stroke', accentSoft)
    .attr('stroke-width', 2.5)
    .attr('stroke-opacity', 0.5)
    .attr('stroke-dasharray', function () {
      const len = this.getTotalLength()
      return `${len} ${len}`
    })
    .attr('stroke-dashoffset', function () {
      return this.getTotalLength()
    })

  path.transition().duration(1400).ease(d3.easeCubicOut).attr('stroke-dashoffset', 0)

  const nodes = svg.selectAll('g.flow-node').data(lanes).join('g').attr('class', 'flow-node')

  nodes
    .attr('transform', (d) => `translate(${d.x},${d.y})`)
    .style('opacity', 0)
    .transition()
    .delay((_, i) => i * 160)
    .duration(500)
    .style('opacity', 1)

  nodes
    .append('circle')
    .attr('r', 26)
    .attr('fill', 'var(--card-bg)')
    .attr('stroke', (_, i) => (i % 2 ? accentSoft : accent))
    .attr('stroke-width', 2)

  nodes
    .append('circle')
    .attr('r', 7)
    .attr('fill', (_, i) => (i % 2 ? accentSoft : accent))

  nodes
    .append('text')
    .attr('y', 48)
    .attr('text-anchor', 'middle')
    .attr('fill', text)
    .attr('font-size', 13)
    .attr('font-weight', 600)
    .text((d) => d.label)

  nodes
    .append('text')
    .attr('y', 66)
    .attr('text-anchor', 'middle')
    .attr('fill', muted)
    .attr('font-size', 11)
    .text((_, i) => `0${i + 1}`)

  const particleLayer = svg.append('g')
  const emitParticle = (delay = 0) => {
    const marker = particleLayer
      .append('circle')
      .attr('r', 5)
      .attr('fill', accent)
      .attr('filter', 'drop-shadow(0 0 8px currentColor)')

    marker
      .transition()
      .delay(delay)
      .duration(3200)
      .ease(d3.easeLinear)
      .attrTween('transform', () => {
        const pathNode = path.node()
        const length = pathNode.getTotalLength()
        return (t) => {
          const point = pathNode.getPointAtLength(t * length)
          return `translate(${point.x},${point.y})`
        }
      })
      .style('opacity', 0)
      .on('end', () => {
        marker.remove()
        emitParticle(450)
      })
  }

  emitParticle()
  emitParticle(1100)
}

const drawCapabilityRadar = () => {
  const width = 420
  const height = 320
  const center = [width / 2, height / 2 + 8]
  const radius = 104
  const accent = themeColor('--accent', '#33ac51')
  const accentSoft = themeColor('--accent-soft', '#68e0ff')
  const text = themeColor('--text', '#eef2f4')
  const muted = themeColor('--text-muted', 'rgba(238, 242, 244, 0.72)')
  const svg = setupSvg('#capabilityRadarViz', width, height)
  const metrics = [
    { label: 'UX', value: 0.86 },
    { label: 'Data', value: 0.92 },
    { label: 'Speed', value: 0.78 },
    { label: 'Resilience', value: 0.9 },
    { label: 'Ops', value: 0.84 },
    { label: 'Scale', value: 0.76 },
  ]

  const angle = (i) => -Math.PI / 2 + (Math.PI * 2 * i) / metrics.length
  const point = (value, i) => [
    center[0] + Math.cos(angle(i)) * radius * value,
    center[1] + Math.sin(angle(i)) * radius * value,
  ]
  const radarLine = d3.line().curve(d3.curveLinearClosed)

  d3.range(1, 5).forEach((ring) => {
    svg
      .append('path')
      .attr('d', radarLine(metrics.map((_, i) => point(ring / 4, i))))
      .attr('fill', 'none')
      .attr('stroke', muted)
      .attr('stroke-opacity', 0.16)
  })

  svg
    .selectAll('line.axis')
    .data(metrics)
    .join('line')
    .attr('x1', center[0])
    .attr('y1', center[1])
    .attr('x2', (_, i) => point(1, i)[0])
    .attr('y2', (_, i) => point(1, i)[1])
    .attr('stroke', muted)
    .attr('stroke-opacity', 0.18)

  svg
    .selectAll('text.metric-label')
    .data(metrics)
    .join('text')
    .attr('x', (_, i) => point(1.22, i)[0])
    .attr('y', (_, i) => point(1.22, i)[1])
    .attr('text-anchor', 'middle')
    .attr('dominant-baseline', 'middle')
    .attr('fill', text)
    .attr('font-size', 12)
    .attr('font-weight', 700)
    .text((d) => d.label)

  const shape = svg
    .append('path')
    .attr('d', radarLine(metrics.map((_, i) => point(0.08, i))))
    .attr('fill', accent)
    .attr('fill-opacity', 0.16)
    .attr('stroke', accentSoft)
    .attr('stroke-width', 2.5)

  shape
    .transition()
    .duration(1100)
    .ease(d3.easeCubicOut)
    .attr('d', radarLine(metrics.map((d, i) => point(d.value, i))))

  svg
    .selectAll('circle.score')
    .data(metrics)
    .join('circle')
    .attr('cx', center[0])
    .attr('cy', center[1])
    .attr('r', 4.5)
    .attr('fill', accent)
    .transition()
    .duration(1100)
    .attr('cx', (d, i) => point(d.value, i)[0])
    .attr('cy', (d, i) => point(d.value, i)[1])
}

const drawOpsPulse = () => {
  const width = 420
  const height = 320
  const center = [width / 2, height / 2]
  const accent = themeColor('--accent', '#33ac51')
  const accentSoft = themeColor('--accent-soft', '#68e0ff')
  const text = themeColor('--text', '#eef2f4')
  const muted = themeColor('--text-muted', 'rgba(238, 242, 244, 0.72)')
  const svg = setupSvg('#opsPulseViz', width, height)
  const ring = svg.append('g').attr('transform', `translate(${center[0]},${center[1]})`)
  const services = [
    { label: 'API', a: -90, r: 96 },
    { label: 'Sync', a: -18, r: 112 },
    { label: 'Queue', a: 54, r: 92 },
    { label: 'DB', a: 126, r: 108 },
    { label: 'UI', a: 198, r: 94 },
  ]

  ring
    .append('circle')
    .attr('r', 78)
    .attr('fill', alphaColor(accent, 0.08))
    .attr('stroke', alphaColor(accent, 0.34))
  ring
    .append('circle')
    .attr('r', 118)
    .attr('fill', 'none')
    .attr('stroke', alphaColor(accentSoft, 0.28))

  const hub = ring
    .append('g')
    .attr('class', 'ops-hub')
    .style('opacity', 0)
    .attr('transform', 'scale(0.8)')

  hub
    .append('circle')
    .attr('r', 36)
    .attr('fill', 'var(--card-bg)')
    .attr('stroke', accent)
    .attr('stroke-width', 2)

  hub
    .append('text')
    .attr('text-anchor', 'middle')
    .attr('dominant-baseline', 'middle')
    .attr('fill', text)
    .attr('font-size', 13)
    .attr('font-weight', 800)
    .text('LIVE')

  hub.transition().duration(700).style('opacity', 1).attr('transform', 'scale(1)')

  const service = ring.selectAll('g.service').data(services).join('g').attr('class', 'service')

  service.attr('transform', (d) => {
    const rad = (d.a * Math.PI) / 180
    return `translate(${Math.cos(rad) * d.r},${Math.sin(rad) * d.r})`
  })

  service
    .append('line')
    .attr('x1', 0)
    .attr('y1', 0)
    .attr('x2', (d) => {
      const rad = (d.a * Math.PI) / 180
      return -Math.cos(rad) * (d.r - 42)
    })
    .attr('y2', (d) => {
      const rad = (d.a * Math.PI) / 180
      return -Math.sin(rad) * (d.r - 42)
    })
    .attr('stroke', muted)
    .attr('stroke-opacity', 0.18)

  service
    .append('circle')
    .attr('r', 17)
    .attr('fill', 'var(--card-bg)')
    .attr('stroke', accentSoft)
    .attr('stroke-width', 1.8)

  service.append('circle').attr('r', 4).attr('fill', accent)

  service
    .append('text')
    .attr('y', 34)
    .attr('text-anchor', 'middle')
    .attr('fill', text)
    .attr('font-size', 12)
    .attr('font-weight', 700)
    .text((d) => d.label)

  const sweep = ring
    .append('line')
    .attr('y1', 0)
    .attr('y2', -118)
    .attr('stroke', accent)
    .attr('stroke-width', 2)
  timers.push(
    d3.timer((elapsed) => {
      sweep.attr('transform', `rotate(${(elapsed / 26) % 360})`)
    }),
  )

  const breathe = () => {
    ring
      .select('circle')
      .transition()
      .duration(1300)
      .attr('r', 86)
      .attr('fill-opacity', 0.6)
      .transition()
      .duration(1300)
      .attr('r', 78)
      .attr('fill-opacity', 1)
      .on('end', breathe)
  }

  breathe()
}

const stopTimers = () => {
  timers.forEach((timer) => timer.stop())
  timers.splice(0, timers.length)
}

const renderVisuals = () => {
  stopTimers()
  drawArchitectureTree()
  drawDeliveryFlow()
  drawCapabilityRadar()
  drawOpsPulse()
}

const toggleTheme = () => {
  const isSoft = document.body.classList.toggle('theme-soft')
  document.body.classList.toggle('theme-dark', !isSoft)
  document.body.classList.toggle('body--dark', !isSoft)
  document.body.classList.toggle('body--light', isSoft)
  document.body.style.setProperty('--q-dark-page', isSoft ? '#faf8f6' : '#07110a')
  renderVisuals()
}

onMounted(renderVisuals)

onBeforeUnmount(stopTimers)
</script>
