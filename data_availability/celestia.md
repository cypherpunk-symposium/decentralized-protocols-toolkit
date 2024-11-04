## celestia's das network

<br>

### tl; dr

<br>

* celestia is a modular data availability network that scales with the number of users, by decoupling execution from consensus and introducing a new primitive, **data availability sampling** (das), through **namespaced merkle trees**.
* celestia da layer consists of a pos blockchain (celestia app), an application that provides transactions to faciliate the da layer and is built using cosmos sdk.
* rollups and l2s use celestia as a network for publishing and making transaction da available, where optimistic rollups require data availability to detect fraud and zero-knowledge rollups require data availability to reconstruct the state of the chain (celestia can scale to the data throughput needed for millions of rollups without compromising on security).

<br>
<p align="center">
<img src="https://github.com/go-outside-labs/decentralized-protocols-research/assets/1130416/9e6e7363-de60-482d-a83a-6095f3c68b0e" width="80%" align="center" style="padding:1px;border:1px solid black;" title="Jan 7th"/>
</p>

* lexicon:
  * **blobs**: data is posted to celestia's da layer by using `MsgPayForBlobs` transactions to the core network.
  * **namespaces**: celestia partitions the block data into multiple namespaces, one for every application. this   allows applications to only download their data, and not the data of other applications.
  * **blockchain cluster:** a group of blockchains that can communicate with each other in a trust-minimized way.
  * **consensus**: the ordering of txs is agreed upon by a set of validators.
  * **data availability commitee (dac)**: permissioned group of nodes responsible for providing da to a blockchain.
  * **data availability layer**: a blockchain that provides for other types of chains (e.g., rollups).
  * **settlement layer**: a modular blockchain whose primary role is to provide proof verification and dispute resolution for rollups.
  * **data throughput**: a measurement of the data capacity of a blockchain, and calculated by the amount of data that a block.
  * **the data availability problem**: concerned with whether the data in the proposed block can be verified that is available.

<br>

-----

### data availability sampling (das)

<br>

* da answers the question "has the data for this blockchain been published?".
  - celestia solves the problem of having to download all the blockchain data by making it possible for users to verify very large blocks with data availability sampling.
  - this new primitive enables celestia light nodes to, instead of downloading all data, download only **block headers that contain commitments** (i.e. merkle roots) of the block data (i.e. the list of transactions).
  - to make das possible, celestia uses as **2D reed-solomon encoding scheme** to encode the block data: every block data is split into `k x k` chunks, arranged in a `k x k` matrix, and extended with parity data into a `2k x 2k` extended matrix by applying multiple times reed-solomon encoding.

<br>

<p align="center">
<img src="https://github.com/go-outside-labs/decentralized-protocols-research/assets/138340846/6e91d396-2e6e-4d71-9383-37cc6b7d1dcf" width="80%" align="center" style="padding:1px;border:1px solid black;" />
<img src="https://github.com/go-outside-labs/decentralized-protocols-research/assets/138340846/881f705f-2e2e-43ae-b2cf-05bb147e1df8" width="80%" align="center" style="padding:1px;border:1px solid black;" />
</p>

<br>

* celestia does not require a majority of the consensus (i.e. block producers) to be honest to guarantee data availability.
  - if the extended data is invalid, the original data might not be recoverable, even if the light nodes are sampling sufficient unique chunks.
  - as a solution, da fraud proofs of incorrectly generated extended data enable light nodes to reject blocks with invalid extended data (data availability proofs using erasure codes).
  - such proofs require reconstructing the encoding and verifying the mismatch.

<br>

<p align="center">
<img src="https://github.com/go-outside-labs/decentralized-protocols-research/assets/1130416/af34dcef-230a-4fb7-b877-228ae287ec5d" width="80%" align="center" style="padding:1px;border:1px solid black;" title="Jan 7th"/>
</p>

<br>  

----

### namespaced merkle trees 

<br>

* celestia partitions the block data into **multiple namespaces**, one for every application (e.g. rollup), using the da layer.
  - every application needs to download only its own data and can ignore the data of other applications.
  - for this to work, the da layer must be able to prove that the provided data is complete, i.e., all the data for a given namespace is returned.
* a nmt is a merkle tree with the leafs ordered by the namespace identifiers and the hash function modified so that every node in the tree includes the range of namespace of all its descendants.
  - when an application requests the data for `namespace 2`, the da layer must provide the data chunks `D3`, `D4`, `D4`, `D6`, and the nodes `N2`, `N8`, `N7` as proof.
  - the application is able to check that the provided data is part of the block data. furthermore, the application can verify that all the data for `namespace 2` was provided. if the DA layer provides only the data chunks `D4` and `D5`, it must also provide nodes `N12` and `N11` as proofs. however, the application can identify that the data is incomplete by checking the namespace range of the two nodes, i.e., both `N12` and `N11` have descendants part of `namespace 2`.

