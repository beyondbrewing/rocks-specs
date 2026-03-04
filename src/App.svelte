<script>
  import Overview from './lib/Overview.svelte';
  import RelayNetwork from './lib/RelayNetwork.svelte';

  let activeSection = 0;

  const sections = [
    "Overview",
    "Relay Network",
  ];
</script>

<div class="app">
  <!-- Header -->
  <header class="header">
    <div class="header-title">
      <span class="logo">ROCKS://</span>
      <span class="version-badge">PROTOCOL SPEC v0.1.0</span>
    </div>
    <div class="header-sub">
      Relay-Oriented Cryptographic Key-addressed Service — Decentralized Identity-Routed Protocol
    </div>
  </header>

  <div class="layout">
    <!-- Sidebar -->
    <nav class="sidebar">
      {#each sections as section, i}
        <button
          class="nav-btn"
          class:active={activeSection === i}
          on:click={() => (activeSection = i)}
        >
          <span class="nav-index">{String(i).padStart(2, "0")}</span>
          {section}
        </button>
      {/each}
    </nav>

    <!-- Main Content -->
    <main class="content">
      {#if activeSection === 0}
        <Overview />
      {/if}

      {#if activeSection === 1}
        <RelayNetwork />
      {/if}
    </main>
  </div>
</div>

<style>
  .app {
    background: var(--bg);
    min-height: 100vh;
    color: var(--text);
    font-family: var(--sans);
  }

  /* Header */
  .header {
    border-bottom: 1px solid var(--border);
    padding: 20px 24px;
    background: var(--surface);
  }
  .header-title {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 4px;
  }
  .logo {
    color: var(--accent);
    font-family: var(--mono);
    font-size: 24px;
    font-weight: 700;
    letter-spacing: 2px;
  }
  .version-badge {
    color: var(--text-dim);
    font-size: 12px;
    font-family: var(--mono);
    padding: 2px 8px;
    border: 1px solid var(--border);
    border-radius: 4px;
  }
  .header-sub {
    color: var(--text-dim);
    font-size: 12px;
    font-family: var(--mono);
  }

  /* Layout */
  .layout {
    display: flex;
    min-height: calc(100vh - 80px);
  }

  /* Sidebar */
  .sidebar {
    width: 220px;
    min-width: 220px;
    border-right: 1px solid var(--border);
    padding: 16px 0;
    background: var(--surface);
  }
  .nav-btn {
    display: block;
    width: 100%;
    text-align: left;
    padding: 10px 20px;
    border: none;
    cursor: pointer;
    background: transparent;
    color: var(--text-dim);
    font-family: var(--mono);
    font-size: 12px;
    letter-spacing: 0.5px;
    border-left: 3px solid transparent;
    transition: all 0.15s;
  }
  .nav-btn:hover {
    background: var(--surface-hover);
    color: var(--text);
  }
  .nav-btn.active {
    background: var(--accent-dim);
    color: var(--accent);
    border-left-color: var(--accent);
  }
  .nav-index {
    opacity: 0.4;
    margin-right: 8px;
  }

  /* Content */
  .content {
    flex: 1;
    padding: 32px 40px;
    overflow-y: auto;
  }

  /* Responsive */
  @media (max-width: 768px) {
    .layout { flex-direction: column; }
    .sidebar {
      width: 100%;
      min-width: 100%;
      display: flex;
      overflow-x: auto;
      padding: 8px;
      border-right: none;
      border-bottom: 1px solid var(--border);
    }
    .nav-btn {
      white-space: nowrap;
      padding: 8px 14px;
      border-left: none;
      border-bottom: 3px solid transparent;
    }
    .nav-btn.active {
      border-left-color: transparent;
      border-bottom-color: var(--accent);
    }
    .content { padding: 20px 16px; }
  }
</style>
