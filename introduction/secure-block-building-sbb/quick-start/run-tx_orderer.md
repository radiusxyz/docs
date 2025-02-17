# Run Tx\_Orderer

## **Prerequisites**

### **1. Installations**

1.  Install

    <pre><code><strong>Rust, Foundry, build-essential, pkg-config, libssl-dev, libclang-dev
    </strong></code></pre>
2.  Run the following shell command to match the correct version:

    ```sh
    foundryup -v nightly-5b7e4cb3c882b28f3c32ba580de27ce7381f415a
    ```

### 2. Contract calls

All smart contract function calls must be executed with success.

_Note:_ We use two separate accounts for different purposes:

* The **operator account** (secured by `OPERATOR_PRIVATE_KEY`) is **only** used for registering the operator in Symbiotic.
* The **tx\_orderer account** (secured by `TX_ORDERER_PRIVATE_KEY`) is responsible for running our tx\_orderer.

This setup follows best practices recommended by other operators. They avoid using their operator private key for running programs to minimize security risks. To enhance security, our system ensures that the operator private key is strictly for registration, while the tx\_orderer private key manages tx\_orderer operations within the network.

<figure><img src="../../../.gitbook/assets/image (26).png" alt=""><figcaption><p>Tx. Orderer (Operator) contract calls to Symbiotic and Radius contracts</p></figcaption></figure>

<details>

<summary>Using Private Key (Holesky version)</summary>

{% code overflow="wrap" %}
```sh
#!/bin/bash

# ============================
# Symbiotic Operator Setup
# ============================
# This script handles registration and opt-in processes for the Symbiotic contract.
# It interacts with the Ethereum Holesky testnet.

# Validation Related
# ---------------------------
# 1. Configuration
# ---------------------------
RPC_URL="https://ethereum-holesky-rpc.publicnode.com"  # Ethereum RPC URL

# Operator registration details
OPERATOR_REGISTRY_CONTRACT_ADDRESS="0x6F75a4ffF97326A00e52662d82EA4FdE86a2C548"
OPERATOR_PRIVATE_KEY=""  # Your operator private key

# Vault opt-in service details
OPERATOR_VAULT_OPT_IN_SERVICE_CONTRACT_ADDRESS="0x95CC0a052ae33941877c9619835A233D21D57351"
VAULT_CONTRACT_ADDRESS="0x919c0EbA1b68803cd453fF218b0E59e174d8C2b0"

# Network opt-in service details
OPERATOR_NETWORK_OPT_IN_SERVICE_CONTRACT_ADDRESS="0x58973d16FFA900D11fC22e5e2B6840d9f7e13401"
NETWORK_ADDRESS="0x47482dA197719f2CE0BAeBB7F72D1d7C1D6cc8bD"  # Ask network (rollup) team

# Operator details
OPERATOR_ADDRESS=""  # Your operator address

# Tx_Orderer registration details
LIVENESS_CONTRACT_ADDRESS="0xBE32Ae8d955747FD4Ab0818C927c3926F373E05E"  # Radius contract address
CLUSTER_ID="radius"  # Cluster ID (Ask network/rollup team)
TX_ORDERER_PRIVATE_KEY=""  # Your tx_orderer private key
TX_ORDERER_ADDRESS=""  # Your tx_orderer address

# ============================
# 2. Register Operator
# ============================
echo "Registering operator..."
cast send "$OPERATOR_REGISTRY_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" --private-key "$OPERATOR_PRIVATE_KEY" \
"registerOperator()"

echo "Checking operator registration..."
cast call "$OPERATOR_REGISTRY_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" \
"isEntity(address who)(bool)" "$OPERATOR_ADDRESS"
echo "Expected output: true"

# ============================
# 3. Opt-in to Vault
# ============================
echo "Opting in to vault..."
cast send "$OPERATOR_VAULT_OPT_IN_SERVICE_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" --private-key "$OPERATOR_PRIVATE_KEY" \
"optIn(address vault)" "$VAULT_CONTRACT_ADDRESS"

echo "Checking vault opt-in status..."
cast call "$OPERATOR_VAULT_OPT_IN_SERVICE_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" \
"isOptedIn(address who, address where)(bool)" "$OPERATOR_ADDRESS" "$VAULT_CONTRACT_ADDRESS"
echo "Expected output: true"

# ============================
# 4. Opt-in to Network
# ============================
echo "Opting in to network..."
cast send "$OPERATOR_NETWORK_OPT_IN_SERVICE_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" --private-key "$OPERATOR_PRIVATE_KEY" \
"optIn(address network)" "$NETWORK_ADDRESS"

echo "Checking network opt-in status..."
cast call "$OPERATOR_NETWORK_OPT_IN_SERVICE_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" \
"isOptedIn(address who, address where)(bool)" "$OPERATOR_ADDRESS" "$NETWORK_ADDRESS"
echo "Expected output: true"

# Liveness Related
# ============================
# 5. Register Tx_Orderer
# ============================
echo "Registering tx_orderer..."
cast send "$LIVENESS_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" --private-key "$TX_ORDERER_PRIVATE_KEY" \
"registerSequencer(string clusterId)" "$CLUSTER_ID"

echo "Checking tx_orderer registration..."
cast call "$LIVENESS_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" \
"isSequencerRegistered(string clusterId, address operating)(bool)" "$CLUSTER_ID" "$TX_ORDERER_ADDRESS"
echo "Expected output: true"

```
{% endcode %}

