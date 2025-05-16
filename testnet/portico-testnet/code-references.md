# Code References

## Encrypted Mempool

<details>

<summary><strong>request_encrypt_tx</strong></summary>

```rust
// RPC request for encrypting the transaction
pub async fn request_encrypt_tx(
    rpc_endpoint: Endpoint,
    parameter: EncryptTx,
) -> Option<EncryptTxResponse> 
```

</details>

<details>

<summary>encrypt_tx_with_zkp</summary>

```rust
pub fn encrypt_tx_with_zkp(
    raw_tx: String,
    time_lock_puzzle_param: TimeLockPuzzleParam,
    key_validation_zkp_param: ParamsKZG<Bn256>,
    key_validation_proving_key: ProvingKey<G1Affine>,
    encryption_zkp_param: ParamsKZG<Bn256>,
    encryption_proving_key: ProvingKey<G1Affine>,
) -> Result<(EncryptedTx, DecryptionKey, Option<PvdeZkp>)
```

</details>

<details>

<summary>EncryptTxResponse</summary>

<pre class="language-rust"><code class="lang-rust"><strong>pub struct EncryptTxResponse {
</strong>    pub encrypted_tx: EncryptedTx,
    pub decryption_key: DecryptionKey,
    pub pvde_zkp: Option&#x3C;PvdeZkp>,
}
</code></pre>

</details>

<details>

<summary>EncryptedTx</summary>

```rust
pub struct EncryptedTx {
   raw_tx_hash: RawTxHash,
   encrypted_data: EncryptedData,
   time_lock_puzzle: TimeLockPuzzle,
}
```

</details>

<details>

<summary>SendEncryptedTx</summary>

```rust
pub struct SendEncryptedTx {
    pub rollup_id: RollupId,
    pub encrypted_tx: EncryptedTx,
    pub pvde_zkp: Option<PvdeZkp>,
}
```

</details>

<details>

<summary>SendEncryptedTxResponse</summary>

```rust
pub struct SendEncryptedTxResponse {
    pub block_height: BlockHeight,
    pub tx_order: TxOrder,
    pub signature: Signature,
}
```

</details>

<details>

<summary>provide_decryption_key</summary>

```rust
pub async fn provide_decryption_key(rpc_endpoint: Endpoint, parameter: ProvideDecryptionKey) {
    match RpcClient::request::<ProvideDecryptionKeyResponse>(rpc_endpoint, parameter, 1.into())
        .await
    {
        Ok(response) => tracing::info!("{:?}", response),
        Err(error) => tracing::error!("{:?}", error),
    }
}
```

</details>

<details>

<summary>ProvideDecryptionKey</summary>

<pre class="language-rust"><code class="lang-rust"><strong>pub struct ProvideDecryptionKey {
</strong>    pub decryption_key: DecryptionKey,

    pub rollup_id: RollupId,
    pub block_height: BlockHeight,
    pub tx_order: TxOrder,
    pub signature: Signature,
}
</code></pre>

</details>

## Sequencing Layer ↔ User

<details>

<summary>send_encrypted_tx</summary>

```rust
if do_verify_tx_with_zkp {
// zkp verification
}
match true => {
    let database: Database = runtime::context().load(DB).await?;
    
    // the rollup information is retrieved from the local database.
    let rollup: Rollup = get_rollup(&database, &self.rollup_id)?;
    
    // ...code
    
    // the block height and the transactions order is determined
    let (block_height, tx_order) = self.add_encrypted_tx().await?;
    
    let raw_tx_hash = self.encrypted_tx.raw_tx_hash.clone();
    
    // the decryption_offloader is passed to offload the task of decryption, 
    // to run it asynchronously without blocking the main execution flow.
    runtime::spawn(decryption_offloader(
        self.rollup_id.clone(),
        block_height.clone(),
        tx_order.clone(),
        self.encrypted_tx.clone(),
        3000,
    ));
    
    // the sequencer's private key is loaded from environment
    let sequencer_private_key: PrivateKey =
        runtime::context().load(SEQUENCER_PRIVATE_KEY).await?;
    
    // block height, transaction order, raw transaction hash, 
    // sequencer's private key and rollup type are signed with sequencer's private key
    let signature = sign_for_order_commitment(
        &block_height,
        &tx_order,
        raw_tx_hash,
        sequencer_private_key,
        &rollup.rollup_type,
    )?;
    
    // the order of the transaction, the block height and the signature 
    // is sent to the user as the pre-confirmation
    Ok(SendEncryptedTxResponse {
        block_height,
        tx_order,
        signature,
    })
}
```

