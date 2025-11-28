# Slot-Ordering

Lighthouse uses a **slot-based transaction ordering mechanism.**

A slot is a unit of transactions, comprising searcher bundles (from Lighthouse) and user transactions (from SBB). Slot ordering is run independently of fixed block times, managing the ordering of transactions within each slot.

Once slots are submitted to the mempool and included in a block, they are executed in a _predetermined order_ defined by the slot. This model guarantees deterministic outcomes and eliminates risks of arbitrary reordering.

***

### **Slot Structure**

Each slot is divided into two segments to ensure value capture and user protection coexist:

1. **Top-of-Slot (Priority Txs):** Arbitrage bundles from searchers via Lighthouse auctions. These transactions backrun the previous slots (user transactions) to capture market opportunities.
2. **Bottom-of-Slot (User Txs):** User transactions from SBB, which are protected from exploitation (e.g., frontrunning or sandwich attacks).

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p><strong>Figure 1. Slot Structure</strong> – Each slot comprises Lighthouse (searcher bundles) and SBB (user transactions), operating independently of block times.</p></figcaption></figure>

***

### **Why slots, not blocks?**

Slot ordering solves key execution and latency limitations of standard block-based ordering:

* **Network Congestion**: Fixed block intervals risk hitting gas or size limits during transaction surges, potentially preventing committed transaction orders from being included.&#x20;
* **Communication Delays**: Mitigates issues caused by latency between the rollup and external systems (e.g., SBB or Lighthouse) that disrupt timely block production.
* **External Failures**: Prevents external system failures from cascading into the rollup's core transaction pipeline, ensuring predictable block production.



