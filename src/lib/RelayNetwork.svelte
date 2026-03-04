<script>
  const relayNodes = [
    { id: "A", label: "Origin Node", x: 40, y: 130, color: "var(--accent)" },
    { id: "R1", label: "Relay 1", x: 200, y: 60, color: "var(--purple)" },
    { id: "R2", label: "Relay 2", x: 360, y: 160, color: "var(--purple)" },
    { id: "R3", label: "Relay 3", x: 520, y: 80, color: "var(--purple)" },
    { id: "B", label: "Destination", x: 680, y: 130, color: "var(--cyan)" },
  ];

  const relayPaths = [[0, 1], [1, 2], [2, 3], [3, 4]];

  const encLayers = [
    { from: 0, label: "Layer 3: Origin ↔ Destination (E2E)", color: "var(--cyan)" },
    { from: 0, label: "Layer 2: Origin → Relay 3", color: "var(--purple)" },
    { from: 0, label: "Layer 1: Origin → Relay 2", color: "var(--accent)" },
  ];
</script>

<section>
  <h2 class="section-title">// Relay Network — Onion-Routed Blockchain Mesh</h2>
  <p class="prose">
    The ROCKS relay network provides <span class="hl purple">Tor-like onion routing</span> over a
    decentralized mesh of blockchain-staked relay nodes. Unlike Tor, relay operators must stake tokens
    on-chain to participate, creating economic incentives against malicious behavior.
  </p>

  <!-- Relay Diagram -->
  <div class="panel">
    <div class="panel-label">Onion-Routed Relay Path (3-hop minimum)</div>
    <svg viewBox="0 0 750 260" class="relay-svg">
      <defs>
        <filter id="glow">
          <feGaussianBlur stdDeviation="3" result="blur" />
          <feMerge>
            <feMergeNode in="blur" />
            <feMergeNode in="SourceGraphic" />
          </feMerge>
        </filter>
      </defs>

      {#each relayPaths as [fi, ti]}
        <line
          x1={relayNodes[fi].x} y1={relayNodes[fi].y}
          x2={relayNodes[ti].x} y2={relayNodes[ti].y}
          stroke="var(--purple)" stroke-width="2" stroke-dasharray="6 4" opacity="0.5"
        />
      {/each}

      {#each encLayers as layer, i}
        <rect x={relayNodes[layer.from].x - 15} y={200 + i * 20} width="12" height="12" rx="2"
          fill={layer.color} opacity="0.3" stroke={layer.color} stroke-width="1" />
        <text x={relayNodes[layer.from].x + 4} y={210 + i * 20} fill="var(--text-dim)" font-size="10" font-family="var(--mono)">
          {layer.label}
        </text>
      {/each}

      {#each relayNodes as node}
        <g filter="url(#glow)">
          <circle cx={node.x} cy={node.y} r="22" fill="var(--bg)" stroke={node.color} stroke-width="2" />
          <text x={node.x} y={node.y + 4} text-anchor="middle" fill={node.color} font-size="11" font-weight="700" font-family="var(--mono)">
            {node.id}
          </text>
          <text x={node.x} y={node.y + 40} text-anchor="middle" fill="var(--text-dim)" font-size="9" font-family="var(--mono)">
            {node.label}
          </text>
        </g>
      {/each}
    </svg>
  </div>

  <p class="prose">
    Every connection between two ROCKS nodes traverses a minimum of <span class="hl">3 relay hops</span>.
    Each relay only knows its immediate predecessor and successor — never the full path.
    The payload is wrapped in multiple encryption layers (onion encryption), and each relay peels
    one layer to discover the next hop.
  </p>

</section>
