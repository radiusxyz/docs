# Run DKG

Repository: [Distributed Key Generation GitHub](https://github.com/radiusxyz/distributed_key_generation)

1.  Clone the repository

    ```sh
    git clone https://github.com/radiusxyz/distributed_key_generation
    ```
2.  Build the binary

    ```jsx
    cd distributed_key_generation
    cargo build --release
    ```
3. Set up environment variables in `./scripts/execute/env.sh`.
4.  Initialize the system:

    ```bash
    ./scripts/execute/01_init_key_generator.sh
    ```
5.  Start the system:

    ```bash
    ./scripts/execute/02_run_key_generator.sh
    ```
6. Set up environment variables in `./scripts/rpc-call/env.sh`.
7.  Initialize RPC: This action serves for registering a key generator by submitting its address and RPC endpoints to an internal system.

    ```bash
    ./scripts/rpc-call/10_initialize.sh
    ```

**Environment Variables**

<details>

<summary>distributed_key_generation/scripts/execute/env.sh</summary>

```sh
#!/bin/bash

#!/bin/bash
CURRENT_PATH="$( cd -- "$(dirname "$0")" >/dev/null 2>&1 ; pwd -P )"
PROJECT_ROOT_PATH="$( cd $SCRIPT_PATH/../.. >/dev/null 2>&1 ; pwd -P )"

BIN_FILE_NAME="key-generator"
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
  echo "Error: Keygenerator binary not found at $BIN_PATH"
  echo "Please run this command 'cp $PROJECT_ROOT_PATH/target/release/$BIN_FILE_NAME $PROJECT_ROOT_PATH/scripts' after building the project"
  exit 1
fi

# ONLY THE FOLLOWING VARIABLES SHOULD BE CHANGED

# Below are the environment variables required for setting up the Distributed Key Generator.

# ============================
# 🔄 RPC Endpoints
# ============================

# Internal RPC URL  
# Used to add a node to the Distributed Key Management System (DKG).  
KEY_GENERATOR_INTERNAL_RPC_URL="http://127.0.0.1:7200"  # Internal IP - Please change this IP.

# Cluster RPC URL  
# Used for communication within the DKG cluster.  
KEY_GENERATOR_CLUSTER_RPC_URL="http://127.0.0.1:7300"  # External IP - Please change this IP.

# External RPC URL  
# Used for retrieving SKDE parameters, encryption keys, and decryption keys from the DKG.  
KEY_GENERATOR_EXTERNAL_RPC_URL="http://127.0.0.1:7100"  # External IP - Please change this IP.

# ============================
# 🔑 Wallet Address
# ============================

# Key Generator Address  
# Used to retrieve the list of RPC URLs from the seeder,  
# registered through the Liveness Radius contract (TBD).  
KEY_GENERATOR_ADDRESS="0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266"  # Please change this key generator address.

```

</details>

<details>

<summary>distributed_key_generation/scripts/rpc-call/env.sh</summary>

```sh
#!/bin/bash

# Below are the environment variables required for setting up the Distributed Key Generator.

# ============================
# 🔄 RPC Endpoints
# ============================

# Internal RPC URL  
# Used to add a node to the Distributed Key Management System (DKG).  
KEY_GENERATOR_INTERNAL_RPC_URL="http://127.0.0.1:7200"  # Internal IP - Please change this IP.

# Cluster RPC URL  
# Used for communication within the DKG cluster.  
KEY_GENERATOR_CLUSTER_RPC_URL="http://127.0.0.1:7300"  # External IP - Please change this IP.

# External RPC URL  
# Used for retrieving SKDE parameters, encryption keys, and decryption keys from the DKG.  
KEY_GENERATOR_EXTERNAL_RPC_URL="http://127.0.0.1:7100"  # External IP - Please change this IP.

# ============================
# 🔑 Wallet Address
# ============================

# Key Generator Address  
# Used to retrieve the list of RPC URLs from the seeder,  
# registered through the Liveness Radius contract (TBD).  
KEY_GENERATOR_ADDRESS="0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266"  # Please change this key generator address.

```

</details>
