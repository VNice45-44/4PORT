<template>
  <q-page class="page landing">
    <div class="topbar">
      <div class="brand">
        <div class="mark">
          <svg width="28" height="28" viewBox="0 0 48 48">
            <g fill="#33ac51">
              <circle cx="20" cy="23" r="2" fill="#000" />
              <circle cx="28" cy="23" r="2" fill="#000" />
            </g>
          </svg>
        </div>
        <span>Kanu Systems</span>
      </div>

      <nav class="desktop-nav">
        <router-link to="/">Home</router-link>
        <router-link to="/about">About</router-link>
        <router-link to="/map">Map</router-link>
        <a href="#systems">Systems</a>
        <a href="#notes">Field Notes</a>
        <a href="#resources">Resources</a>
      </nav>
    </div>

    <section class="hero">
      <div class="hero-text">
        <h1>Systems</h1>
        <p class="tagline">Designed, built, and maintained to hold under real conditions.</p>
        <p class="sub">
          Work happens, conditions shift — environments change, execution moves, constraints appear.
          Systems need to remain stable through that.
        </p>
      </div>

      <div class="hero-visual">
        <div class="hero-map-cta">
          <h2>Interactive Kenya map</h2>
          <p class="sub">
            The full county map lives on its own page, built from the HUMDATA GeoJSON dataset.
          </p>
          <router-link to="/map" class="map-link">Open the map</router-link>
        </div>
      </div>
    </section>

    <section id="about" class="card">
      <h2>About Kanu Systems</h2>
      <p>
        We are an engineering and execution firm based in Nairobi, Kenya. We do not just design
        architecture in isolation; we build systems intended to survive the realities of field
        execution.
      </p>
      <p class="sub">
        Our core philosophy is that the gap between a theoretical design and a deployed system is
        where most failures occur. We specialize in bridging that gap through rigorous structure,
        proactive maintenance, and highly observable workflows.
      </p>
    </section>

    <section class="card">
      <h2>How systems are placed</h2>
      <div class="design-flow">
        <div class="design-step">
          <h3>Design</h3>
          <p>Define structure, constraints, and expected behavior before execution begins.</p>
        </div>

        <div class="design-branch">
          <div class="design-step">
            <h3>Build</h3>
            <p>Execute with awareness of flow, timing, and interaction between parts.</p>
          </div>
          <div class="design-step">
            <h3>Maintain</h3>
            <p>Monitor, adjust, and reinforce systems as conditions change over time.</p>
          </div>
        </div>

        <div class="design-step final">
          <h3>Stability</h3>
          <p>Systems remain predictable under pressure, not just in theory.</p>
        </div>
      </div>
    </section>

    <section class="card">
      <h2>Field context</h2>
      <div class="impact-flow">
        <div class="impact-item">
          <h4>Work is interconnected</h4>
          <p>Power, structure, tools, and people operate together — not in isolation.</p>
        </div>
        <div class="impact-item">
          <h4>Conditions are always shifting</h4>
          <p>Weather, load, material flow, and timing continuously change.</p>
        </div>
        <div class="impact-item">
          <h4>Breakdowns happen between systems</h4>
          <p>Most issues appear in the interaction between parts, not within a single component.</p>
        </div>
        <div class="impact-item final">
          <h4>Clarity stabilizes execution</h4>
          <p>When behavior is understood early, systems remain predictable as conditions evolve.</p>
        </div>
      </div>
    </section>

    <section id="systems" class="card transparent-card">
      <h2>System contexts</h2>
      <p class="sub">
        These systems appear differently depending on what is being done — how energy flows, and how
        work progresses on site.
      </p>
    </section>

    <section class="card">
      <h2>Energy Flow Systems</h2>
      <p class="sub">
        Systems are structured around how energy moves — not just how it is generated.
      </p>

      <div class="flow">
        <div class="node-box active">
          <div class="icon">☀️</div>
          <span>Input</span>
        </div>
        <div class="line"><div class="pulse"></div></div>
        <div class="node-box active">
          <div class="icon">⚡</div>
          <span>Conversion</span>
        </div>
        <div class="line"><div class="pulse"></div></div>
        <div class="node-box">
          <div class="icon">🔋</div>
          <span>Storage</span>
        </div>
        <div class="line"></div>
        <div class="node-box highlight">
          <div class="icon">🏠</div>
          <span>Load</span>
        </div>
      </div>

      <div class="logs-modern q-mt-md">
        <div class="log-item">
          <span class="timestamp">08:12</span><span class="message">Load stable</span>
        </div>
        <div class="log-item">
          <span class="timestamp">08:14</span><span class="message">Storage buffering</span>
        </div>
        <div class="log-item">
          <span class="timestamp">08:16</span
          ><span class="message" style="color: #f2c037">Input fluctuation detected</span>
        </div>
      </div>
    </section>

    <section class="card">
      <h2>Field Execution Systems</h2>
      <p class="sub">
        Work is structured in phases, but performance depends on coordination between them.
      </p>

      <div class="timeline">
        <div class="timeline-row">
          <div class="timeline-marker done"></div>
          <div class="timeline-content">
            <strong>Preparation</strong>
            <div class="meta">Completed</div>
          </div>
        </div>
        <div class="timeline-row">
          <div class="timeline-marker active"></div>
          <div class="timeline-content">
            <strong>Groundwork</strong>
            <div class="meta" style="color: cyan">In progress</div>
          </div>
        </div>
        <div class="timeline-row">
          <div class="timeline-marker"></div>
          <div class="timeline-content">
            <strong>Build</strong>
            <div class="meta">Pending</div>
          </div>
        </div>
        <div class="timeline-row">
          <div class="timeline-marker"></div>
          <div class="timeline-content">
            <strong>Reinforcement</strong>
            <div class="meta">Pending</div>
          </div>
        </div>
      </div>

      <div class="logs-modern q-mt-md">
        <div class="log-item">
          <span class="message">Weather shift affecting excavation pace</span>
        </div>
        <div class="log-item">
          <span class="message" style="color: #f2c037">Material delivery delayed</span>
        </div>
        <div class="log-item">
          <span class="message" style="color: cyan">Crew redistributed to maintain flow</span>
        </div>
      </div>
    </section>

    <section id="notes" class="card transparent-card">
      <h2>Field Notes & Insights</h2>
      <p class="sub">Observations and post-mortems from active deployments.</p>

      <div class="grid-2-col q-mt-md">
        <a href="#" class="system-card">
          <div class="meta">Oct 12, 2025</div>
          <h4>The Illusion of Perfect Models</h4>
          <p class="sub">
            Why theoretical design falls apart during the groundwork phase and how to adjust
            dynamically.
          </p>
        </a>
        <a href="#" class="system-card">
          <div class="meta">Sep 04, 2025</div>
          <h4>Energy Buffering at Scale</h4>
          <p class="sub">
            A breakdown of input fluctuation management across distributed solar loads.
          </p>
        </a>
      </div>
    </section>

    <section id="resources" class="card transparent-card">
      <h2>Architecture & Tooling</h2>
      <p class="sub">Publicly available frameworks and documentation.</p>

      <div class="resource-list">
        <div class="resource-item">
          <strong>WAKO Project Specs</strong>
          <span>Phase 1 Documentation</span>
          <q-btn flat dense icon="download" color="cyan" size="sm" />
        </div>
        <div class="resource-item">
          <strong>Node WL-01 API</strong>
          <span>Telemetry Endpoints</span>
          <q-btn flat dense icon="code" color="cyan" size="sm" />
        </div>
      </div>
    </section>

    <footer class="footer">
      <div class="footer-grid">
        <div class="footer-col">
          <h4>Kanu Systems</h4>
          <p class="sub">Execution-focused engineering.<br />Designed to hold.</p>
        </div>

        <div class="footer-col">
          <h4>Directory</h4>
          <a href="#about">About</a>
          <a href="#systems">Systems</a>
          <a href="#notes">Field Notes</a>
        </div>

        <div class="footer-col">
          <h4>Contact & Location</h4>
          <p>Nairobi, Kenya</p>
          <a href="mailto:ops@kanusystems.com">ops@kanusystems.com</a>
        </div>
      </div>

      <div class="footer-bottom">
        <p class="subtle-sign">© 2026 Kanu Systems. All systems nominal.</p>
      </div>
    </footer>
  </q-page>
</template>

<style scoped lang="scss">
.desktop-nav a.router-link-active {
  display: none;
}

.hero-map-cta {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 1rem;
  background: rgba(10, 16, 24, 0.95);
  border-radius: 24px;
  padding: 2rem;
  min-height: 300px;
}

.map-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.9rem 1.6rem;
  background: #33ac51;
  color: #07110a;
  border-radius: 999px;
  font-weight: 700;
  text-decoration: none;
  width: fit-content;
}

.map-link:hover {
  opacity: 0.92;
}
</style>
