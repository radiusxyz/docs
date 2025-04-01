# Quick Start

### Overview

This document provides guidance on setting up and running four main components:

1.  **Seeder**

    Repository: [Seeder GitHub](https://github.com/radiusxyz/seeder.git)
2.  **Key Management System**

    Repository: [Distributed Key Generation GitHub](https://github.com/radiusxyz/distributed_key_generation)
3.  **Secure RPC**

    Repository: [Secure RPC GitHub](https://github.com/radiusxyz/secure-rpc.git)
4.  **Sequencer**

    Repository: [Sequencer GitHub](https://github.com/radiusxyz/sequencer.git)

    _**Note**:_ A cluster is a group of sequencers with a leader. This process can run with a single sequencer as well. Do not be confused by the `.env` variables referencing clusters.

### Key Details

* **Language and Build Requirements:** All components are written in Rust and must be built using `cargo build --release` in the root directory of each repository.
* **Environment Variables:**
  * Create an `env.sh` file at `<repository>/scripts/execute/env.sh` based on the contents of `env_example.sh`.
  * Ensure the ports defined in `env.sh` are available.
  * Shared variables across components must have consistent values.
  * Another `env.sh` is needed at `<repository>/scripts/rpc-call/env.sh` for RPC-related scripts, also derived from `env_example.sh`.
* **Initialization Scripts:**
  * Each component is initialized and run using scripts located in the repository:
    * `<repository>/scripts/execute/01_init_....sh`
    * `<repository>/scripts/execute/02_run_....sh`
* **Inter-Component Integration:**
  * Some components require registration with others via JSON RPC calls to internal RPC URLs. The necessary scripts are found in `<repository>/scripts/rpc-call`, except for the Secure RPC component, which does not require this step.

***
