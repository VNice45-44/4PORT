<template>
  <q-page class="page landing">

    <!-- TOPBAR -->
    <div class="topbar">
      <div class="brand">
        <div class="mark">
          <svg width="28" height="28" viewBox="0 0 48 48">
            <g fill="#33ac51">
              <circle cx="20" cy="23" r="2" fill="#000"/>
              <circle cx="28" cy="23" r="2" fill="#000"/>
            </g>
          </svg>
        </div>
        <span>Kanu Systems</span>
      </div>
    </div>

    <!-- HERO -->
    <section class="hero">
      <div class="hero-text">
        <h1>Systems</h1>

        <p class="tagline">
          Designed, built, and maintained to hold under real conditions.
        </p>

        <p class="sub">
          Work happens, conditions shift — environments change,
          execution moves, constraints appear.
          Systems need to remain stable through that.
        </p>
      </div>

      <div class="hero-visual">
        <canvas id="sphereCanvas"></canvas>
      </div>
    </section>

    <!-- CORE FLOW -->
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

    <!-- FIELD CONTEXT -->
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

    <!-- SYSTEM CONTEXT BRIDGE -->
    <section class="card">
      <h2>System contexts</h2>

      <p class="sub">
        These systems appear differently depending on what is being done —
        how energy flows, and how work progresses on site.
      </p>
    </section>

    <!-- ENERGY FLOW SYSTEMS -->
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
    <li><span class="timestamp">08:12</span><span class="message">Load stable</span></li>
    <li><span class="timestamp">08:14</span><span class="message">Storage buffering</span></li>
    <li><span class="timestamp">08:16</span><span class="message">Input fluctuation detected</span></li>
  </div>
</section>

    <!-- FIELD EXECUTION SYSTEMS -->
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
        <div class="meta">In progress</div>
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

  <ul class="logs q-mt-md">
    <li>Weather shift affecting excavation pace</li>
    <li>Material delivery delayed</li>
    <li>Crew redistributed to maintain flow</li>
  </ul>

</section>

    <!-- WORK -->
    <section class="card">
      <h2>Work</h2>

      <p>
        Focused on placing systems through design, build, and maintenance
        in environments where execution must remain stable.
      </p>

      <p class="sub">
        Field work · Infrastructure · Ongoing support
      </p>
    </section>

    <!-- FOOTER -->
    <section class="footer">
      <p>Nairobi, Kenya</p>
      <p class="subtle-sign">Kanu Systems</p>
    </section>

  </q-page>
</template>
