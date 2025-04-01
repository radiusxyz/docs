# Tx\_Orderer Cluster

**Overview**

The cryptographic approach employed by the system ensures a trustless environment for the tx\_orderer operation. However, the architecture still faces the challenge of a Single Point of Failure (SPOF). To mitigate this risk, Radius adopts a distributed tx\_orderer network. This network comprises multiple tx\_orderers operating concurrently to ensure system reliability and continuity.

**Functionality**

In the event of a tx\_orderer failure, the distributed nature of the network allows the remaining tx\_orderers to continue operations without interruption. This redundancy enhances the robustness of the system against individual node failures.

**Communication and Decision making**

To ensure efficient communication and syncing among multiple nodes, Radius adopts a leader-based decision-making process. This strategy eliminates the need for consensus regarding the order and formation of blocks. It clearly outlines the roles and duties of the tx\_orderers in the network, distinguishing between the leader and the followers.

**Key Benefits**

* **Reliability:** The distributed tx\_orderer network significantly reduces the risk associated with a single point of failure, ensuring higher system uptime.
* **Efficiency:** By eliminating the need for consensus between network members, Radius ensures efficient decision-making among tx\_orderers, leading to a swift and reliable sequencing process.
* **Scalability:** The distributed architecture allows for scalability, accommodating an increasing number of tx\_orderers as the network grows.

**Conclusion**

The implementation of a distributed tx\_orderer network represents a strategic approach to enhancing the reliability, scalability, and decision making efficiency of tx\_orderer set. This ensures that the system remains robust against failures and maintains continuous operation.
