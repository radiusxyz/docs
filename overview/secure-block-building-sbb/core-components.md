---
description: >-
  There are three components in SBB: Secure-RPC, Tx_Orderer (Operators), and
  Distributed Key Generator (DKG).
---

# Core Components

**Secure-RPC**

The Secure-RPC is responsible for creating the initial state of transaction blindness necessary for the ordering mechanism.

* **Encryption**: Encrypts transactions using the public key from DKG before they are sent to any external system (e.g., a Tx\_Orderer)
* **Key Management**: Manages the communication and retrieval of encryption keys from DKG.

This ensures sensitive transaction data is protected both in transit and at rest, guaranteeing data integrity during the ordering phase.

* Secure-RPC is designed to be operated by the RPC provider.
* All necessary code will be provided by Radius to support integration.
* The component is fully dockerized.

***

### **Tx\_Orderer (Operators)**

Tx\_Orderer is a node within Radius AVS (Actively Validated Services), responsible for deterministic transaction ordering. The Tx\_Orderer is protocol-constrained to only order encrypted data, fundamentally removing the technical ability to front-run or exploit transactions.

* Multiple Tx\_Orderers operate as a cluster to guarantee system fault tolerance and availability. For each block, one Tx\_Orderer is selected from the cluster as the leader, while others serve as verifiers.
* Tx\_Orderers are run by independent operators and receive rewards directly from the rollup via restaking protocol integration (e.g., Symbiotic, EigenLayer), ensuring economic alignment. Rollups may choose to run the Tx\_Orderer directly.
* The component is fully dockerized.

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption><p>A monitoring tool for operators</p></figcaption></figure>

***

### **Distributed Key Generator (DKG)**

The Distributed Key Generator (DKG) is a critical protocol component responsible for provisioning cryptographic keys for a secure, time-locked encryption/decryption mechanism. This mechanism is formalized via Single Key Delay Encryption (SKDE).

Learn more about DKG in the [next section](distributed-key-generator-dkg.md).

