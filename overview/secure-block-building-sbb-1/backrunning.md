# Backrunning

### Increasing Rollup Revenue with Radius’ Backrunning Feature

Radius provides a Backrunning feature to enhance rollup profitability. This feature ensures that user transactions maintain their order-commitment sequence while also sharing block information with MEV searchers.

#### How it works:

1. User transactions are ordered according to the order-commitment principle.
2. Block information is shared with the MEV searcher.
3. 3\. The MEV searcher analyzes the rollup state and transactions within the block to identify arbitrage opportunities.
4. The identified opportunities are then provided to the tx\_orderer (send MEV\_tx).
5. The tx\_orderer then creates a block based on the transaction it received from the user and the MEV\_tx it received from the mev searcher and propagates it to the rollup.

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

This process protects user transactions while enabling the rollup to generate additional revenue. To facilitate this, Radius’ tx\_orderer provides a dedicated API for communication with MEV searchers.
