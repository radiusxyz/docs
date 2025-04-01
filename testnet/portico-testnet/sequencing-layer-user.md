# Sequencing Layer ↔ User

The shared sequencing layer specializes in assembling blocks of transactions and submitting them to rollups. Its design ensures two key features: liveness, meaning it maintains operation even in the presence of faults (fault-tolerance), and interoperability, allowing it to work seamlessly with various systems.

#### **Importance of zk-Proof** <a href="#importance-of-zk-proof" id="importance-of-zk-proof"></a>

Encrypting the transaction and tying its decryption to a time-lock puzzle primarily **protect users** by ensuring their transactions remain confidential until a predetermined time. This mechanism safeguards against premature decryption and manipulation. The zk-proof validates the solvability of the time-lock puzzle, serving to **protect sequencers**. Without this proof, sequencers have no assurance the puzzle is solvable, risking excessive resource consumption and vulnerability to denial of service (DOS) attacks.

The process by which the shared sequencing layer interacts with user-submitted data involves several critical steps, designed to ensure the security and efficiency of transactions. Here’s a simplified breakdown:

**Processing by the Sequencing Layer**:

1. **Receive User Data**: The sequencing layer receives three key pieces of information from the user: the encrypted transaction, the time-lock puzzle, and the zk-proof.
2. **Validate and Verify zk-proof**: Upon receipt, the sequencing layer verifies the zk-proof. If the proof is validated, the process proceeds.
3. **Retrieve Rollup Information**: Essential details such as rollup information are fetched from the local database.
4. **Determine Transaction Order In The Block**: The order of transactions is determined on a First-Come, First-Served (FCFS) basis.
5. **Sign The Order-Commitment**: The sequencer (leader) signs the order-commitment, which contains details such as block height, transaction order, raw transaction hash, rollup type, using its private key.
6. **Provide Pre-Confirmation to User**: Finally, the sequencing layer sends pre-confirmation (order-commitment) to the user, serving as proof of the transaction's position and integrity within the block.
7. **Offload The Decryption**: To minimize the workload on the leader sequencer, the task of decryption is offloaded to other sequencers. This allows the decryption process to occur independently and concurrently, without impacting the main sequencer's operations.

This structured approach ensures that transactions are processed securely, efficiently, and transparently, balancing the protection of both users and sequencers.

* [send\_encrypted\_tx](code-references.md#send_encrypted_tx)

Currently, transaction ordering is managed on a First Come First Serve (FCFS) basis. This approach is evident in the `add_encrypted_tx` function, where the transaction order is determined by incrementing the current number of transactions in the list. We plan to introduce a Fee Auction mechanism in the future.&#x20;

* [add\_encrypted\_tx](code-references.md#add_encrypted_tx)

For a clearer understanding, take a look at the sequence diagram below.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption><p><em>Sequencing layer - User interaction</em></p></figcaption></figure>
