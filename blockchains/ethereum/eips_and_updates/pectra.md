## [DRAFT] security considerations for **[pectra](https://eips.ethereum.org/EIPS/eip-7600)** (early 2025)

<br>

#### ✅🔐🏋🏻‍♀️ **[eip-2537: precompile for bls12-381 curve operations, by a. vlasov et al.](https://eips.ethereum.org/EIPS/eip-2537)**

<br>

  - adds bls signature verification and operations over bls12-381, a cryptographic primitive allowing to get 120+ bits of security for operations 
  - security: notes on constant time (tba)

<br>

---

#### ✅🔐🤝🏋🏻‍♀️ **[eip-6110: supply validator deposits on chain, by m. kalinin et al.](https://eips.ethereum.org/EIPS/eip-61100)**

<br>

  - faster for validators to deposit their eth (12 hours -> 30 min)
  - removes the need for deposit voting from the cl, reducing the complexity of client software design
  - security: data complexity, dos, weak subjectivity period (tba)

<br>

---

#### ✅🔐🤝🏋🏻‍♀️ **[eip-7002: execution layer triggerable exits, by djrtwo et al.](https://eips.ethereum.org/EIPS/eip-7002)**

<br>

  - improves ux for validators, giving them more flexibility
  - allows validators to trigger exits and partial withdrawals via their execution layer withdrawal credentials (e.g., enabling more trustless staking pool designs)  
  - security: impact on existing custody relationships, fee overpayment (tba)

<br>

---

#### ✅🔐🤝 **[eip-7251: increase the `MAX_EFFECTIVE_BALANCE`, by m. neuder et al.](https://eips.ethereum.org/EIPS/eip-7251)**

<br>

  - biggest ux improvement for validators
  - raises the validator stake limit (maximum effective balance from 32 -> 2048 eth, with reward compounding)
  - potentially can reduce the number of inactive nodes and possibly improving the network efficiency
  - security: attestation committees, aggregator selection, proposer selection probability, sync committee selection probability, churn invariants, fee overpayment (tba)

<br>

---

#### ✅🔐🤝 **[eip-7549: move committee index outside attestation, by dapplion](https://eips.ethereum.org/EIPS/eip-7549)**

<br>

  - makes the aggregation of validator votes (attestation) in blocks more efficient, reducing networking load and saving node bandwidth
  - security: first block after fork, mutation over gossip (tba)

<br>

---

#### ✅🔐🤝🏋🏻‍♀️ **[eip-7702: set eoa account code, by vub et al.](https://eips.ethereum.org/EIPS/eip-7702)**

<br>

  - improves the functionality of crypto wallets by giving them smart contract properties (the so called "account abstraction")

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

  - introduces a new transaction, the setcode tx, very similar to eip-1559 txs, with an additional authorization list elements ("authorizing some code to live into your account" through creating by template)

<p align="center">
<img src="https://github.com/user-attachments/assets/76a0d234-61d9-4617-bc3e-e3fe8903bb40" width="80%"/>
</p>

  - e.g., gas fees could be outsourced to services to pay on another erc-20 token
  - security: secure delegation, `tx.origin`, sponsored tx relayers, frontrunning initialization, tx propagation (tba)

<br>

---

#### ✅🤝🏋🏻‍♀️ **[eip-7742: uncouple blob count between cl and el, by a. stokes](https://eips.ethereum.org/EIPS/eip-7742)**

<br>

  - extends functionalities from blobs
  - execution layer no longer verifies data blobs's maximum value and instead gets this value dynamically from the consensus layer

<br>

---

#### ✅🏋🏻‍♀️ **[eip-7685: general purpose execution layer requests, by lightclient](https://eips.ethereum.org/EIPS/eip-7685)**

<br>

  - boosts the interoperability between the execution and the consensus layer (helping with surge demand on the execution layer) by defining a general purpose framework for storing contract-triggered requests:
    - extends the execution header with a single field to store the request information
    - requests are later on exposed to the consensus layer, which then processes each one
  - more efficient way to code, test, and implement execution triggered requests such as eip-6110 and eip-7002
  - note on "exec" concern: *"a request’s validity can often not be fully verified at the execution layer. this is why they are referred to merely as “requests”; they do not carry the authority on their own to unilaterally catalyze an action. we expect the system contracts to perform whatever validation is possible by the el and then pass it on to the cl for further validation."*

<br>

---

#### ✅🏋🏻‍♀️ **[eip-2935: save historical block hashes from state, by vub et al.](https://eips.ethereum.org/EIPS/eip-2935)**

