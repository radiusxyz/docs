# Distributed Sequencing

**Overview**

The cryptographic approach employed by the system ensures a trustless environment for the sequencer operation. However, the architecture still faces the challenge of a Single Point of Failure (SPOF). To mitigate this risk, Radius adopts a distributed sequencer network. This network comprises multiple sequencers operating concurrently to ensure system reliability and continuity.

**Functionality**

In the event of a sequencer failure, the distributed nature of the network allows the remaining sequencers to continue operations without interruption. This redundancy enhances the robustness of the system against individual node failures.

**Communication and Decision making**

To ensure efficient communication and syncing among multiple nodes, Radius adopts a leader-based decision-making process grounded in the RAFT algorithm. This strategy eliminates the need for consensus regarding the order and formation of blocks. It clearly outlines the roles and duties of the sequencers in the network, distinguishing between the leader and the followers.

**Key Benefits**

* **Reliability:** The distributed sequencer network significantly reduces the risk associated with a single point of failure, ensuring higher system uptime.
* **Efficiency:** By leveraging a modified RAFT algorithm, Radius ensures efficient decision making mechanisms among sequencers, facilitating swift and reliable sequencing state.
* **Scalability:** The distributed architecture allows for scalability, accommodating an increasing number of sequencers as the network grows.

**Conclusion**

The implementation of a distributed sequencer network, complemented by a modified RAFT algorithm, represents a strategic approach to enhancing the reliability, scalability, and decision making efficiency of Radius. This ensures that the system remains robust against failures and maintains continuous operation.
