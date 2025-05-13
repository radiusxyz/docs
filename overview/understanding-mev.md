# Understanding MEV

**Maximal Extractable Value (MEV)** refers to the profit earned by including, reordering, or excluding transactions in a blockchain, typically by actors such as sequencers, block builders, or validators.&#x20;

MEV strategies leverage transaction ordering to capture value. This section categorizes MEV into Good MEV and Bad MEV based on their effects on L2 ecosystems.

***

### Good MEV

Good MEV encompasses strategies that enhance market efficiency, stabilize protocols, and incentivize beneficial behavior in L2 ecosystems. These activities align prices and promote a healthy blockchain environment.

#### **Arbitrage**

* Arbitrage involves capitalizing on price differences for an asset across different markets, such as: DEXs on the same rollup, DEXs across multiple L2s, L2s and L1 networks, or CEXs and DEXs.
* _Benefits_: Arbitrage reduces inefficiencies by aligning prices across and stabilizes markets across the ecosystem.

#### **Liquidations**&#x20;

* Liquidations involve closing undercollateralized positions in lending protocols, often due to price changes or accrued interest reducing a borrower’s collateral value below a protocol-defined threshold.
* _Benefits_: Liquidations protect lenders by ensuring loan repayment, maintains protocol solvency and stability, and Incentivizes liquidators to monitor and manage systemic risks.

***

### Bad MEV

Bad MEV refers to strategies that harm users, distort markets, or create unfair advantages through transaction ordering. These activities undermine fairness and trust in L2 ecosystems, particularly when transaction ordering is influenced by centralized sequencers.

#### Frontrunning

* Frontrunning involves placing a transaction ahead of a known trade to profit from its price impact
* _Drawbacks_: Frontrunning increases slippage for the original user, leading to worse execution prices. This creates an unfair advantage for actors with access to transaction data or faster transaction submission.

#### Sandwich Attacks

* Sandwich attacks involve placing two transactions, one before and one after, a user’s transaction to profit from the price movement it induces.
* _Drawbacks_: Sandwich attacks artificially inflates or deflates prices, costing users more. This undermines fairness and transparency in transaction ordering.

***

### Backrunning: A Good MEV Strategy

**Backrunning** involves submitting a transaction immediately after another to profit from a market event (e.g. a large trade).  A common example is backrunning arbitrage, which capitalize on the resulting state change without affecting the original transaction. This enhances market efficiency by correcting imbalances (e.g., rebalancing DEX pools after a large trade).

However, backrunning isn’t limited to arbitrage. It can also involve speculative strategies. For example, a large trade swaps ETH for USDC on Uniswap, causing ETH’s price to drop temporarily. A backrunner places a transaction immediately after to buy ETH at the lower price, anticipating a recovery. If ETH’s price stabilizes, the backrunner can sell for a profit. Unlike arbitrage, this strategy carries risk since the price may not recover, but it still leverages the price impact of the initial trade.

***

**Radius** optimizes MEV strategies by promoting good MEV strategies like arbitrage, liquidations, and backrunning, and mitigates bad MEV like frontrunning and sandwich attacks to foster efficient, fair, and stable L2 ecosystems.

