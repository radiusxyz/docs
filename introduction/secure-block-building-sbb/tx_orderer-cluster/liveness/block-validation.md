# Block Validation

#### Block Commitment Verification Process

Since each follower is synchronized with leader's encrypted transactions and respective order commitments, this enables them to build the block similarly to the leader. The following steps outline the block commitment verification _process_:

<figure><img src="../../../../.gitbook/assets/image (15).png" alt=""><figcaption><p>Block Validation Flow</p></figcaption></figure>

1. **Initiating the Build**:
   * Upon receiving the build block request, the leader initiates the build function.
   * The leader propagates the close message to all followers, prompting them to close their blocks and begin building.
2. **Submitting Block to Rollup Operator**:
   * The rollup operator requests a block from the leader.
   * The leader submits the block to the rollup operator.
3. **Generating Block Commitments**:
   * The leader and followers generate a block commitment based on the encrypted transactions and order commitments.
   * This process occurs in parallel across all members of the cluster.
4. **Submitting Block Commitment by Leader**:
   * The leader creates a task and submits its block commitment to ValidationServiceManager contract, triggering an event that followers listen to.
5. **Submitting Block Commitment by Followers**:
   * The followers submit their block commitments as a respond to the same task.
6. **Commitment Validation**:
   * ValidationServiceManager contract aggregates commitments from all members of the cluster.
   * It validates the commitments by comparing them with the leader's block commitment through a smart contract.
   * Rewards are determined based on the validation results.

This process ensures that block commitments are accurately validated.

**Validation Scenarios**

* **Scenario 1: Majority Coincidence**
  * If the majority of the followers' commitments coincide with the leader's commitment, the leader's commitment is considered valid.
  * The leader is rewarded.
* **Scenario 2: Majority Discrepancy**
  * If the majority of the followers' commitments do not coincide with the leader's commitment, the leader's commitment is considered invalid.
  * The leader is not rewarded.

**Assumptions**

* There is no slashing of the tx\_orderer in this flow as of now, regardless of the result of the evaluation of block commitments.
* It is assumed that all members of the cluster, both followers and the leader, are motivated to earn fees and thus will not act maliciously.

This process ensures that the block commitments are verified in a decentralized manner, promoting fairness and accuracy in the blockchain network.
