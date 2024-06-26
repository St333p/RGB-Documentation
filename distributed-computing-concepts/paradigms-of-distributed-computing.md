# Paradigms of Distributed Computing

Before divining into the technical details of the RGB, the introduction to the fundamental concepts of the technology and the study of the base terminology represent an essential step towards a thorough understanding of the subject.

Indeed RGB it's a combination of several pieces of the Distributed Computing Domain, in particular:

* [Commitment](../annexes/glossary.md#commitment) scheme with cryptographic hash functions.
* [Client-side Validation](../annexes/glossary.md#client-side-validation).
* [Single-use Seals](../annexes/glossary.md#single-use-seal).

The combination of these topics is the underlying substrate that makes RGB operational.

RGB locates itself as a new additional piece of the vast world of _Distributed Computing_.

**Distributed computing**, is a branch of Computer Science that studies the protocol systems able to exchange and compute data information between a network of computer nodes: the set of computer nodes and the underlying protocol rules that allow the computation of these data are the constituents of a **Distributed System**.

The **nodes** composing the network **are able to independently verify and validate some set of data** and they can construct, depending on the protocol, complete or partial snapshots of information elaborated by the network: these are called the **states** of the distributed system and essentially represent the expression of properties and the underlying agreement over those properties that are established during network operations.

The most important property of a distributed system is represented by the **Chronological Ordering** of the operations and thus the **ordered sequence of state changes** that take place inside the system. In fact when we talk about **Consensus**, we are talking about:

1. **Recognizing the validity of the state changes** by the nodes according to the protocol rules.
2. **Establishing consensus on the order of the state changes** so that every node knows which operation precedes the other and the state cannot be reversed once it has changed: the so-called **anti double-spend property**.

The achievement of a _resilient and reliable_ chronological ordering for distributed systems, which embeds important properties such as permissiveness and censorship resistance, was reached by Satoshi Nakamoto with the invention of Bitcoin, using the blockchain data structure and a **Proof-of-Work (PoW)** consensus which is able to entrust different validating participants to the system according to their computational power. Indeed Bitcoin can be considered the first working example of a permissionless **Distributed Consensus System**.

We will discuss various kinds of **Distributed Consensus Systems** which have some degree of hierarchy and interrelated properties between them. They are differentiated on **how they determine and enforce the most updated state of the system**:

* **Blockchain + PoW Mechanism**. The sequence of **state transitions** is public and auditable and is organized in **transactions** included in ordered blocks which are added one upon the other. The system's security lies in the amount of work required to produce an alternative chain which reverts the actual greater-work chain, which is considered the valid chain. For instance, **Bitcoin** is based on this technological stack.
* **State Channel**. It's a system constructed between 2 (or more) parties and which **depend hierarchically** on the blockchain layer. **The final state is represented by the last transaction out of sequence of ordered invalidating transactions, signed and agreed by the parties **_**off-chain**_. The final state can be enforced by each parties by publishing that last valid transaction on the layer 1. The most known application of payment channels, a simplified form of state channels, is the [Lightning Network](../annexes/glossary.md#lightning-network).
* **Client Side Validated Data - Stash**. It's a system that **can be implemented both on top of blockchain and state channels** and it is based on a certain amount of data whose validity, computation tasks and uplocatesdate is entrusted to a limited number of nodes. Unlike layer 1, the data to be validated by each client node represent a **defined subset of the entirety of all state transitions of the client-side protocol, and not every transition happened within it**. This validated subset of data in possession of a client node is what is called **Stash**. Basically, the client needs to validate the whole history of the state transitions that occurred from the first to the last [transition](../annexes/glossary.md#state-transition) and which relate to some digital properties exchanged among the counterparties involved. Seen as a whole, the validation mechanism of the shard that produces the stash is called **Client-side Validation** and is at the base of all **RGB** operations.

<figure><img src="../.gitbook/assets/distributed-data-inc.png" alt=""><figcaption><p><strong>The 3 set of Distributed System - Blockchain (Layer 1) is self-sustaining while the other 2 rely on Layer 1 for operating. In turn, Stashes can operate on top of both Blockchain and State Channels.</strong></p></figcaption></figure>

In order to precisely frame the applications of each Distributed Consensus System and their underlying data structure it's important to understand the limitations that affect each one of these technology. This condition is expressed in form of a **Trilemma** which is connected to an important theoretical result of Distributed Computing, known as [CAP Theorem](https://en.wikipedia.org/wiki/CAP\_theorem). which states that:

> Any distributed system can provide simultaneously only two of the following three guarantees:
>
> * Consistency - Every node in the system agree on the current global state.
> * Availability - Every request to the system receives a response.
> * Partition Tolerance - The system continues to operate correctly despite a network partition, e.g. failures or delays between nodes.

<figure><img src="../.gitbook/assets/cap-theorem-full.png" alt=""><figcaption><p><strong>Application of CAP Theorem to Distributed Consensus System - Each Distributed Consensus System can fit 2 - and only 2 - out of the 3 properties.</strong></p></figcaption></figure>

Seen from a more consensus-focused point of view, the properties of the theorem can be reformulated in the following way:

* **Consistency** ==> Integrity
* **Availability** ==> Decentralization
* **Partition Tolerance** ==> Scalability and Confidentiality

<figure><img src="../.gitbook/assets/trilemma1.png" alt=""><figcaption><p><strong>A more in-depth view of the inherent degree of application of the Trilemma to Distributed Consensus System.</strong></p></figcaption></figure>

In synthesis:

* **Blockchains** preserve Integrity and Decentralization but **lack Scalability** and Confidentiality as each node needs to replicate _publicly and in full_ every state transition.
* **State Channels** preserve Decentralization and Scalability but **don't preserve Integrity** as the state can be changed or updated asynchronously by the counterparties.
* **Stashes of client-side validated data** are Scalable and maintain Integrity however, they **are not replicated** by the vast majority of nodes of the network **lacking Availability**. For this reason, these data are not fully recoverable in a completely decentralized way and some form of centralized backup is needed to recover them in case of loss.

An important feature to take into account is the different ways through which State Channel and Client-Side validation architectures update the state of the data:

* Channel state must be **synchronous** between the counterparts.
* Client-side validated state updates can be **asynchronous**.

Naturally, if the client-side validated data are embedded in the state channels, the state update will be ultimately based on an asynchronous process.

<figure><img src="../.gitbook/assets/triangle-bifi.png" alt=""><figcaption><p><strong>Blockchain is the base layer over which multiple-interacting layers can be constructed</strong></p></figcaption></figure>

In addition to the three layers just described, a fourth layer of Bitcoin Finance (#BiFi) which leverages both state channels and blockchain can complete the whole ecosystem. The general picture and the deep interconnections of all the layers, with the blockchain layer at the base, allow to achieve all the properties of the CAP theorem in a composite way.

In the next section, we will delve into Client-side Validation and its features.

***
