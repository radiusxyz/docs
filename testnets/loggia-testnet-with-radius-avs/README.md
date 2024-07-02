# Loggia Testnet With Radius AVS

The testnet describes the process of applying the Decentralized Sequencing function using Radius AVS within the Rollup framework and its subsequent operations.

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption><p>Architecture Overview</p></figcaption></figure>

In the Radius structure, Decentralized Rollup is organized as shown in the accompanying diagram. Rollup consists of the Proposer, which includes a decentralized Sequencer Set that sequences transactions from users, and the Full Node that receives and executes blocks from the Proposer.

Radius AVS operates after the Rollup Developer configures it, taking into account factors like the Proposer's setup and the Rollup block creation time. Before any processes begin, the Rollup Developer must directly manage a Full Node, which includes an adapter to interact with the Proposer.
