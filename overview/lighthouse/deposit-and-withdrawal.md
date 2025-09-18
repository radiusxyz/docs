# Deposit & Withdrawal

### Deposits

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption><p><strong>Figure 3. Deposit Workflow</strong> – steps to deposit funds within Lighthouse.</p></figcaption></figure>



1. **Deposit Tokens**: Searchers deposit tokens into the Lighthouse contract to fund bidding fees.
2. **Send `Deposited` Event:** The server receives deposits instantly and updates searcher balances, avoiding redundant on-chain queries.
3. **Submit Bid:** Searchers submit MEV bundles with a `BidMsg`; the server verifies that each bid is fully backed by the searcher’s deposit.
4. **Send Auction Closed Message**: The server informs the chain of auction close, triggering settlement. The server deducts the winning bid and distributes it between Lighthouse and the rollup per a predefined ratio.

***

### Withdrawals

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption><p><strong>Figure 3. Withdrawal Workflow</strong> – steps to withdraw funds within Lighthouse.</p></figcaption></figure>

1. **Reserve Withdrawal:** To withdraw, a searcher reserves a withdrawal. This enforces a delay to prevent inconsistencies. For example, ensuring the same deposit cannot be used simultaneously in a bid and a withdrawal.
2. **Send `WithdrawalReserved` Event:** Upon receiving the reservation event, the server marks the searcher as _ineligible to bid_. From this point, the searcher cannot submit bids.
3. **Withdraw:** After the withdrawal window opens, the searcher withdraws their funds from the contract.
4. **Send `Withdrew` Event:** The server detects withdrawal and updates the searcher’s deposit balance.