</details>

<details>

<summary>Using Ledger</summary>

```sh
#!/bin/bash

# ============================
# Symbiotic Operator Setup (Ledger)
# ============================
# This script registers an operator and opts into services using a Ledger device for signing.
# All transactions interact with the Ethereum Holesky testnet.

# ---------------------------
# 1. Configuration
# ---------------------------
RPC_URL="https://ethereum-holesky-rpc.publicnode.com"  # Ethereum RPC URL

# Operator registration details
OPERATOR_REGISTRY_CONTRACT_ADDRESS="0x6F75a4ffF97326A00e52662d82EA4FdE86a2C548"

# Vault opt-in service details
OPERATOR_VAULT_OPT_IN_SERVICE_CONTRACT_ADDRESS="0x95CC0a052ae33941877c9619835A233D21D57351"
VAULT_CONTRACT_ADDRESS="0x919c0EbA1b68803cd453fF218b0E59e174d8C2b0"

# Network opt-in service details
OPERATOR_NETWORK_OPT_IN_SERVICE_CONTRACT_ADDRESS="0x58973d16FFA900D11fC22e5e2B6840d9f7e13401"
NETWORK_ADDRESS="0x47482dA197719f2CE0BAeBB7F72D1d7C1D6cc8bD"  # Ask network (rollup) team

# Operator details
OPERATOR_ADDRESS=""   # Your operator address

# Tx_orderer registration details
LIVENESS_CONTRACT_ADDRESS="0xBE32Ae8d955747FD4Ab0818C927c3926F373E05E"  # Radius contract address
CLUSTER_ID="radius"   # Cluster ID (Ask network/rollup team)
TX_ORDERER_ADDRESS=""  # Your tx_orderer address

# Validation Related
# ============================
# 2. Register Operator
# ============================
echo "Registering operator..."
cast send "$OPERATOR_REGISTRY_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" --ledger \
"registerOperator()"

echo "Checking operator registration..."
cast call "$OPERATOR_REGISTRY_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" \
"isEntity(address who)(bool)" "$OPERATOR_ADDRESS"
echo "Expected output: true"

# ============================
# 3. Opt-in to Vault
# ============================
echo "Opting in to vault..."
cast send "$OPERATOR_VAULT_OPT_IN_SERVICE_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" --ledger \
"optIn(address vault)" "$VAULT_CONTRACT_ADDRESS"

echo "Checking vault opt-in status..."
cast call "$OPERATOR_VAULT_OPT_IN_SERVICE_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" \
"isOptedIn(address who, address where)(bool)" "$OPERATOR_ADDRESS" "$VAULT_CONTRACT_ADDRESS"
echo "Expected output: true"

# ============================
# 4. Opt-in to Network
# ============================
echo "Opting in to network..."
cast send "$OPERATOR_NETWORK_OPT_IN_SERVICE_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" --ledger \
"optIn(address network)" "$NETWORK_ADDRESS"

echo "Checking network opt-in status..."
cast call "$OPERATOR_NETWORK_OPT_IN_SERVICE_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" \
"isOptedIn(address who, address where)(bool)" "$OPERATOR_ADDRESS" "$NETWORK_ADDRESS"
echo "Expected output: true"

# Liveness Related
# ============================
# 5. Register Tx_Orderer
# ============================
echo "Registering tx_orderer..."
cast send "$LIVENESS_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" --ledger \
"registerSequencer(string clusterId)" "$CLUSTER_ID"

echo "Checking tx_orderer registration..."
cast call "$LIVENESS_CONTRACT_ADDRESS" --rpc-url "$RPC_URL" \
"isSequencerRegistered(string clusterId, address operating)(bool)" "$CLUSTER_ID" "$TX_ORDERER_ADDRESS"
echo "Expected output: true"

```

</details>

### **3. Running Tx\_Orderer**

Repository: Tx\_Orderer GitHub

_**Note**:_ A cluster is a group of tx\_orderers with a leader. This process can run with a single tx\_orderer as well. Do not be confused by the `.env` variables referencing clusters.

### Key Details

