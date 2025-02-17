---
description: Key Requirements, Architecture, Specifications, and Security
---

# Lighthouse Network

### 1. Key Requirements

#### User Protection

Lighthouse balances revenue generation with user protection through a **Top-of-Block (ToB) / Bottom-of-Block (BoB)** framework that allocates blockspace strategically:

Top-of-Block (ToB):&#x20;

* **Builder Revenue**: ToB provides builders with access to liquidity across rollups and Ethereum, unlocking strategic MEV opportunities to increase profits.
* **Rollup Revenue**: Builders compete in blockspace auctions, and this competition—enhanced by cross-rollup arbitrage—maximizes revenue for rollups.
* **Market Stability**: By enabling arbitrage between centralized and decentralized exchanges, Lighthouse helps minimize price disparities and stabilize the market.

Bottom-of-Block (BoB):&#x20;

* **User Safety**: BoB secures blockspace for regular user transactions, protecting them from harmful MEV practices like frontrunning and sandwich attacks, while ensuring censorship resistance.

#### Revenue Maximization

Lighthouse uses advanced auction mechanisms to optimize builder revenue:

* **Just-in-Time Auction**: Builders can make real-time profitability assessments.
* **Cross-Rollup Bundle Auction**: Winning a ToB auction allows builders to coordinate transactions across multiple rollups for consistent MEV capture and seamless atomic execution.

#### Governance Integrity

Lighthouse is designed to integrate smoothly with existing rollup governance frameworks without causing disruptions:

* **Flexible Auction Scheduling**: Adapts to the unique block production times of rollups, enabling broad, simultaneous support.
* **Custom Auction Cycles**: Divides Lighthouse operations into intervals that match rollup-specific governance and block production processes.

By addressing these requirements, Lighthouse promotes a unified, revenue-enhancing system that protects users while fostering a dynamic, competitive blockspace ecosystem.

***

### 2. Lighthouse Network Architecture

<figure><img src="../.gitbook/assets/image (26) (1).png" alt=""><figcaption></figcaption></figure>

Lighthouse runs trustless, permissionless auctions between rollups and builders, creating an open ecosystem for blockspace allocation. Builders can bid for the Top-of-Block (ToB) segment, capture MEV, and settle auction fees using L1 native tokens.

Each block in Lighthouse is divided into two distinct parts:

* **Top-of-Block (ToB)**
  * Transactions in ToB are secured through Lighthouse auctions.
  * Builders participate in permissionless auctions to secure ToB, optimizing MEV strategies such as backrunning arbitrage and CEX-DEX arbitrage.
  * Builders analyze the previous state of rollups to make informed bids, maximizing their potential returns. Once ToB rights are secured, they can achieve atomic execution across rollups, enhancing profitability.
* **Bottom-of-Block (BoB)**
  * Reserved exclusively for user transactions, ensuring secure and interference-free execution.
  * Secure Block Building (SBB) protects user transactions against censorship and harmful MEV.

