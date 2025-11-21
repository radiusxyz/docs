# OP Stack Compatibility

### &#x20;SBB with Rollup-Boost + rBuilder

* OP Stack’s `op-geth` orders transactions strictly by gas price.
* However, SBB requires pre-confirmation of inclusion order before decryption, meaning transactions must follow a **first-come, first-served (FCFS)** sequence based on the encrypted arrival time.
* This deterministic ordering logic is **incompatible with the OP Stack’s default `tx_list` construction**.
* To avoid modifying core OP Stack core logic, we use a **sidecar** with Rollup Boost + a modified `rBuilder`.

***

### Why Rollup-Boost Ensures Superchain Compatibility

* Rollup-Boost acts as a bridge between `op-node` and `op-geth`, preserving canonical interfaces.
* It enables modular Builder integration (i.e., `rBuilder`) **without altering protocol logic**.
* This allows us to support custom ordering and payload logic **while remaining aligned with OP Stack standards**.
* As a result, SBB is **fully compatible with Superchain governance and upgrades**.

