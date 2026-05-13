<template>
  <q-page class="page about">
    <div class="topbar">
      <div class="brand">
        <router-link to="/" class="brand-link">
          <div class="mark">
            <svg width="28" height="28" viewBox="0 0 48 48">
              <g fill="#33ac51">
                <circle cx="20" cy="23" r="2" fill="#000" />
                <circle cx="28" cy="23" r="2" fill="#000" />
              </g>
            </svg>
          </div>
          <span>Kanu Systems</span>
        </router-link>
      </div>

      <nav class="desktop-nav">
        <router-link to="/">Home</router-link>
        <router-link to="/map">Map</router-link>
      </nav>
    </div>

    <section class="hero">
      <div class="hero-body">
        <p class="eyebrow">At Kanu Systems, we...</p>
        <h1>Build systems that stay intact when the field changes.</h1>
        <p class="hero-sub">
          Engineering, installation, and planning work together in one continuous flow rather than
          in isolated phases.
        </p>
      </div>

      <div class="hero-viz">
        <div id="aboutViz" class="viz-shell"></div>
      </div>
    </section>

    <section class="info-grid">
      <div class="info-card">
        <h2>What we bring</h2>
        <p>
          A practical approach to construction, solar energy, security, and site design — focused on
          stability, visibility, and long-term performance.
        </p>
      </div>
      <div class="info-card accent">
        <h2>How we make it work</h2>
        <p>
          We treat systems as connected pieces, not separate deliverables. The shape of the work is
          as important as the final asset.
        </p>
      </div>
    </section>

    <section class="details">
      <div class="detail-block">
        <h3>Design, build, maintain</h3>
        <p>
          The strongest systems are designed with execution in mind, monitored during deployment,
          and adjusted before they fail.
        </p>
      </div>
      <div class="detail-block">
        <h3>Portfolio without flash</h3>
        <p>
          The site is intentionally direct: a map asset, a structured narrative, and a clean point
          of view on how systems are assembled.
        </p>
      </div>
    </section>

    <footer class="footer">
      <div class="footer-grid">
        <div class="footer-col">
          <h4>Kanu Systems</h4>
          <p class="sub">Field-ready systems and site work, based in Nairobi.</p>
        </div>

        <div class="footer-col">
          <h4>Contact</h4>
          <p>Samuel Kanu</p>
          <p>VersityVille House</p>
          <p>Nairobi 1928-00300</p>
          <p>ops@kanusystems.com</p>
        </div>
      </div>
    </footer>
  </q-page>
</template>

<script setup>
import { onMounted } from 'vue'
import * as d3 from 'd3'

const nodes = [
  { id: 'Kanu Systems', radius: 42, fixed: true },
  { id: 'Construction', radius: 26 },
  { id: 'Solar', radius: 24 },
  { id: 'Security', radius: 24 },
  { id: 'Resort Planning', radius: 21 },
  { id: 'Maintenance', radius: 29 },
]

const links = [
  { source: 'Kanu Systems', target: 'Construction' },
  { source: 'Kanu Systems', target: 'Solar' },
  { source: 'Kanu Systems', target: 'Security' },
  { source: 'Kanu Systems', target: 'Resort Planning' },
  { source: 'Kanu Systems', target: 'Maintenance' },
]

