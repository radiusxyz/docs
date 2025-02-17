# Secure Block Building (SBB)

The **Secure Block Builder (SBB)** by Radius is designed to **ensure liveness for rollups** while leveraging the **security of restaking protocols**. It consists of several key components that work together to maintain network integrity and secure transaction processing.

#### **Secure Block Builder (SBB) by Radius**

The **Secure Block Builder (SBB)** is Radius's solution for ensuring **liveness for rollups** while leveraging the **security of restaking protocols**. It consists of several key components that work together to provide efficient block production and secure transaction handling.

* **Seeder**
  * The **Seeder** manages the **IP addresses of tx\_orderers and rollups**. It verifies nodes by referencing blockchain smart contract data and stores the **IP addresses** of verified nodes, ensuring seamless communication within the network.
* **Secure RPC**&#x20;
  * The **Secure RPC** is designed to **protect sensitive transaction data** within a blockchain or rollup environment. Its primary goal is to ensure that transactions are encrypted after leaving the client environment, preserving data integrity and security throughout the broadcasting process.&#x20;
* **Distributed Key Generation Service (DKG)**
  * The **DKG service** is a crucial component of Radius's **SKDE encryption method**. Each node generates a **partial key**, which is then combined to create an **aggregated encryption key**. A **delay function** is applied to generate the **decryption key**.
  * **Users receive an encryption key** from DKG to encrypt transactions.
  * **Tx\_orderers obtain a decryption key** to decrypt the encrypted transactions.
*   **Liveness Service Manager Contract (`LivenessServiceManager.sol`)**

    <figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption><p>Relationship between LivenessServiceManager related entities</p></figcaption></figure>

    * The **LivenessServiceManager contract** ensures **tx\_orderer availability**. It helps rollups and tx\_orderer sets **determine the leader tx\_orderer**, allowing for **block creation and transaction ordering**. Within the above structure, a **cluster** consists of both a **tx\_orderer set** and a **rollup set.** The **tx\_orderer set** manages all registered rollups within the cluster. Each **rollup stores the addresses of executors**, responsible for its operation, and is registered with specific enabled features provided by Radius.
      * **Additional Rollup Configurations:**
        * **`rollupType`**:  **rollupType:** Specifies the rollup framework responsible for executing transactions and updating the rollup's state. It processes transactions in the order provided by the **tx\_orderer**. Supported options include **`polygon_cdk`** and **op\_stack.**
          * **`encryptedTransactionType`**: Specifies the encryption method used for transactions. Options include **PVDE** and **SKDE**, provided by Radius. If `none` is selected, transactions will not be encrypted.
          * **`ValidationInfo`**: Contains **protocol details for re-staking**, specifying:
            * **`platform`**: The blockchain where the validation contract is deployed.
            * **`serviceProvider`**: The specific re-staking service used (**EigenLayer or Symbiotic**).
* **Validation Service Manager Contract (`ValidationServiceManager.sol`)**
  * The **ValidationServiceManager contract** integrates with **restaking protocols** like **Symbiotic**. It facilitates **tx\_orderer validation and reward distribution** through the following process:
    1. The **leader tx\_orderer** submits **block commitment information** by creating a task using `createTask`.
    2. **Follower tx\_orderers** participate in validation by responding to the task with `respondToTask`.
    3. Once validation is complete, the contract **allocates rewards or applies slashing** based on operator performance.

These components work together to provide a **decentralized, secure, and restaking-enabled rollup infrastructure**.
