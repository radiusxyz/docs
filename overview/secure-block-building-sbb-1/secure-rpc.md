# Secure RPC

Repository: [Secure RPC GitHub](https://github.com/radiusxyz/secure-rpc.git)

### Introduction

The **secure-rpc** framework enables **confidential transmission** of transaction data by:

* Encrypting transactions before sending them to any external system (e.g., a tx\_orderer).
* Managing encryption keys via a **Distributed Key Generation (DKG)** service.

This approach ensures sensitive transaction data is protected both **at rest** and **in transit**.

***

### System Overview

The **secure-rpc** framework is designed to safeguard sensitive transaction data in a blockchain or rollup environment. Its core objective is to ensure that whenever a transaction needs to be broadcast, it can be protected by powerful encryption mechanisms after leaving the client environment. This encryption can later be undone by the tx\_orderer. At the heart of the system lies a Distributed Key Generation (DKG) service, which manages the cryptographic keys needed to execute these operations.

Rather than manually tracking encryption keys or pre-sharing them among participants, the **secure-rpc** approach offloads most key-related responsibilities to this DKG service. The DKG is capable of serving the latest encryption keys for encrypting new transactions, while also storing and providing the corresponding decryption keys.

1. **Encryption Flows**
   * **SKDE**\
     A default encryption method that uses a distributed key approach. A “delay” aspect is introduced ensuring data is only decryptable after a certain time or condition.
   * **PVDE**\
     Leverages time-lock puzzles to enforce a minimum waiting period before decryption is possible.
2. **Decryption Flows**
   * The system fetches the correct decryption key from the DKG service based on a `key_id`.
   * Applies the corresponding decryption mechanism.
   * Reconstructs the original transaction.
3. **RPC Endpoints**
   * **Send Raw Transaction** (`send_raw_transaction`): Based on the configuration the tx can be encrypted or tx. encryption type can be changed.
4. **Distributed Key Generation Service**
   * Provides encryption keys, decryption keys, and SKDE parameters.
   * Manages key rotation or updates so that the client always uses the latest encryption key.

***

### Key Components & Flows

#### DKG Integration

* The secure-rpc client retrieves:
  * **Encryption Key** for encrypting outgoing transactions.
  * **Decryption Key** for decrypting incoming or stored transactions.
  * **SKDE Parameters** needed for the SKDE algorithm.

#### Encryption Flow (SKDE Example)

1. **Raw Transaction** (e.g., Ethereum transaction) is provided.
2. **Transaction Splitting**:
   * **Open Data**: Non-sensitive metadata or fields that must remain unencrypted.
   * **Encrypted Data**: Sensitive fields that should remain confidential.
3. **Key Retrieval** from the DKG service (latest or specific `key_id`).
4. **Encryption** using SKDE routines (`skde::delay_encryption`) along with the **encryption\_key**.
5. **Result** is an `EncryptedTransaction` with a reference to the `key_id` used.

#### Time-Lock Puzzle (PVDE)

Though currently a minimal or “unsupported” flow in the provided code, the concept is:

1. Generate a puzzle parameter (`time_lock_puzzle_param`) which involves a carefully chosen modulus `n`, base `g`, and exponent `y`.
2. The encryption includes a puzzle, meaning that _even with the correct key_, it takes a certain number of sequential operations to unlock the data.
3. The puzzle is combined with zero-knowledge proofs (`sigma_protocol_public_input`) to prove that data was encrypted correctly without revealing it.

### Usage Scenario

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption><p>Secure RPC data flow</p></figcaption></figure>

1. **Client** needs to submit a transaction to a tx\_orderer, but data is sensitive.
2. **AppState / Config** indicates encryption is enabled with SKDE.
3. Client calls `send_raw_transaction`, which internally:
   * Calls `encrypt_transaction` → obtains an `EncryptedTransaction`.
   * Sends this encrypted data to the tx\_orderer via a chosen RPC endpoint from a configured URL list.
4. The tx\_orderer provides the secure-rpc with order-commitment.
5. The secure RPC forwards it to the user.&#x20;
6. Later, the tx-orderer needs to retrieve the original transaction.
   * Tx\_orderer fetches the decryption key from the DKG system and obtains the original transaction.
