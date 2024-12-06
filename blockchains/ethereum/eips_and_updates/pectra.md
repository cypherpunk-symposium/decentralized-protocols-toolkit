## [DRAFT] security considerations for **[pectra](https://eips.ethereum.org/EIPS/eip-7600)** (early 2025)

<br>

* ✅🔐🏋🏻‍♀️ **[eip-2537: precompile for bls12-381 curve operations, by a. vlasov et al.](https://eips.ethereum.org/EIPS/eip-2537)**
  - add bls signature verification and operations over bls12-381, a cryptographic primitive allowing to get 120+ bits of security for operations 
  - security: notes on constant time (tba)

<br>

---

* ✅🔐🤝🏋🏻‍♀️ **[eip-6110: supply validator deposits on chain, by m. kalinin et al.](https://eips.ethereum.org/EIPS/eip-61100)**
  - faster for validators to deposit their eth (12 hours -> 30 min)
  - remove the need for deposit voting from the cl, reducing the complexity of client software design
  - security: data complexity, dos, weak subjectivity period (tba)

<br>

---

* ✅🔐🤝🏋🏻‍♀️ **[eip-7002: execution layer triggerable exits, by djrtwo et al.](https://eips.ethereum.org/EIPS/eip-7002)**
  - improve ux for validators, giving them more flexibility
  - allow validators to trigger exits and partial withdrawals via their execution layer withdrawal credentials (e.g., enabling more trustless staking pool designs)  
  - security: impact on existing custody relationships, fee overpayment (tba)

<br>

---

* ✅🔐🤝 **[eip-7251: increase the `MAX_EFFECTIVE_BALANCE`, by m. neuder et al.](https://eips.ethereum.org/EIPS/eip-7251)**
  - biggest ux improvement for validators
  - raise the validator stake limit (maximum effective balance from 32 -> 2048 eth, with reward compounding)
  - potentially can reduce the number of inactive nodes and possibly improving the network efficiency
  - security: attestation committees, aggregator selection, proposer selection probability, sync committee selection probability, churn invariants, fee overpayment (tba)

<br>

---

* ✅🔐🤝 **[eip-7549: move committee index outside attestation, by dapplion](https://eips.ethereum.org/EIPS/eip-7549)**
  - makes the aggregation of validator votes (attestation) in blocks more efficient, reducing networking load and saving node bandwith
  - security: first block after fork, mutation over gossip (tba)

<br>

---


* ✅🔐🤝🏋🏻‍♀️ **[eip-7702: set eoa account code, by vub et al.](https://eips.ethereum.org/EIPS/eip-7702)**
  - improve the functionality of crypto wallets by giving them smart contract properties (the so called "account abstraction")

<p align="center">
<img src="https://github.com/user-attachments/assets/e7ae1ae1-bcae-4444-8f61-c76ab60d8d9a" width="80%"/>
</p>

  - more usability in crypto, enhanced security features:
    - batching (allowing multiple operations from the same user in one atomic transaction)
    - sponsorship (an account can pay for a transaction on behalf of another account)
    - privilege de-escalation (users can sign sub-keys, giving them specific permissions that are much weaker than global access to the account)
   
<p align="center">
<img src="https://github.com/user-attachments/assets/3cb0f48b-88aa-4844-9a46-ede10e09837e" width="80%"/>
</p>

  - introduce a new transaction, the setcode tx, very similar to eip-1559 txs, with an addition autorization list elements ("authorizing some code to live into your account" through creating by template)

<p align="center">
<img src="https://github.com/user-attachments/assets/76a0d234-61d9-4617-bc3e-e3fe8903bb40" width="80%"/>
</p>

  - e.g.: gas fees could be outsourced to services to pay on another erc-20 token
  - security: secure delegation, `tx.origin`, sponsored tx relayers, frontrunning initialization, tx propagation (tba)

<br>

---

* ✅🤝🏋🏻‍♀️ **[eip-7742: uncouple blob count between cl and el, by a. stokes](https://eips.ethereum.org/EIPS/eip-7742)**
  - extend functionalities from blobs
  - execution layer no longer verifies data blobs’s maximum value and instead gets this value dynamically from the consensus layer

<br>

---

* ✅🏋🏻‍♀️ **[eip-7685: general purpose execution layer requests, by lightclient](https://eips.ethereum.org/EIPS/eip-7685)**
  - boost the interoperability between the execution and the consensus layer (helping with surge demand on the execution layer)
  - more efficient way to code, test, and implement execution triggered requests such as eip-6110 and eip-7002

<br>

---

* ✅🏋🏻‍♀️ **[eip-2935: save historical block hashes from state, by vub et al.](https://eips.ethereum.org/EIPS/eip-2935)**
  - increase amount of data from past blocks that can be stored on new blocks
  - set the stage for verkle tree
  - improves solo staking ux: enabling stateless validator clients, allowing staking nodes to run with very little hard disk space and quick sync
  - security: notes on branch poisoning (tba)

<br>

---

* ✅🤝 **[eip-7594: peerdas - peer data availability Sampling, by djrtwo et al.](https://eips.ethereum.org/EIPS/eip-7594)**
  - allow beacon nodes to perform data availability sampling, improving how da is handled across the network
  - crucial feature for layer 2s (making them more efficient and cost-effective)
  - compare to celestia (tba)
 
<br>

---

* ✅ **[eip-7692: evm object format meta, by a. beregszaszi et al.](https://eips.ethereum.org/EIPS/eip-7692)**
  - add a bunch of evm object format for smart contract deployment and execution efficiency
  - include optimized code validation, better function handling, more efficient data access instructions

<br>

---

* 🟡 **[eip-7623: increase calldata cost, by t. wahrstätter et al.](https://eips.ethereum.org/EIPS/eip-7623)**
  - increase the calldata cost for transactions (increase the cost of calldata to 10/40 gas for transactions that do not exceed a certain threshold of gas spent on evm operations)
  - highligting data availability

<br>

---

* 🟡 **[eip-7762: increase `MIN_BASE_FEE_PER_BLOB_GAS`, by m. resnick](https://eips.ethereum.org/EIPS/eip-7762)**
  -  speed up discovery on blob space
  -  security: "rollups that use blobs as da will need to update their posting strategies"

<br>

----

### cool resources

<br>

* **[what's going into the pectra upgrade?, by c. kim (2024)](https://www.youtube.com/watch?v=ufIDBCgdGwY)**
* **[eip-7702: a technical deep dive, by lightclient (2024)](https://www.youtube.com/watch?v=_k5fKlKBWV4)**