<br>

  - increases amount of data from past blocks that can be stored on new blocks
  - sets the stage for verkle tree
  - improves solo staking ux: enabling stateless validator clients, allowing staking nodes to run with very little hard disk space and quick sync
  - security: notes on branch poisoning (tba)

<br>

---

#### ✅🤝 **[eip-7594: peerdas - peer data availability Sampling, by djrtwo et al.](https://eips.ethereum.org/EIPS/eip-7594)**

<br>

  - allows beacon nodes to perform data availability sampling, improving how da is handled across the network
  - crucial feature for layer 2s (making them more efficient and cost-effective)
  - compare to celestia (tba)
 
<br>

---

#### ✅ **[eip-7692: evm object format meta, by a. beregszaszi et al.](https://eips.ethereum.org/EIPS/eip-7692)**

<br>

  - adds a bunch of evm object format for smart contract deployment and execution efficiency, including optimized code validation, better function handling, more efficient data access instructions:
    - **[eip-3540](https://eips.ethereum.org/EIPS/eip-3540)**:
      - introduces an extensive container format for the evm with a once-off validation at deploy time
      - `magic, version, (section_kind, section_size_or_sizes)+, 0, <section contents>`
    - **[eip-3670](https://eips.ethereum.org/EIPS/eip-3670)**:
      - validates eof bytecode for correctness at the time of deployment
    - **[eip-4200](https://eips.ethereum.org/EIPS/eip-4200)**:
      - `RJUMP`, `RJUMPI`, and `RJUMPV` instructions with a signed immediate encoding the jump destination
    - **[eip-4750](https://eips.ethereum.org/EIPS/eip-4750)**:
      - individual sections for functions with `CALLF` and `RETF` instructions
    - 🔐 **[eip-5450](https://eips.ethereum.org/EIPS/eip-5450)**:
      - deploy-time validation of stack usage for eof functions
      - security: introduces extended validation of eof code sections to guarantee that neither stack underflow nor overflow can happen during execution of validated contracts)
    - **[eip-6206](https://eips.ethereum.org/EIPS/eip-6206)**:
      - introduces instruction for chaining function calls
    - **[eip-7480](https://eips.ethereum.org/EIPS/eip-7480)**:
      - instructions to read data section of eof container (clear separation between code and data from eof1)
    - **[eip-663](https://eips.ethereum.org/EIPS/eip-663)**:
      - introduces additional instructions for manipulating the stack which allows accessing the stack at higher depths
      - the evm stack is fixed at 1024 items and most implementations keep that in memory at all times - this change increases the number of stack items accessible via single instruction
    - 🔐 **[eip-7069](https://eips.ethereum.org/EIPS/eip-7069)**:
      - introduces `EXTCALL`, `EXTDELEGATECALL`, `EXTSTATICALL`, with simplified semantics
      - security: when implemented in eof - where the `GAS` opcode and the original `CALL` operations are removed - existing out of gas attacks will be slightly more difficult, but not entirely prevented as transactions can still pass in arbitrary gas values
    - **[eip-7620](https://eips.ethereum.org/EIPS/eip-7620)**:
      - introduces `EOFCREATE` and `RETURNCONTRACT` instructions
    - 🔐 **[eip-7620](https://eips.ethereum.org/EIPS/eip-7698)**:
      - deploys eof contracts using creation transactions 
      - security: external unverified code (e.g., check for correct price, dos)

<br>

---

#### 🟡 **[eip-7623: increase calldata cost, by t. wahrstätter et al.](https://eips.ethereum.org/EIPS/eip-7623)**

<br>

  - increases the calldata cost for transactions (increase the cost of calldata to 10/40 gas for transactions that do not exceed a certain threshold of gas spent on evm operations)
  - highligting data availability

<br>

---

#### 🟡 **[eip-7762: increase `MIN_BASE_FEE_PER_BLOB_GAS`, by m. resnick](https://eips.ethereum.org/EIPS/eip-7762)**

<br>

  -  speeds up discovery on blob space
  -  security: "rollups that use blobs as da will need to update their posting strategies"

<br>

----

### cool resources

<br>

* **[what's going into the pectra upgrade?, by c. kim (2024)](https://www.youtube.com/watch?v=ufIDBCgdGwY)**
* **[eip-7702: a technical deep dive, by lightclient (2024)](https://www.youtube.com/watch?v=_k5fKlKBWV4)**
