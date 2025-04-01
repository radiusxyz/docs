# Run Seeder

Repository: [Seeder GitHub](https://github.com/radiusxyz/seeder.git)

1.  Clone the repository:

    <pre class="language-bash"><code class="lang-bash"><strong>git clone https://github.com/radiusxyz/seeder
    </strong></code></pre>
2.  Build the binary

    ```sh
    cd seeder
    cargo build --release
    ```
3. Set up environment variables in `./scripts/execute/env.sh`.
4.  Initialize the Seeder:

    ```bash
    ./scripts/execute/01_init_seeder.sh
    ```
5.  Start the Seeder:

    ```bash
    ./scripts/execute/02_run_seeder.sh
    ```
6. Set up environment variables in `./scripts/rpc-call/env.sh`.
7.  Initialize RPC: This action serves for is **r**egistering sequencing information related to the LivenessServiceManager

    <pre class="language-bash"><code class="lang-bash"><strong>./scripts/rpc-call/10_initialize.sh
    </strong></code></pre>

**Environment Variables**

<details>

<summary>seeder/scripts/execute/env.sh</summary>

```sh
#!/bin/bash
CURRENT_PATH="$( cd -- "$(dirname "$0")" >/dev/null 2>&1 ; pwd -P )"
PROJECT_ROOT_PATH="$( cd $SCRIPT_PATH/../.. >/dev/null 2>&1 ; pwd -P )"

BIN_FILE_NAME="seeder"
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

# Used by transaction orderers to register their IP addresses  
# and retrieve the IP addresses of peers when they register  
# in the LivenessServiceManager contract.  
SEEDER_EXTERNAL_RPC_URL="http://127.0.0.1:6000"  

# Used by the network owner to add sequencing information,  
# including the RPC and WebSocket URLs for interacting with  
# the LivenessServiceManager contract, the contract address itself, and  
# the platform with the service provider.  
SEEDER_INTERNAL_RPC_URL="http://127.0.0.1:6001"  
```

</details>

<details>

<summary><strong>seeder/scripts/rpc-call/env.sh</strong></summary>

{% code overflow="wrap" %}
```sh
#!/bin/bash

# Used by the network owner to add sequencing information,  
# including the RPC and WebSocket URLs for interacting with  
# the liveness contract, the contract address itself, and  
# the platform with the service provider.  
SEEDER_INTERNAL_RPC_URL="http://127.0.0.1:6001"  # Internal IP - Please change this IP.

# Used as parameters for registering liveness-related data  
# through the internal RPC URL.  
LIVENESS_PLATFORM="ethereum"  # Option: [ethereum]  
LIVENESS_SERVICE_PROVIDER="radius"  # Option: [radius]  
LIVENESS_RPC_URL="http://127.0.0.1:8545"  # Please change this IP.  
LIVENESS_WS_URL="ws://127.0.0.1:8545"  # Please change this IP.  
LIVENESS_CONTRACT_ADDRESS="0x0000000000000000000000000000000000000000"  # Please change this liveness contract address.  
```
{% endcode %}

</details>
