# Seeder

Repository: [Seeder GitHub](https://github.com/radiusxyz/seeder.git)

The **Seeder** plays a crucial role in coordinating **transaction orderers (tx-orderers)** by providing the necessary information for network communication.

To become a tx. orderer, a node must first **register itself in the LivenessRadius contract**. Once registered, it can join a cluster through the Seeder. The Seeder then **verifies the node’s wallet address** in the Liveness Contract before storing its **IP address**.

After successful registration, the **tx. orderer receives the IP addresses of other peers in the cluster**, enabling seamless **internal communication** between nodes.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Seeder - Tx. Orderer Interaction</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Seeder - Rollup Operator Interaction</p></figcaption></figure>

### **Seeder: Managing Tx. Orderer RPC URLs**

The **Seeder** functions as a **key-value store**, mapping tx. orderer addresses to their corresponding RPC URLs.

#### **Key Responsibilities**

* Stores **tx. orderer addresses** as keys and their **RPC URLs** as values.
* Ensures that only **tx. orderers registered in the LivenessServiceManager contract** can register on the Seeder.

***

### **Registration Process**

To register, a **tx. orderer** must send a **signed message** containing:

* **Tx. Orderer Address**
* **External RPC URL** (handles user transactions)
* **Cluster RPC URL** (for inter-cluster messages with signature verification)
* **Cluster ID** (received upon registering with the LivenessServiceManager contract)

#### **Validation Steps**

When a **registration request** is received, the Seeder:

1. **Verifies the message signature**.
2. **Confirms that the tx. orderer is registered on the LivenessServiceManger contract**.
3. **Checks the accessibility of the external RPC URL** via the `/health` endpoint.

**Upon successful validation, the tx. orderer's address and RPC URLs are stored in the Seeder**, making them available to **Secure RPC, Tx. Orderers, and Rollups**.

***

### **Deregistration Process (TBD)**

A **tx. orderer** can deregister by sending a **signed message** containing:

* **Tx. Orderer Address**
* **Cluster ID**

#### **Validation Steps**

When a **deregistration request** is received, the Seeder:

1. **Verifies the message signature**.
2. **Checks if the tx. orderer has been removed from the LivenessServiceManager contract**.

If confirmed, the **Seeder removes the tx. orderer’s address**, making its **RPC URLs unavailable**.
