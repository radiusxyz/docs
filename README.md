# Product Overview

### Lighthouse and Secure Block Building (SBB)

Radius is developing Lighthouse and Secure Block Building (SBB) to help rollups stay profitable, healthy, and sustainably growing.

***

### Lighthouse: MEV Internalization

<figure><img src=".gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

**Lighthouse** is a decentralized network designed to help rollups capture MEV (Maximal Extractable Value). By connecting rollups with specialized traders like searchers and builders, Lighthouse facilitates the coordination of MEV bundles which are profitable arbitrage strategies. Rollups prioritize these bundles at the top of each block, ensuring execution and generating revenue.&#x20;

The goal of Lighthouse is to create a sustainable revenue model for rollups by internalizing MEV opportunities. It promotes an open, competitive blockspace marketplace, benefiting both rollups and builders through optimized MEV capture and efficient coordination.

Lighthouse supports a variety of high-value strategies, including: CEX-DEX arbitrage, atomic arbitrage, liquidations, cross-rollup arbitrage, and Ethereum-rollup arbitrage.

### Secure Block Building: User Protection

**Secure Block Building (SBB)** is a protection module for protecting users from harmful MEV, like frontrunning and sandwich attacks, which can happen during MEV internalization. By using zero-knowledge (ZK) proofs and encrypted mempools, SBB encrypts user transactions without disrupting the user experience. It enables rollups to capture MEV profitably while keeping users protected from economic threats.

SBB runs entirely in the user's browser, so there's no need to install additional apps or extensions. Thanks to recent optimizations, encryption and proof generation now take just one second, making the process almost instant.

Curie Testnet: [https://x.com/radius\_xyz/status/1724082176818573399](https://x.com/radius\_xyz/status/1724082176818573399)​

### SBB Encryption Algorithms

**Practical Verifiable Delay Encryption (PVDE)**: This zero-knowledge (ZK) algorithm, developed by Radius, eliminates the need for external trust in key generation. PVDE allows rollups to create proofs for complex cryptographic operations and timelock puzzles in just one second, ensuring fast and secure performance.

{% embed url="https://ethresear.ch/t/mev-resistant-zk-rollups-with-practical-vde-pvde/12677" %}

**Single Key Delay Encryption (SKDE)**: Another ZK algorithm, SKDE reduces the load on sequencers by using a single encryption key for all transactions within a block. This design boosts efficiency while still protecting against MEV attacks like frontrunning and censorship.Benefits of Building with Radius

{% embed url="https://ethresear.ch/t/radius-skde-enhancing-rollup-composability-with-trustless-sequencing/19185" %}

#### **Slashing for Security**

SBB includes built-in slashing mechanisms to prevent sequencers from reordering transactions. Rollups can secure this system using their own tokens or leverage Ethereum’s security via restaking protocols like [EigenLayer](https://www.eigenlayer.xyz/) and [Symbiotic](https://symbiotic.fi/).

***

### Revenue Maximization

Radius enhances liquidity access across the Ethereum ecosystem, enabling profitable MEV strategies such as CEX-DEX arbitrage, cross-rollup arbitrage, and Ethereum-rollup arbitrage (based sequencing). Both Lighthouse and SBB are continuously upgraded to unlock new revenue opportunities.

#### Cross-Rollup Arbitrage

Radius is partnering with [Avail](https://www.availproject.org/) to create a protocol for guaranteed cross-rollup transaction execution, ensuring synchronous atomic transactions. This integration into Lighthouse and SBB will help rollups capture value from cross-rollup arbitrage, maximizing profits.

Demo: [https://x.com/radius\_xyz/status/1809120933631963165](https://x.com/radius\_xyz/status/1809120933631963165)

{% embed url="https://ethresear.ch/t/cross-rollup-synchronous-atomic-execution/20193" %}

#### Based Sequencing

By connecting Ethereum liquidity to rollups, Radius enables searchers to discover new arbitrage opportunities, ultimately boosting rollup revenue.

{% embed url="https://ethresear.ch/t/derivatives-market-for-implementing-based-sequencing/19593" %}



