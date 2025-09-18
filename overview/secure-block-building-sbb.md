# Secure Block Building (SBB)

**Secure Block Building (SBB)** is a high-efficiency transaction ordering framework that optimizes block production for stronger economic outcomes. SBB helps rollups capture new revenue sources through orderly execution while mitigating risks like arbitrary reordering and exploitative tactics. This improves market efficiency, strengthens operational transparency, and aligns incentives across participants.

***

### **Why Use SBB?**

SBB provides three key benefits:

* **More Revenue**: Works with searchers to capture MEV, creating a flexible revenue stream that scales with rollup adoption and adapts to market conditions—beyond just transaction fees.
* **User Safety**: Stops harmful MEV practices like frontrunning and sandwich attacks through one-second encryption and proof generation. This keeps user transactions secure while enabling rollups to profit from MEV.
* **Easy Integration**: Fits into existing rollup frameworks without added complexity, providing a straightforward path to increased revenue.

***

### How It Works

SBB integrates into rollups as a plug-in with two main features:

* **Arbitrage Support**: Searchers spot arbitrage opportunities and submit bundles to SBB blockspace. This also includes CEX-DEX trades and liquidations, which generate additional revenue for the rollup.
* **Encrypted Mempool**: User transactions are encrypted and sent to SBB user blockspace, This protects them from manipulation while ensuring inclusion through preconfirmations.

***

> #### **Transaction Handling for SBB and Lighthouse**
>
> **Standalone SBB**: Coordinates both user transaction ordering and searcher bundles, optimized for local value capture.
>
> **SBB + Lighthouse**: SBB manages user transactions, while Lighthouse coordinates cross-market auctions. This expands arbitrage opportunities and supports more advanced trading strategies across interconnected venues.