* **Language and Build Requirements:** The Tx\_Orderer is written in Rust and must be built using `cargo build --release` in the root directory.
* **Environment Variables:**
  * Create an `env.sh` file at `tx_orderer/scripts/execute/env.sh` based on the contents of `env_example.sh`.
  * Ensure the ports defined in `env.sh` are available.
  * Another `env.sh` is needed at `tx_orderer/scripts/rpc-call/env.sh` for RPC-related scripts, also derived from `env_example.sh`.
* **Initialization Scripts:**
  * Tx\_orderer is initialized and run using scripts located in the repository:
    * `tx_orderer/scripts/execute/01_init_tx_orderer.sh`
    * `tx_orderer/scripts/execute/02_run_tx_orderer.sh`

_Note_: the tx\_orderer is configured to support various types of liveness and validation. Additionally, a single tx\_orderer is not limited to operating for just one rollup but is designed to manage multiple rollups. If the components currently provided through APIs were converted into configurations, the tx\_orderer serving an existing rollup would need to be restarted each time a new rollup is added. To prevent this, these components are structured as APIs.

***

#### Hardware Specs

* CPU: 4
* Memory (GiB): 16
* Network (Gbps): 1
* Storage (GB): 256

#### Running the Tx\_Orderer

1.  Clone the repository&#x20;

    ```sh
    git clone https://github.com/radiusxyz/tx_orderer
    ```
2.  Build the binary

    ```sh
    cd tx_orderer
    cargo build --release
    ```
3. Set up environment variables in `./scripts/execute/env.sh`.
4.  Initialize the Tx\_Orderer:

    ```bash
    ./scripts/execute/01_init_tx_orderer.sh
    ```
5.  Start the Tx\_Orderer:

    ```bash
    ./scripts/execute/02_run_tx_orderer.sh
    ```
6. Set up environment variables in `tx_orderer/scripts/rpc-call/env.sh`.
7.  **Initialize RPC for adding the sequencing info related to LivenessServiceManager contract:** This action serves for integrating liveness information from the LivenessServiceManager smart contract into the tx\_orderer. Upon completion, the tx\_orderer will be able to listen to events related to the LivenessServiceManager smart contract on the `LIVENESS_PLATFORM`, retrieve information about tx\_orderers and rollups, and invoke functions within the smart contract:

    ```bash
    ./scripts/rpc-call/11_add_sequencing_info.sh
    ```
8.  **Add validation service details with RPC:** This action serves for integrating validation information from the ValidationServiceManager smart contract into the tx\_orderer. Upon completion, the tx\_orderer will be able to listen to events related to the ValidationServiceManager smart contract on the VALIDATION\_PLATFORM, retrieve information from the ValidationServiceManager contract, and invoke its functions.

    ```bash
    ./scripts/rpc-call/12_add_symbiotic_validation_info.sh
    ```
9.  **Add cluster info:** This action serves for integrating cluster information, registered in the smart contract, into the tx\_orderer. Upon completion, the tx\_orderer will collect events whenever a block is generated in LIVENESS\_PLATFORM and automatically update itself with the relevant cluster information.&#x20;

    ```bash
    ./scripts/rpc-call/13_add_cluster.sh
    ```

**Environment Variables**

<details>

<summary>tx_orderer<strong>/scripts/execute/env.sh</strong></summary>

