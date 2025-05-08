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

**Maximal Extractable Value (MEV)** is the profit that can be made (usually by a block builder or validator) by reordering, including, or excluding transactions. MEV strategies generally fall into two broad categories based on their impact:



**Good MEV**

*   **Arbitrage**: Capturing price differences across markets. For example, between AMM pools on the same rollup, or across multiple L2s, or between L2s and L1.

    _Why it’s beneficial_: Arbitrage helps align prices across the ecosystem, reduces inefficiencies, and stabilizes market for traders.
*   **Liquidations**: Closing out of undercollateralized positions in lending protocols, often triggered by price changes or accrued interest.

    _Why it’s beneficial_: Liquidations protect lenders and keep protocols solvent, while offering incentives to actors who help enforce risk thresholds.



**Bad MEV**

*   **Frontrunning**: Placing a transaction ahead of known trade to profit from its price impact.

    _Why it’s harmful_: It increases slippage for users and creates an uneven playing field by exploiting the visibility of a transaction.
*   **Sandwich Attacks**: Placing a trade before and after a user’s transaction to profit.

    _Why it’s harmful_: Sandwiching extracts value directly from users by distorting market prices around their trades.



As L2 ecosystems grow, **managing MEV** and **designing aligned incentives** will be critical to keeping the economy healthy. That means:

* Encouraging good MEV like arbitrage and liquidations
* Preventing harmful MEV like frontrunning or sandwiching

***

### Getting Started

* **Explore**: [GitHub](https://github.com/radiusxyz)
* **Contact Us**: [Contact Form](https://www.theradius.xyz/contact)

