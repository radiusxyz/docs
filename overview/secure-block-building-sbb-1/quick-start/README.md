# Quick Start

Out of all the components of SBB, only two are likely to be run by most users:

1. **Tx\_Orderer** – This component is responsible for ordering transactions, providing order commitments for users, block commitments for block validation, and delivering blocks(raw transaction lists) to rollup operators.
2. **Secure RPC** – This component receives raw transactions from clients/wallets and formats them in a way that is acceptable to the tx\_orderers.

Radius provides a Secure RPC service, but since it involves trust, clients should have the option to run their own.

You can run both the tx\_orderer and Secure RPC by following the instructions on the next two pages. For more details, please refer to the relevant section.
