# Slot-Based Transaction Ordering

### Understanding Slot-Based Transaction Ordering

Radius introduces a slot-based transaction ordering model in Lighthouse.

A **slot** is a unit of transactions, comprising searcher bundles (from Lighthouse) and user transactions (from SBB). Slot-based ordering runs independently of block times, managing the ordering of transactions within each slot.

Once slots are submitted to the mempool and included in a block, they are executed in a _predetermined order_ defined by the slot. This model guarantees deterministic outcomes and eliminates risks of arbitrary reordering.

***

### **Slot Structure**

Each slot is divided into two segments:

1. **Top-of-Slot (Priority Txs):** Arbitrage bundles from searchers via Lighthouse auctions. These transactions backrun previous slots and capture market opportunities.
2. **Bottom-of-Slot (User Txs):** User transactions via SBB, protected from manipulation such as frontrunning or sandwich attacks.

This two-tier structure ensures value-capturing arbitrage and user activity coexist under fair, transparent rules.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p><strong>Figure 1. Slot Structure</strong> – Each slot comprises Lighthouse (searcher bundles) and SBB (user transactions), operating independently of block times.</p></figcaption></figure>

***

### **Why slots, not blocks?**

Slot ordering guarantees deterministic execution. It solves key limitations of block-based ordering:

* **Network Congestion**: Fixed block intervals risk hitting gas or size limits during transaction surges, preventing committed transaction orders from being included in the block.
* **Communication Delays**: Latency between rollups and external systems (e.g., SBB or Lighthouse) disrupts timely block production.
* **External Failures**: Failures in external systems (such as SBB or Lighthouse) can cascade into the transaction pipeline, impacting how the rollup processes transactions.

***

### **Transaction Handling for SBB and Lighthouse**

* **Standalone SBB**: Coordinates both user transaction ordering and searcher bundles, optimized for local value capture.
* **SBB + Lighthouse**: SBB manages user transactions, while Lighthouse coordinates cross-market auctions. This expands arbitrage opportunities and supports more advanced trading strategies across interconnected venues.



