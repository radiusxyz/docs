# L1 Security

The contract deployed on Ethereum performs several critical functions for the system, including block validation, order validation, registering and deregistering proposers, and distributing rewards to the leader proposer in the case of successful block validation.

1. **Order Validation with Order Commitment**
   * Using the order commitment issued by the leader proposer and the Merkle Proof, users can verify the inclusion and order of their transaction through a smart contract. This is done by computing the Merkle Root, which should match the Merkle Root stored by the leader proposer.
2. **Block Validation**
   * The aggregator verifies block commitments submitted by follower proposers through a smart contract.
3. **Slashing / Reward**
   * In case of failed order validation with an order commitment, the leader proposer can be slashed. Conversely, in the case of successful block validation, the leader proposer can be rewarded.
4. **Proposer Management**
   * When new proposers register or deregister, or when block commitments are submitted to Ethereum, the contract notifies all entities of these events.

This structured approach ensures that all critical functions are managed efficiently, maintaining the integrity and performance of the system.
