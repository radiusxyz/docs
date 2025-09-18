# Alpha Engine by Radius, Symbiotic, Avail

## **1. Introduction**

#### **1.1 The Challenge of Sustainable Rollup Growth**

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Rollups have improved Ethereum’s scalability by executing transactions off-chain while maintaining Ethereum’s security. However, deploying a rollup is not enough to ensure long-term sustainability. Key challenges include:

* **Revenue Instability:** Transaction fees alone are unpredictable and insufficient.
* **High Security Costs:** Robust security requires significant capital.
* **Network Fragmentation:** Limited interoperability leads to isolated ecosystems.
* **Liquidity Barriers:** Acquiring liquidity is competitive.
* **User Onboarding Complexity:** Poor user experiences hinder adoption.
* **Diverse, Costly Infrastructure:** Selecting tailored infrastructure is challenging.

#### 1.2 What is Alpha Engine?

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Alpha Engine is a modular infrastructure stack designed to support the **sustainable growth of rollups**. It integrates three key components:

* **Radius (MEV capture):**
  * [Lighthouse](../overview/lighthouse/) enables rollups to capture and internalize MEV (Maximal Extractable Value), turning it into a new revenue source beyond transaction fees.
  * This revenue can incentivize users, subsidize projects, and fuel ecosystem growth.
