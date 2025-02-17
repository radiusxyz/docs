# Block Validation

#### Block Commitment Verification Process

In this process, each follower proposer is synchronized with the encrypted transactions and their respective order commitments. This synchronization allows each proposer to build the block similarly to the leader. The following steps outline the block commitment verification process:

#### Block Commitment Verification Process Documentation

Since each follower proposer is synchronized with leader proposer's encrypted transactions and respective order commitments, this enables them to build the block similarly to the leader. The following steps outline the block commitment verification process:

1. **Initiating the Build**:
   * Upon receiving the build block request, the leader proposer initiates the build function.
   * The leader proposer propagates the close message to all follower proposers, prompting them to close their blocks and begin building.
2. **Submitting Block to Rollup**:
   * The rollup requests a block from the leader proposer.
   * The leader proposer submits the block to the rollup.
3. **Generating Block Commitments**:
   * The leader proposer and follower proposers generate a block commitment based on the encrypted transactions and order commitments.
   * This process occurs in parallel across all proposers.
4. **Submitting Block Commitment by Leader**:
   * The leader proposer submits its block commitment to Ethereum, triggering an event that follower proposers listen to.
5. **Submitting Block Commitment by Followers**:
   * The follower proposers submit their block commitments to an off-chain or on-chain solution designed to aggregate these commitments.
   * In the Eigenlayer Testnet implementation, this entity is referred to as the Aggregator.
6. **Commitment Aggregation and Validation**:
   * The solution aggregates commitments from all proposers.
   * It validates the commitments by comparing them with the leader's block commitment through a smart contract.
   * Rewards are determined based on the validation results.

This process ensures that block commitments are accurately validated.

<figure><img src="../../../../.gitbook/assets/image (7) (1).png" alt=""><figcaption><p>Block Validation</p></figcaption></figure>

**Validation Scenarios**

* **Scenario 1: Majority Coincidence**
  * If the majority of the proposers' commitments coincide with the leader's commitment, the leader's commitment is considered valid.
  * The leader proposer is rewarded.
* **Scenario 2: Majority Discrepancy**
  * If the majority of the proposers' commitments do not coincide with the leader's commitment, the leader's commitment is considered invalid.
  * The leader proposer is not rewarded.

**Assumptions**

* There is no slashing of the proposer in this flow, regardless of the result of the evaluation of block commitments.
* It is assumed that all proposers, both followers and the leader, are motivated to earn fees and thus will not act maliciously.

This process ensures that the block commitments are verified in a decentralized manner, promoting fairness and accuracy in the blockchain network.
