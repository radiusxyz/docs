# Run Secure RPC

### Key Details

* **Language and Build Requirements:** The Secure RPC is written in Rust and must be built using `cargo build --release` in the root directory.
* **Environment Variables:**
  * Create an `env.sh` file at `secure-rpc/scripts/execute/env.sh` based on the contents of `env_example.sh`.
  * Ensure the ports defined in `env.sh` are available.
* **Initialization Scripts:**
  * Secure RPC is initialized and run using scripts located in the repository:
    * `secure-rpc/scripts/execute/01_init_secure_rpc.sh`
    * `secure-rpc/scripts/execute/02_run_secure_rpc.sh`

#### Steps

1.  Clone the repository

    ```sh
    git clone https://github.com/radiusxyz/secure-rpc/
    ```
2.  Build the binary

    ```sh
    cd secure-rpc
    cargo build --release
    ```
3. Set up environment variables in `./scripts/execute/env.sh`.
4.  Initialize the service:

    ```bash
    ./scripts/execute/01_init_secure_rpc.sh
    ```
5.  Start the service:

    ```bash
    ./scripts/execute/02_run_secure_rpc.sh
    ```

**Environment Variables**

<details>

<summary>secure-rpc/scripts/execute/env.sh</summary>

{% code overflow="wrap" %}
```bash
#!/bin/bash
SCRIPT_PATH="$( cd -- "$(dirname "$0")" >/dev/null 2>&1 ; pwd -P )"
PROJECT_ROOT_PATH="$( cd $SCRIPT_PATH/../.. >/dev/null 2>&1 ; pwd -P )"

BIN_FILE_NAME="secure-rpc"
BIN_PATH="$PROJECT_ROOT_PATH/scripts/$BIN_FILE_NAME"

DATA_PATH=$PROJECT_ROOT_PATH/data
CONFIG_FILE_PATH=$DATA_PATH/Config.toml

# Copy the new version's binary to the scripts directory
if [[ -f "$PROJECT_ROOT_PATH/target/release/$BIN_FILE_NAME" ]]; then
  cp $PROJECT_ROOT_PATH/target/release/$BIN_FILE_NAME $PROJECT_ROOT_PATH/scripts
fi

# Check if the binary exists
if [[ ! -f "$BIN_PATH" ]]; then
    echo "Error: Secure RPC binary not found at $BIN_PATH"
    echo "Please run this command 'cp $PROJECT_ROOT_PATH/target/release/$BIN_FILE_NAME $PROJECT_ROOT_PATH/scripts' after building the project"
    exit 1
fi

# ONLY THE FOLLOWING VARIABLES SHOULD BE CHANGED

# ============================
# 🔒 Secure RPC Configuration
# ============================

# 🎯 Used to configure the RPC endpoint that can be identified and accessed 
# by users and transaction orderers.
SECURE_RPC_EXTERNAL_RPC_URL="http://127.0.0.1:6666"  # 🌐 External IP - Please update this.

# ============================
# 🔵 Rollup Configuration
# ============================

# 🏗️ Due to the ordering of transactions across multiple rollups, 
# the Rollup ID is required to identify the target rollup executor.
ROLLUP_ID="nodeinfra_rollup"  # ⚠️ Please update this Rollup ID.

# 💡 Since wallets support adding only a single network RPC URL, Secure-RPC must provide 
# all the methods that would be accessible without it when directly communicating 
# with the blockchain. Therefore, ROLLUP_RPC_URL is used to retrieve rollup information 
# and forward it to the wallet or client.
ROLLUP_RPC_URL="http://131.153.159.15:8123"  # 🌐 Please update this Rollup RPC URL.

# ============================
# 🔄 Tx_Orderer Configuration
# ============================

# 🎯 Used to identify the target IP of the transaction orderer (tx_orderer) 
# responsible for receiving encrypted transactions and responding with order commitments.
TX_ORDERER_RPC_RPC_URL="http://127.0.0.1:7777"  # 🌐 Please update this Tx_Orderer (external) RPC URL.

# ============================
# 🔐 Encrypted Transaction Type
# ============================

# 🔏 Specifies the cryptographic scheme used for encrypting the user's transactions.
# Options: skde / pvde
ENCRYPTED_TRANSACTION_TYPE="skde"

# ============================
# 🔑 DKG (Distributed Key Generator)
# ============================

# 🔓 Used for retrieving SKDE parameters, encryption keys, and decryption keys from the DKG.
DISTRIBUTED_KEY_GENERATOR_RPC_URL="http://127.0.0.1:7100"  # 🌐 Please update this Distributed Key Generator (external) RPC URL.
```
{% endcode %}

</details>
