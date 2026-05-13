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
        <router-link to="/about">About</router-link>
        <a href="/#systems">Systems</a>
        <a href="/#notes">Field Notes</a>
        <a href="/#resources">Resources</a>
      </nav>
    </div>

    <section class="about-content">
      <div class="content-wrapper">
        <h1>About</h1>

        <div class="about-text">
          <p>Systems are placed in environments that don't stay still.</p>

          <p>Work moves. Conditions shift. Assumptions break.</p>

          <p>
            Most failures are not caused by a single component going wrong — they emerge from how
            parts interact under changing conditions.
          </p>

          <h2>Typical approaches separate things:</h2>

          <ul>
            <li>Design is done first.</li>
            <li>Execution follows.</li>
            <li>Maintenance reacts later.</li>
          </ul>

          <p>In practice, these phases overlap.</p>

          <p>
            Decisions made early affect behavior much later. Conditions during execution reshape the
            system in real time. Maintenance reveals what was never accounted for.
          </p>

          <p>This work focuses on treating those phases as one continuous system.</p>

          <ul>
            <li>Design considers how things will behave under pressure.</li>
            <li>Execution follows structure, not improvisation.</li>
            <li>Maintenance is part of the system — not an afterthought.</li>
          </ul>

          <h2>The goal is not complexity.</h2>

          <p>It is clarity.</p>

          <p>Understanding how a system behaves before, during, and after it is placed.</p>

          <p>
            So that when conditions change,
            <br />
            the system does not.
          </p>
        </div>
      </div>
    </section>
  </q-page>
</template>

<script setup></script>

<style scoped lang="scss">
.page.about {
  padding: var(--space-5) var(--space-3);
  color: #fff;
  min-height: 100vh;
  display: flex;
  flex-direction: column;

  .topbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: var(--space-4);
    margin-left: calc(var(--space-3) * -1);
    margin-right: calc(var(--space-3) * -1);
    margin-top: calc(var(--space-5) * -1);
    padding-bottom: var(--space-3);
    padding-left: var(--space-3);
    padding-right: var(--space-3);
    padding-top: var(--space-5);
    border-bottom: 1px solid var(--border);

    .brand {
      display: flex;
      align-items: center;
      gap: var(--space-2);
      font-size: 1.1rem;
      font-weight: 500;
      letter-spacing: 1px;
    }

    .brand-link {
      display: flex;
      align-items: center;
      gap: var(--space-2);
      text-decoration: none;
      color: #fff;
      transition: opacity 0.2s;

      &:hover {
        opacity: 0.7;
      }
    }

    .mark {
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .desktop-nav {
      display: flex;
      gap: var(--space-3);
      margin: 0;
      padding: 0;

      a {
        color: #fff;
        text-decoration: none;
        font-size: 0.9rem;
        opacity: 0.6;
        transition: opacity 0.2s;

        &:hover {
          opacity: 1;
          color: cyan;
        }

        &.router-link-active {
          display: none;
        }
      }
    }
  }

  .about-content {
    flex: 1;
    max-width: 920px;
    width: 100%;
    margin: 0 auto;

    .content-wrapper {
      h1 {
        font-size: 2.5rem;
        font-weight: 600;
        letter-spacing: -1px;
        margin-bottom: var(--space-4);
      }

      h2 {
        font-size: 1.8rem;
        font-weight: 500;
        margin-top: var(--space-4);
        margin-bottom: var(--space-2);
      }

      .about-text {
        line-height: 1.6;
        font-size: 1rem;

        p {
          margin-bottom: var(--space-2);

          &:last-child {
            margin-bottom: 0;
          }
        }

        ul {
          margin: var(--space-3) 0;
          padding-left: var(--space-3);
          display: flex;
          flex-direction: column;
          gap: 8px;

          li {
            margin: 0;
          }
        }
      }
    }
  }
}

@media (max-width: 768px) {
  .page.about {
    .topbar {
      flex-direction: column;
      gap: var(--space-2);
      align-items: flex-start;
    }

    .desktop-nav {
      display: flex;
      flex-wrap: wrap;
      gap: var(--space-2);
    }
  }
}
</style>
