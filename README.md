---
description: 'Learn about Secure Block Building (SBB) and Lighthouse: Tools for L2 Revenue'
---

# Introduction

Radius presents a new approach to reshape the rollup economic landscape by unlocking MEV as a revenue source. While rollups are critical for Ethereum's growth, their reliance on user fees introduces economic uncertainty. These fees fluctuate with network demand, leading to unpredictable revenue and constrained growth.

***

### What We Do

Radius addresses this challenge through two solutions: **Secure Block Building (SBB)** and **Lighthouse**. These tools enable rollups to access MEV that would otherwise be unavailable to them. SBB enhances L2 block building through searcher collaboration to capture MEV, while Lighthouse creates a network for rollups to share MEV opportunities across platforms. Together, they provide stable, scalable revenue for rollups—establishing the foundation for a unified and economically aligned Ethereum ecosystem.



**Secure Block Building (SBB)**

A powerful tool that enhances L2 block building to capture MEV through efficient searcher collaboration, increasing revenue generation

→ [SBB Overview](overview/secure-block-building-sbb.md)



**Lighthouse**

A decentralized network that connects multiple rollups, enabling them to capture cross-rollup MEV and expand their revenue opportunities

→ [Lighthouse Overview](overview/lighthouse.md)

***

### Understanding MEV

Maximal Extractable Value (MEV) is the profit rollups can earn by strategically ordering transactions during block production: a potential that most Layer 2s currently cannot access.&#x20;

MEV takes several forms:

* **Beneficial MEV**:
  * **Arbitrage**: Captures price differences across markets (e.g., CEX-DEX, cross-rollup, L1-L2, atomic) to align prices and improve market efficiency
  * **Liquidations**: Closes undercollateralized positions to maintain protocol stability
* **Harmful MEV**:
  * **Frontrunning**: Profits by executing ahead of user transactions, increasing user costs through slippage
  * **Sandwich Attacks**: Manipulates prices around a user's trade for profit, resulting in higher costs for the user

SBB and Lighthouse focus on capturing user-safe MEV (arbitrage and liquidations) through backrunning—placing searcher transactions right after profitable opportunities without affecting users. This approach eliminates harmful practices like frontrunning and sandwich attacks, boosting rollup revenue while creating a fairer, more efficient Ethereum ecosystem.

***

### Getting Started

* **Explore**: [GitHub](https://github.com/radiusxyz)
* **Contact Us**: [Contact Form](https://www.theradius.xyz/contact)

