# Distributed Key Generator (DKG)

The Distributed Key Generator (DKG) is a critical protocol component responsible for provisioning cryptographic keys for a secure, time-locked encryption/decryption mechanism. This mechanism is formalized via Single Key Delay Encryption (SKDE).

{% hint style="info" %}
_Initially, the DKG is operated by Radius, with plans for transitioning to decentralized operator management to further enhance network robustness._
{% endhint %}

#### **Core Functions**

DKG is designed to provide the foundational certainty necessary for high-value operations:

* **Byzantine Fault Tolerance (BFT)**: Implements BFT to safeguard the system. By decentralizing key management, DKG ensures that operator failure does not compromise the cryptographic security of the entire system.
* **Distributed Architecture**: Multiple specialized nodes decentralize the key management process, eliminating the single point of failure inherent in centralized key storage.
* **Time-Lock Encryption**: Keys for encryption are available immediately; decryption keys are released only after pre-determined time intervals.
* **SKDE Integration**: Seamlessly integrates with the SKDE framework to guarantee the integrity of time-locked cryptographic operations.
* **High Performance**: Achieves efficient key generation and consensus via asynchronous task processing.



#### **Architecture**

DKG operates through four specialized node types, each contributing to the security and integrity of the key lifecycle:

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>



#### **Node Roles**

| **Role**  | **Purpose**           | **Key Responsibilities**                                                                        |
| --------- | --------------------- | ----------------------------------------------------------------------------------------------- |
| Authority | Trusted Setup Manager | Constructs, manages, and securely distributes SKDE parameters.                                  |
| Committee | Key Generation Leader | Generates encryption keys and coordinates consensus among nodes.                                |
| Solver    | Decryption Provider   | Computes the time-lock decryption keys.                                                         |
| Verifier  | Network Monitoring    | Detects, monitors, and reports any Byzantine (malicious or faulty) behavior within the network. |



#### **How DKG Works**

DKG utilizes a time-locked encryption model:

1. Setup Phase: The Authority node initializes the system by generating and distributing foundational SKDE parameters.
2. Key Generation: Committee nodes create the encryption keys corresponding to scheduled time intervals.
3. Immediate Access: Encryption Keys are immediately available for external services.
4. Time-Locked Release: Solver nodes compute and release the corresponding decryption keys after pre-determined delays.
5. Verification: Verifier nodes continuously monitor the network operations, ensuring all nodes adhere to the protocol and maintaining fault tolerance.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>



#### **Operational Lifecycle**

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>



#### **Key States and Transitions**

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>
