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
      </nav>
    </div>

    <section class="hero">
      <div class="hero-text">
        <h1>Field-ready systems for built environments.</h1>
        <p class="tagline">
          Construction, solar energy, security, and estate planning — delivered from Nairobi, Kenya.
        </p>
        <p class="sub">
          We design and execute systems that continue to work when conditions change. The map is a
          live demonstration of our attention to place, structure, and data.
        </p>
      </div>
    </section>

    <section class="card">
      <h2>What we deliver</h2>
      <div class="service-grid">
        <div class="service-card">
          <h3>Construction</h3>
          <p>Structural work designed and built with durability and field conditions in mind.</p>
        </div>
        <div class="service-card">
          <h3>Solar & electrical systems</h3>
          <p>Power installations that are compact, maintainable, and designed to keep operating.</p>
        </div>
        <div class="service-card">
          <h3>CCTV & security</h3>
          <p>Site visibility systems that integrate into the broader execution workflow.</p>
        </div>
        <div class="service-card">
          <h3>Resort & ranch planning</h3>
          <p>High-end property layouts and site planning tuned for operational flow.</p>
        </div>
      </div>
    </section>

    <section class="card">
      <h2>How we think</h2>
      <p class="sub">
        Systems are not separate pieces. The work is successful when the whole remains stable.
      </p>

      <div class="design-flow">
        <div class="design-step">
          <h3>Define</h3>
          <p>Set the constraints, the site logic, and what needs to stay working.</p>
        </div>

        <div class="design-branch">
          <div class="design-step">
            <h3>Build</h3>
            <p>Execute with the structure of the system as the guide.</p>
          </div>
          <div class="design-step">
            <h3>Maintain</h3>
            <p>Keep the system observable and ready to adapt.</p>
          </div>
        </div>

        <div class="design-step final">
          <h3>Deliver</h3>
          <p>Work that remains predictable after handover.</p>
        </div>
      </div>
    </section>

    <section class="card transparent-card">
      <h2>Portfolio note</h2>
      <p class="sub">
        The map, the site logic, and the way systems are presented are part of how we show our work.
        It is a display of method, not just finished assets.
      </p>
    </section>

    <footer class="footer">
      <div class="footer-grid">
        <div class="footer-col">
          <h4>Kanu Systems</h4>
          <p class="sub">Field-ready systems and site work from Nairobi.</p>
          <p class="sub">Samuel Kanu<br />VersityVille House<br />Nairobi 1928-00300</p>
        </div>

        <div class="footer-col">
          <h4>Quick links</h4>
          <router-link to="/map">Map</router-link>
          <router-link to="/about">About</router-link>
        </div>

        <div class="footer-col">
          <h4>Contact</h4>
          <p>ops@kanusystems.com</p>
          <p>+254 700 000 000</p>
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

.service-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(220px, 1fr));
  gap: 1rem;
  margin-top: 1.5rem;
}

.service-card {
  background: rgba(11, 23, 44, 0.9);
  border: 1px solid rgba(51, 172, 81, 0.18);
  border-radius: 20px;
  padding: 1.2rem 1.25rem;
}

.service-card h3 {
  margin-top: 0;
}

.footer-col a.router-link-active,
.footer-col a {
  display: block;
  color: #e7edf7;
  text-decoration: none;
  margin-bottom: 0.55rem;
}

.footer-col a:hover {
  color: #33ac51;
}
</style>
