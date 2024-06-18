# Sequencing Liveness

### What is Sequencing Liveness?

Sequencing liveness involves the continuous processing of transactions and block production within rollups, guaranteeing uninterrupted sequencing of transactions even in the face of potential rollup disruptions or failures. This is crucial for a seamless user experience and fostering trust in rollups while preventing any transaction delays.

Before delving into how Radius ensures sequencing liveness, let's examine two key approaches it employs:

* [**Leader-Based Sequencing**](../../developer/distributed-sequencing/leader-based.md): Radius adopts a leader-based sequencing approach enabled by the encrypted mempool. A designated sequencer node (known as the leader) takes the lead in block sequencing. Other sequencer nodes (followers) receive the sequenced block from the leader. This design choice significantly enhances block production efficiency without exposing the network to censorship or sandwich attacks_._
* [**Pre-Confirmation Mechanism**](../../developer/encrypted-mempool.md#pre-confirmation): The leader provides order commitment (pre-confirmations) of ordered transactions to the users before decrypting the transactions. This step prevents manipulative behavior and mitigates centralization risks_._

### Sequencing Liveness Failure Scenarios

Two potential scenarios of sequencing liveness failures can disrupt rollup operation:

* [**Failure due to malicious users**](../../developer/sequencing-layer-user.md#importance-of-zk-proof): Delays in the sequencer providing the block to the rollup operator may occur due to potential attacks by malicious users. Practical Verifiable Delay Encryption (PVDE) enables users to generate proofs for the decryption key, helping the sequencer in identifying transactions that might lead to decryption failures. _Refer to_ [_Curie Testnet_](https://docs.theradius.xyz/testnet/curie-testnet)
* **Leader Failure**: Leader failure can result in interruptions during the block sequencing process

### RAFT Algorithm for Sequencing Liveness During Leader Failure

To ensure sequencing liveness during leader failure, Radius employs the RAFT algorithm for leader recovery where a new leader is elected from among the followers. This algorithm is effective for leader-based sequencing, ensuring high availability, consistency, and fault tolerance in leader election, log replication, and security.

The shared sequencing layer involves a designated leader determining the order and broadcasting transactions to the followers. The RAFT algorithm, based on the Crash Fault Tolerance (CFT) consensus algorithm, enhances broadcasting efficiency and minimizes communication overhead compared to the Byzantine Fault Tolerance (BFT) algorithm.

A modification to the RAFT algorithm ensures data consistency among followers during leader election. In the original RAFT model, followers lacked an identical view of the data. However, in our modified version, the candidate requesting votes to become a new leader must have data identical to the majority of followers. This modification ensures the block inclusion of pre-confirmations determined by a failed leader.

### [**Leader election within the RAFT Algorithm:**](../../developer/distributed-sequencing/fault-tolerant.md#leader-election)

1. **Initial:** All nodes begin as followers.
2. **Timeout:** If a follower doesn’t receive a message from a leader or candidate during the election timeout, it transitions to a candidate state, initiating a new round.
3. **Voting Request:** The candidate sends a vote request to all nodes, including a vote for itself and its data.
4. **(Modified) Voting Process:** Nodes vote for the candidate only if their data matches the candidate's data.
5. **Leader Election:** The candidate with the majority of votes becomes the leader.

### **Sequencing Liveness in Portico Testnet**

Explore a demonstration of [Sequencing Liveness on the Portico Testnet](https://portico.theradius.xyz/sequencing-liveness).

* _Please note that the speed of interactions in the testnet has been adjusted for demonstration purposes and does not reflect the actual speed of sequencing events_
* _To view all sequencing events in real-time, refer to the_ [_real-time log_](https://portico-logs.theradius.xyz/)_, which is synchronized with the visualization on the testnet_

The transaction ordering process within the shared sequencing layer involves four components: User, Leader (Sequencer), Follower (Sequencer), and Rollup.

For sequencing liveness, the leader ensures that the majority of followers receive the order commitment (pre-confirmation) before it is sent to the user. For example, with a total of 10 followers, the leader ensures at least 6 followers receive the order commitment before sending it to the user.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

### Potential Scenarios in the Shared Sequencer Network

The following scenarios illustrate the diverse interactions within the shared sequencer network.

#### Scenario 1: User Receives Order Commitment from Leader

<figure><img src="../../.gitbook/assets/01.gif" alt=""><figcaption></figcaption></figure>

1. User submits encrypted transactions to the leader.
2. Leader orders transactions in an encrypted state.
3. Leader provides order commitment (pre-confirmation) to followers before sending it to the user.
4. Rollup operator receives the transaction list (block) from the leader.

**Scenario 2: Majority of Followers Receive Order Commitment Before User**

<figure><img src="../../.gitbook/assets/02.gif" alt=""><figcaption></figcaption></figure>

1. User submits encrypted transactions to an initial follower.
2. Initial follower forwards encrypted transactions to the leader.
3. Leader orders transactions in an encrypted state.
4. Leader provides order commitment to the majority of followers before sending it to the initial follower. _Example: In a set of 5 sequencers, the leader ensures order commitment to at least 3 followers before reaching the user (including itself, initial follower, and another follower)._
5. Initial follower forwards the order commitment to the user.
6. Rollup operator receives the block from the leader.

#### **Scenario 3: Leader Failure**

<figure><img src="../../.gitbook/assets/03.gif" alt=""><figcaption></figcaption></figure>

1. In case of leader failure, a new leader is elected among follower nodes.
2. Rollup receives the transaction list (block) from the newly elected leader.

### **Leader Election**

In the event of a leader's failure, candidates receive votes based on their latest status ([see more](../../developer/distributed-sequencing/fault-tolerant.md#leader-election)). The eligible candidate securing the majority of votes becomes the newly elected leader. Once elected, the new leader synchronizes data with all followers, ensuring identical order commitment data across the network.

### **Vote Eligibility**

Nodes cast votes for a candidate only if the candidate's data matches theirs. This ensures the newly elected leader possesses identical order commitment data with the majority of followers to guarantee sequencing liveness for the rollup in the event of leader failure.