onMounted(() => {
  const width = 620
  const height = 420
  const svg = d3
    .select('#aboutViz')
    .append('svg')
    .attr('width', width)
    .attr('height', height)
    .attr('viewBox', `0 0 ${width} ${height}`)
    .attr('preserveAspectRatio', 'xMidYMid meet')

  const link = svg
    .append('g')
    .attr('class', 'links')
    .selectAll('line')
    .data(links)
    .enter()
    .append('line')
    .attr('stroke', 'rgba(255,255,255,0.0009)')
    .attr('stroke-width', 1.2)

  const node = svg
    .append('g')
    .attr('class', 'nodes')
    .selectAll('g')
    .data(nodes)
    .enter()
    .append('g')
    .attr('class', 'node')
    .call(
      d3
        .drag()
        .on('start', (event, d) => {
          if (!event.active) simulation.alphaTarget(0.3).restart()
          d.fx = d.x
          d.fy = d.y
        })
        .on('drag', (event, d) => {
          d.fx = event.x
          d.fy = event.y
        })
        .on('end', (event, d) => {
          if (!event.active) simulation.alphaTarget(0)
          d.fx = null
          d.fy = null
        }),
    )

  node
    .append('circle')
    .attr('r', (d) => d.radius)
    .attr('fill', (d) => (d.id === 'Kanu Systems' ? '#33ac51' : 'rgba(255,255,255,0.08)'))
    .attr('stroke', '#33ac51')
    .attr('stroke-width', (d) => (d.id === 'Kanu Systems' ? 2.4 : 1.4))

  node
    .append('text')
    .text((d) => d.id)
    .attr('fill', '#ffffff')
    .attr('font-size', (d) => (d.id === 'Kanu Systems' ? 14 : 12))
    .attr('font-weight', (d) => (d.id === 'Kanu Systems' ? 700 : 400))
    .attr('text-anchor', 'middle')
    .attr('dy', (d) => (d.id === 'Kanu Systems' ? 5 : 4))
    .call((text) =>
      text.each(function (d) {
        const el = d3.select(this)
        const words = d.id.split(' ')
        el.text('')
        words.forEach((word, i) => {
          el.append('tspan')
            .attr('x', 0)
            .attr('dy', i === 0 ? 0 : 14)
            .text(word)
        })
      }),
    )

  const simulation = d3
    .forceSimulation(nodes)
    .force(
      'link',
      d3
        .forceLink(links)
        .id((d) => d.id)
        .distance(140)
        .strength(0.95),
    )
    .force('charge', d3.forceManyBody().strength(-220))
    .force('center', d3.forceCenter(width / 2, height / 2))
    .force(
      'collision',
      d3.forceCollide().radius((d) => d.radius + 16),
    )
    .on('tick', () => {
      link
        .attr('x1', (d) => d.source.x)
        .attr('y1', (d) => d.source.y)
        .attr('x2', (d) => d.target.x)
        .attr('y2', (d) => d.target.y)

      node.attr('transform', (d) => `translate(${d.x},${d.y})`)
    })

  svg
    .append('circle')
    .attr('cx', width / 2)
    .attr('cy', height / 2)
    .attr('r', 176)
    .attr('fill', 'none')
    .attr('stroke', 'rgba(255,255,255,0.06)')
    .attr('stroke-width', 1)

  svg
    .append('circle')
    .attr('cx', width / 2)
    .attr('cy', height / 2)
    .attr('r', 240)
    .attr('fill', 'none')
    .attr('stroke', 'rgba(255,255,255,0.04)')
    .attr('stroke-width', 1)
})
</script>

<style scoped lang="scss">
.page.about {
  padding: 1.5rem 1rem;
  color: #fff;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.topbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.brand-link {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  color: #fff;
  text-decoration: none;
}

.brand-link:hover {
  opacity: 0.8;
}

.desktop-nav {
  display: flex;
  gap: 1.5rem;
}

.desktop-nav a {
  color: rgba(255, 255, 255, 0.78);
  text-decoration: none;
  font-size: 0.95rem;
}

.desktop-nav a.router-link-active,
.desktop-nav a:hover {
  color: #33ac51;
}

.hero {
  display: grid;
  grid-template-columns: 1.4fr 1fr;
  gap: 2rem;
  align-items: center;
  margin-bottom: 1.75rem;
}

.hero-body {
  max-width: 520px;
}

.eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.24em;
  font-size: 0.78rem;
  color: #33ac51;
  margin-bottom: 1rem;
}

.hero h1 {
  font-size: clamp(2.5rem, 3.5vw, 4rem);
  line-height: 1.03;
  margin: 0;
}

.hero-sub {
  margin-top: 1rem;
  color: rgba(255, 255, 255, 0.78);
  line-height: 1.8;
}

.hero-viz {
  display: flex;
  justify-content: center;
}

.viz-shell {
  width: 100%;
  max-width: 620px;
  min-height: 420px;
  border-radius: 28px;
  background: rgba(10, 16, 24, 0.95);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: 0 28px 60px rgba(0, 0, 0, 0.32);
  overflow: hidden;
}

.info-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(220px, 1fr));
  gap: 1rem;
  margin-bottom: 1.75rem;
}

.info-card {
  padding: 1.5rem;
  background: rgba(10, 16, 24, 0.95);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 22px;
}

.info-card.accent {
  border-color: rgba(51, 172, 81, 0.24);
  background: rgba(19, 38, 62, 0.9);
}

.info-card h2 {
  margin-top: 0;
  font-size: 1.3rem;
}

.details {
  display: grid;
  grid-template-columns: repeat(2, minmax(220px, 1fr));
  gap: 1rem;
  margin-bottom: 2rem;
}

.detail-block {
  padding: 1.3rem;
  background: rgba(11, 23, 44, 0.9);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 20px;
}

.detail-block h3 {
  margin-top: 0;
  margin-bottom: 0.75rem;
}

.detail-block p {
  margin: 0;
  color: rgba(255, 255, 255, 0.82);
  line-height: 1.8;
}

.footer {
  margin-top: auto;
  padding-top: 1.5rem;
  border-top: 1px solid rgba(255, 255, 255, 0.08);
}

.footer-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.footer-col h4 {
  margin-bottom: 0.75rem;
}

.footer-col p {
  margin: 0.45rem 0;
  color: rgba(255, 255, 255, 0.75);
}

@media (max-width: 960px) {
  .hero {
    grid-template-columns: 1fr;
  }

  .info-grid,
  .details,
  .footer-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 640px) {
  .desktop-nav {
    flex-wrap: wrap;
    gap: 1rem;
  }
}
</style>
