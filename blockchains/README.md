## blockchains 101

<br>

### chapters

<br>

* **[ethereum](ethereum)**
* **[bitcoin](bitcoin)**

<br>

---

### tl; dr

<br>

* **in general, blockchains have four core functions** (although modular blockchains specialize in one or two):
  * execution: transaction execution and state update.
  * settlement: finality and dispute resolution.
  * consensus: agreement on transaction ordering.
  * data availability: prove data was published to the network.
    
* **in general, each block in a blockchain consists of two pieces**:
  * a block header: metadata for the block, which consists of some basic information about the block, including the merkle root of txs.
  * the transaction data: making up the majority of the block, and consisting of actual transactions.

* **in general, a blockchain has two types of nodes**:
  * full nodes (fully validating nodes): they download and check that every tx in the blockchain is valid, and require lots of resources.
  * light clients: they don't download or validate any tx, but instead thye only download the block header and assume that the block only contains valid txs (less secure). light clients can rely on full nodes sending them a fraud proof if a block contains a invalid tx.

* **the data availability problem:**
  * in order to a full node to generate a fraud proof for a block, they need to know the tx data for that block. if a block producer just publishes the block header, but not the tx data, then full nodes won't be able to check if the txs are valid and generate fraud proofs.
  * it's a requirement that block producers must publish all the data for the blocks, but this needs to be enforced.
  * to solve this problem, there need to be a way for light clients to check that the tx data for a block was actually published to the network so full nodes can check it.   
   
<br>

----

### cool resources

<br>

#### cool learning

* **[authenticated data structures, generically (2014)](https://www.cs.umd.edu/~mwh/papers/gpads.pdf)**
* **[authenticated data structures as a library (2016)](https://bentnib.org/posts/2016-04-12-authenticated-data-structures-as-a-library.html)**
* **[understanding trie databases, by d. brickwood (2018)](https://medium.com/shyft-network/understanding-trie-databases-in-ethereum-9f03d2c3325d)**
* **[optimizing sparse merkle trees (2018)](https://ethresear.ch/t/optimizing-sparse-merkle-trees/3751)**
* **[leaves of hash, by trail of bits (2019)](https://blog.trailofbits.com/2019/06/17/leaves-of-hash/)**
* **[jellyfish merkle tree, by z. gao et al. (2021)](https://developers.diem.com/papers/jellyfish-merkle-tree/2021-01-14.pdf?ref=127.0.0.1)**
* **[on uploading your soul to the interplanetary sys, by bt3gl (2023)](https://mirror.xyz/go-outside.eth/A3iJGhXTJI5fgQoZVgIu3ovPV1P8zrxigpwngm0n4I0)**
* **[on a rusty sparse merkle tree experiment, by bt3gl (2023)](https://mirror.xyz/go-outside.eth/zX1BaGZLHAcQOKdhFnSSM0VW67_-OFCi5ZegGFPryvg)**
* **[how merkle trees work, by consensys (2024)](https://media.consensys.net/ever-wonder-how-merkle-trees-work-c2f8b7100ed3)**

<br>

#### cool tools

* **[bitcoin memory pool](https://www.blockchain.com/explorer/mempool/btc)**
* **[celestia's namespaced merkle tree](https://github.com/celestiaorg/nmt)**

<br>

#### cool discussions

* **[revisiting the world computer, by l. yang et al. (2024)](https://user.fm/files/v2-261b7914c204931fbf213d7d35307264/worldcomputer.pdf)**
* **[dba's journey towards ethereum's north star (2024)](https://dba.xyz/ethereums-north-star/)**
  

