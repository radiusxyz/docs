# Distributed Key Management System (DKG)

Repository: [Distributed Key Generation GitHub](https://github.com/radiusxyz/distributed_key_generation)

## Overview of DKG

## Distributed Key Generation (DKG) Overview

The Distributed Key Generation (DKG) service is a core component of Radius’s Single Key Delay Encryption (SKDE) method. It ensures secure encryption and decryption by distributing key generation across multiple nodes. Each node contributes a partial key, which is aggregated into an encryption key. A delay function is then applied to derive the decryption key later. This enables:

* Users and secure-RPC to encrypt transactions.
* The transaction orderer to obtain the decryption key for secure processing.

### SBB with SKDE

#### Background

SKDE powers encrypted mempool operations within SBB. Traditionally, each blockchain network requires independent SKDE systems, which introduces inefficiencies. Since networks have different block generation cycles, managing unique encryption schemes for each is impractical.

A unified DKG network addresses this by supporting all block intervals, optimizing key management across blockchain ecosystems. This Proof of Concept (PoC) lays out a scalable DKG protocol designed to enhance security, interoperability, and efficiency.

#### SKDE Workflow

1. **Partial Key Generation**
   * Nodes generate partial keys and validity proofs using RSA-based parameters and time-lock puzzles to distribute trust.
2. **Partial Key Verification**
   * Ensures the authenticity of generated partial keys.
3. **Partial Key Aggregation**
   * A block proposer collects and combines partial keys using Multi-Party Computation (MPC).
4. **Transaction Encryption**
   * Users encrypt transactions with the aggregated key to prevent pre-execution visibility, mitigating MEV and censorship risks.
5. **Puzzle Solving**
   * A solver derives the decryption key by solving a time-lock puzzle, ensuring transactions remain encrypted until processing time.
6. **Transaction Decryption**
   * Transactions are decrypted in an ordered manner for execution<mark style="color:orange;">.</mark>

### Key Assumptions

* **Key Committee**: A designated committee ensures secure and efficient operation.
* **Minimal Delay Impact**: Time fluctuations should not disrupt protocol effectiveness.
* **Network Latency**: Assumed round-trip time (RTT) is 100–200ms.
* **Key Rotation**: New keys are generated every second, with overlapping cycles ensuring availability.
* **Participation Requirements**: Nodes must stake tokens to participate in the DKG network.

### Key Life Cycle & Usage

#### Life Cycle

A defined key committee generates partial keys and aggregates them into a master encryption key (AggKey). Until it is decrypted, transactions remain encrypted. The decryption key (DevKey) is used once the delay function is solved.

#### Key-Related Periods

* **Key Request Period**: Users request encryption keys before submission deadlines.
* **Transaction Submission**: Encrypted transactions must be submitted within the given timeframe.
* **Key Solve Period**: Decryption keys are computed with a 2-second delay.
* **Order Commit Period**: Transactions are committed to blocks in an ordered sequence.

### DKG Protocol with Fast Consensus

#### Overview

Committees precompute partial keys and proofs ahead of time, maintaining two key instances to optimize encryption order commitments. Initial blocks include valid key lists, followed by decryption key releases.

#### Protocol Workflow

1. **Setup**: Nodes exchange and validate partial keys, forming a consensus on a valid key list.
2. **Key Aggregation**: All nodes independently compute the aggregated encryption key.
3. **Transaction Encryption**: Users encrypt transactions with the aggregated key (AggKey).
4. **Order Commitment**: SBB nodes establish transaction order before decryption.
5. **Puzzle Solving**: Anyone can solve the time-lock puzzle to reveal the decryption key.
6. **Decryption & Execution**: The decrypted key is shared with SBB nodes to execute transactions.
7. **Key Cycle Reiteration**: New keys are continuously generated to maintain security and efficiency.

### Consensus Considerations

* **Without Consensus (Ethereum Dependency)**: Relies on Ethereum for validation.
* **With Consensus**: A decentralized approach where committee members reach agreement independently.

By leveraging a unified DKG system, this protocol enhances encryption efficiency, reduces redundant infrastructure, and ensures seamless blockchain interoperability.
