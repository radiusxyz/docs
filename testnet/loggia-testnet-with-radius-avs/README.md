# Loggia Testnet with Radius AVS

Radius launches Loggia Testnet, offering decentralized sequencing for rollups. Powered by Radius AVS (Actively Validated Services) built on Eigenlayer, Loggia enables rollups to achieve censorship resistance, while economically securing sequencing liveness and block safety with restaked ETH.

<figure><img src="../../.gitbook/assets/image (20) (1).png" alt=""><figcaption><p>Architecture Overview</p></figcaption></figure>

A decentralized rollup includes the following components:

* Proposer: A decentralized sequencer set responsible for ordering transactions.
* Full Node: Receives and executes blocks from the proposer.

Developers can configure Radius AVS by considering the proposer's setup and the rollup block creation time. Initially, rollups must run their own full node, which includes an adapter to interact with the proposer.
