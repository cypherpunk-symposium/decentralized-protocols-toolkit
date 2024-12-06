## [DRAFT] security considerations for **[pectra](https://eips.ethereum.org/EIPS/eip-7600)** (q1/25)

<br>

* ✅🔐🏋🏻‍♀️ **[eip-2537: precompile for bls12-381 curve operations, by a. vlasov et al.](https://eips.ethereum.org/EIPS/eip-2537)**
  - add bls signature verification and operations over bls12-381, a cryptographic primitive allowing to get 120+ bits of security for operations 
  - security: notes on constant time (tba)

<br>

* ✅🔐🤝🏋🏻‍♀️ **[eip-6110: supply validator deposits on chain, by m. kalinin et al.](https://eips.ethereum.org/EIPS/eip-61100)**
  - faster for validators to deposit their eth (12 hours -> 30 min)
  - security: data complexity, dos, weak subjectivity period (tba)

<br>

* ✅🔐🏋🏻‍♀️ **[eip-7002: execution layer triggerable exits, by djrtwo et al.](https://eips.ethereum.org/EIPS/eip-7002)**
  - improve ux for validators, giving them more flexibility
  - security: impact on existing custody relationships, fee overpayment (tba)

<br>

* ✅🔐🤝 **[eip-7251: increase the `MAX_EFFECTIVE_BALANCE`, by m. neuter et al.](https://eips.ethereum.org/EIPS/eip-7251)**
  - biggest ux improvement for validators
  - raise the validator stake limit (maximum effective balance from 32 -> 2048 eth, with reward compounding)
  - potentially can reduce the number of inactive nodes and possibly improving the network efficiency
  - security: attestation committees, aggregator selection, proposer selection probability, sync committee selection probability, churn invariants, fee overpayment (tba)

<br>

* ✅🔐🤝 **[eip-7549: move committee index outside attestation, by dappling](https://eips.ethereum.org/EIPS/eip-7549)**
  - shuffle the consensus message, making it more efficient
  - security: first block after fork, mutation over gossip (tba)

<br>

* ✅🔐🤝🏋🏻‍♀️ **[eip-7702: set eoa account code, by vub et al.](https://eips.ethereum.org/EIPS/eip-7702)**
  - improve the functionality of crypto wallets by giving them smart contract properties (the so called "account abstraction")
  - more usability in crypto, enhanced security features:
    - batching (allowing multiple operations from the same user in one atomic transaction)
    - sponsorship (an account can pay for a transaction on behalf of another account)
    - privilege de-escalation (users can sign sub-keys and given them specific permissions that are much weaker than global access to the account)
  - e.g.: gas fees could be outsourced to services to pay on another erc-20 token
  - security: secure delegation, `tx.origin`, sponsored tx relayers, frontrunning initialization, tx propagation (tba)

<br>

* ✅🤝🏋🏻‍♀️ **[eip-7742: uncouple blob count between cl and el, by a. stokes](https://eips.ethereum.org/EIPS/eip-7742)**
  - extend functionalities from blobs
  - execution layer no longer verifies data blobs’s maximum value and instead gets this value dynamically from the consensus layer

<br>

* ✅🏋🏻‍♀️ **[eip-7685: general purpose execution layer requests, by lightclient](https://eips.ethereum.org/EIPS/eip-7685)**
  - boost the interoperability between the execution and the consensus layer (helping with surge demand on the execution layer)

<br>

* ✅🏋🏻‍♀️ **[eip-2935: save historical block hashes from state, by vub et al.](https://eips.ethereum.org/EIPS/eip-2935)**
  - increase amount of data from past blocks that can be stored on new blocks
  - set the stage for verkle tree
  - improves solo staking ux: enabling stateless validator clients, allowing staking nodes to run with very little hard disk space and quick sync
  - security: notes on branch poisoning (tba)

<br>

* ✅🤝 **[eip-7594: peerdas - peer data availability Sampling, by djirtwo et al.](https://eips.ethereum.org/EIPS/eip-7594)**
  - allow beacon nodes to perform data availability sampling, improving how da is handled across the network
  - crucial feature for layer 2s (making them more efficient and cost-effective)
  - compare to celestia (tba)
 
<br>

* ✅ **[eip-7692: evm object format meta, by a. beregszaszi et al.](https://eips.ethereum.org/EIPS/eip-7692)**
  - add a bunch of evm object format for smart contract deployment and execution efficiency
  - include optimized code validation, better function handling, more efficient data access instructions

<br>

* 🟡 **[eip-7623: increase calldata cost, by t. wahrstätter et al.](https://eips.ethereum.org/EIPS/eip-7623)**
  - increasing the calldata cost for transactions (increase the cost of calldata to 10/40 gas for transactions that do not exceed a certain threshold of gas spent on evm operations)
  - highligting data availability

<br>

* 🟡 **[eip-7762: increase `MIN_BASE_FEE_PER_BLOB_GAS`, by maxy riesnick](https://eips.ethereum.org/EIPS/eip-7762)**
  -  speed up discovery on blob space
  -  security: "rollups that use blobs as da will need to update their posting strategies"

<br>

----

### cool resources

<br>

* **[what's going into the pectra upgrade?, by c. kim (2024)](https://www.youtube.com/watch?v=ufIDBCgdGwY)**
  
