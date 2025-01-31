# Overview

### Lighthouse and Secure Block Building (SBB)

Radius builds economic infrastructure that enables rollups to capture MEV revenue while protecting users. Our solutions include:

* **Lighthouse**: A decentralized network that connects rollups with searchers to capture MEV opportunities for sustainable revenue generation.
* **Secure Block Building (SBB**): A built-in component for rollups that minimizes harmful MEV and secures user transactions through cryptographic techniques.

<figure><img src=".gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

***

### Lighthouse: MEV-Powered Revenue Engine

Lighthouse is a decentralized network that connects rollups with searchers to capture MEV during block production. Instead of relying on harmful MEV practices like censorship and reordering, Lighthouse enables rollups to harness MEV strategies that improve market efficiency, such as arbitrage and liquidations.

**How It Works:**&#x20;

1. **Searchers** identify MEV opportunities in rollups and create MEV bundles.
2. **Bundles** are submitted to Lighthouse, where searchers compete by bidding for inclusion.
3. **Rollups** execute winning bundles and earn fees, creating a sustainable revenue stream beyond transaction fees.

**Lighthouse supports diverse MEV strategies including:**

* CEX-DEX arbitrage
* Atomic arbitrage
* Liquidations
* Cross-rollup arbitrage
* Ethereum-rollup arbitrage

Lighthouse continuously evolves to support new MEV strategies, ensuring consistent and scalable revenue for rollups.



### Advanced Features

**Cross-Rollup MEV**

Our partnership with [Avail](https://www.availproject.org/) enables synchronous atomic transactions across rollups, maximizing value capture from cross-rollup opportunities.

* Demo Video: [https://x.com/radius\_xyz/status/1809120933631963165](https://x.com/radius_xyz/status/1809120933631963165)
* Technical Details: [https://ethresear.ch/t/cross-rollup-synchronous-atomic-execution/20193](https://ethresear.ch/t/cross-rollup-synchronous-atomic-execution/20193)

{% embed url="https://ethresear.ch/t/cross-rollup-synchronous-atomic-execution/20193" %}

**Based Sequencing**

Based Sequencing bridges Ethereum liquidity with rollups, unlocking new MEV opportunities and increasing rollup revenue.

{% embed url="https://ethresear.ch/t/derivatives-market-for-implementing-based-sequencing/19593" %}

***

### Secure Block Building (SBB): Built-In User Protection

Secure Block Building is a cryptographic primitive designed to protect users from harmful MEV attacks such as frontrunning and reordering while capturing MEV. SBB is an individual component that Radius customizes and integrates for each rollup.

**Key** **Features**

* **Encrypted Transactions**: User transactions are encrypted directly in the user’s browser, requiring no additional installations or software.
* **Minimal Latency**: Optimized cryptographic techniques reduce encryption and proof generation to under one second.

**Encryption Technologies**

**Practical Verifiable Delay Encryption (PVDE)**: A ZK-based encryption algorithm developed by Radius, PVDE eliminates external trust in key generation. It generates proofs for cryptographic operations and timelock puzzles in under one second.

{% embed url="https://ethresear.ch/t/mev-resistant-zk-rollups-with-practical-vde-pvde/12677" %}

**Single Key Delay Encryption (SKDE)**: SKDE optimizes sequencer efficiency by using a unified encryption key per block, preserving MEV protection while maintaining rollup composability and performance.

{% embed url="https://ethresear.ch/t/radius-skde-enhancing-rollup-composability-with-trustless-sequencing/19185" %}

**Slashing Mechanisms**&#x20;

SBB includes a slashing mechanism that prevents a single sequencer from reordering transactions. This is enforced via:

* Native rollup security
* Shared security protocols like [EigenLayer](https://www.eigenlayer.xyz/) or [Symbiotic](https://symbiotic.fi/).



See Curie Testnet (SBB): [https://x.com/radius\_xyz/status/1724082176818573399](https://x.com/radius_xyz/status/1724082176818573399)

***

### Getting Started

Ready to integrate Lighthouse or Secure Block Building? Here’s how you can get started:

* **Explore**: [GitHub](https://github.com/radius_xyz)
* **Contact Us**: [Contact Form](https://www.theradius.xyz/contact)



