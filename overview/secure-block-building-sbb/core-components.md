---
description: >-
  Understand the roles of DKG,  Tx_Orderer, Secure-RPC, anSeeder—and who
  operates them.
---

# Core Components

### **Distributed Key Generation (DKG)**

* Distributed Key Generation (DKG) service is a core component of Radius’s Single Key Delay Encryption (SKDE) method. It ensures secure encryption and decryption by distributing key generation across multiple nodes.
* **DKG is operated by Radius.**

***

### **Tx\_Orderer**

* Tx\_Orderer is a specialized node within Radius’ AVS (Actively Validated Services) network, responsible for deterministic transaction ordering. To ensure liveness and censorship resistance, multiple Tx\_Orderers operate as part of a coordinated Tx\_Orderer cluster. For each rollup block, a Tx\_Orderer is selected from the cluster to act as the leader, while others serve as verifiers.
* **Tx\_Orderers are run by independent operators** and receive rewards directly from the Rollup. Radius enables this through integration with **restaking protocol** (e.g. Symbiotic, EigenLayer), ensuring AVS-level ordering services with verifiable accountability and economic alignment. The Rollup team may also choose to run one of the Tx\_Orderer directly.
* The component is **fully dockerized**, making deployment and integration straightforward. The documentaion is available upon request.
* A monitoring tool for operators are provided.

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

***

### **Secure-RPC**

*   The **Secure-RPC** enables confidential transmission of transaction data by:

    * **Encrypting transactions** before they are sent to any external system (e.g., a `Tx_Orderer`)
    * **Managing encryption keys** via a Distributed Key Generation (DKG) service

    This ensures that sensitive transaction data is protected both **in transit** and **at rest**, preserving user privacy and enabling MEV-safe transaction processing.
* Secure-RPC is designed to be **operated by the RPC provider**, and all necessary code will be provided by Radius to support integration.
* The component is **fully dockerized**, making deployment and integration straightforward. The documentaion is available upon request.

***

### **Seeder**

* Seeder is responsible for enabling communication and coordination among Tx\_Orderers by distributing peer connection data.
* To maintain availability and integrity of the Tx\_Orderer cluster, we recommend the Seeder to be operated by the **RaaS provider.**
* The component is **fully dockerized**, making deployment and integration straightforward. The documentaion is available upon request.

{% hint style="info" %}
_To minimize network latency and avoid delays, we recommend deploying all nodes within the same geographic region._
{% endhint %}

