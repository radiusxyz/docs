---
description: >-
  These components form SBB: Distributed Key Generator (DKG),  Tx_Orderer
  (Operators), Secure-RPC, and Seeder.
---

# Core Components

### **Distributed Key Generator (DKG)**

Distributed Key Generator (DKG) is the core component responsible for managing the cryptographic keys necessary for Single Key Delay Encryption (SKDE). It distributes key generation across multiple nodes, ensuring the keys themselves are decentralized.

DKG currently operated by Radius, with plans to transition to decentralized operator management to further enhance network robustness.

***

### **Tx\_Orderer (Operators)**

Tx\_Orderer is a node within Radius AVS (Actively Validated Services), responsible for deterministic transaction ordering. The Tx\_Orderer is protocol-constrained to only order encrypted data, fundamentally removing the technical ability to front-run or exploit transactions.

* Multiple Tx\_Orderers operate as a cluster to guarantee system fault tolerance and availability. For each block, one Tx\_Orderer is selected from the cluster as the leader, while others serve as verifiers.
* Tx\_Orderers are run by independent operators and receive rewards directly from the rollup via restaking protocol integration (e.g., Symbiotic, EigenLayer), ensuring economic alignment. Rollups may choose to run the Tx\_Orderer directly.
* The component is fully dockerized.

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption><p>A monitoring tool for operators</p></figcaption></figure>

***

### **Secure-RPC**

The Secure-RPC is the component responsible for creating the initial state of transaction blindness necessary for the ordering mechanism.

* **Encryption**: Encrypts transactions using the public key from DKG before they are sent to any external system (e.g., a Tx\_Orderer)
* **Key Management**: Manages the communication and retrieval of encryption keys from DKG.

This ensures sensitive transaction data is protected both in transit and at rest, guaranteeing data integrity during the ordering phase.

* Secure-RPC is designed to be operated by the RPC provider.
* All necessary code will be provided by Radius to support integration.
* The component is fully dockerized.

***

### **Seeder**

Seeder is responsible for enabling communication and coordination among Tx\_Orderers by distributing peer connection data.

* Seeder helps maintain the availability and integrity of the Tx\_Orderer cluster.
* We recommend the Seeder to be operated by the **RaaS (Rollup-as-a-Service)** provide&#x72;**.**
* The component is fully dockerized.

{% hint style="info" %}
_To minimize network latency and avoid delays, we recommend deploying all nodes within the same geographic region._
{% endhint %}

