# Syncing

### Normal Operation

* A well functioning leader proposer consistently shares its state with the followers in a concurrent manner, who then synchronize their states to match that of the leader. This synchronization process ensures consistency across the network.

### Failover Operation

When the leader proposer becomes unresponsive or fails, the following process ensures continuity and proper synchronization within the system:

1. **Leader Recovery and Request**:
   * Upon recovery, the leader proposer makes a request to all other proposers to check if any of them have received the "build block" request from the rollup.
2. **No Build Block Request Received**:
   * If no other proposer has received the "build block" request from the rollup, the leader proposer resumes its leadership role.
3. **Build Block Request Received by Follower**:
   * If another proposer has received the build block request, the recovered proposer will synchronize its block height with that of the new leader proposer, as the leadership role has been transferred to it.

This process ensures that the leader proposer can either continue its role seamlessly or synchronize appropriately with the follower to maintain the integrity and continuity of the system.

This mechanism ensures that the network remains robust and consistent, aligning the states of all nodes with the selected leader's state, whether it includes the latest transactions and commitments or necessitates a rollback to maintain network integrity.
