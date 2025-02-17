# Encrypted Preconfirmations

### **Introduction**

Users are entities that submit transactions to the proposer, aiming to safeguard themselves against malicious proposers.

In the context of preventing malicious Miner Extractable Value (MEV) actions, users interact with the proposer through a sequence of steps designed to ensure transaction integrity and order. This process involves encryption techniques to protect transactions from being censored or reordered maliciously. Radius uses a cryptographic method called [Practical Verifiable Delay Encryption (PVDE)](https://ethresear.ch/t/mev-resistant-zk-rollups-with-practical-vde-pvde/12677), which relies on a time-lock puzzle to conceal transaction details until a predetermined time is reached.

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>User's actions before receiving order commitment</p></figcaption></figure>

### **Receiving The Order Commitment**

1. **Generate transaction**: Users initiate the process by generating a transaction intended for submission to the proposer.
2. **Generate symmetric encryption key**: Utilizing the time-lock puzzle, a symmetric encryption key is generated. This key is specifically designed to encrypt the transaction and ensure its security until the appropriate time for decryption.
3. **Encrypt transaction**: With the symmetric key, the user encrypts the transaction. This encryption step is critical for protecting the transaction from premature exposure or manipulation.
4. **Generate zk-SNARK Proof**: To ensure that decryption is achievable and to avoid wasting proposer's resources, the user generates a zero-knowledge succinct non-interactive argument of knowledge (zk-SNARK) proof. This proof verifies the integrity of both the time-lock puzzle and the encrypted transaction, ensuring that the transaction has not been tampered with. The proposers can independently decrypt the transaction by successfully solving the time-lock puzzle.
5. **Send Encrypted Transaction:** The user sends the encrypted transaction to the proposer, awaiting the arrival of the order before the decryption time elapses.
6. **Receive Order Commitment**: Prior to decryption, users receive an order-commitment. This commitment assures the user that their transaction's order has been preserved and will not be altered.
7. _**Optional: Send Decryption Key**_**:** The user sends the decryption key to the proposer immediately upon receiving the order commitment, aiming to reduce fees.
8. _**Request and receive cryptographic proof of inclusion**_**:** The user requests the Merkle Proof needed for verification of inclusion and order from the proposer.
9. _**Verify inclusion and the order of transaction**_**:** The user verifies the inclusion and order of the transaction through the contract.

Once the time-lock puzzle and its corresponding zk-proof are prepared, and the transaction is encrypted, the user sends these components to the proposer. It's important to highlight that encrypting the transaction is not mandatory; users have the flexibility to submit transactions directly to the proposer in their original, unencrypted form. However, choosing to submit a transaction without encryption means that the system cannot ensure protection against Miner Extractable Value (MEV) risks. This optionality allows users to balance their need for security against MEV with their preferences for transaction processing.

#### Order Commitment <a href="#pre-confirmation" id="pre-confirmation"></a>

If a user receives the order-commitment before a specified time $$t$$ has elapsed, it confirms that the proposer has sequenced the transaction without decrypting it. This is due to the encryption mechanism that makes it impossible to decrypt the transaction before time $$t$$. In case the proposer attempts to reorder transactions after providing the user with this order commitment, the user has a basis to challenge such actions. The order commitment includes critical details such as the exact promised order of the transaction within the block, the partial Merkle Proof, the rollup block number, and the proposer's signature. These elements serve as evidence of the original commitment made by the proposer. How exactly the verification of the order works, will be explained in the **Claim** section.

It's important to note that users have the option to reduce transaction fees by sending the decryption key to the proposer immediately after receiving the order commitment. This action relieves the proposer of the computational resources and time needed to solve the time-lock puzzle, making the process more efficient.

### Processing of the encrypted transaction by the Proposer

#### **Importance of zk-Proof** <a href="#importance-of-zk-proof" id="importance-of-zk-proof"></a>

Encrypting the transaction and tying its decryption to a time-lock puzzle primarily **protect users** by ensuring their transactions remain confidential until a predetermined time. This mechanism safeguards against premature decryption and manipulation. The zk-proof validates the solvability of the time-lock puzzle, serving to **protect proposers**. Without this proof, proposers have no assurance the puzzle is solvable, risking excessive resource consumption and vulnerability to denial of service (DOS) attacks.

The process by which the proposer interacts with user-submitted data involves several critical steps, designed to ensure the security and efficiency of transactions. Here’s a simplified breakdown:

**Processing by the Proposer**:

1. **Receive User Data**: The proposer receives three key pieces of information from the user: the encrypted transaction, the time-lock puzzle, and the zk-proof.
2. **Validate and Verify zk-proof**: Upon receipt, the proposer verifies the zk-proof. If the proof is validated, the process proceeds.
3. **Determine Transaction Order In The Block**: The order of transactions is determined on a First-Come, First-Served (FCFS) basis.
4. **Sign The Order-Commitment**: The proposer (leader) signs the order-commitment, which contains details such as block height, transaction order, raw transaction hash, rollup type, using its private key.
5. **Provide Order Commitment to User**: Finally, the proposer sends order-commitment to the user, serving as proof of the transaction's position and integrity within the block.
6. **Solve Time-Lock Puzzle:** The leader proposer solves the time-lock puzzle to retrieve the decryption key.
7. **Decrypt The Encrypted Transaction:** The proposer decrypts the transaction using the key obtained during the previous step.
8. **Provide Block to Rollup:** The leader proposer set provides the block to the rollup operator upon request.
9. **Generate Merkle Root:** The leader proposer generates the Merkle root, which serves as the block commitment and plays a crucial role in block validation.
10. **Store the Merkle Root on L1:** The Merkle root is stored on Ethereum for trustless verification.

This structured approach ensures that transactions are processed securely, efficiently, and transparently, balancing the protection of both users and proposers.

Currently, transaction ordering is managed on a First Come First Serve (FCFS) basis. We are planning to introduce a Fee Auction mechanism in the future.&#x20;

For a clearer understanding, take a look at the sequence diagram below.

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>Proposer Actions</p></figcaption></figure>

### Order Verification

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>Order Verification with Order Commitment</p></figcaption></figure>

#### Purpose and Structure of the Order Commitment

Each component of the order commitment serves a specific purpose:

1. **Signature**
   * Ensures that the order commitment was authentically issued by the leader proposer.
2. **Block Number**
   * Indicates the rollup block associated with the given transaction.
3. **Order**
   * Denotes the committed index of the transaction in the upcoming block as determined by the proposer.
4.  **Partial Merkle Proof**

    * **Purpose**: Even though the promised index (order) of a transaction cannot be taken by any other transaction, the user lacks information about the transactions in the preceding indexes. This gap allows the proposer to potentially leave those indexes blank and insert its own transactions after decrypting the user's transaction. Such a violation would go unnoticed since the order of the user's transaction itself remains unviolated.
    * **Solution**: To prevent this, the user must be provided with a commitment that includes information about the previous indexes. An unviolated block can be visualized as a Merkle Tree of transactions growing in one direction (assume to the right). The Merkle Proof for any given transaction in the subtree containing all previous transactions (to the left) will remain unchanged regardless of how large the tree grows by adding leaves to the right side.
    * **Consistency**: Even though the final Merkle Proof for the given transaction will differ in the final tree, the earlier partial Merkle Proof will consist of elements that form the initial parts of the final Merkle Tree. This ensures the integrity of the transaction order and prevents the proposer from inserting unauthorized transactions.

    <figure><img src="../../.gitbook/assets/image (19) (1).png" alt=""><figcaption><p>Partial Merkle Proof vs Final Merkle Proof</p></figcaption></figure>

#### Finalization and Verification Process

Once the block is finalized, the user requests the final Merkle Proof with the leader proposer's signature and invokes the verify function in the smart contract. This function performs the following checks:

1. **Blank Space Verification**:
   * Ensures there are no blank spaces filled after the order commitment by comparing the partial Merkle Proof with the final Merkle Proof.
2. **Order Verification**:
   * Confirms the order of the transaction by checking if the Merkle Root computed from the Merkle Proof matches the Merkle Root stored on L1 by the leader proposer.

### Complete Sequence Diagram

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Transaction Lifecycle</p></figcaption></figure>

