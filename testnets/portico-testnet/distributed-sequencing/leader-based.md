# Leader-based

The RAFT algorithm divides entities into two categories: leaders and followers. Followers are responsible for routing data to and from the leader and users, as well as synchronizing the state. Meanwhile, the leader takes on more complex tasks such as sequencing transactions into blocks, providing preliminary confirmations, signing transactions, and interacting with rollups. This method offers several advantages.

#### 1. Simplified Coordination and decision making <a href="#simpler-decision-making" id="simpler-decision-making"></a>

* **Simplicity:** With a single leader responsible for sequencing, the system simplifies the decision-making process. This centralized approach reduces the complexity and overhead associated with achieving consensus among multiple nodes.
* **Efficiency:** Leader-based systems can implement more efficient ordering and syncing related decisions  since the leader node acts as the authoritative source for sequencing. This streamlines the process of agreeing on the state of the system, as there's no need for multiple nodes to negotiate each sequence.

#### 2. Improved System Performance

* **Reduced Latency:** By centralizing the sequencing tasks, leader-based systems can often reduce communication latency. Messages do not need to traverse multiple nodes to reach a consensus, as the leader directly sequences and processes requests. However, note that the leader manages all processing, meaning its performance directly influences the overall network's functionality.
* **Optimized Throughput:** The leader can optimize sequencing and resource allocation based on the current system load and priorities, potentially improving the overall throughput of the system.

To avoid confusion, the details regarding the leader-follower interaction were not included in the previous sections. This was done to simplify the concept, allowing readers to view the sequencing layer as a singular entity. However, below is an overview of how leader-follower interactions are handled:

For every RPC request made to any of the followers, the request and its associated data are redirected to the leaders. This redirection mechanism is evident in the sequencer's RPC methods:

* [forwarding to the leader](../code-references.md#forwarding-to-the-leader)

The leader distributes the data to the followers to maintain a synchronized and updated state across the entire sequencing layer. Generally, synchronization in the sequencing process involves every piece of data being propagated during the follower RAFT nodes. For the `RaftNode` structure, syncing encrypted transactions, syncing raw transactions, syncing block, and syncing block metadata implementations are carried out.

* [requesting followers to sync](../code-references.md#request-from-followers-to-sync)

<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>Follower ↔ Leader communication</p></figcaption></figure>
