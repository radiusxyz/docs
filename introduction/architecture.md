# Architecture

#### 1. User Protection

Lighthouse balances revenue generation with user protection through a **Top-of-Block (ToB) / Bottom-of-Block (BoB)** framework that allocates blockspace strategically:

**Top-of-Block (ToB)**

* **Builder Revenue**: ToB provides builders with access to liquidity across rollups and Ethereum, unlocking strategic MEV opportunities to increase profits.
* **Rollup Revenue**: Builders compete in blockspace auctions, and this competition—enhanced by cross-rollup arbitrage—maximizes revenue for rollups.
* **Market Stability**: By enabling arbitrage between centralized and decentralized exchanges, Lighthouse helps minimize price disparities and stabilize the market.

**Bottom-of-Block (BoB)**

* **User Safety**: BoB secures blockspace for regular user transactions, protecting them from harmful MEV practices like frontrunning and sandwich attacks, while ensuring censorship resistance.

#### 2. Revenue Maximization

Lighthouse uses advanced auction mechanisms to optimize builder revenue:

* **Just-in-Time Auction**: Builders can make real-time profitability assessments.
* **Cross-Rollup Bundle Auction**: Winning a ToB auction allows builders to coordinate transactions across multiple rollups for consistent MEV capture and seamless atomic execution.

#### 3. Governance Integrity

Lighthouse is designed to integrate smoothly with existing rollup governance frameworks without causing disruptions:

* **Flexible Auction Scheduling**: Adapts to the unique block production times of rollups, enabling broad, simultaneous support.
* **Custom Auction Cycles**: Divides Lighthouse operations into intervals that match rollup-specific governance and block production processes.

By addressing these requirements, Lighthouse promotes a unified, revenue-enhancing system that protects users while fostering a dynamic, competitive blockspace ecosystem.

***

## Architecture

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption><p>Lighthouse Architecture</p></figcaption></figure>

Lighthouse runs trustless, permissionless auctions between rollups and builders, creating an open ecosystem for blockspace allocation. Builders can bid for the Top-of-Block (ToB) segment, capture MEV, and settle auction fees using L1 native tokens.

Each block in Lighthouse is divided into two distinct parts:

* **Top-of-Block (ToB)**
  * Transactions in ToB are secured through Lighthouse auctions.
  * Builders participate in permissionless auctions to secure ToB, optimizing MEV strategies such as backrunning arbitrage and CEX-DEX arbitrage.
  * Builders analyze the previous state of rollups to make informed bids, maximizing their potential returns. Once ToB rights are secured, they can achieve atomic execution across rollups, enhancing profitability.
* **Bottom-of-Block (BoB)**
  * Reserved exclusively for user transactions, ensuring secure and interference-free execution.
  * Secure Block Building (SBB) protects user transactions against censorship and harmful MEV.

The [**Secure Block Building**](../#secure-block-building-sbb-user-protection) component within each rollup manages ToB and BoB, distinguishing builder transactions from regular user transactions. Once a block is formed, the rollup sequencer executes the entire block.

This balanced architecture benefits both builders and users: builders gain access to lucrative opportunities while users receive strong protections. Through Lighthouse’s trustless and decentralized auction system, rollups enjoy a sustainable revenue model that promotes a thriving market.

***

#### Entities

1. **Seller (`Proposer`)**
   * **Role**: The Proposer is an entity with the signing key responsible for submitting blocks.
   * **Responsibilities:** Includes the winning builder's transactions in the Top-of-Block (ToB) for the assigned slot.
   * **Block Creation**: The rollup sequencer acts as the proposer, constructing the block by including the builder's bundle. The proposer ensures the block includes both ToB and BoB. Ultimately, the sequencer is fully responsible for the final block contnet, managing the complete execution of transactions.
2. **Buyer (`Builder`)**:
   * **Role**: The Builder constructs the content of the block.
   * **Responsibilities:** Purchases the right to include transactions in ToB for a designated slot.
3. **Mediator (`Lighthouse`)**:
   * **Role**: Acts as the intermediary facilitating the auction process
   * **Responsibilities**: Ensures a secure and trustless contract between the seller (proposer) and buyer (builder).

#### Process Overview

1. **Seller Registration**:
   * The **Rollup Sequencer** registers as a seller by locking collateral on Layer 1 (L1).
   * **Bridge**: Lighthouse securely stores the Sequencer’s registration details.
2. **Blockspace Listing**:
   * The **Rollup Sequencer** lists blockspace for sale by registering with Lighthouse.
   * Lighthouse verifies the seller’s details and publicly shares the details of available slots.
3. **Buyer Registration**:
   * **Builders** deposit auction fees into Lighthouse to participate.
   * **Bridge**: Assets are locked on L1 and transferred to Lighthouse.
4. **Bid Submission**:
   * **Builders** compete for ToB space by submitting their bids through Lighthouse.
   * Lighthouse verifies all bids, selects the highest, and announces the winning Builder.
5. **ToB Submission**:
   * The winning **Builder** constructs the ToB and submits it to Lighthouse.
6. **Block Creation**:
   * The **Rollup Sequencer** includes the ToB while generating the block.
7.  **Non-compliance Handling**:

    If the Rollup Sequencer fails to include the ToB:

    * **Bridge**: A **Slasher** forwards details (auction information, winning builder’s address, and ToB) from Lighthouse to L1
    * L1 reviews the Sequencer’s actions and, if necessary, enforces a penalty by slashing the Sequencer’s collateral.

***

