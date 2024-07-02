# Introduction

### What is Radius?

Radius is a coordination layer designed to enable rollups to achieve key decentralization properties: censorship resistance, liveness, and safety for fast finality.\
Our goal is to create trustless rollup networks by leveraging cryptographic algorithms and enable true rollup scalability, followed by our [user-centric model that is essential for rollup success](https://mirror.xyz/0x957084A1F20AB33cfA0cE07ed57F50c05954999C/2ESPmsJyzm5QhL\_Xmogt9yG9vLvjkJ\_PPTri2qgTD5k).

Before we explain why Radius’s user-centric features and designs are needed, it is critical to understand why and where existing rollup designs fall short, causing downstream consequences for users.

### Current Challenges

Despite the scalability offered by rollups, creating a sustainable rollup ecosystem remains challenging due to several pain points faced by users: censorship and harmful MEV risks (such as frontrunning and sandwiching) that extract value from users, no finality guarantees on Ethereum with a lack of incentive alignment between rollups and Ethereum, and the complexity and poor user experience of cross-rollup transactions due to a lack of shared entity. As more rollups and appchains emerge, these issues will only intensify.

Radius addresses these challenges through a **user-centric model**, focusing on providing robust solutions to prevent transactions from censorship and harmful MEV, guarantee inclusion on Ethereum, and simplify cross-rollup interactions.

### With Radius, rollups can:

* Adopt enhanced security measures, protecting users from censorship and harmful Miner Extractable Value (MEV) such as frontrunning and sandwiching
* Guarantee fast finality with strong preconfirmations for inclusion guarantees on Ethereum
* Provide seamless interoperability eliminating the complexities of cross-rollup bridging.

### Benefits of Building with Radius

1. **Autonomy in sequencing**: Rollups have flexible sequencing options that align with their values and goals, including using their own proposer and maintaining full control over their sequencing rights.
2. **Selective composability**: Rollups can choose which rollups to communicate with based on their composability requirements, allowing ones with different execution environments to achieve customized scalability. Rollups also have the flexibility to opt out of selective composability as needed.
3. **User-protected revenue**: Rollups can generate revenue while protecting users through a divided block design: For example, in top-of-block (ToB) rollups can build ToB for revenue with backrunning bundles based on the previous state of the rollup, and in bottom-of-block (BoB) includes a built-in _trustless sequencing engine_.

### Key components of Radius

1. **Trustless Sequencing Engine**: Uses cryptographic algorithms to prevent censorship and harmful MEV within [encrypted mempools](https://docs.theradius.xyz/deep-dive/encrypted-mempool).
2. **Based Sequencing**: Ensures fast preconfirmations without relying on the trust of the rollup, allowing users to create the next transactions confidently.
3. **Shared Sequencing**: Unifies rollups through state synchronization for atomic composability, providing a seamless interoperability experience for users.

