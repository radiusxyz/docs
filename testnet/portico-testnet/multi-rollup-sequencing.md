# Multi-Rollup Sequencing

Now that we've explored how Radius ensures sequencing liveness for rollups, let's delve into multi-rollup sequencing.

### **Overview**

_Shared_ sequencing involves multiple rollups sharing the same sequencer. This sequencer sequences blocks and submits them to respective rollup operators.

To manage multiple rollups, the shared sequencer must distinguish data associated with each rollup. Using _rollup identification_, it selectively provides relevant transactions when a rollup operator requests the transaction list (block) for execution.

### [Rollup Identification](../../developer/sequencing-layer-rollup.md#adding-a-rollup)

Rollup identification is facilitated through a unique Rollup ID assigned to each rollup, issued by the rollup itself. The rollup operator registers its address (Operator Address) with the shared sequencing layer, allowing it to associate each operator with the correct rollup.

Each rollup is assigned a unique identifier known as the **Rollup ID**, issued by the rollup itself. The rollup operator registers its address (referred to as the **Operator Address**) with the shared sequencing layer. The mapping of the Rollup ID and the Operator Address allows the shared sequencing layer to associate each operator with the correct rollup.

* **Rollup ID**: Unique identifier assigned to each rollup
* **Operator Address**: Address of the rollup node operator
* **Operator Public Key**: Public key of the rollup node operator

To identify transactions for each rollup, the leader manages the following information and provides it to the followers:

* Transaction Hash
* Rollup ID
* Block Height
* Order
* Sequencer Signature

### [Rollup Identification Process](../../developer/sequencing-layer-rollup.md#getting-the-block-from-the-sequencing-layer)

1. **Transaction Identification**: Leader pre-determines execution order and assigns and stores the rollup identification data, including Rollup ID, Block Height, Transaction Order, and Sequencer's Signature.
2. **Block Request**: Rollup node operator requests a block (a list of transactions to be executed) from the shared sequencing layer, including Rollup ID, Operator Address, and Operator Signature.
3. **Operator Verification**: Leader verifies the node operator based on the requested data, validating the operator's signature using the rollup’s Operator Address list.
4. **Block Height Update**: After verification, the leader provides the next block height (current block height +1) as a pre-confirmation for subsequent user transactions, closing the current block height.
5. **Transaction Decryption**: Leader checks the decryption status of all transactions in the requested block. If any transactions remain undecrypted, the operator is informed that the block is still being generated. Once all transactions are decrypted, the leader provides the complete transaction list to the operator."

### **Multi-Rollup Sequencing in Portico Testnet**

Explore a demonstration of [Multi-Rollup Sequencing on the Portico Testnet](https://portico.theradius.xyz/multi-rollup-sequencing). The shared sequencer submits blocks to two rollup operators in Rollup A and B, both deployed with the [Madara](https://www.madara.build/) rollup framework.&#x20;

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p><em>The latest block and block times for each rollup are displayed as transactions are sequenced.</em></p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption><p><em>Rollup block explorer</em></p></figcaption></figure>