</details>

<details>

<summary>add_encrypted_tx</summary>

<pre class="language-rust"><code class="lang-rust"><strong>pub async fn add_encrypted_tx(&#x26;self) -> Result&#x3C;(BlockHeight, TxOrder), Error> {
</strong>    // ...code
    let tx_order = match get_locked_block_metadata(&#x26;database, &#x26;self.rollup_id, &#x26;block_height) {
        Ok(mut locked_block_metadata) => {
            let tx_order = locked_block_metadata.increment_encrypted_tx_order();
            locked_block_metadata.commit()?;

            tx_order
        } // ...error handling
    };

    // add encrypted tx to the database
    set_encrypted_tx(
        &#x26;database,
        &#x26;self.rollup_id,
        &#x26;block_height,
        &#x26;tx_order,
        Some(self.encrypted_tx.clone()),
    )?;

    Ok((block_height, tx_order))
}
</code></pre>

</details>

## Sequencing Layer ↔ Rolup

<details>

<summary>AddRollup</summary>

```rust
pub struct AddRollup {
    pub rollup_id: RollupId,
    pub rollup_type: RollupType,
    pub operator: Operator,
    pub da_info: Option<DataAvailability>,
}
```

</details>

<details>

<summary>RollupType</summary>

```rust
pub enum RollupType {
    Madara = "madara",
}

impl Default for RollupType {
    fn default() -> Self {
        Self::Madara
    }
}
```

</details>

<details>

<summary>Operator</summary>

```rust
pub struct Operator {
    address: Address,
    public_key: PublicKey,
}
```

</details>

<details>

<summary>add_rollup</summary>

```rust
pub async fn add_rollup(&self) -> Result<Rollup, Error> {
 
    // loads database
    
    match get_rollup(&database, &self.rollup_id) {
        // throws an error if successful, meaning the given rollup is already registered
        // or
        // registers new rollup if unsuccessful by
            // adding it to the list of rollups
            // adding it to the database
            // adding its metadata to the database
    }
}
```

</details>

<details>

<summary>GetRawTxList</summary>

```rust
pub struct GetRawTxList {
    pub rollup_id: RollupId,
    pub block_height: Option<BlockHeight>,
    pub operator_signature: Option<Signature>,
}
```

</details>

<details>

<summary>GetRawTxListResponse</summary>

```rust
pub struct GetRawTxListResponse {
    pub is_building_block: bool,
    pub raw_tx_list: RawTxList,
}
```

</details>

<details>

<summary>get_raw_tx_list</summary>

```rust
let database: Database = runtime::context().load(DB).await?;

let rollup = get_rollup(&database, &self.rollup_id)?;

// if block_height is None, get rollup's current block height
let block_height: BlockHeight =
    get_block_height(&database, &self.rollup_id, &self.block_height)?;
    
// ...code for checking if block_height is greater than 
// rollup's current block height, return error 
```

</details>

<details>

<summary>BlockMetadata</summary>

```rust
pub struct BlockMetadata {
    is_decrypted_tx_info_list: Vec<bool>,
    is_closed: bool,
}
```

</details>

<details>

<summary>Block</summary>

```rust
pub struct Block {
    block_height: BlockHeight,
    encrypted_tx_list: EncryptedTxList,
    raw_tx_list: RawTxList,
    sequencer_address: Address,
    signature: Signature,
    rollup_signature: Signature,
    timestamp: Timestamp,
}
```

</details>

<details>

<summary>impl BlockMetadata</summary>

```rust
impl BlockMetadata {
    pub fn increment_encrypted_tx_order(&mut self) -> TxOrder {
    // implementation of FCFS ↓
    
        // 1. gets the length of the current list, which is going to be the order of                   the next tx
        // 2. pushes it's `false` decryption status into the decrypted_tx_info_list
        // 3. returns the tx order
    }

    pub fn set_decrypted_tx(&mut self, tx_order: &TxOrder) {
       // sets the tx of order tx_order as decrypted
    }

    pub fn is_decryption_done(&self) -> bool {
        // checks if all the transactions in the tx info list are decrypted
    }

    pub fn set_closed(&mut self) {
        // closes the block
    }

    pub fn is_closed(&self) -> bool {
        // checks is the block is closed
    }
}
```

</details>

<details>

<summary>block is not closed</summary>

