# Leader Selection

## Leader selection <a href="#leader-election" id="leader-election"></a>

Dynamic leader selection is a crucial part of the current product to ensure the fair distribution of reward and ensure the liveness of the tx\_orderer set. Unlike the RAFT algorithm, which involves voting based leader election process, in the Eigenlayer Testnet we introduce the new algorithmic method of leader selection.

## Algorithm

**Arguments**

* **L1 Block Number**: Provides access to the instance of the tx\_orderer list stored on Ethereum for a given block number.
* **Rollup Block Number**: The number of the rollup's next block.

**Method**

1. Access the tx\_orderer list using the L1 block number.
2. Compute the index:

$$
\text{index} = (\text{rollup block number})\bmod(\text{number of elements in the tx_orderer list})
$$

3. Determine the leader as the _**index**_-th element of the cluster.

## Corner Cases

* The rollup will provide the necessary arguments to the leader responsible for building the current block. However, if the leader tx\_orderer is unresponsive, the rollup will send the same request to any of the followers. The leader for the next block will be determined in the usual manner. For the current block, the follower contacted by the rollup will assume the [role of the leader](../../../../testnet/loggia-testnet-with-radius-avs/decentralized-sequencing/leader-based.md#id-2.-improved-system-performance).
* Tx\_orderers must verify that the L1 block number provided by the rollup falls within a predefined block margin. This ensures that the rollup adheres to the fair leader change mechanism (round robin) and prevents the rollup from using an L1 block number that would result in the same index as the previous block.

## Benefits

* **Encourages Participation**: Ensures that every member of cluster has an equal opportunity to become a leader and earn rewards, motivating more participants to opt in.
* **Promotes Decentralization**: Enhances decentralized sequencing even with a leader-based system. Although a single entity orders transactions for each block, the frequent rotation of leaders reduces centralization.
* **Ensures Consistent Leader Selection**: Eliminates the need for voting or trust among nodes. Since the contract block number and rollup block number are shared with all nodes, the calculation of the next leader will consistently produce the same result for everyone.

