# Encrypted Mempool

### **Encrypted Mempool for Trustless Sequencing**

Radius introduces a unique encrypted mempool solution for decentralization through trustless sequencing.

In this trustless sequencing model, transactions remain encrypted, keeping them encrypted from the sequencer until their order is determined. This approach ensures a fully trustless process, distinguishing it from traditional encrypted mempools where users must trust sequencers.

Here's a breakdown of the transaction handling process:

1. **Encryption**: Transactions are encrypted using a timelock puzzle.
2. **Order Commitment:** The sequencer determines the order of encrypted transactions for inclusion in the next block and issues an order commitment.
3. **Decryption**: The sequencer solves the timelock puzzle to decrypt the transactions.
4. **Sequencing**: Following the commitment, the sequencer constructs the block according to the predetermined order.

For details, refer to [encrypted mempool](https://docs.theradius.xyz/developer/encrypted-mempool) in the documentation.



### **Encrypted Mempool Open Source for Madara**

[Madara](https://www.madara.build/) is an open-source rollup stack for building scalable, modular Starknet appchains or L3. Madara plays a crucial role in the Starknet ecosystem as it allows for everyone to easily deploy their customized chains on top of Starknet.

Last year, we have open-source the encrypted mempool development for Madara stack. The introduction of the encrypted mempool for Madara is pivotal towards achieving decentralization in rollups. We invite Starknet and Madara developers to explore our open-sourced code on [GitHub](https://github.com/radiusxyz/madara) and refer to the guidelines on [ReadMe](https://github.com/radiusxyz/madara/blob/encrypted-mempool/docs/getting-started-with-encrypted-mempool.md) for using the encrypted mempool.

We are actively building the shared sequencing layer, built upon the foundation of the Radius encrypted mempool including trustless encryption. Our first testnet [Curie](https://twitter.com/radius\_xyz/status/1722570451237634049?s=20), demonstrated a successful implementation and functionality of the encrypted mempool.

Refer to our [blog](https://mirror.xyz/0x957084A1F20AB33cfA0cE07ed57F50c05954999C/I77x90l\_fyMjSnKjPuFtPymy153xlQXTjCeboQd08vA) for further details.
