---
hidden: true
---

# Internal Secure Block Building (SBB)

The **Secure Block Builder (SBB)** by Radius is designed to **ensure liveness for rollups** while leveraging the **security of restaking protocols**. It consists of several key components that work together to maintain network integrity and secure transaction processing.

#### **Secure Block Builder (SBB) by Radius**

The **Secure Block Builder (SBB)** is Radius's solution for ensuring **liveness for rollups** while leveraging the **security of restaking protocols**. It consists of several key components that work together to provide efficient block production and secure transaction handling.

* **Seeder**
  * The **Seeder** manages the **IP addresses of tx. orderers and rollups**. It verifies nodes by referencing blockchain smart contract data and stores the **IP addresses** of verified nodes, ensuring seamless communication within the network.
* **Secure RPC**&#x20;
  * The **Secure RPC framework** is designed to **protect sensitive transaction data** within a blockchain or rollup environment. Its primary goal is to ensure that transactions are encrypted after leaving the client environment, preserving data integrity and security throughout the broadcasting process.&#x20;
* **Distributed Key Generation Service (DKG)**
  * The **DKG service** is a crucial component of Radius's **SKDE encryption method**. Each node generates a **partial key**, which is then combined to create an **aggregated encryption key**. A **delay function** is applied to generate the **decryption key**.
  * **Users receive an encryption key** from DKG to encrypt transactions.
  * **Tx. orderers obtain a decryption key** to process and execute transactions securely.
*   **Liveness Service Manager Contract (`LivenessServiceManager.sol`)**

    <figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption><p>Relationship between LivenessServiceManager related entities</p></figcaption></figure>

    * The **LivenessServiceManager contract** ensures **tx. orderer availability**. It helps rollups and tx. orderer sets **determine the leader tx. orderer**, allowing for **block creation and transaction ordering**. Within the above structure, a **cluster** consists of both a **tx. orderer set** and a **rollup set.** The **tx. orderer set** manages all registered rollups within the cluster. Each **rollup stores the addresses of executors**, responsible for its operation, and is registered with specific enabled features provided by Radius.
      * **Additional Rollup Configurations:**
        * **`rollupType`**: Determines the **block creation mechanism**, based on the transaction list provided by the tx. orderer. Supported options include **`polygon_cdk`**.
        * **`encryptedTransactionType`**: Defines the encryption method used, with **PVDE and SKDE** offered by Radius.
        * **`ValidationInfo`**: Contains **protocol details for re-staking**, specifying:
          * **`platform`**: The blockchain where the validation contract is deployed.
          * **`serviceProvider`**: The specific re-staking service used (**EigenLayer or Symbiotic**).
* **Validation Service Manager Contract (`ValidationServiceManager.sol`)**
  * The **ValidationServiceManager contract** integrates with **restaking protocols** like **Symbiotic**. It facilitates **tx. orderer validation and reward distribution** through the following process:
    1. The **leader tx. orderer** submits **block commitment information** by creating a task using `createTask`.
    2. **Follower tx. orderers** participate in validation by responding to the task with `respondToTask`.
    3. Once validation is complete, the contract **allocates rewards or applies slashing** based on operator performance.

These components work together to provide a **decentralized, secure, and restaking-enabled rollup infrastructure**.