<br>

<p align="center">
<img src="https://github.com/go-outside-labs/decentralized-protocols-research/assets/1130416/9fb8fb21-c68b-4bff-9613-f87c0d17347b" width="80%" align="center" style="padding:1px;border:1px solid black;" title="Jan 7th"/>
</p>

<br>

----

### building a pos blockchain for da

<br>

* celestia-app is built on top of celestia-core, a modified version of the tendermint consensus algorithm. it ensures:
  * the erasure coding of block data (using the 2D reed-solomon encoding scheme).
  * the replacement of regular merkle tree used by tendermint to store block data wiht a namespaced merkle tree that enables the above layers (execution and settlement) to only download the needed data.
* celestia-core nodes are still using the tendermint p2p network.
* similarly to tendermint, celestia-core is connected to the application layer (i.e., the state machine) by ABCI++.
  - like its predecessor, ABCI++ is the interface between tendermint (a state-machine replication engine) and the actual state machine being replicated (i.e., the application). yhe api consists of a set of methods, each with a corresponding request and response message type.
  - all ABCI++ messages and methods are defined in protocol buffers.
* the celestia-app state machine is necessary to execute the pod logic and to enable the governance of the fs layer. however, the celestia-app is data-agnostic - the state machine neither validates nor stores the data that is made available by the celestia-app.    

<br>

----

### celestia light nodes

<br>

* light nodes ensure da, and they are the most common way to interact with celestia.

<br>

<p align="center">
<img src="https://github.com/go-outside-labs/decentralized-protocols-research/assets/138340846/fe6907a2-1189-4b03-92b3-e70279004a72" width="80%" align="center" style="padding:1px;border:1px solid black;" title="Jan 7th"/>
</p>


<br>

---

### celestia full nodes

<br>

* full nodes store all the data.
* they send block shares, headers, and fraud proofs to light nodes (while light nodes gossif headers, fraud proofs, and sometimes block shares between one another).

<br>

<p align="center">
<img src="https://github.com/go-outside-labs/decentralized-protocols-research/assets/138340846/39e2b9a8-283a-42c6-b7dc-ec9c7d2fe48e" width="80%" align="center" style="padding:1px;border:1px solid black;" title="Jan 7th"/>
</p>

<br>

---

### ethereum fallback

<br>

* a mechanism that enables l2s to "fallback" to using ethereum calldata for da when celestia mainnet is under downtime. it's triggered whenever the sequencer has an error sending the `PayForBlobs` transacations to celestia.
* fallback can also be triggered due a congested mempool or nonce error, and can be simulated with an error as low as balance or incorrect sequence.

<br>

<p align="center">
<img src="https://github.com/go-outside-labs/decentralized-protocols-research/assets/138340846/fb1597fd-c4c7-4fdb-8ebd-d19811c2c256" width="80%" align="center" style="padding:1px;border:1px solid black;" title="Jan 7th"/>
</p>

<br>

-----

### blockspace

<br>

* to publish data on celestia, developers can submit `PayForBlobs` transactions, which consist of the identity of the sender, the data to be made available, the data size, the namespace, and a signature.
* each `PayForBlobs` transaction is split into two parts: the blob or blobs which include the data to be made available along with the namespace, and the executable payment transaction which includes a commitment to the data.
* both the blobs and executable payment transactions are put into the block within the appropriate namespace, the block data is extended using erasure coding and then merkelized into a data root commitment included in the block header.

<br>

<p align="center">
<img src="https://github.com/go-outside-labs/decentralized-protocols-research/assets/138340846/b62c80fe-d40a-493f-86da-d880bd867d99" width="80%" align="center" style="padding:1px;border:1px solid black;" title="Jan 7th"/>
</p>

<br>

* celestia uses a standard gas-price prioritised mempool, where transactions with higher fees will be prioritised by validators. fees are comprised of a flat fee per transaction and then a variable fee based on the size of each blob in the transaction.
  
<br>

---

### cool resources

<br>

* **[celestia docs](https://docs.celestia.org/learn/how-celestia-works/data-availability-layer#namespaced-merkle-trees-nmts)**
* **[cosmos sdk](https://docs.cosmos.network/)**
* **[tendermint consensus algorithm docs](https://docs.tendermint.com/)**
* **[building a sparse merkle tree from scratch in rust, by bt3gl](https://mirror.xyz/go-outside.eth/zX1BaGZLHAcQOKdhFnSSM0VW67_-OFCi5ZegGFPryvg)**
* **[lazyledger: a distributed da ledger with client-side smart contracts, by m. al-bassam](https://arxiv.org/abs/1905.09274)**
* **[fraud and da proofs: maximising light client security, by m. al-bassam et al.](https://arxiv.org/abs/1809.09044)**
