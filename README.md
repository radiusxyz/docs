---
description: 'Learn about Secure Block Building (SBB) and Lighthouse: Tools for L2 Revenue'
---

# Introduction

Radius introduces a new approach to strengthen the rollup economy by unlocking MEV as a new revenue source. While rollups are critical for Ethereum's growth, their reliance on user fees introduces economic uncertainty, limiting their scalability. These fees fluctuate with network demand, leading to unpredictable revenue and constrained growth.

***

### What We Do

**Secure Block Building (SBB)** and **Lighthouse** are solutions that ensure the economic viability of L2s while managing the complexities of MEV. By turning MEV from a potential drawback (e.g. frontrunning that harms users) into a safe revenue source, these tools incentivize rollup adoption and development, ultimately benefitting the Ethereum ecosystem.

SBB collaborates with searchers to capture MEV for L2s, while Lighthouse establishes a decentralized network that connects rollups and searchers to capture broader MEV opportunities across networks. Together, they unlock otherwise inaccessible MEV, delivering scalable revenue and fostering a unified, economically aligned Ethereum ecosystem.



**Secure Block Building (SBB)**

A rollup-integrated solution with MEV capture capabilities for L2s enabled through searcher collaborations, unlocking new revenue for rollups.

→ [SBB Overview](overview/secure-block-building-sbb.md)



**Lighthouse**

A decentralized network that maximizes MEV revenue opportunities by connecting multiple L2s and searchers, enabling the execution of cross-rollup strategies.

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

