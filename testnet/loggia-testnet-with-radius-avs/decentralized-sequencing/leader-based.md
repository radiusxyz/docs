# Leader-based

The proposer entities are divided into two categories: leaders and followers. Followers are responsible for routing data to and from the leader and users, as well as synchronizing the state. Meanwhile, the leader takes on more complex tasks such as sequencing transactions into blocks, providing order commitments, signing transactions, and interacting with rollups. This method offers several advantages.

#### 1. Simplified Decision Making <a href="#simpler-decision-making" id="simpler-decision-making"></a>

* **Simplicity:** With a single leader responsible for sequencing, the system simplifies the decision-making process. This centralized approach reduces the complexity and overhead associated with achieving consensus among multiple nodes.
* **Efficiency:** Leader-based systems can implement more efficient ordering and syncing related decisions  since the leader node acts as the authoritative source for sequencing. This streamlines the process of agreeing on the state of the system, as there's no need for multiple nodes to negotiate each sequence.

#### 2. Improved System Performance

* **Reduced Latency:** By centralizing the sequencing tasks, leader-based systems can often reduce communication latency. Messages do not need to traverse multiple nodes to reach a consensus, as the leader directly sequences and processes requests. However, note that the leader manages all processing, meaning its performance directly influences the overall network's functionality.
* **Optimized Throughput:** The leader can optimize sequencing and resource allocation based on the current system load and priorities, potentially improving the overall throughput of the system.

To avoid confusion, the details regarding the leader-follower interaction were not included in the previous sections. This was done to simplify the concept, allowing readers to view the proposer set as a singular entity. However, below is an overview of how leader-follower interactions are handled:

For every RPC request made to any of the followers, the request and its associated data are redirected to the leaders. This redirection mechanism is evident in the proposer's RPC methods:

The leader distributes the data to the followers to maintain a synchronized and updated state across the entire cluster. Generally, synchronization in the sequencing process involves every piece of data being propagated among the follower nodes. Syncing encrypted transactions, time-lockm puzzles, order commitments are carried out.

<figure><img src="../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption><p>Leader's responsibilities</p></figcaption></figure>

The sequence diagram illustrates the actions that are managed by the leader proposer, eliminating the need for consensus:

1. **Verification of zk-proof:** The leader proposer verifies the zk-proof.
2. **Ordering of Encrypted Transactions:** The leader proposer arranges the encrypted transactions for the upcoming block.
3. **Generating an Order Commitment:** The leader proposer creates order commitments for the encrypted transactions.
4. **Signing the Order Commitment:** The leader proposer signs the order commitments.
5. **Decrypting Transactions:**
   * While single-node decryption of all transactions typically introduces overhead with PVDE, the new Single Key Delay Encryption (SKDE) mechanism resolves this issue.
   * SKDE allows decryption of all transactions using a single key obtained from solving a single time-lock puzzle.
6. **Interacting with Rollup for Block Provision:** The leader proposer coordinates with the rollup to provide blocks.
7. **Generating Merkle Proofs:** The leader proposer generates Merkle proofs, which users can use to verify the order and inclusion of their transactions according to the issued order commitment.
