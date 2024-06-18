# Introduction

This document provides a detailed explanation of the Radius shared sequencing layer, focusing on the roles of entities involved in processing transactions. The explanation is structured into sections detailing the entities involved and their interactions.

Let’s start starting with an overview of the transaction flow.

#### **User:**

1. Generates an encryption key through a time-lock puzzle and encrypts the transaction symmetrically.
2. Sends the encrypted transaction, along with the time-lock puzzle and a zero-knowledge proof (zk-proof), to the sequencer. The zk-proof ensures that the sequencer can derive the decryption key by solving the time-lock puzzle, enabling the decryption of the transaction.

#### **Sequencing Layer:**

1. Validates the zk-proof to confirm the transaction's validity.
2. Orders transactions. Transactions remain encrypted at this stage, pending decryption key access through the time-lock puzzle solution.
3. Issues an order-commitment (pre-confirmation) to the user.
4. After obtaining the decryption key by solving the time-lock puzzle, decrypts the transactions and collects them into a block according to protocol.
5. Transmits the block to the rollup operator.

#### **Rollup Operator:**

1. Acquires the block from the sequencer.
2. Executes the transactions in the specified order.
3. Based on the rollup model, either submits the updated state and state proof or a list of transactions to the settlement layer.

#### **Settlement Layer:**

1. Reviews the submitted state and state proof from the rollup, validating the proof to confirm the state.

This explanation breaks down the complex transaction process into understandable parts, showing how each component contributes to the system's overall function.
