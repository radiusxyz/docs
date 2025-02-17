# Seeder

Repository: [Seeder GitHub](https://github.com/radiusxyz/seeder.git)

The **Seeder** plays a crucial role in coordinating **transaction orderers (tx\_orderers)** by providing the necessary information for network communication.

To become a tx\_orderer, a node must first **register itself in the LivenessServiceManager contract**. Once registered, it can join a cluster through the Seeder. The Seeder then **verifies the node’s wallet address** in the Liveness Contract before storing its **IP address**.

After successful registration, the **tx\_orderer receives the IP addresses of other peers in the cluster**, enabling seamless **internal communication** between nodes.

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption><p>Seeder - Tx_Orderer interaction</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption><p>Seeder - Rollup Operator Interaction</p></figcaption></figure>

### **Seeder: Managing Tx\_Orderer RPC URLs**

The **Seeder** functions as a **key-value store**, mapping tx\_orderer addresses to their corresponding RPC URLs.

#### **Key Responsibilities**

* Stores **tx\_orderer addresses** as keys and their **RPC URLs** as values.
* Ensures that only **tx\_orderers registered in the LivenessServiceManager contract** can register on the Seeder.

***

### **Registration Process**

To register, a **tx\_orderer** must send a **signed message** containing:

* **Tx\_Orderer Address**
* **External RPC URL** (handles user transactions)
* **Cluster RPC URL** (for inter-cluster messages with signature verification)
* **Cluster ID** (received upon registering with the LivenessServiceManager contract)

#### **Validation Steps**

When a **registration request** is received, the Seeder:

1. **Verifies the message signature**.
2. **Confirms that the tx\_orderer is registered on the LivenessServiceManger contract**.
3. **Checks the accessibility of the external RPC URL** via the `/health` endpoint.

**Upon successful validation, the tx\_orderer's address and RPC URLs are stored in the Seeder**, making them available to **Secure RPC, Tx\_Orderers, and Rollups**.

***

### **Deregistration Process (TBD)**

A **tx\_orderer** can deregister by sending a **signed message** containing:

* **Tx\_Orderer Address**
* **Cluster ID**

#### **Validation Steps**

When a **deregistration request** is received, the Seeder:

1. **Verifies the message signature**.
2. **Checks if the tx\_orderer has been removed from the LivenessServiceManager contract**.

If confirmed, the **Seeder removes the tx\_orderer’s address**, making its **RPC URLs unavailable**.
