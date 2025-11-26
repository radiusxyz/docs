# Lighthouse Auctions

Lighthouse runs on a hybrid architecture that combines **off-chain execution** (a dedicated server runs real-time auctions and processes data) with **on-chain settlement** (smart contracts manage deposits/withdrawals and final auction settlement), balancing performance with security. \[Figure 2]

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption><p><strong>Figure 2. Interaction Overview</strong> – Shows how the rollup, Lighthouse, SBB, and searchers interact.</p></figcaption></figure>

***

### **Lighthouse Auction Process**

1. **Deposit**: Searchers deposit tokens into the Lighthouse auction contract to collateralize bids, ensuring settlement integrity.
2. **Slot Transition & Real-time Auctions (Concurrent):**
   * **2-1. Create Auction (Slot N+1):** The rollup requests an auction for the next slot; Lighthouse notifies all searchers participating in the rollup’s auction.
   * **2-2. Deliver Bundles (Slot N)**: Confirmed winning bundles from the previous Lighthouse auction are submitted to the rollup.
   * **2-3. Fetch Transactions (Slot N)**: The rollup retrieves the list of user transactions from SBB.
   * **2-4. Broadcast Transactions:** The rollup merges Lighthouse bundles with SBB transactions and broadcasts the complete list to searchers participating in the auction, enabling backrunning opportunities for the next auction.
   * **2-5. Include in Mempool (Slot N):** Transactions for Slot N are added to the mempool and executed in the defined order.
3. **Simulate Transactions (Private Node):** Searchers simulate MEV opportunities on private full nodes using the latest transaction order flow.
4. **Submit Bids:** Searchers submit MEV bundles and a `BidMsg`, which includes:&#x20;
   * `BidPrice`, `AuctionNonce`, `bidderAddress`, `mevTxHashes`, and `Signature`.
   * Each signature is verified against the bidder’s private key to prevent unauthorized withdrawals.
5. **Auction Close & Settlement** **(Concurrent):**
   * **5-1. Order Bundles**: After the auction closes, bundles are sorted by descending bid price.
   * **5-2. Simulate Bundles:** Bundles are simulated in sequence; only valid bundles are confirmed and forwarded to the rollup for Slot N+1 (Step 2-2).
   * **5-3. Submit Auction Closed Msg**: The Lighthouse contract executes settlement and closes the auction.&#x20;

***

{% hint style="info" %}
### **Transaction Handling for SBB and Lighthouse**

* **Standalone SBB**: Manages both FCFS user transaction ordering and local searcher bundles, optimized for value capture within a single rollup.
* **SBB + Lighthouse**: SBB manages user transactions, while Lighthouse coordinates cross-market auctions, expanding arbitrage opportunities and supporting more advanced trading strategies across connected venues.
{% endhint %}