{% code overflow="wrap" %}
```bash
#!/bin/bash
SCRIPT_PATH="$( cd -- "$(dirname "$0")" >/dev/null 2>&1 ; pwd -P )"
PROJECT_ROOT_PATH="$( cd $SCRIPT_PATH/../.. >/dev/null 2>&1 ; pwd -P )"

BIN_FILE_NAME="tx_orderer"
BIN_PATH="$PROJECT_ROOT_PATH/scripts/$BIN_FILE_NAME"

DATA_PATH=$PROJECT_ROOT_PATH/data
CONFIG_FILE_PATH=$DATA_PATH/Config.toml
PRIVATE_KEY_PATH=$DATA_PATH/signing_key

# Copy the new version's binary to the scripts directory
if [[ -f "$PROJECT_ROOT_PATH/target/release/$BIN_FILE_NAME" ]]; then
  cp $PROJECT_ROOT_PATH/target/release/$BIN_FILE_NAME $PROJECT_ROOT_PATH/scripts
fi

# Check if the binary exists
if [[ ! -f "$BIN_PATH" ]]; then
    echo "Error: Tx_orderer binary not found at $BIN_PATH"
    echo "Please run this command 'cp $PROJECT_ROOT_PATH/target/release/$BIN_FILE_NAME $PROJECT_ROOT_PATH/scripts"
    exit 1
fi

# ONLY THE FOLLOWING VARIABLES SHOULD BE CHANGED

# ============================
# Tx_Orderer Configuration
# ============================

# ⚠️ NOTE: The following values are provided for contracts deployed on the Ethereum Holesky testnet. 
# ⚠️ If you're deploying to a different network, update these values accordingly.

# ---------------------------------
# 🔑 Tx_Orderer Private Key
# ---------------------------------
# Used for signing various data, such as order commitments for users, block commitments for validation, etc.
TX_ORDERER_PRIVATE_KEY="0xe090d38fc4b19212e1b61fd32f02c9f928fedaa3338c13e0911fde837762d9ee"  # ⚠️ Change this before deploying.

# ---------------------------------
# 🔄 Tx_Orderer RPC URLs
# ---------------------------------
# Used for storing node-related information.
TX_ORDERER_INTERNAL_RPC_URL="http://127.0.0.1:4000"  # Internal IP - Update as needed.

# Used for communication within the cluster.
TX_ORDERER_CLUSTER_RPC_URL="http://127.0.0.1:5555"   # External IP - Update as needed.

# Used for retrieving blocks and order commitments from the transaction orderer.
TX_ORDERER_EXTERNAL_RPC_URL="http://127.0.0.1:5556"  # External IP - Update as needed.

# ---------------------------------
# 🔐 DKG (Distributed Key Generator)
# ---------------------------------
# Used for retrieving the decryption key from the DKG.
DISTRIBUTED_KEY_GENERATOR_RPC_URL="http://127.0.0.1:7100"  # External DKG RPC URL - Update as needed.

# ---------------------------------
# 🌱 Seeder Configuration
# ---------------------------------
# Used for registering the transaction orderer's IP and providing the IPs of other transaction orderers in the cluster.
SEEDER_RPC_URL="http://127.0.0.1:6000"  # External Seeder RPC URL - Update as needed.
```
{% endcode %}

</details>

<details>

<summary>tx_orderer<strong>/scripts/rpc-call/env.sh</strong></summary>

<pre class="language-bash" data-overflow="wrap"><code class="lang-bash"><strong>#!/bin/bash
</strong>
# ============================
# Tx_Orderer Configuration
# ============================

# ⚠️ NOTE: The following values are for the Ethereum Holesky testnet.
# ⚠️ If you're deploying to a different network, update them accordingly.

# ---------------------------------
# 🔄 Tx_Orderer RPC Configuration
# ---------------------------------
# The RPC endpoint for registering the transaction orderer for both the Liveness and Validation services.
TX_ORDERER_INTERNAL_RPC_URL="http://127.0.0.1:4000"  # Internal IP - Update this with your correct IP.

# ============================
# 🔵 LivenessServiceManager Contract
# ============================

# ⚠️ DO NOT CHANGE THESE VALUES ⚠️
# The blockchain on which the LivenessServiceManager contract is deployed, currently Ethereum.
LIVENESS_PLATFORM="ethereum"  # Options: [ethereum]

# The network that provides liveness service, currently Radius.
LIVENESS_SERVICE_PROVIDER="radius"  # Options: [radius]

# Ethereum RPC &#x26; WebSocket URLs for the LivenessServiceManager contract.
LIVENESS_RPC_URL="https://ethereum-holesky-rpc.publicnode.com"
LIVENESS_WS_URL="wss://ethereum-holesky-rpc.publicnode.com"

# 📍 LivenessServiceManager contract address (provided by Radius).
LIVENESS_CONTRACT_ADDRESS="0xBE32Ae8d955747FD4Ab0818C927c3926F373E05E"

# 🏗️ Cluster ID (provided by the network/rollup team).
# A unique identifier for the cluster.
CLUSTER_ID="radius"  # ⚠️ Update this if necessary.

# ============================
# 🟡 ValidationServiceManager Contract
# ============================

# ⚠️ DO NOT CHANGE THESE VALUES ⚠️
# The blockchain on which the ValidationServiceManager is deployed, currently Ethereum.
VALIDATION_PLATFORM="ethereum"  # Options: [ethereum]

# The network providing validation services, either Symbiotic or EigenLayer.
VALIDATION_SERVICE_PROVIDER="symbiotic"  # Options: [eigen_layer / symbiotic]

# Ethereum RPC &#x26; WebSocket URLs for the ValidationServiceManager contract.
VALIDATION_RPC_URL="https://ethereum-holesky-rpc.publicnode.com"
VALIDATION_WS_URL="wss://ethereum-holesky-rpc.publicnode.com"

# 📍 ValidationServiceManager contract (provided by the network/rollup team).
# The address of the deployed ValidationServiceManager, used for validating block commitments and other restaking-related matters.
VALIDATION_SERVICE_MANAGER_CONTRACT_ADDRESS="0x886404D7b959B01E351FC975Aa298e4c2b6F9d55"
</code></pre>

</details>
