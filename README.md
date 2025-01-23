# Overview

### Lighthouse and Secure Block Building (SBB)

Radius builds economic infrastructure enabling rollups to capture MEV revenue while protecting users. Our solution combines **Lighthouse** to connect rollups with searchers to capture MEV opportunities with **Secure Block Building (SBB)** to ensure safe MEV capture while protecting user transactions. Together, they enable rollups to generate sustainable revenue without compromising user trust.

<figure><img src=".gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

***

### Lighthouse: MEV-Powered Revenue Engine

**Lighthouse** is a decentralized network that connects rollups with searchers to capture MEV during block production. Instead of relying on harmful practices like censorship and transaction reordering, it helps generate revenue through strategies that improve market efficiency, such as arbitrage and liquidations.

**How It Works:**&#x20;

1. **Searchers** identify MEV opportunities within rollups and create MEV bundles.
2. **Bundles** are submitted to Lighthouse, where searchers compete by bidding for inclusion.
3. **Rollups** execute winning bundles and earn fees, creating a sustainable revenue stream beyond transaction fees.

Lighthouse supports diverse MEV strategies including:

* CEX-DEX arbitrage
* Atomic arbitrage
* Liquidations
* Cross-rollup arbitrage
* Ethereum-rollup arbitrage

These strategies ensure consistent, scalable revenue while benefiting both rollups and searchers through optimized MEV capture.



#### Advanced Features

Radius enhances liquidity access across the Ethereum ecosystem, enabling profitable MEV strategies such as CEX-DEX arbitrage, cross-rollup arbitrage, and Ethereum-rollup arbitrage (based sequencing). Both Lighthouse and SBB are continuously upgraded to unlock new revenue opportunities.



**Cross-Rollup MEV**

Our partnership with [Avail](https://www.availproject.org/) enables synchronous atomic transactions across rollups, maximizing value capture from cross-rollup opportunities.

* Demo Video: [https://x.com/radius\_xyz/status/1809120933631963165](https://x.com/radius_xyz/status/1809120933631963165)
* Technical Details: [https://ethresear.ch/t/cross-rollup-synchronous-atomic-execution/20193](https://ethresear.ch/t/cross-rollup-synchronous-atomic-execution/20193)

{% embed url="https://ethresear.ch/t/cross-rollup-synchronous-atomic-execution/20193" %}

**Based Sequencing**

Based Sequencing bridges Ethereum liquidity with rollups, unlocking new MEV opportunities and further increasing rollup revenue.

{% embed url="https://ethresear.ch/t/derivatives-market-for-implementing-based-sequencing/19593" %}

***

### Secure Block Building (SBB): Built-In User Protection

**Secure Block Building** leverages cryptographic techniques to enable MEV revenue generation while protecting user transactions from harmful practices like censorship and transaction reordering.

* Transactions are encrypted directly in the user’s browser, requiring no additional installations or extensions.
* Recent optimizations have reduced encryption and proof generation to under one second, ensuring minimal latency.

See Curie Testnet (SBB): [https://x.com/radius\_xyz/status/1724082176818573399](https://x.com/radius_xyz/status/1724082176818573399)

​

#### Encryption Technologies

**Practical Verifiable Delay Encryption (PVDE)**: A ZK algorithm developed by Radius that eliminates external trust in key generation. It creates proofs for cryptographic operations and timelock puzzles in under one second.

{% embed url="https://ethresear.ch/t/mev-resistant-zk-rollups-with-practical-vde-pvde/12677" %}

**Single Key Delay Encryption (SKDE)**: A ZK algorithm that optimizies sequencer efficiency by using a unified encryption key for all transactions within a block. This approach maintains protection against MEV attacks while improving system performance and rollup composability.

{% embed url="https://ethresear.ch/t/radius-skde-enhancing-rollup-composability-with-trustless-sequencing/19185" %}

#### Slashing Mechanisms&#x20;

SBB includes a slashing mechanism to prevent any single sequencer from reordering transactions. This is implemented through the rollup’s native security or by smart contracts that leverage shared security protocols like [EigenLayer](https://www.eigenlayer.xyz/) or [Symbiotic](https://symbiotic.fi/).

***

### Getting Started

Ready to integrate Lighthouse or Secure Block Building? Here’s how you can get started:

* **Explore**: [GitHub](https://github.com/radius_xyz)
* **Contact Us**:&#x20;