<pre class="language-rust"><code class="lang-rust"><strong>// if there was not block request from the rollup operator, the block is not closed
</strong>if !block_metadata.is_closed() {
<strong>    // only the registered operator can close the block for getting raw_tx_list,
</strong>    // therefore, the sequencer checks if the operator's signature is valid
    
    // if all the validations and verifications are valid 
         // 1. the block is closed
         // 2. the current block height is incremented
         // 3. an empty metadata is set for the future block
    
    // in any other case, an appropriate error is thrown
}
</code></pre>

</details>

<details>

<summary>block is empty, no decrypted transactions</summary>

<pre class="language-rust"><code class="lang-rust">// 1. check if the block is empty
<strong>if block_metadata.is_decrypted_tx_info_list.is_empty() {
</strong><strong>
</strong><strong>    // if indeed there is none
</strong><strong>    //     1.1. record, timestamp, generate empty encrypted and raw transaction lists,
</strong><strong>    //     1.2. sign the block by passing the lists, timestamp, block height,
</strong><strong>    //    sequencer's private key, and rollup type into the signer function
</strong><strong>    //     1.3. build the block by calling 
</strong>                build_block(
                    &#x26;database,
                    block_metadata,
                    &#x26;self.rollup_id,
                    &#x26;block_height,
                    &#x26;sequencer_address,
                    &#x26;block_signature,
                    &#x26;rollup_signature,
                    current_time,
                );
    //    1.4. return the empty raw tx list and its status of not building
    return Ok(GetRawTxListResponse {
        is_building_block: false,
        raw_tx_list: RawTxList::default(),
    });

</code></pre>

</details>

<details>

<summary>block is not empty, all transactions are decrypted</summary>

```rust
// 2. if there are transactions, check if they all are decrypted
match block_metadata.is_decryption_done() {
    // 2.1. if they are, attempt to get the raw transaction list and if successful, return it
    true => match get_raw_tx_list(&database, &self.rollup_id, &block_height) {
        Ok(value) => {
            let get_raw_tx_list_response = GetRawTxListResponse {
                is_building_block: false,
                raw_tx_list: value,
            };
            Ok(get_raw_tx_list_response)
        }
        Err(error) => {
            //     2.1.1 get encrypted and raw transaction lists from the db
            //     2.2.2 ~ repeat 1.2, 1.3 and return the raw transaction list
            Ok(GetRawTxListResponse {
                is_building_block: false,
                raw_tx_list,
            })
        }
    },  
}
```

</details>

<details>

<summary>block is not empty, not all transactions are decrypted</summary>

```rust
// ...code from the Case 2
// otherwise, if any encrypted transaction isn't decrypted, the sequencing layer returns
// an empty list of raw transactions along with the status is_building_block: true, 
// signaling that the building block remains incomplete
false => {
     Ok(GetRawTxListResponse {
        is_building_block: true,
        raw_tx_list: RawTxList::default(),
    })    
}
```

</details>

## Leader-based

<details>

<summary>forwarding to the leader</summary>

```rust
/*

The following code can be found in all of the methods, such as:

add_raw_tx, add_rollup, get_block_metadata, get_block, get_current_block_height,
get_encrypted_tx_list, get_encrypted_tx, get_raw_tx_list, get_raw_tx,
get_rollup_list, get_rollup, provide_decryption_key, send_encrypted_tx, send_raw_tx

*/

fn method_name() -> &'static str {
    // method's name
}

async fn handler(self) -> Result<Self::Output, Error> {
    match is_leader().await? {
        true => {
            // perform leader's actions and send syncing proposal message to the 
            // if needed follower's
        }
        false => forward_to_leader(self).await,
    }
}
```

</details>

<details>

<summary>request from followers to sync</summary>

```rust
RaftNode::send_proposal_message(...).await?;
```

```rust
RaftNode::sync_encrypted_txs(
    &raft_endpoint_list,
    rollup_id,
    &merged_rollup_snapshot.rollup.current_block_height,
    &merged_rollup_snapshot.block_metadata,
)
.await?;

RaftNode::sync_raw_txs(
    &raft_endpoint_list,
    rollup_id,
    &merged_rollup_snapshot.rollup.current_block_height,
    &merged_rollup_snapshot.block_metadata,
)
.await?;

RaftNode::sync_block(
    &raft_endpoint_list,
    rollup_id,
    &BlockHeight::from(block_height),
)
.await?;

RaftNode::sync_block_metadata(
    &raft_endpoint_list,
    &rollup_id,
    &block_height,
)
.await
```

</details>
