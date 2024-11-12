# Sequencing Layer ↔ Rollup

## Adding a rollup <a href="#adding-a-rollup" id="adding-a-rollup"></a>

To begin functioning as a sequencing layer for a rollup, the initial step involves registering the rollup within the sequencing layer's list of rollups. In Radius, a rollup is defined using a specific structure, that contains rollup's id, type, and operator.

* [AddRollup](code-references.md#addrollup)

By default, the rollup type is set to "Madara", since, currently, Radius only supports Madara. Additional rollup types will be introduced in the future.

* [RollupType](code-references.md#rolluptype)

### Rollup operator's description

The rollup operator is described by its address and public\_key.

* [Operator](code-references.md#operator)

### Saving the rollup

The `add_rollup()` function verifies if a rollup with the specified ID already has a corresponding key in the database. If not, it adds the rollup along with its metadata to the database.

* [add\_rollup](code-references.md#add\_rollup)

## Getting the block from the sequencing layer

<figure><img src="../../.gitbook/assets/image (11) (1).png" alt=""><figcaption><p><em>Getting the block of raw transactions from the sequencing layer</em></p></figcaption></figure>

After the rollup has been added to the list of rollups, sequencing can commence. The process involves the rollup initiating a request for a block of raw transactions. This is done by making an RPC call to the `get_raw_tx_list` method on the sequencing layer. The method, in response, returns a structure named `GetRawTxListResponse`.&#x20;

1. **Request Structure (`GetRawTxList`):**
   * This structure defines the request format for fetching raw transaction lists. It includes:
     * `rollup_id`: Identifier for the specific rollup within the blockchain from which to fetch the block's transactions.
     * `block_height`: An optional field specifying the height of the block for which the raw transaction list is requested. If not provided, the current block height of the rollup is used.
     * `operator_signature`: An optional digital signature from the operator, potentially used for authorization or validation purposes.
2. **Response Structure (`GetRawTxListResponse`):**
   * This structure outlines the format of the response to the request. It includes:
     * `is_building_block`: A boolean indicating whether the block is currently in the process of being built (true) or is completed (false).
     * `raw_tx_list`: The list of raw transactions from the specified block.

* [GetRawTxList](code-references.md#getrawtxlist)
* [GetRawTxListResponse](code-references.md#getrawtxlistresponse)

### Block and BlockMetadata for optimized request processing

To minimize the overhead associated with database operations, the `BlockMetadata` structure along with its traits has been implemented.

The `Block` structure holds various pieces of information including its height, lists of transactions in both encrypted and unencrypted forms, rollup signature, the address and the signature of the leader sequencer, and a timestamp marking when it was created.

The `BlockMetadata` structure keeps track of which transactions in a block have been decrypted and whether the block is open or closed for adding more transactions. It's a straightforward way to manage the state of transactions within a block and the block's overall status in the blockchain.

* [Block](code-references.md#block)
* [BlockMetadata](code-references.md#blockmetadata)
* [Methods of BlockMetadata](code-references.md#impl-blockmetadata)

The `BlockMetadata` structure is designed to manage transactions within a block, focusing on their encryption status and the block's availability for adding new transactions. It includes functionality to add new encrypted transactions and mark them as decrypted over time. Additionally, it can check if all transactions have been decrypted and manage the block's open or closed status, indicating whether new transactions can be added. Essentially, it's a system for overseeing transaction processing and ensuring the block moves from an active state, where transactions are being processed, to a finalized state, where all transactions are decrypted and the object returned to rollup is determined.

### Possible states of block formation

When the rollup operator requests a block, the sequencing layer verifies several conditions, including the operator's credentials, before closing the block by setting `is_closed` to true.

Initially, it checks if a block is already closed. If the block is still open, the system then ensures that only a recognized operator can initiate the closure by verifying the operator's signature. If the signature is verified along with all other required validations, three actions are taken: the block is closed, the blockchain's current height is increased to account for the addition of the newly closed block, and a new, empty metadata structure is prepared for the next block. If any validation fails, the system will halt the process and report an error. This mechanism ensures that blocks are closed securely and orderly, preparing the blockchain for subsequent blocks.

* [if the block is not closed](code-references.md#block-is-not-closed)

Once the block is closed, three specific cases are checked to determine the return value to the rollup.

### Case 1: No decrypted transactions

When a block is closed, the system evaluates the transactions to determine the appropriate response for the rollup process. Here's a simplified explanation for the first case scenario:

If there are no decrypted transactions present, the system first checks if the transaction list within the block metadata is empty. If it finds no transactions:

1. It records the current state, noting the absence of transactions. It then creates empty lists for both encrypted and raw transactions.
2. The block is signed. This involves taking the empty transaction lists, the current timestamp, the block's height, the sequencer's private key, and the type of rollup, and passing them to a function designed to officially sign the block.
3. A new block is constructed. This step involves calling a `build_block` function with several parameters, including the database, block metadata, rollup ID, block height, sequencer address, and the signatures obtained from the previous step, along with the current time.
4. Finally, the process returns a response indicating that the block is not in the process of being built and includes the default (empty) raw transaction list.

In essence, this scenario deals with the situation where a closed block contains no decrypted transactions, outlining the steps to officially close and sign off the block while preparing for future transactions.

* [empty block, no decrypted txs](code-references.md#block-is-empty-no-decrypted-transactions)

### Case 2: All transactions are decrypted

\
In this part of the code, the process checks for the presence and decryption status of transactions in a block once it is closed. Here's the simplified flow:

1. The system checks if all transactions in the block have been decrypted.
2. If all transactions are decrypted:
   * It attempts to retrieve the raw transaction list from the database. If successful, this list is returned as part of the response, indicating that the block is not currently being built, and provides the raw transaction list directly.
3. In case of an error while retrieving the raw transaction list:
   * The system fetches both encrypted and raw transaction lists from the database.
   * It follows a similar procedure to record, timestamp, generate transaction lists, and sign the block, similar to the process outlined in the first case.
   * After these steps, it returns the raw transaction list in the response, indicating again that the block is not being built.

This process ensures that, for blocks with decrypted transactions, an attempt is made to fetch and return the raw transaction list directly. If there's an issue in fetching this list, the block is processed similarly to the case of an empty block, ensuring that the transactions are recorded, signed, and a response is provided.

* [all transactions are decrypted](code-references.md#block-is-not-empty-all-transactions-are-decrypted)

### Case 3: Not all transactions are decrypted

In this continuation, the focus is on handling the scenario where not all transactions within the block are decrypted after it has been closed. Here's what happens:

* If it's determined that any of the transactions remain encrypted, meaning not every transaction has been decrypted successfully, the system takes a different approach compared to when all transactions are decrypted.
* Instead of proceeding with building the block or fetching raw transactions from the database, the system acknowledges that the block cannot be completed at this moment. This is due to the presence of encrypted transactions that haven't been decrypted yet.
* To reflect this, the system returns a response indicating that the block is still in the process of being built (`is_building_block: true`). This response also includes an empty list for the raw transactions (`raw_tx_list: RawTxList::default()`), signaling that, without all transactions decrypted, the block's construction isn't finalized.

Essentially, this part deals with the situation where the block remains incomplete due to undecrypted transactions, informing the rollup process that the block is still under construction and not ready for finalization.

* [not all transactions are decrypted](code-references.md#block-is-not-empty-not-all-transactions-are-decrypted)

This finalizes the sequencing layer's interaction with the rollup's operator.&#x20;