The [**Secure Block Building**](../#secure-block-building-sbb-user-protection) component within each rollup manages ToB and BoB, distinguishing builder transactions from regular user transactions. Once a block is formed, the rollup tx\_orderer executes the entire block.

This balanced architecture benefits both builders and users: builders gain access to lucrative opportunities while users receive strong protections. Through Lighthouse’s trustless and decentralized auction system, rollups enjoy a sustainable revenue model that promotes a thriving market.

#### Entities

1. **Seller (`Proposer`)**
   * **Role**: The Proposer is an entity with the signing key responsible for submitting blocks.
   * **Responsibilities:** Includes the winning builder's transactions in the Top-of-Block (ToB) for the assigned slot.
   * **Block Creation**: The rollup tx\_orderer acts as the proposer, constructing the block by including the builder's bundle. The proposer ensures the block includes both ToB and BoB. Ultimately, the tx\_orderer is fully responsible for the final block content, managing the complete execution of transactions.
2. **Buyer (`Builder`)**:
   * **Role**: The Builder constructs the content of the block.
   * **Responsibilities:** Purchases the right to include transactions in ToB for a designated slot.
3. **Mediator (`Lighthouse`)**:
   * **Role**: Acts as the intermediary facilitating the auction process
   * **Responsibilities**: Ensures a secure and trustless contract between the seller (proposer) and buyer (builder).

#### Process Overview

1. **Seller Registration**:
   * The **Rollup Tx\_Orderer** registers as a seller by locking collateral on Layer 1 (L1).
   * **Bridge**: Lighthouse securely stores the Tx\_Orderer’s registration details.
2. **Blockspace Listing**:
   * The **Rollup Tx\_Orderer** lists blockspace for sale by registering with Lighthouse.
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
   * The **Rollup Tx\_Orderer** includes the ToB while generating the block.
7.  **Non-compliance Handling**:

    If the Rollup Tx\_Orderer fails to include the ToB:

    * **Bridge**: A **Slasher** forwards details (auction information, winning builder’s address, and ToB) from Lighthouse to L1
    * L1 reviews the Tx\_Orderer’s actions and, if necessary, enforces a penalty by slashing the Tx\_Orderer’s collateral.

***

### 3. Technical Specifications

#### Design

Lighthouse operates based on a set of design dimensions that shape the interaction between Rollup Tx\_Orderers and Builders. Each dimension influences the auction mechanics, participant experience, and overall efficiency of the Lighthouse ecosystem. Below are the design dimensions we considered, along with the choices we made and the rationale for each decision.

1. **Bidder Access Control: Permissioned / Permissionless**
   * **Choice:** **Permissionless**
   * **Rationale:** We chose a permissionless system to ensure that any participant can access the auction without requiring prior approval or authorization. This open approach increases competition and fosters a more decentralized ecosystem, and encourages diverse participation in MEV opportunities.
2. **Winner Selection: Highest Bid (Auction) / Lottery**
   * **Choice:** **Highest Bid (Auction)**
   * **Rationale:** Selecting the highest bid as the winner promotes a competitive environment where Builders are incentivized to bid their true valuation of blockspace. This approach maximizes revenue for Rollup Tx\_Orderers and aligns with our goal of creating an efficient and economically sustainable marketplace.
3. **Bid Time: After Previous State Disclosure / Before Previous State Disclosure**
   * **Choice:** **After Previous State Disclosure**
   * **Rationale:** Allowing bids to be placed after the previous state is disclosed provides Builders with the information they need to make informed bidding decisions. This transparency reduces uncertainty and allows Builders to optimize their MEV strategies based on the most recent data, ultimately improving the quality of bids.
4. **Bidder’s Fee Payment Method: Instant Payment with Winner Update and Refund / Prepayment with Refund / Postpayment**
   * **Choice:** **Instant Payment with Winner Update and Refund**
   * **Rationale:** Requiring instant payment at the time of bidding ensures the auction is efficiently settled, minimizing potential delays and reducing the risk of non-payment. This mechanism provides a clear and immediate commitment from Builders while allowing refunds for unsuccessful bids, streamlining the auction process.
5. **Winning Bidders per Slot: 1 (Bid for Entire ToB) / Multiple (Bid for Partial Space)**
   * **Choice:** **1 (Bid for Entire ToB)**
   * **Rationale:** By allowing a single winning bidder for the entire ToB, we simplify the auction structure and provide Builders with full control over the top blockspace. This approach optimizes MEV capture for Builders by allowing them to fully utilize the ToB, making it a more attractive and valuable position to bid for.
6. **Seller’s Previous State Disclosure Method: Data Availability (DA) / Tx\_Orderer Self-Disclosure with Builder Tool / Lighthouse (Broadcast Relay)**
   * **Choice:** **Tx\_Orderer Self-Disclosure with Builder Tool**
   * **Rationale:** Having the Tx\_Orderer directly disclose the previous state and provide a Builder tool enables efficient and direct access to state information. This setup reduces dependency on external relays and ensures that Builders have the tools necessary to interpret state data accurately, making it easier to participate in the auction effectively.
7. **Transaction Guarantee: Inclusion / Execution**
   * **Choice:** **Execution**
   * **Rationale:** We chose to guarantee both the inclusion and execution of transactions in the specified order. This level of assurance gives Builders confidence that their transactions will not only be included but also executed as intended, which is crucial for complex MEV strategies that rely on specific transaction sequencing.

By selecting these options, we have designed Lighthouse to support an open, efficient, and reliable blockspace marketplace. Each choice is intended to align with our goals of decentralization, transparency, and maximizing economic incentives, creating a robust platform for both Rollup Tx\_Orderers and Builders to interact in a trustless and decentralized manner.



<figure><img src="../.gitbook/assets/image (25) (1).png" alt=""><figcaption></figcaption></figure>

The diagram illustrates the sequence of actions and interactions between the **Tx\_Orderer**, **Lighthouse**, **Builder**, and **L1** contracts within the Lighthouse. The process is as follows:

1. **Auction Initiation**: The Tx\_Orderer begins by calling `startAuction()` on Lighthouse, initiating the auction process for blockspace.
2. **Auction Notification**: Lighthouse broadcasts the auction event, allowing Builders to listen for and participate in the auction.
3. **Bid Submission**: Builders submit bids via Lighthouse’s `bid()` function. Lighthouse records the bids and identifies the highest bidder.
4. **Winning Bid Record**: The highest bid is recorded in Lighthouse, and the winning Builder is notified.
5. **ToB Submission**: The winning Builder submits their transactions for the **Top of Block (ToB)** section to Lighthouse.
6. **Block Building**: Lighthouse notifies the Tx\_Orderer to include the ToB transactions, and the Tx\_Orderer constructs the block, incorporating the Builder's ToB.
7. **Slash Mechanism**: If the Tx\_Orderer fails to fulfill its obligations, the Builder can call `slashTxOrderer()` on L1, triggering a penalty (slashing) of the Tx\_Orderer’s collateral.

This diagram captures the core interactions and enforcements in Lighthouse, ensuring an efficient, secure, and transparent auction process for blockspace.

#### Contract overview

1. L1 Contracts
   1. `Asset Bridge Contract` : facilitates asset transfers between L1 and Lighthouse by locking and unlocking assets.
      1. `send`: Lock assets on L1 and transfers wrapped tokens to Lighthouse.
      2. `receive`: Unlocks wrapped tokens on Lighthouse and sends the equivalent assets back to L1 users.
   2. `Tx_Orderer Registry and Slashing Contract` : manages the registration, deregistration, and slashing of Tx\_Orderers to ensure accountability.
      1. `registerTxOrderer`: Registers a Tx\_Orderer by locking collateral.
      2. `deregisterTxOrderer`: Allows Tx\_Orderers to unregister, releasing locked collateral.
      3. `slashTxOrderer`: Slashes the collateral of a Tx\_Orderer if obligations are not met, enforcing penalties for non-compliance.
2. Lighthouse Contracts
   1. `Asset Bridge Contract` : mirrors the L1 Asset Bridge functionality, managing the minting and burning of wrapped tokens on Lighthouse.
      1. `receive`: Mints wrapped tokens on Lighthouse after assets are locked on L1.
      2. `send`: Burns wrapped tokens on Lighthouse to release equivalent assets back to L1.
   2. `Payment Token Contract` : manages payment tokens used in Lighthouse for auction transactions.
      1. `transfer`: Transfers payment tokens (e.g., wrapped ETH) within Lighthouse.
      2. `approve`: Grants permission to other contracts to use the tokens on behalf of the owner.
   3. `Blockspace Auction Management Contract` : manages the auctioning of blockspace, handling the bidding process and transaction submission.
      1. `registerTxOrderer`: Verifies and registers Tx\_Orderers eligible to participate in auctions.
      2. `deregisterTxOrderer`: Deregisters Tx\_Orderers, removing them from eligible participants.
      3. `startAuction`: Initializes an auction, defining parameters like auction ID, block height, duration, and bundle size.
      4. `bid`: Allows Builders to place bids, transferring payment tokens and updating the highest bid.
      5. `submitToB`: Records the transactions for the winning Builder’s ToB space.

#### The timing and sequence of actions

<figure><img src="../.gitbook/assets/image (23) (1).png" alt=""><figcaption></figcaption></figure>

Here’s a breakdown of each step in terms of timing:

1. **Auction Start Timing**:
   * Tx\_Orderer initiates the auction for the **Top of Block (ToB)** space in an upcoming rollup block (#3 in this example).
   * This auction begins after the completion of block #2, allowing Builders to prepare their bids in advance of block #3.
2. **Auction Process in Lighthouse (Bid Submission and Selection)**:
   * During this phase, Builders actively participate in the auction by submitting their bids for the ToB space in block #3.
   * The bid submission and selection happen concurrently, with Lighthouse evaluating bids in real-time to determine the highest bid, which will secure the ToB space.
3. **ToB Submission Timing**:
   * Once the auction concludes and a winning bid is selected, the chosen Builder submits their ToB transactions to Lighthouse.
   * This submission occurs before block #3 is finalized, ensuring that the winning transactions are available for inclusion in the top portion of the block.
4. **Block Building and Finalization**:
   * With the ToB transactions from the winning Builder, the Rollup Tx\_Orderer constructs block #3, positioning the Builder’s transactions at the top as specified.
   * This process completes the integration of the auctioned ToB, aligning with the timing and sequence requirements for Lighthouse.

***

### 4. Security

#### Threat models

In the Lighthouse, various entities participate in the auction and blockspace allocation process, each with potential vulnerabilities and risks. To maintain a secure and trustless environment, it is crucial to address the threat models associated with each entity involved: the Tx\_Orderer, Builder, and Mediator.

| Entity                | Threat models                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tx\_Orderer (Seller)  | <p>- Fails to include the transactions as agreed upon in the designated slot, violating the terms of the auction.<br>- Lacks legitimate authority over the slot it intends to sell, potentially resulting in invalid transaction processing.<br></p>                                                                                                                                                                                                                                                    |
| Builder (Buyer)       | - Does not fulfill the required bit payment, compromising the fairness and economic balance of the auction.                                                                                                                                                                                                                                                                                                                                                                                             |
| Mediator (Lighthouse) | <p>- Publishes invalid or incorrect information, leading to misinformation and potential exploitation by participants.<br>- Fails to execute the auction according to the established rules, undermining the trust in the auction process.<br>- Sells overlapping slots to different buyers, creating conflicts and issues in transaction inclusion and execution.<br>- Does not refund bids to participants who did not win the auction, leading to financial losses for non-winning Builders.<br></p> |

#### Mitigation Strategies

For each entity involved in the Lighthouse, specific reliability methods are implemented to mitigate the potential risks outlined in the threat models. These strategies are designed to ensure compliance, protect users, and maintain trust within the Lighthouse ecosystem.

1. Tx\_Orderer (Seller) Reliability Measures
   *   To ensure that the Tx\_Orderer fulfills its commitment to include the designated transactions in the assigned block, Lighthouse has implemented a collateral-based enforcement mechanism on L1. When a Tx\_Orderer is registered, it locks collateral on L1, which can only be withdrawn after a set block delay, preventing premature withdrawal.

       If the Tx\_Orderer fails to meet its obligations, a slashing mechanism is triggered. This mechanism verifies the Tx\_Orderer’s actions by comparing the finalized block information on L1 with the contract information on Lighthouse. If the Tx\_Orderer has violated its contract terms by omitting required transactions, its locked collateral is slashed. This approach ensures accountability and provides a strong financial disincentive against non-compliance, upholding the integrity of the Lighthouse.
2. Builder (Buyer) Reliability Measures
   *   To prevent unpaid bids, Lighthouse enforces real-time settlement of bid payments. Builders are required to fulfill the bid payment immediately upon placing a bid, ensuring that only financially committed bids are processed. This instant settlement mechanism eliminates the possibility of delayed or unpaid bids, maintaining the fairness of the auction and protecting against time-delay attacks.

       Additionally, any deviation in the Builder’s blockspace configuration or failure to submit transactions within the designated slot impacts only the Builder, as Lighthouse’s design isolates these risks, minimizing disruptions to the broader ecosystem.
3. Mediator (Lighthouse) Reliability Measures
   * Lighthouse is built with L1-grade security to prevent vulnerabilities and ensure a reliable auction process. Immutable smart contracts enforce established auction rules, delivering fair and transparent execution that sustains participant trust. Each slot is uniquely allocated to prevent overlapping sales, while an automated refund mechanism immediately returns bids to non-winning participants, safeguarding against financial losses and promoting a fair, trustworthy experience.