* **Symbiotic (Shared Security Protocol):**
  * [Symbiotic protocol](https://blog.symbiotic.fi/symbiotic-intro/) provides a flexible, sovereign security layer that rollups can integrate plug-and-play solution without building in-house solutions.
  * Allows tailored security collaborations across networks.
* **Avail (High-Throughput Data Availability):**
  * [Avail DA](https://www.availproject.org/da) supplies scalable, verifiable data availability at low costs, critical for high-throughput operations.
  * [Avail Nexus](https://blog.availproject.org/the-avail-vision-accelerating-the-unification-of-web3/#avail-nexus) enables cross-chain transactions between Avail-powered rollups, enhancing interoperability, liquidity, and user onboarding by connecting fragmented ecosystems.

In addition, Symbiotic infrastructure providers (Networks) and Fuel partners of Alpha Engine contribute to delivering a comprehensive solution for economic sustainability, security, and interoperability.

***

## **2. Alpha Engine Components**

### 2.1. Radius : SBB & Lighthouse

Radius enables **rollups to capture MEV revenue** with Secure Block Building(SBB) and Lighthouse.

#### 2.1.1 [Lighthouse](../overview/lighthouse/): Cross-rollup MEV capture

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

[Lighthouse](../overview/lighthouse/) is a decentralized network that runs auctions to monetize rollup blockspace during block production. Rollups offer blockspace, and searchers bid to include MEV transactions—such as arbitrage and liquidations—that enhance market efficiency.

* **Expanded MEV Market**: Enables cross-rollup arbitrage and L1-L2 arbitrage, alongside CEX-DEX arbitrage, atomic arbitrage, and liquidations.
* **Higher Revenue**: Increases MEV opportunities to attract more searchers while auction mechanisms minimize spam, resulting in higher bids and greater rollup profits.
* **Aligned Incentives**: Distributes MEV profits between rollups and searchers through a transparent and competitive system.

{% hint style="info" %}
_Lighthouse seamlessly connects to rollups via Secure Block Building (SBB). Once rollups integrate SBB, no extra work is needed to integrate Lighthouse. This guide walks through SBB integration._
{% endhint %}

#### **2.1.2** [**Secure Block Building (SBB)**](../overview/secure-block-building-sbb/)**: User-safe MEV Capture**

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

[Secure Block Building (SBB)](../overview/secure-block-building-sbb/) enhances L2 block building to capture MEV, collaborating with searchers to increase revenue.

SBB provides three key benefits:

* **More Revenue**: Works with searchers to capture MEV. This creates a flexible revenue stream that adapts to market conditions and scales with rollup adoption beyond transaction fees.
* **User Safety**: Stops harmful MEV practices like frontrunning and sandwich attacks using one-second encryption and proof generation. This keeps user transactions secure while letting rollups profit from MEV.
* **Easy Integration**: Fits into existing rollup frameworks without added complexity. It’s a simple way to increase revenue.

### 2.2 Symbiotic: Shared Security Protocol

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Symbiotic is a [**shared security protocol**](https://blog.symbiotic.fi/symbiotic-intro/) that enables rollups to retain full control over their security implementations which includes management of collateral assets, operator selection, and slashing mechanisms.

Rollup developers can leverage **Symbiotic's slashable, restaked assets** to secure their rollups efficiently. By utilizing **Symbiotic network services**, developers can bring applications to market more quickly and cost-effectively. The process works as follows:

1. **User Deposits:** Users deposit funds into Symbiotic vaults.
2. **Economic Security for Rollups:** Rollup developers use these assets to secure their rollups, with slashing mechanisms in place to penalize misbehavior.
3. **Fee Distribution:** Rollups pay fees(rewards) for these services, which Symbiotic redistributes to token stakers.

#### 2.2.1 Core Participants

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

* **Stakers** - Entities looking to earn rewards by providing their assets as a stake through vault deposits. They can be individual token holders, institutions, or liquid (re)staking protocols. Stakers deposit funds into specialized smart contracts (vaults) managed by curators who handle delegation decisions.
* **Networks** - Systems that need economic security to operate safely. These can be Layer 1 blockchains, Layer 2 solutions, or other decentralized systems that require stake-based security guarantees. Currently, Symbiotic’s infrastructure providers(a.k.a. Networks) includes [**Radius**](https://www.theradius.xyz) and the following.
  * [RedStone](https://x.com/redstone_defi), [Hyve DA](https://x.com/Hyve_DA), [Capx Cloud](https://x.com/0xCapx), [Kalypso](https://x.com/KalypsoProver), [Drosera](https://x.com/KalypsoProver), [Cycle Network](https://x.com/cyclenetwork_GO), and [Ditto](https://x.com/Ditto_Network)
* **Operators** - Professional entities that maintain network infrastructure by running validators, nodes, or other required systems. They receive stake allocations to perform their duties and are responsible for network operations.

### 2.3 Avail: Avail DA & Avail Nexus

#### 2.3.1 [Avail DA](https://blog.availproject.org/avails-core-features-explained/): Scalable Data Availability Layer

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

[Avail’s DA Layer](https://docs.availproject.org/docs/the-avail-trinity/avail-da?ref=blog.availproject.org) is a decentralized blockchain network. It produces and secures blockspace that other blockchains can use as their own ‘pluggable’ data availability layer.

Using a dedicated AppID, blockchains publish transaction data to Avail which gets committed and made available.

* Avail’s data availability blockchain can support any blockchain network.
* The data published on Avail’s blocks is validated by the Avail network, but not executed.
* After block finalization by validator, validity proofs guarantee immediate data availability.
* Developers and users can verify data availability independently by using validity proofs.
* Avail applies erasure encoding to published data, generating extra pieces for redundancy and ensuring recoverability even if some parts are lost.
* Avail embeds data footprints in the Avail block headers using KZG commitments.
* Avail’s nominated proof of stake (NPoS) blockchain was built using the Polkadot SDK, and it will support up to 1,000 external validators.

#### 2.3.2 [Avail Nexus](https://blog.availproject.org/the-avail-vision-accelerating-the-unification-of-web3/): Cross-Rollup Interoperability

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

The ability to easily spin up rollups means there will be thousands of rollups. That means, the end-user experience of interacting with these rollups will be fragmented. Blockchain user's experience already suffers in the multichain world with a few chains and by increasing the number further without having fundamental changes in composability will lead to even bigger issues. **That is why Avail is building Avail Nexus, which acts as the verification hub unifying the rollups, using Avail DA as the root of trust.**

[Avail Nexus](https://docs.availproject.org/docs/the-avail-trinity/avail-nexus?ref=blog.availproject.org) is a custom ZK coordination rollup on top of Avail that consists of:

* Proof aggregation and verification layer
* Sequencer selection/slot auction mechanism

Nexus also submits the aggregated proof periodically to Ethereum and the Avail DA layer for verification. A custom module within Avail DA verifies the aggregate proof.

#### 2.3.3 Avail Fusion

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

A unifying layer needs unified security. The biggest value proposition for spinning up a new rollup rather than creating a separate L1 is the ability to inherit security from the base layer. For Avail to be the web3 coordination layer, it needs to be extremely secure - as the crypto-economic guarantees along with cryptographic ones will ultimately define the Avail ecosystem.

To cater to that, we are developing [Fusion Security](https://docs.availproject.org/docs/the-avail-trinity/avail-fusion?ref=blog.availproject.org), which takes the native assets of the most mature ecosystems such as BTC, ETH and more and allows them to contribute to the Avail consensus. Not only that, it allows the new rollup tokens to also play a role in securing the base layer which empowers them.

***

## **3. Integrated System Architecture & Data Flow**

### 3.1 Architecture Overview

#### 3.1.1 Supported Rollup Stacks

|            | Polygon CDK | OP Stack | Orbit | ZKSync |
| ---------- | ----------- | -------- | ----- | ------ |
| **Radius** | O           | O        | TBD   | TBD    |
| **Avail**  | O           | O        | O     | O      |

Avail DA offers a plug-and-play solution compatible with all major rollup stacks, including Polygon CDK, [OP Stack](https://docs.availproject.org/docs/build-with-avail/deploy-rollup-on-avail/Optimium/op-stack), [Orbit](https://docs.availproject.org/docs/build-with-avail/deploy-rollup-on-avail/Optimium/arbitrum-nitro/overview), and [zkSync](https://docs.availproject.org/docs/build-with-avail/deploy-rollup-on-avail/Validium/zksync/zksync). Comprehensive integration guides are available for each stack.

Radius currently supports Polygon CDK and OP Stack, and integration guides are available upon request.

#### 3.1.2 Integration Options

The system can be deployed in various configurations based on project requirements:

* **Radius X Symbiotic X Avail**: Full integration with MEV capture, data availability, cross-rollup interoperability, and economic security.
* **Radius X Symbiotic**: MEV capture, and economic security without Avail DA/Nexus.
* **Symbiotic X Avail**: Data availability, cross-rollup interoperability, and economic security without MEV capture.

This document focuses on two real-world cases: **Radius X Symbiotic X Avail** and **Radius X Symbiotic**.

### 3.2 Fully Integrated System (Radius X Symbiotic X Avail)

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

#### 3.2.1 Radius with Symbiotic

Maximal Extractable Value (MEV) is a additional revenue source for rollups but is often harmful to users when exploited through frontrunning and sandwich attacks. A robust MEV capture model must protect users while enabling sustainable value extraction.

Radius proposes two core components to address this: SBB and Lighthouse. Among these, SBB utilizes the Symbiotic Security Protocol to support secure decentralized ordering. In this architecture:

* Vaults stake user-delegated funds to Operators, providing security to the network.
* Operators run the SBB TX Orderers, earning rewards for maintaining transaction integrity.
* Slashing mechanisms automatically penalize Operators for malicious behavior, ensuring honest participation.

Since close coordination between Operators and Vaults is essential for secure and efficient operations, contractual agreements are typically established. While Rollups can independently source both Operators and Vaults when using the Radius Network (SBB & Lighthouse), Radius also offers comprehensive support for Rollups that encounter difficulties in sourcing these components.

#### 3.2.2 Avail with Symbiotic

Integrating Symbiotic with Avail’s modular data availability network, offers [validity proofs](https://blog.availproject.org/avails-core-features-explained/#validity-proofs) and [data availability sampling](https://blog.availproject.org/avails-core-features-explained/#data-availability-sampling-das), making the launch of blockchain apps and services that are trust minimized, publicly verifiable and game theoretically robust far less complicated. It’s a powerful combination, enabling builders to sharply accelerate their go-to-market and significantly reduce development costs.

It also introduces a new class of innovative, validated services within the Avail network to provide critical services for a future built on horizontally scalable blockchains. These validated services can cover everything from custom intent networks, insurance networks, policy engines, computation engines, coprocessors, validation and sequencing services, and a whole lot more.

Symbiotic's modular architecture allows for rapid development and seamless integration with existing systems. By pairing Symbiotic with Avail's native staking mechanism, Fusion becomes truly asset agnostic, enabling a diverse range of cryptocurrencies to participate in securing the network. This approach not only strengthens the overall security by distributing risk across multiple assets but also enhances the economic resilience of the Avail ecosystem. The flexibility of Symbiotic's framework allows Fusion to dynamically adjust its security parameters based on market conditions and network requirements. This adaptability ensures that Avail can maintain optimal security levels and handle any external conditions.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Avail's integration showcases how Symbiotic can be seamlessly integrated into any protocol at any stage of development:

* **Enhancing the Fusion Security Layer**: Symbiotic enables Avail Fusion to pool different tokens, including established assets like ETH and BTC, to bolster the overall security of the Avail network.
* **Complementing the Unification Stack**: Symbiotic’s modular design allows Avail to integrate shared security exactly where it's needed, complementing the DA layer and Nexus aggregation layer.
* **Future-Proofing Security**: As Avail's ecosystem grows, Symbiotic's flexible framework can easily adapt to secure new components and include new assets.

#### 3.2.3. Data Flow Overview

1. **User Encryption**: Users encrypt transactions in-browser using Radius-provided sample code or Secure-RPC, ensuring protection from censorship, frontrunning, and reordering.
2. **Transaction Ordering**: Multiple TX Orderers provide cryptographic preconfirmation of transaction inclusion, preventing manipulation.
3. **Decryption and Execution**: The SBB Plugin requests transaction lists from TX Orderers. Transactions are decrypted using DKG-generated keys and forwarded to the Rollup Executor.
4. **Proof Aggregation and Storage**: The Executor aggregates proofs via the Avail Plugin and submits them to Avail Nexus. Proofs are stored on Ethereum and Avail DA, ensuring low-cost verification and enabling interoperability across multiple rollups.

***

## 4. Nitro Program

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Nitro is an initiative designed to accelerate rollup adoption by leveraging the Alpha Engine. It enables rollups to access various ecosystem incentives, driving growth in total value locked (TVL) and user adoption.

#### **4.1 Incentive Structure**

The incentive structure is tiered based on the number of Alpha Engine cores adopted by the rollup. The three key cores are:

* **Radius: Lighthouse & SBB**
* **Symbiotic: Shared Security Protocol**
* **Avail: DA & Avail Nexus**

Rollups that adopt the full stack of Alpha Engine cores receive higher incentives, encouraging comprehensive integration and maximizing benefits for user acquisition and ecosystem growth.

#### **4.1.1 Tier Breakdown**

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

**Tier 1 (50% of Total Incentives)**

* **Eligibility:** Rollups using all three cores (Radius, Symbiotic, Avail).
* **Key Advantage:** Full-stack adoption leads to maximum incentives, promoting user growth and network effects.
* **Current Candidates:** Fuse, CapX, Ternoa.

**Tier 2 (30% of Total Incentives)**

* **Eligibility:** Rollups using any two cores, with the following combinations:
  1. Symbiotic + Avail
  2. Radius + Avail
  3. Symbiotic + Radius
* **Incentive Distribution:**
  * Avail supports combinations (1) and (2).
  * Radius supports combinations (2) and (3).

**Tier 3 (20% of Total Incentives)**

* **Eligibility:** Rollups using only one core.
* **Incentives:** Allocated based on the specific core utilized.

#### 4.1.2 Most Optimal Case for Tier 1 Rollup

**Scenario:** A rollup utilizing all three cores (Radius, Symbiotic, Avail), integrated with Symbiotic Networks and Nucleus.

* A user of rollup will be able farm all these incentives at once by conducting two actions
  1. Depositing ETH (diverse form) through Nucleus into the rollup.
  2. Depositing stAvail into Rollup
* Rollup will be able to attract more users / TVL by utilizing these incentives based on their own criteria.
  * Bridge, Trading Volume, Txs and etc.
* Once rollups acquire meaningful number of users / TVL, they can leverage Alpha Engine at its maximum.
  * Acquire users from Incentives → Utilize Alpha Engine to provide best value → attract more users (Positive flywheel)
  * Depositing ETH (diverse form) through Nucleus into the rollup.
  * Depositing stAvail into Rollup

***

## 5. Real world use cases

### **5.1 Fuse : Full Integration with Radius, Symbiotic, and Avail**

[Fuse](https://www.fuse.io/) provides a blockchain-based financial infrastructure for small-to-medium-sized businesses (SMBs) and emerging markets. It is designed to improve accessibility and efficiency, particularly for those underserved by traditional financial systems.

Fuse have worked on breaking down the barriers that keep many businesses and individuals locked out of the global financial system, paving the way for a decentralized, borderless, and fair economy. The latest upgrade increases scalability, moving toward a target of 9,000 TPS to approach VISA’s transaction processing capacity in web2 environments.

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

Fuse utilizes the combined capabilities of **Radius**, **Symbiotic**, and **Avail**, positioning it as a **1st Tier** network in the **Nitro system**. The integration includes:

* **Radius**: By using **SBB**, Fuse captures MEV revenue through backrunning arbitrage and distributes it to its stakers.
* **Symbiotic Security Protocol**: Ensures validator integrity through staking and slashing mechanisms.
* **Avail**: **Avail DA** for efficient data availability, making zkEVM payments cheaper and more scalable.

#### **5.1.1 Data Flow Overview**

The data flow in Fuse’s L2 network mirrors the standardized process used by Tier 1 rollups, as described in Section 3.2.3.

#### 5.1.2 Incentive Flow

Symbiotic points are transferred to the Network, not directly to Rollups. In this context, they are sent to Radius, which then forwards both its own points and Symbiotic points to fuse. Since fuse is also integrated with Avail, The incentive provided by Avail will be sent to fuse as well.

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

### 5.2 Silicon : Integration with Radius, Symbiotic, and Ethereum L1

[**Silicon**](https://silicon.network/) is designed to address Ethereum’s scalability challenges by leveraging rollup technology. It aggregates multiple transactions off-chain and settles them on Ethereum mainnet as a single batch, thereby:

* **Increasing throughput** by processing more transactions per second.
* **Reducing gas fees** by lowering the cost per transaction.
* **Maintaining security** by inheriting Ethereum's base-layer security guarantees.

#### **5.2.1 Key Partnerships**

* **Ozys**: Provides technical expertise and development support. Ozys is known for blockchain infrastructure solutions and cross-chain protocols like Orbit Bridge.
* **Korbit**: As one of Korea’s leading crypto exchanges, Korbit’s involvement is expected to facilitate integration between Silicon and trading platforms, enhancing user access and liquidity.

#### **5.2.2 Integration with Radius and Symbiotic**

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Silicon is based on Polygon CDK, and fully integrated with **Radius** and **Symbiotic**, operating as a **second-tier rollup** within the **Nitro system**. The integration includes:

* **Radius**: By using SBB, Silicon captures MEV revenue through backrunning arbitrage wㅍhile providing MEV protection and decentralized ordering through the SBB component.
* **Symbiotic Security Protocol**: Secures validator integrity via staking and slashing mechanisms.

#### **5.2.3 Data Flow Overview**

The data flow in Silicon’s L2 network mirrors the standardized process used by Symbiotic-Radius-integrated rollups:

1. **User Transaction Encryption**: Users encrypt transactions in-browser using Radius-provided sample code or Secure-RPC, ensuring protection from censorship, frontrunning, and reordering.
2. **Transaction Ordering**: Multiple TX Orderers provide cryptographic preconfirmation of transaction inclusion, preventing manipulation.
3. **Decryption and Execution**: The SBB Plugin requests transaction lists from TX Orderers. Transactions are decrypted using DKG-generated keys and forwarded to the Rollup Executor.
4. **Proof Aggregation and Storage**: The Rollup Executor generates proofs for each batch, and Proofs are stored directly on Ethereum L1.

#### 5.2.4 Incentive Flow

Symbiotic points are transferred to the Network, not directly to Rollups. In this context, they are sent to Radius, which then forwards both its own points and Symbiotic points to fuse.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

***

## 6. Symbioitic Networks and Fuel Partners

### **6.1 Symbiotic Networks**

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Networks are the systems that need economic security to operate safely. These can be Layer 1 blockchains, Layer 2 solutions, or other decentralized systems that require stake-based security guarantees.

Symbiotic supports diverse networks serving as essential building blocks for shared security. The Alpha Engine ecosystem is secured by Symbiotic’s infrastructure providers, which enhance rollup growth:

* [**RedStone**](https://x.com/redstone_defi): RedStone is the fastest-growing oracle in 2024, specialising in yield-bearing collateral for lending markets. Its Total Value Secured (TVS) grew from below $1bn in January to $6bn+ now.
* [**Hyve DA**](https://x.com/Hyve_DA): Hyve is the first Data Availability (DA) solution designed to power any data-intensive Layer 2s, rollups, appchains, and even Layer 1s. Fully chain- and token-agnostic, HyveDA seamlessly supports any blockchain, regardless of its settlement layer, virtual machine, or native token.
* [**Capx Cloud**](https://x.com/0xCapx) : Capx Cloud is a Symbiotic network that enables decentralized AI agent deployment, crypto-economically secured through Symbiotic protocol
* [**Kalypso**](https://x.com/KalypsoProver)**:** Kalypso by Marlin is a circuit-agnostic ZK Proof Marketplace supporting private inputs, using Symbiotic restaking to provide liveness and response times guarantees for proof generation.
* [**Drosera**](https://x.com/KalypsoProver)**:** Drosera is an automated risk management protocol for addressing any risk within the EVM (not just smart contract exploits).
* [**Cycle Network**](https://x.com/cyclenetwork_GO) : Cycle Network offers bridgeless liquidity abstraction through verifiable state aggregation, supporting all Bitcoin and EVM blockchain ecosystems and secured by Symbiotic.
* [**Ditto**](https://x.com/Ditto_Network)**:** Ditto is building a trustless execution protocol to run event driven workflows on-chain with economic guarantees from restaking protocols.

### **6.2 Fuel Partners**

Fuel partners are integral to the Alpha Engine, providing specialized infrastructure that further enhances rollup growth capabilities. Rollups can tap into these partners to strengthen key aspects of their ecosystem:

* **Swell:** Focused on security.
* **Nucleus:** Offers yield generation and liquidity solutions.
* **Ternoa IVS:** Delivers trust-minimization mechanisms.
* **Fuse:** Provides SDKs and APIs for consumer applications.
* **More:** Additional partners expanding the ecosystem's potential.

***

## 7. Conclusion

Deploying a rollup is just the first step toward building a sustainable blockchain ecosystem. Long-term success requires addressing fundamental challenges such as revenue instability, high security costs, network fragmentation, liquidity constraints, user onboarding friction, and infrastructure complexity.

By leveraging innovative solutions, rollups can overcome these barriers and create a more resilient and interconnected ecosystem:

* **Revenue Stability:** Mechanisms like backrunning from SBB and Lighthouse introduce additional revenue streams beyond volatile transaction fees.
* **Enhanced Security:** Symbiotic Shared Security enables capital-efficient protection, reducing the burden on individual rollups.
* **Interoperability & Connectivity:** Avail’s Unification Layer via Nexus and modular DA layers facilitate seamless cross-rollup communication.
* **Liquidity Efficiency:** Nucleus enhances liquidity access and yield opportunities, while Avail ensures liquidity mobility across networks.
* **Seamless User Onboarding:** Connected rollups improve user experience by abstracting complexity and simplifying interactions.
* **Optimized Infrastructure:** Alpha Engine integrates best-in-class solutions—including Avail, Radius, Symbiotic, Redstone, and others—to provide scalable, cost-effective, and modular infrastructure.

***

## 8. Get Started

Please feel free to reach out to Sunshine from Radius: Telegram (@realsunny16)

***

## 9. Additional References

* [Alpha Engine blog post](https://mirror.xyz/0x957084A1F20AB33cfA0cE07ed57F50c05954999C/tTVKHPhlqYGmzou71_7NrUvMkqT0bujMvQhW4vf4tVQ)
* [Alpha Engine by Avail](https://x.com/availproject/status/1887263843673354320?s=46)
* [Symbiotic Network Highlight: Radius Secure Block Building](https://blog.symbiotic.fi/network-highlight-radius-secure-block-building/)
* [Symbiotic Docs](https://docs.symbiotic.fi/)
* [Avail & Symbiotic Partner to Create a Unified Framework for Innovation](https://blog.availproject.org/avail-symbiotic-partner-to-create-a-unified-framework-for-innovation/?utm_source=chatgpt.com)
* [Avail's Vision: The unification layer for web3](https://blog.availproject.org/the-avail-vision-accelerating-the-unification-of-web3/)
* [Fuse Network](https://x.com/Fuse_network/status/1891888959808233841)
