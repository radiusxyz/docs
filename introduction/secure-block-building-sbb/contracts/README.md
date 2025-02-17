# Contracts

The system involves two key contracts:

1. **LivenessServiceManager**
   * Ensures the overall **liveness** of the **SBB**.
   * Coordinates multiple entities, including:
     * **Transaction Orderers**
     * **Seeder**
     * **Clusters**
     * **Rollups** and their **Executors**
   * Plays a **crucial role** in maintaining network activity and availability.
2. **ValidationServiceManager**
   * Manages **operators, network participation, vaults, stakes, and rewards**.
   * Every **rollup** that registers with the **LivenessServiceManager** must also **add their ValidationServiceManager contract**.
   * This is required to **participate in the Symbiotic restaking protocol**.

These contracts work together to **maintain network liveness, coordination, and incentive mechanisms**.
