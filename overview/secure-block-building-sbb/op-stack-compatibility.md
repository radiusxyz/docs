# OP Stack Compatibility

OP Stack's standard execution client (`op-geth`) strictly order transactions by priority fee (gas price).

However, SBB requires preconfirmation of inclusion order before the transaction contents are decrypted, meaning transactions must follow a first-come, first-served (FCFS) order based on the encrypted arrival time. This deterministic ordering logic is fundamentally incompatible with the OP Stack’s default `tx_list` block production mechanism.

**To maintain compliance and alignment with the Superchain, and avoid modifying core OP Stack logic, we integrate SBB using a specialized sidecar architecture (**&#x52;ollup Boost + a modified `rBuilder`).

***

#### SBB Integration: Rollup-Boost + rBuilder Sidecar

Our integration solution leverages Flashbots' Rollup-Boost technology alongside a custom rBuilder implementation.

* **Rollup-Boost**: This functions as a bridge between OP Stack's `op-node` and `op-geth`, preserving canonical interfaces.
* **rBuilder**: This is the external, modular block builder that incorporates SBB's logic. It is modified to incorporate SBB's cryptographic ordering constraints (FCFS pre-confirmation logic) when constructing the transaction payload.

This sidecar integration ensures we can fully support SBB while maintaining full alignment with Superchain governance and upgrade paths.

