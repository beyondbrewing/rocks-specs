<section>
  <h2 class="section-title">// ROCKS Protocol — Overview</h2>
  <p class="prose">
    <span class="hl">ROCKS</span> (Relay-Oriented Cryptographic Key-addressed Service) is a decentralized
    application-layer protocol that uses <span class="hl cyan">EIP-55 checksummed Ethereum addresses</span> as
    native network identifiers. It provides two scheme variants:
  </p>

  <div class="grid-2">
    <div class="card card-accent">
      <div class="card-title accent">rocks://</div>
      <div class="card-body">End-to-end encrypted transport via onion-routed relay network. All traffic is authenticated and encrypted using keys derived from the destination's Ethereum keypair.</div>
    </div>
    <div class="card card-warning">
      <div class="card-title warning">rock://</div>
      <div class="card-body">Unencrypted relay transport. Traffic is still routed through the relay network for censorship resistance, but payload is not E2E encrypted. Signed for authenticity only.</div>
    </div>
  </div>

  <p class="prose">
    Unlike DNS-based protocols, ROCKS uses <span class="hl purple">cryptographic identity as the address itself</span>.
    Your address IS your public key (derived). No registrars, no DNS, no certificate authorities. Identity is
    self-sovereign and rooted in the same key material that secures Ethereum wallets.
  </p>

  <div class="code-block">
    <div class="code-title">URI Format</div>
    <pre>{`rocks://0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045/path/to/resource
rock://0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045/path/to/resource

Full URI grammar:
  scheme    := "rocks" | "rock"
  authority := "0x" <40 hex chars, EIP-55 checksummed>
  path      := "/" <resource path>
  query     := "?" <key=value pairs>
  fragment  := "#" <section>

  URI = scheme "://" authority [path] [query] [fragment]

Examples:
  rocks://0xAb5801a7D398351b8bE11C439e05C5B3259aeC9B
  rocks://0xAb5801a7D398351b8bE11C439e05C5B3259aeC9B/api/v1/data?format=json
  rock://0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045/public/status`}</pre>
  </div>

  <p class="prose">
    The protocol stack: <span class="hl">Application → ROCKS Session → Relay Circuit → Transport (TCP/UDP/QUIC)</span>
  </p>
</section>
