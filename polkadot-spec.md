<div class="ribbon">

<a href="https://github.com/w3f/polkadot-spec"
target="_blank">Contributions welcome!</a>

</div>

<div id="header">

# Polkadot Protocol Specification

<div class="details">

<span id="author" class="author">Web 3.0 Technologies
Foundation</span>  
<span id="revnumber">version 0.2.1</span>

</div>

<div id="toc" class="toc2">

<div id="toctitle">

Table of Contents

</div>

- [Polkadot Protocol](#id-polkadot-protocol)
- [Polkadot Host](#part-polkadot-host)
  - [1. Overview](#chap-overview)
    - [1.1. Light Client](#sect-client-light)
    - [1.2. Full Node](#sect-node-full)
    - [1.3. Authoring Node](#sect-node-authoring)
    - [1.4. Relaying Node](#sect-node-relaying)
  - [2. States and Transitions](#chap-state)
    - [2.1. Introduction](#id-introduction)
    - [2.2. State Replication](#sect-state-replication)
    - [2.3. Extrinsics](#sect-extrinsics)
    - [2.4. State Storage Trie](#sect-state-storage)
    - [2.5. Child Storage](#sect-child-storages)
    - [2.6. Runtime Interactions](#sect-runtime-interaction)
  - [3. Synchronization](#chap-sync)
    - [3.1. Warp Sync](#sect-sync-warp)
    - [3.2. Fast Sync](#sect-sync-fast)
    - [3.3. Full Sync](#id-full-sync)
    - [3.4. Importing and Validating Block](#sect-block-validation)
  - [4. Networking](#chap-networking)
    - [4.1. Introduction](#id-introduction-2)
    - [4.2. External Documentation](#sect-networking-external-docs)
    - [4.3. Node Identities](#id-node-identities)
    - [4.4. Discovery mechanism](#sect-discovery-mechanism)
    - [4.5. Connection establishment](#sect-connection-establishment)
    - [4.6. Encryption Layer](#sect-encryption-layer)
    - [4.7. Protocols and Substreams](#sect-protocols-substreams)
    - [4.8. Network Messages](#sect-network-messages)
  - [5. Block Production](#sect-block-production)
    - [5.1. Introduction](#id-introduction-3)
    - [5.2. Block Production Lottery](#sect-block-production-lottery)
    - [5.3. Slot Number Calculation](#sect-slot-number-calculation)
    - [5.4. Production Algorithm](#block-production)
    - [5.5. Epoch Randomness](#sect-epoch-randomness)
    - [5.6. Verifying Authorship Right](#sect-verifying-authorship)
    - [5.7. Block Building Process](#sect-block-building)
  - [6. Finality](#sect-finality)
    - [6.1. Introduction](#id-introduction-4)
    - [6.2. Initiating the GRANDPA
      State](#id-initiating-the-grandpa-state)
    - [6.3. Rejoining the Same Voter
      Set](#id-rejoining-the-same-voter-set)
    - [6.4. Voting Process in Round
      \\r\\](#id-voting-process-in-round-r)
    - [6.5. Forced Authority Set Changes](#sect-finality-forced-changes)
    - [6.6. Block Finalization](#sect-block-finalization)
    - [6.7. Bridge design (BEEFY)](#sect-grandpa-beefy)
  - [7. Light Clients](#sect-lightclient)
    - [7.1. Requirements for Light
      Clients](#sect-requirements-lightclient)
    - [7.2. Warp Sync for Light Clients](#sect-sync-warp-lightclient)
    - [7.3. Runtime Environment for Light
      Clients](#sect-runtime-environment-lightclient)
    - [7.4. Light Client Messages](#sect-light-msg)
    - [7.5. Storage for Light Clients](#sect-storage-lightclient)
  - [8. Availability & Validity](#chapter-anv)
    - [8.1. Collations](#sect-collations)
    - [8.2. Candidate Backing](#sect-candidate-backing)
    - [8.3. Candidate Validation](#sect-candidate-validation)
    - [8.4. Availability](#sect-availability)
    - [8.5. Approval Voting](#sect-approval-voting)
    - [8.6. Disputes](#sect-disputes)
    - [8.7. Network Messages](#sect-anv-network-messages)
    - [8.8. Definitions](#sect-anv-definitions)
- [Polkadot Runtime](#part-polkadot-runtime)
  - [9. Extrinsics](#id-extrinsics)
    - [9.1. Introduction](#id-introduction-5)
    - [9.2. Preliminaries](#id-preliminaries-3)
    - [9.3. Extrinsics Body](#id-extrinsics-body)
  - [10. Weights](#id-weights)
    - [10.1. Motivation](#id-motivation)
    - [10.2. Assumptions](#sect-assumptions)
    - [10.3. Calculation of the weight
      function](#sect-runtime-primitives)
    - [10.4. Benchmarking](#sect-benchmarking)
    - [10.5. Practical examples](#sect-practical-examples)
    - [10.6. Fees](#id-fees)
  - [11. Consensus](#id-consensus)
    - [11.1. BABE digest messages](#id-babe-digest-messages)
  - [12. Metadata](#sect-metadata)
    - [12.1. Structure](#sect-rtm-structure)
    - [12.2. Pallet Metadata](#sect-rtm-pallet-metadata)
    - [12.3. Extrinsic Metadata](#sect-rtm-extrinsic-metadata)
- [Appendix A: Cryptography & Encoding](#id-cryptography-encoding)
  - [A.1. Cryptographic Algorithms](#chapter-crypto-algos)
  - [A.2. Auxiliary Encodings](#chapter-encoding)
  - [A.3. Genesis State](#chapter-genesis)
  - [A.4. Erasure Encoding](#chapter-erasure-encoding)
- [Appendix B: Host API](#chap-host-api)
  - [B.1. Preliminaries](#id-preliminaries-4)
  - [B.2. Storage](#sect-storage-api)
  - [B.3. Child Storage](#sect-child-storage-api)
  - [B.4. Crypto](#sect-crypto-api)
  - [B.5. Hashing](#sect-hashing-api)
  - [B.6. Offchain](#sect-offchain-api)
  - [B.7. Trie](#sect-trie-api)
  - [B.8. Miscellaneous](#sect-misc-api)
  - [B.9. Allocator](#sect-allocator-api)
  - [B.10. Logging](#sect-logging-api)
  - [B.11. Abort Handler](#id-abort-handler)
- [Appendix C: Runtime API](#chap-runtime-api)
  - [C.1. General Information](#id-general-information)
  - [C.2. Runtime Constants](#id-runtime-constants)
  - [C.3. Runtime Call Convention](#id-runtime-call-convention)
  - [C.4. Module Core](#sect-runtime-core-module)
  - [C.5. Module Metadata](#sect-runtime-metadata-module)
  - [C.6. Module BlockBuilder](#sect-runtime-blockbuilder-module)
  - [C.7. Module TaggedTransactionQueue](#sect-runtime-txqueue-module)
  - [C.8. Module OffchainWorkerApi](#sect-runtime-offchainapi-module)
  - [C.9. Module ParachainHost](#sect-anv-runtime-api)
  - [C.10. Module GrandpaApi](#id-module-grandpaapi)
  - [C.11. Module BabeApi](#id-module-babeapi)
  - [C.12. Module AccountNonceApi](#id-module-accountnonceapi)
- [Bibliography](#id-bibliography)
- [Glossary](#id-glossary)

</div>

</div>

<div id="content">

<div class="sect1">

## <a href="#id-polkadot-protocol" class="anchor"></a><a href="#id-polkadot-protocol" class="link">Polkadot Protocol</a>

<div class="sectionbody">

<div class="admonitionblock warning">

|     |                                                                                                                                  |
|-----|----------------------------------------------------------------------------------------------------------------------------------|
|     | This specification is **Work-In-Progress** and any content, structure, design and/or hyper/anchor-link **is subject to change**. |

</div>

<div class="paragraph">

Formally, Polkadot is a replicated sharded state machine designed to
resolve the scalability and interoperability among blockchains. In
Polkadot vocabulary, shards are called *parachains* and Polkadot *relay
chain* is part of the protocol ensuring global consensus among all the
parachains. The Polkadot relay chain protocol, henceforward called
*Polkadot protocol*, can itself be considered as a replicated state
machine on its own. As such, the protocol can be specified by
identifying the state machine and the replication strategy.

</div>

<div class="paragraph">

From a more technical point of view, the Polkadot protocol has been
divided into two parts, the [Polkadot Runtime](#part-polkadot-runtime)
and the [Polkadot Host](#part-polkadot-host). The Runtime comprises the
state transition logic for the Polkadot protocol and is designed and be
upgradable via the consensus engine without requiring hard forks of the
blockchain. The Polkadot Host provides the necessary functionality for
the Runtime to execute its state transition logic, such as an execution
environment, I/O, consensus and network interoperability between
parachains. The Polkadot Host is planned to be stable and mostly static
for the lifetime duration of the Polkadot protocol, the goal being that
most changes to the protocol are primarily conducted by applying Runtime
updates and not having to coordinate with network participants on manual
software updates.

</div>

</div>

</div>

# <a href="#part-polkadot-host" class="anchor"></a><a href="#part-polkadot-host" class="link">Polkadot Host</a>

<div class="openblock partintro">

<div class="content">

With the current document, we aim to specify the Polkadot Host part of
the Polkadot protocol as a replicated state machine. After defining the
different types of hosts in [Chapter 1](#chap-overview), we proceed to
specify the representation of a valid state of the Protocol in [Chapter
2](#chap-state). We also identify the protocol states, by explaining the
Polkadot state transition and discussing the detail based on which the
Polkadot Host interacts with the state transition function, i.e. Runtime
in the same chapter. Following, we specify the input messages triggering
the state transition and the system behavior. In [Chapter
4](#chap-networking), we specify the communication protocols and network
messages required for the Polkadot Host to communicate with other nodes
in the network, such as exchanging blocks and consensus messages. In
[Chapter 5](#sect-block-production) and [Chapter 6](#sect-finality), we
specify the consensus protocol, which is responsible for keeping all the
replica in the same state. Finally, the initial state of the machine is
identified and discussed in [Section A.3](#chapter-genesis). A Polkadot
Host implementation which conforms with this part of the specification
should successfully be able to sync its states with the Polkadot
network.

</div>

</div>

<div class="sect1">

## <a href="#chap-overview" class="anchor"></a><a href="#chap-overview" class="link">1. Overview</a>

<div class="sectionbody">

<div class="paragraph">

The Polkadot Protocol differentiates between different classes of
Polkadot Hosts. Each class differs in their trust roots and how active
or passively they interact with the network.

</div>

<div class="sect2">

### <a href="#sect-client-light" class="anchor"></a><a href="#sect-client-light" class="link">1.1. Light Client</a>

<div class="paragraph">

The light client is a mostly passive participant in the protocol. Light
clients are designed to work in resource constrained environments like
browsers, mobile devices or even on-chain. Its main objective is to
follow the chain, make queries to the full node on specific information
on recent state of the blockchain, and to add extrinsics (transactions).
It does not maintain the full state, rather queries the full node on the
latest finalized state and verifies the authenticity of the responses
trustlessly. Details of specifications focused for Light Clients can be
found in [Chapter 7](#sect-lightclient).

</div>

</div>

<div class="sect2">

### <a href="#sect-node-full" class="anchor"></a><a href="#sect-node-full" class="link">1.2. Full Node</a>

<div class="paragraph">

While the full node is still a mostly passive participant of the
protocol, they follow the chain by receiving and verifying every block
in the chain. It maintains full state of the blockchain by executing the
extrinsics in blocks. Their role in consesus mechanism is limited to
following the chain and not producing the blocks.

</div>

<div class="ulist">

- **Functional Requirements:**

  <div class="olist arabic">

  1.  The node must populate the state storage with the official genesis
      state, elaborated further in [Section A.3](#chapter-genesis).

  2.  The node should maintain a set of around 50 active peers at any
      time. New peers can be found using the discovery protocols
      ([Section 4.4](#sect-discovery-mechanism))

  3.  The node should open and maintain the various required streams
      ([Section 4.7](#sect-protocols-substreams)) with each of its
      active peers.

  4.  Furthermore, the node should send block requests ([Section
      4.8.2](#sect-msg-block-request)) to these peers to receive all
      blocks in the chain and execute each of them.

  5.  The node should exchange neighbor packets ([Section
      4.8.6.1](#sect-grandpa-neighbor-msg)).

  </div>

</div>

</div>

<div class="sect2">

### <a href="#sect-node-authoring" class="anchor"></a><a href="#sect-node-authoring" class="link">1.3. Authoring Node</a>

<div class="paragraph">

The authoring node covers all the features of the full node but instead
of just passivly following the protocol, it is an active participant,
producing blocks and voting in Grandpa.

</div>

<div class="ulist">

- **Functional Requirements:**

  <div class="olist arabic">

  1.  Verify that the Host’s session key is included in the current
      Epoch’s authority set ([Section 3.3.1](#sect-authority-set)).

  2.  Run the BABE lottery ([Chapter 5](#sect-block-production)) and
      wait for the next assigned slot in order to produce a block.

  3.  Gossip any produced blocks to all connected peers ([Section
      4.8.1](#sect-msg-block-announce)).

  4.  Run the catch-up protocol ([Section 6.6.1](#sect-grandpa-catchup))
      to make sure that the node is participating in the current round
      and not a past round.

  5.  Run the GRANDPA rounds protocol ([Chapter 6](#sect-finality)).

  </div>

</div>

</div>

<div class="sect2">

### <a href="#sect-node-relaying" class="anchor"></a><a href="#sect-node-relaying" class="link">1.4. Relaying Node</a>

<div class="paragraph">

The relaying node covers all the features of the authoring node, but
also participants in the availability and validity process to process
new parachain blocks as described in [Chapter 8](#chapter-anv).

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#chap-state" class="anchor"></a><a href="#chap-state" class="link">2. States and Transitions</a>

<div class="sectionbody">

<div class="sect2">

### <a href="#id-introduction" class="anchor"></a><a href="#id-introduction" class="link">2.1. Introduction</a>

<div id="defn-state-machine" class="exampleblock">

<div class="title">

Definition 1. [Discrete State Machine (DSM)](#defn-state-machine)

</div>

<div class="content">

<div class="paragraph">

A **Discrete State Machine (DSM)** is a state transition system that
admits a starting state and whose set of states and set of transitions
are countable. Formally, it is a tuple of

</div>

<div class="stemblock">

<div class="content">

\\(\Sigma, S, s_0, \delta)\\

</div>

</div>

<div class="paragraph">

where

</div>

<div class="ulist">

- \\\Sigma\\ is the countable set of all possible inputs.

- \\S\\ is a countable set of all possible states.

- \\s_0 in S\\ is the initial state.

- \\\delta\\ is the state-transition function, known as **Runtime** in
  the Polkadot vocabulary, such that

</div>

<div class="stemblock">

<div class="content">

\\\delta : S \times \Sigma \rightarrow S\\

</div>

</div>

</div>

</div>

<div id="defn-path-graph" class="exampleblock">

<div class="title">

Definition 2. [Path Graph](#defn-path-graph)

</div>

<div class="content">

<div class="paragraph">

A **path graph** or a **path** of \\n\\ nodes formally referred to as
**\\P_n\\**, is a tree with two nodes of vertex degree 1 and the other
n-2 nodes of vertex degree 2. Therefore, \\P_n\\ can be represented by
sequences of \\(v_1, \ldots, v_n)\\ where \\e_i = (v_i, v\_{i + 1})\\
for \\1 \<= i \<= n - 1\\ is the edge which connect \\v_i\\ and
\\v\_{i + 1}\\.

</div>

</div>

</div>

<div id="defn-blockchain" class="exampleblock">

<div class="title">

Definition 3. [Blockchain](#defn-blockchain)

</div>

<div class="content">

<div class="paragraph">

A **blockchain** \\C\\ is a [directed path
graph](https://en.wikipedia.org/wiki/Directed_graph). Each node of the
graph is called **Block** and indicated by **\\B\\**. The unique sink of
\\C\\ is called **Genesis Block**, and the source is called the
\\"Head"\\ of \\C\\. For any vertex \\(B_1, B_2)\\ where \\B_1 -\> B_2\\
we say \\B_2\\ is the **parent** of \\B_1\\, which is the **child** of
\\B_2\\, respectively. We indicate that by:

</div>

<div class="stemblock">

<div class="content">

\\B_2 := P(B_1)\\

</div>

</div>

<div class="paragraph">

The parent refers to the child by its hash value ([Definition
10](#defn-block-header)), making the path graph tamper proof since any
modifications to the child would result in its hash value being changed.

</div>

<div class="admonitionblock note">

|     |                                                                                                                                        |
|-----|----------------------------------------------------------------------------------------------------------------------------------------|
|     | The term "blockchain" can also be used as a way to refer to the network or system that interacts or maintains the directed path graph. |

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-block-tree" class="anchor"></a><a href="#id-block-tree" class="link">2.1.1. Block Tree</a>

<div class="paragraph">

In the course of formation of a (distributed) blockchain, it is possible
that the chain forks into multiple subchains in various block positions.
We refer to this structure as a *block tree*:

</div>

<div id="defn-block-tree" class="exampleblock">

<div class="title">

Definition 4. [Block](#defn-block-tree)

</div>

<div class="content">

<div class="paragraph">

The **block tree** of a blockchain, denoted by \\BT\\ is the union of
all different versions of the blockchain observed by the Polkadot Host
such that every block is a node in the graph and \\B_1\\ is connected to
\\B_2\\ if \\B_1\\ is a parent of \\B_2\\.

</div>

</div>

</div>

<div class="paragraph">

When a block in the block tree gets finalized, there is an opportunity
to prune the block tree to free up resources into branches of blocks
that do not contain all of the finalized blocks or those that can never
be finalized in the blockchain ([Chapter 6](#sect-finality)).

</div>

<div id="defn-pruned-tree" class="exampleblock">

<div class="title">

Definition 5. [Pruned Block Tree](#defn-pruned-tree)

</div>

<div class="content">

<div class="paragraph">

By **Pruned Block Tree**, denoted by \\"PBT"\\, we refer to a subtree of
the block tree obtained by eliminating all branches which do not contain
the most recent finalized blocks ([Definition
90](#defn-finalized-block)). By **pruning**, we refer to the procedure
of \\BT larr "PBT"\\. When there is no risk of ambiguity and is safe to
prune BT, we use \\"BT"\\ to refer to \\"PBT"\\.

</div>

</div>

</div>

<div class="paragraph">

[Definition 6](#defn-chain-subchain) gives the means to highlight
various branches of the block tree.

</div>

<div id="defn-chain-subchain" class="exampleblock">

<div class="title">

Definition 6. [Subchain](#defn-chain-subchain)

</div>

<div class="content">

<div class="paragraph">

Let \\G\\ be the root of the block tree and \\B\\ be one of its nodes.
By \\"Chain"(B)\\, we refer to the path graph from \\G\\ to \\B\\ in
\\"BT"\\. Conversely, for a chain \\C = "Chain"(B)\\, we define **the
head of \\C\\** to be \\B\\, formally noted as \\B := bar C\\. We define
\\\|C\|\\, the length of \\C\\ as a path graph.

</div>

<div class="paragraph">

If \\B'\\ is another node on \\"Chain"(B)\\, then by \\"SubChain"(B',
B)\\ we refer to the subgraph of \\"Chain"(B)\\ path graph which
contains \\B\\ and ends at \\B'\\ and by \\\|"SubChain"(B', B)\|\\ we
refer to its length.

</div>

<div class="paragraph">

Accordingly, \\bbb C\_(B')(BT)\\ is the set of all subchains of \\BT\\
rooted at \\B'\\. The set of all chains of \\BT\\, \\bbb C_G(BT))\\ is
denoted by \\bbb C(BT)\\ or simply \\bbb C\\, for the sake of brevity.

</div>

</div>

</div>

<div id="defn-longest-chain" class="exampleblock">

<div class="title">

Definition 7. [Longest Chain](#defn-longest-chain)

</div>

<div class="content">

<div class="paragraph">

We define the following complete order over \\bbb C\\ as follows. For
chains \\C_1, C_2 in bbb C\\ we have that \\C_1 \> C_2\\ if either
\\\|C_1\| \> \|C_2\|\\ or \\\|C_1\| = \|C_2\|\\.

</div>

<div class="paragraph">

If \\\|C_1\| =\| C_2\|\\ we say \\C_1 \> C_2\\ if and only if the block
arrival time ([Definition 67](#defn-block-time)) of \\bar C_1\\ is less
than the block arrival time of \\bar C_2\\, from the *subjective
perspective* of the Host. We define the \\"Longest-Chain"(BT)\\ to be
the maximum chain given by this order.

</div>

</div>

</div>

<div id="defn-longest-path" class="exampleblock">

<div class="title">

Definition 8. [Longest Path](#defn-longest-path)

</div>

<div class="content">

<div class="paragraph">

\\"Longest-Path"(BT)\\ returns the path graph of \\BT\\ which is the
longest among all paths in \\BT\\ and has the earliest block arrival
time ([Definition 67](#defn-block-time)). \\"Deepest-Leaf"(BT)\\ returns
the head of \\"Longest-Path"(BT)\\ chain.

</div>

</div>

</div>

<div class="paragraph">

Because every block in the blockchain contains a reference to its
parent, it is easy to see that the block tree is de facto a tree. A
block tree naturally imposes partial order relationships on the blocks
as follows:

</div>

<div id="defn-descendant-ancestor" class="exampleblock">

<div class="title">

Definition 9. [Descendant and Ancestor](#defn-descendant-ancestor)

</div>

<div class="content">

<div class="paragraph">

We say \\B\\ is **descendant** of \\B'\\, formally noted as \\B \> B'\\,
if \\(\|B\| \> \|B'\|) in C\\. Respectively, we say that \\B'\\ is an
**ancestor** of \\B\\, formally noted as \\B \< B'\\, if \\(\|B\| \<
\|B'\|) in C\\.

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-state-replication" class="anchor"></a><a href="#sect-state-replication" class="link">2.2. State
Replication</a>

<div class="paragraph">

Polkadot nodes replicate each other’s state by syncing the history of
the extrinsics. This, however, is only practical if a large set of
transactions are batched and synced at the time. The structure in which
the transactions are journaled and propagated is known as a block of
extrinsics ([Section 2.2.1](#sect-block-format)). Like any other
replicated state machines, state inconsistency can occure between
Polkadot replicas. [Section 2.4.5](#sect-managing-multiple-states) gives
an overview of how a Polkadot Host node manages multiple variants of the
state.

</div>

<div class="sect3">

#### <a href="#sect-block-format" class="anchor"></a><a href="#sect-block-format" class="link">2.2.1. Block Format</a>

<div class="paragraph">

A Polkadot block consists a *block header* ([Definition
10](#defn-block-header)) and a *block body* ([Definition
13](#defn-block-body)). The *block body* in turn is made up out of
*extrinsics* , which represent the generalization of the concept of
*transactions*. *Extrinsics* can contain any set of external data the
underlying chain wishes to validate and track.

</div>

seq: - id: header type: block_header - id: body type: block_body

<div id="defn-block-header" class="exampleblock">

<div class="title">

Definition 10. [Block Header](#defn-block-header)

</div>

<div class="content">

<div class="paragraph">

The **header of block B**, \\H_h(B)\\, is a 5-tuple containing the
following elements:

</div>

<div class="ulist">

- **parent_hash:** formally indicated as \\H_p\\, is the 32-byte Blake2b
  hash ([Section A.1.1.1](#sect-blake2)) of the SCALE encoded parent
  block header ([Definition 12](#defn-block-header-hash)).

- **number:** formally indicated as \\H_i\\, is an integer, which
  represents the index of the current block in the chain. It is equal to
  the number of the ancestor blocks. The genesis state has number 0.

- **state_root:** formally indicated as \\H_r\\, is the root of the
  Merkle trie, whose leaves implement the storage for the system.

- **extrinsics_root:** is the field which is reserved for the Runtime to
  validate the integrity of the extrinsics composing the block body. For
  example, it can hold the root hash of the Merkle trie which stores an
  ordered list of the extrinsics being validated in this block. The
  <span class="sans-serif">extrinsics_root</span> is set by the runtime
  and its value is opaque to the Polkadot Host. This element is formally
  referred to as \\H_e\\.

- **digest:** this field is used to store any chain-specific auxiliary
  data, which could help the light clients interact with the block
  without the need of accessing the full storage as well as
  consensus-related data including the block signature. This field is
  indicated as \\H_d\\ ([Definition 11](#defn-digest)).

</div>

</div>

</div>

seq: - id: parent_hash size: 32 - id: number type: scale::compact_int -
id: state_root size: 32 - id: extrinsic_root size: 32 - id: num_digests
type: scale::compact_int - id: digests type: digest repeat: expr
repeat-expr: num_digests.value

<div id="defn-digest" class="exampleblock">

<div class="title">

Definition 11. [Header Digest](#defn-digest)

</div>

<div class="content">

<div class="paragraph">

The header **digest** of block \\B\\ formally referred to by \\H_d (B)\\
is an array of **digest items** \\H_d^i\\’s, known as digest items of
varying data type ([Definition 188](#defn-varrying-data-type)) such
that:

</div>

<div class="stemblock">

<div class="content">

\\H_d(B) := H_d^1, ..., H_d^n\\

</div>

</div>

<div class="paragraph">

where each digest item can hold one of the following type identifiers:

</div>

<div class="stemblock">

<div class="content">

\\H_d^i = { (4, to, (t, "id", m)), (5, to, (t, "id", m)), (6, to, (t,
"id", m)), (8, to, (t)) :}\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\"id"\\ is a 4-byte ASCII encoded consensus engine identifier

- \\"m"\\ is a scale encoded byte array containing the message payload

</div>

</div>

<div class="hdlist">

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td class="hdlist1">\$t = 4\$</td>
<td class="hdlist2"><p><strong>Consensus Message</strong>, contains
scale-encoded message \$m\$ from the Runtime to the consensus engine.
The receiving engine is determined by the \$"id"\$ identifier:</p>
<div class="dlist">
<dl>
<dt>\$"id" = tt "BABE"\$</dt>
<dd>
<p>a message to BABE engine (<a
href="#defn-consensus-message-babe">Definition 58</a>)</p>
</dd>
<dt>\$"id" = tt "FRNK"\$</dt>
<dd>
<p>a message to GRANDPA engine (<a
href="#defn-consensus-message-grandpa">Definition 86</a>)</p>
</dd>
<dt>\$"id" = tt "BEEF"\$</dt>
<dd>
<p>a message to BEEFY engine (<a
href="#defn-consensus-message-beefy">Definition 87</a>)</p>
</dd>
</dl>
</div></td>
</tr>
<tr class="even">
<td class="hdlist1">\$t = 5\$</td>
<td class="hdlist2"><p><strong>Seal</strong>, is produced by the
consensus engine and proves the authorship of the block producer. The
engine used for this is provided through \$"id"\$ (at the moment
<code>BABE</code>), while \$m\$ contains the scale-encoded signature (<a
href="#defn-block-signature">Definition 70</a>) of the block producer.
In particular, the Seal digest item must be the last item in the digest
array and must be stripped off by the Polkadot Host before the block is
submitted to any Runtime function including for validation. The Seal
must be added back to the digest afterward.</p></td>
</tr>
<tr class="odd">
<td class="hdlist1">\$t = 6\$</td>
<td class="hdlist2"><p><strong>Pre-Runtime</strong> digest, contains
messages from the consensus engines to the runtime. Currently only used
by BABE to pass the scale encoded BABE Header (<a
href="#defn-babe-header">Definition 69</a>) in \$m\$ with \$"id" = tt
"BABE"\$</p></td>
</tr>
<tr class="even">
<td class="hdlist1">\$t = 8\$</td>
<td class="hdlist2"><p><strong>Runtime Environment Updated</strong>
digest, indicates that changes regarding the Runtime code or heap pages
(<a href="#sect-memory-management">Section 2.6.3.1</a>) occurred. No
additional data is provided.</p></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

seq: - id: type type: u1 enum: type_id - id: value type: switch-on: type
cases: 'type_id::pre_runtime': pre_runtime 'type_id::post_runtime':
post_runtime 'type_id::seal': seal 'type_id::runtime_updated': empty
enums: type_id: 4: post_runtime 5: seal 6: pre_runtime 8:
runtime_updated types: pre_runtime: seq: - id: engine type: str
encoding: ASCII size: 4 - id: payload type: scale::bytes post_runtime:
seq: - id: engine type: str encoding: ASCII size: 4 - id: payload type:
scale::bytes seal: seq: - id: engine type: str encoding: ASCII size: 4 -
id: payload type: scale::bytes empty: {}

<div id="defn-block-header-hash" class="exampleblock">

<div class="title">

Definition 12. [Header Hash](#defn-block-header-hash)

</div>

<div class="content">

<div class="paragraph">

The **block header hash of block \\B\\**, \\H_h(B)\\, is the hash of the
header of block \\B\\ encoded by simple codec:

</div>

<div class="stemblock">

<div class="content">

\\H_h(B) := "Blake2b"("Enc"\_(SC)("Head"(B)))\\

</div>

</div>

</div>

</div>

<div id="defn-block-body" class="exampleblock">

<div class="title">

Definition 13. [Block Body](#defn-block-body)

</div>

<div class="content">

<div class="paragraph">

The block body consists of an sequence of extrinsics, each encoded as a
byte array. The content of an extrinsic is completely opaque to the
Polkadot Host. As such, from the point of the Polkadot Host, and is
simply a SCALE encoded array of byte arrays. The **body of Block** \\B\\
represented as \\"Body"(B)\\ is defined to be:

</div>

<div class="stemblock">

<div class="content">

\\"Body"(B) := "Enc"\_(SC)(E_1,...,E_n)\\

</div>

</div>

<div class="paragraph">

Where each \\E_i in bbb B\\ is a SCALE encoded extrinsic.

</div>

seq: - id: num_transactions type: scale::compact_int - id: transactions
type: transaction repeat: expr repeat-expr: num_transactions.value
types: transaction: seq: - id: len_data type: scale::compact_int - id:
data size: len_data.value

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-extrinsics" class="anchor"></a><a href="#sect-extrinsics" class="link">2.3. Extrinsics</a>

<div class="paragraph">

The block body consists of an array of extrinsics. In a broad sense,
extrinsics are data from outside of the state which can trigger state
transitions. This section describes extrinsics and their inclusion into
blocks.

</div>

<div class="sect3">

#### <a href="#id-preliminaries" class="anchor"></a><a href="#id-preliminaries" class="link">2.3.1. Preliminaries</a>

<div class="paragraph">

The extrinsics are divided into two main categories defined as follows:

</div>

<div class="paragraph">

**Transaction extrinsics** are extrinsics which are signed using either
of the key types ([Section A.1.4](#sect-cryptographic-keys)) and
broadcasted between the nodes. **Inherent extrinsics** are unsigned
extrinsics which are generated by Polkadot Host and only included in the
blocks produced by the node itself. They are broadcasted as part of the
produced blocks rather than being gossiped as individual extrinsics.

</div>

<div class="paragraph">

The Polkadot Host does not specify or limit the internals of each
extrinsics and those are defined and dealt with by the Runtime
([Definition 1](#defn-state-machine)). From the Polkadot Host point of
view, each extrinsics is simply a SCALE-encoded blob ([Section
A.2.2](#sect-scale-codec)).

</div>

</div>

<div class="sect3">

#### <a href="#id-transactions" class="anchor"></a><a href="#id-transactions" class="link">2.3.2. Transactions</a>

<div class="paragraph">

Transaction are submitted and exchanged through *Transactions* network
messages ([Section 4.8.5](#sect-msg-transactions)). Upon receiving a
Transactions message, the Polkadot Host decodes the SCALE-encoded blob
and splits it into individually SCALE-encoded transactions.

</div>

<div class="paragraph">

Alternative transaction can be submitted to the host by offchain worker
through the Host API ([Section
B.6.2](#sect-ext-offchain-submit-transaction)).

</div>

<div class="paragraph">

Any new transaction should be submitted to the Runtime ([Section
C.7.1](#sect-rte-validate-transaction)). This will allow the Polkadot
Host to check the validity of the received transaction against the
current stat and if it should be gossiped to other peers. If it
considers the submitted transaction as valid, the Polkadot Host should
store it for inclusion in future blocks. The whole process of handling
new transactions is described in more detail by
[Validate-Transactions-and-Store](#algo-validate-transactions).

</div>

<div class="paragraph">

Additionally valid transactions that are supposed to be gossiped are
propagated to connected peers of the Polkadot Host. While doing so the
Polkadot Host should keep track of peers already aware of each
transaction. This includes peers which have already gossiped the
transaction to the node as well as those to whom the transaction has
already been sent. This behavior is mandated to avoid resending
duplicates and unnecessarily overloading the network. To that aim, the
Polkadot Host should keep a *transaction pool* and a *transaction queue*
defined as follows:

</div>

<div id="defn-transaction-queue" class="exampleblock">

<div class="title">

Definition 14. [Transaction Queue](#defn-transaction-queue)

</div>

<div class="content">

<div class="paragraph">

The **Transaction Queue** of a block producer node, formally referred to
as \\TQ\\ is a data structure which stores the transactions ready to be
included in a block sorted according to their priorities ([Section
4.8.5](#sect-msg-transactions)). The **Transaction Pool**, formally
referred to as \\TP\\, is a hash table in which the Polkadot Host keeps
the list of all valid transactions not in the transaction queue.

</div>

</div>

</div>

<div class="paragraph">

Furthermore
[Validate-Transactions-and-Store](#algo-validate-transactions) updates
the transaction pool and the transaction queue according to the received
message:

</div>

<div class="sidebarblock">

<div class="content">

\state \$L \leftarrow Dec\_{SC}(M_T)\$ \forall{\$\\T \in L \mid T \notin
TQ \mid T \notin TP\\\$} \state \$B_d \leftarrow\$
\call{Head}{\call{Longest-Chain}{\$BT\$}} \state \$N \leftarrow
H_n(B_d)\$ \state \$R \leftarrow\$
\call{Call-Runtime-Entry}{\$\texttt{TaggedTransactionQueue\\validate\\transaction},
N, T\$} \if{\call{Valid}{\$R\$}} \if{\call{Requires}{\$R\$}\$ \subset
\bigcup\_{\forall T \in (TQ~\cup~B_i \mid \exists i \< d)}\$
\call{Provided-Tags}{\$T\$}} \state \call{Insert-At}{\$TQ, T,
\$\call{Requires}{\$R\$}\$, \$\call{Priority}{\$R\$}} \else \state
\call{Add-To}{\$TP,T\$} \endif \state \call{Maintain-Transaction-Pool}{}
\if{\call{ShouldPropagate}{\$R\$}} \state \call{Propagate}{\$T\$} \endif
\endif \endfor

<div class="dlist">

where  
<div class="ulist">

- \\M_T\\ is the transaction message (offchain transactions?)

- \\"Dec"\_(SC)\\ decodes the SCALE encoded message.

- \\"Longest-Chain"\\ is defined in [Definition 7](#defn-longest-chain).

- \\tt "TaggedTransactionQueue_validate_transaction"\\ is a Runtime
  entrypoint specified in [Section
  C.7.1](#sect-rte-validate-transaction) and \\Requires(R)\\,
  \\Priority(R)\\ and \\Propagate(R)\\ refer to the corresponding fields
  in the tuple returned by the entrypoint when it deems that \\T\\ is
  valid.

- \\"Provided-Tags"(T)\\ is the list of tags that transaction \\T\\
  provides. The Polkadot Host needs to keep track of tags that
  transaction \\T\\ provides as well as requires after validating it.

- \\"Insert-At"(TQ,T,"Requires"(R),"Priority"(R))\\ places \\T\\ into
  \\TQ\\ approperietly such that the transactions providing the tags
  which \\T\\ requires or have higher priority than \\T\\ are ahead of
  \\T\\.

- \\"Maintain-Transaction-Pool"\\ is described in
  [Maintain-Transaction-Pool](#algo-maintain-transaction-pool).

- \\"ShouldPropagate"\\ indictes whether the transaction should be
  propagated based on the `Propagate` field in the `ValidTransaction`
  type as defined in [Definition 225](#defn-valid-transaction), which is
  returned by \\tt "TaggedTransactionQueue_validate_transaction"\\.

- \\"Propagate"(T)\\ sends \\T\\ to all connected peers of the Polkadot
  Host who are not already aware of \\T\\.

</div>

</div>

</div>

</div>

<div class="sidebarblock">

<div class="content">

\state Scan the pool for ready transactions \state Move them to the
transaction queue \state Drop invalid transactions

<div class="admonitionblock note">

|     |                                |
|-----|--------------------------------|
|     | This has not been defined yet. |

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-inherents" class="anchor"></a><a href="#sect-inherents" class="link">2.3.3. Inherents</a>

<div class="paragraph">

Inherents are unsigned extrinsics inserted into a block by the block
author and as a result are not stored in the transaction pool or
gossiped across the network. Instead they are generated by the Polkadot
Host by passing the required inherent data, as listed in [Table
1](#tabl-inherent-data), to the Runtime method \\tt
"BlockBuilder_inherent_extrinsics"\\ ([Section
C.6.3](#defn-rt-builder-inherent-extrinsics)). Then the returned
extrinsics should be included in the current block as explained in
[Build-Block](#algo-build-block).

</div>

| Identifier | Value Type                                                                | Description                                                                |
|------------|---------------------------------------------------------------------------|----------------------------------------------------------------------------|
| timstap0   | Unsigned 64-bit integer                                                   | Unix epoch time ([Definition 181](#defn-unix-time))                        |
| babeslot   | Unsigned 64-bit integer                                                   | The babe slot (*DEPRECATED*) ([Definition 54](#defn-epoch-slot))           |
| parachn0   | Parachain inherent data ([Definition 103](#defn-parachain-inherent-data)) | Parachain candidate inclusion ([Section 8.2.2](#sect-candidate-inclusion)) |

Table 1. Inherent Data

<div id="defn-inherent-data" class="exampleblock">

<div class="title">

Definition 15. [Inherent Data](#defn-inherent-data)

</div>

<div class="content">

<div class="paragraph">

`Inherent-Data` is a hashtable ([Definition 192](#defn-scale-list)), an
array of key-value pairs consisting of the inherent 8-byte identifier
and its value, representing the totality of inherent extrinsics included
in each block. The entries of this hash table which are listed in [Table
1](#tabl-inherent-data) are collected or generated by the Polkadot Host
and then handed to the Runtime for inclusion
([Build-Block](#algo-build-block)).

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-state-storage" class="anchor"></a><a href="#sect-state-storage" class="link">2.4. State Storage Trie</a>

<div class="paragraph">

For storing the state of the system, Polkadot Host implements a hash
table storage where the keys are used to access each data entry. There
is no assumption either on the size of the key nor on the size of the
data stored under them, besides the fact that they are byte arrays with
specific upper limits on their length. The limit is imposed by the
encoding algorithms to store the key and the value in the storage trie
([Section A.2.2.1](#sect-sc-length-and-compact-encoding)).

</div>

<div class="sect3">

#### <a href="#id-accessing-system-storage" class="anchor"></a><a href="#id-accessing-system-storage" class="link">2.4.1. Accessing
System Storage</a>

<div class="paragraph">

The Polkadot Host implements various functions to facilitate access to
the system storage for the Runtime ([Section
2.6.1](#sect-entrypoints-into-runtime)). Here we formalize the access to
the storage when it is being directly accessed by the Polkadot Host (in
contrast to Polkadot runtime).

</div>

<div id="defn-stored-value" class="exampleblock">

<div class="title">

Definition 16. [Stored Value](#defn-stored-value)

</div>

<div class="content">

<div class="paragraph">

The \\sf "StoredValue"\\ function retrieves the value stored under a
specific key in the state storage and is formally defined as:

</div>

<div class="stemblock">

<div class="content">

\\sf "StoredValue" ": "cc K -\> cc V\\ \\k -\> {(v,"if " (k,v), "exists
in state storage"),(phi,,"otherwise"):}\\

</div>

</div>

<div class="paragraph">

where \\cc K sub bbb B\\ and \\cc V sub bbb B\\ are respectively the set
of all keys and values stored in the state storage. \\cc V\\ can be an
empty value.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-general-structure" class="anchor"></a><a href="#id-general-structure" class="link">2.4.2. General
Structure</a>

<div class="paragraph">

In order to ensure the integrity of the state of the system, the stored
data needs to be re-arranged and hashed in a *radix tree*, which
hereafter we refer to as the ***State Trie*** or just ***Trie***. This
rearrangment is necessary to be able to compute the Merkle hash of the
whole or part of the state storage, consistently and efficiently at any
given time.

</div>

<div class="paragraph">

The trie is used to compute the *merkle root* ([Section
2.4.4](#sect-merkl-proof)) of the state, \\H_r\\ ([Definition
10](#defn-block-header)), whose purpose is to authenticate the validity
of the state database. Thus, the Polkadot Host follows a rigorous
encoding algorithm to compute the values stored in the trie nodes to
ensure that the computed Merkle hash, \\H_r\\, matches across the
Polkadot Host implementations.

</div>

<div class="paragraph">

The trie is a *radix-16* tree ([Definition 17](#defn-radix-tree)). Each
key value identifies a unique node in the tree. However, a node in a
tree might or might not be associated with a key in the storage.

</div>

<div id="defn-radix-tree" class="exampleblock">

<div class="title">

Definition 17. [Radix-r Tree](#defn-radix-tree)

</div>

<div class="content">

<div class="paragraph">

A ***Radix-r tree*** is a variant of a trie in which:

</div>

<div class="ulist">

- Every node has at most \\r\\ children where \\r = 2^x\\ for some
  \\x\\;

- Each node that is the only child of a parent, which does not represent
  a valid key is merged with its parent.

</div>

<div class="paragraph">

As a result, in a radix tree, any path whose interior vertices all have
only one child and does not represent a valid key in the data set, is
compressed into a single edge. This improves space efficiency when the
key space is sparse.

</div>

</div>

</div>

<div class="paragraph">

When traversing the trie to a specific node, its key can be
reconstructed by concatenating the subsequences of the keys which are
stored either explicitly in the nodes on the path or implicitly in their
position as a child of their parent.

</div>

<div class="paragraph">

To identify the node corresponding to a key value, \\k\\, first we need
to encode \\k\\ in a way consistent with the trie structure. Because
each node in the trie has at most 16 children, we represent the key as a
sequence of 4-bit nibbles:

</div>

<div id="defn-trie-key-encode" class="exampleblock">

<div class="title">

Definition 18. [Key Encode](#defn-trie-key-encode)

</div>

<div class="content">

<div class="paragraph">

For the purpose of labeling the branches of the trie, the key \\k\\ is
encoded to \\k\_("enc")\\ using \\sf "KeyEncode"\\ functions:

</div>

<div class="stemblock">

<div class="content">

\\k\_("enc") := (k\_("enc"\_1), ..., k\_("enc"\_(2n))) := sf
"KeyEncode"(k)\\

</div>

</div>

<div class="paragraph">

such that:

</div>

<div class="stemblock">

<div class="content">

\\sf "KeyEncode": bbb B -\> "Nibbles"^4\\ \\k \|-\>
(k\_("enc"\_1),...,k\_("enc"\_(2n)))\\ \\(b_1,...,b_n) \|-\>
(b_1^(1),b_1^2,b_2^1,b_2^2,...,b_n^1,b_n^2 )\\

</div>

</div>

<div class="paragraph">

where \\"Nibble"^4\\ is the set of all nibbles of 4-bit arrays and
\\b_i^1\\ and \\b_i^2\\ are 4-bit nibbles, which are the big endian
representations of \\b_i\\:

</div>

<div class="stemblock">

<div class="content">

\\k\_("enc"\_i) := (b_i^1,b_i^2) := (b_i -: 16,b_i mod 16)\\

</div>

</div>

<div class="paragraph">

where \\mod\\ is the remainder and \\-:\\ is the integer division
operators.

</div>

</div>

</div>

<div class="paragraph">

By looking at \\k\_("enc")\\ as a sequence of nibbles, one can walk the
radix tree to reach the node identifying the storage value of \\k\\.

</div>

</div>

<div class="sect3">

#### <a href="#sect-state-storage-trie-structure" class="anchor"></a><a href="#sect-state-storage-trie-structure" class="link">2.4.3. Trie
Structure</a>

<div class="paragraph">

In this subsection, we specify the structure of the nodes in the trie as
well as the trie structure:

</div>

<div id="defn-trie-nodeset" class="exampleblock">

<div class="title">

Definition 19. [Set of Nodes](#defn-trie-nodeset)

</div>

<div class="content">

<div class="paragraph">

We refer to the **set of the nodes of Polkadot state trie** by \\cc N\\.
By \\N in cc N\\ to refer to an individual node in the trie.

</div>

</div>

</div>

<div id="defn-nodetype" class="exampleblock">

<div class="title">

Definition 20. [State Trie](#defn-nodetype)

</div>

<div class="content">

<div class="paragraph">

The state trie is a radix-16 tree ([Definition 17](#defn-radix-tree)).
Each node in the trie is identified with a unique key \\k_N\\ such that:

</div>

<div class="ulist">

- \\k_N\\ is the shared prefix of the key of all the descendants of
  \\N\\ in the trie.

</div>

<div class="paragraph">

and, at least one of the following statements holds:

</div>

<div class="ulist">

- \\(k_N, v)\\ corresponds to an existing entry in the State Storage.

- \\N\\ has more than one child.

</div>

<div class="paragraph">

Conversely, if \\(k, v)\\ is an entry in the state trie then there is a
node \\N in cc N\\ such that \\k_N = k\\.

</div>

</div>

</div>

<div id="defn-trie-branch" class="exampleblock">

<div class="title">

Definition 21. [Branch](#defn-trie-branch)

</div>

<div class="content">

<div class="paragraph">

A **branch** node \\N_b in cc N_b\\ is a node which has one child or
more. A branch node can have at most 16 children. A **leaf** node \\N_l
in cc N_l\\ is a childless node. Accordingly:

</div>

<div class="stemblock">

<div class="content">

\\cc N_b := {N_b in cc N \| N_b " is a branch node"}\\ \\cc N_l := {N_l
in cc N \| N_l " is a leaf node"}\\

</div>

</div>

</div>

</div>

<div class="paragraph">

For each node, part of \\k_N\\ is built while the trie is traversed from
the root to \\N\\ and another part of \\k_N\\ is stored in \\N\\
([Definition 22](#defn-node-key)).

</div>

<div id="defn-node-key" class="exampleblock">

<div class="title">

Definition 22. [Aggregated Prefix Key](#defn-node-key)

</div>

<div class="content">

<div class="paragraph">

For any \\N in cc N\\, its key \\k_N\\ is divided into an **aggregated
prefix key, \\"pk"\_N^("Agr")\\**, aggregated by
[Aggregate-Key](#algo-aggregate-key) and a **partial key**,
**\\"pk"\_N\\** of length \\0 \<= l\_("pk"\_N)\\ in nibbles such that:

</div>

<div class="stemblock">

<div class="content">

\\"pk"\_N := (k\_("enc"\_i),...,k\_("enc"\_(i+l\_("pk"\_N))))\\

</div>

</div>

<div class="paragraph">

where \\"pk"\_N^("Agr")\\ is a prefix subsequence of \\k_N\\; \\i\\ is
the length of \\"pk"\_N^("Agr")\\ in nibbles and so we have:

</div>

<div class="stemblock">

<div class="content">

\\sf "KeyEncode"(k_N) = "pk"\_N^("Agr") \|\| "pk"\_N = (k\_("enc"\_1),
..., k\_("enc"\_(i-1)),k\_("enc"\_i),k\_("enc"\_(i+l\_("pk"\_N))))\\

</div>

</div>

</div>

</div>

<div class="paragraph">

Part of \\"pk"\_N^("Agr")\\ is explicitly stored in \\N\\’s ancestors.
Additionally, for each ancestor, a single nibble is implicitly derived
while traversing from the ancestor to its child included in the
traversal path using the \\"Index"\_N\\ function ([Definition
23](#defn-index-function)).

</div>

<div id="defn-index-function" class="exampleblock">

<div class="title">

Definition 23. [Index](#defn-index-function)

</div>

<div class="content">

<div class="paragraph">

For \\N in cc N_b\\ and \\N_c\\ child of \\N\\, we define \\sf
"Index"\_N\\ function as:

</div>

<div class="stemblock">

<div class="content">

\\sf "Index"\_N: {N_C in cc N \| N_c " is a child of " N} -\>
"Nibbles"\_1^4\\ \\N_c -\> i\\

</div>

</div>

<div class="paragraph">

such that

</div>

<div class="stemblock">

<div class="content">

\\k\_(N_c) = k_N \|\| i \|\| "pk"\_(N_c)\\

</div>

</div>

</div>

</div>

<div class="sidebarblock">

<div class="content">

\require{\$P_N \coloneqq (\$\textsc{TrieRoot}\$ = N_1, \dots, N_j =
N)\$} \state \$pk^{Agr}\_N \leftarrow \phi\$ \state \$i \leftarrow 1\$
\forall{\$N_i \in P_N\$} \state \$pk^{Agr}\_N \leftarrow pk^{Agr}\_N
\|\| pk\_{N_i} \|\| \textrm{Index}\_{N_i}(N\_{i + 1})\$ \endfor \state
\$pk^{Agr}\_N \leftarrow pk^{Agr}\_N \|\| pk\_{N}\$ \return
\$pk^{Agr}\_N\$

<div class="paragraph">

Assuming that \\P_N\\ is the path ([Definition 2](#defn-path-graph))
from the trie root to node \\N\\, [Aggregate-Key](#algo-aggregate-key)
rigorously demonstrates how to build \\"pk"\_N^("Agr")\\ while
traversing \\P_N\\.

</div>

</div>

</div>

<div id="defn-node-value" class="exampleblock">

<div class="title">

Definition 24. [Node Value](#defn-node-value)

</div>

<div class="content">

<div class="paragraph">

A node \\N in cc N\\ stores the **node value**, \\v_N\\, which consists
of the following concatenated data:

</div>

<div class="stemblock">

<div class="content">

\\"Node Header"\|\|"Partial Key"\|\|"Node Subvalue"\\

</div>

</div>

<div class="paragraph">

Formally noted as:

</div>

<div class="stemblock">

<div class="content">

\\v_N := "Head"\_N\|\|"Enc"\_"HE"(pk_N)\|\|sv_N\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\"Head"\_N\\ is the node header from [Definition
  25](#defn-node-header)

- \\pk_N\\ is the partial key from [Definition 22](#defn-node-key)

- \\"Enc"\_"HE"\\ is hex encoding ([Definition 199](#defn-hex-encoding))

- \\sv_N\\ is the node subvalue from [Definition
  27](#defn-node-subvalue)

</div>

</div>

</div>

</div>

<div id="defn-node-header" class="exampleblock">

<div class="title">

Definition 25. [Node Header](#defn-node-header)

</div>

<div class="content">

<div class="paragraph">

The **node header**, consisting of \\\>= 1\\ bytes, \\N_1...N_n\\,
specifies the node variant and the partial key length ([Definition
22](#defn-node-key)). Both pieces of information can be represented in
bits within a single byte, \\N_1\\, where the amount of bits of the
variant, \\v\\, and the bits of the partial key length, \\p_l\\ varies.

</div>

<div class="stemblock">

<div class="content">

\\v = { (01, "Leaf", p_l = 2^6), (10, "Branch Node with " k_N !in cc K,
p_l = 2^6), (11, "Branch Node with " k_N in cc K, p_l = 2^6), (001,
"Leaf containing a hashed subvalue", p_l = 2^5), (0001, "Branch
containing a hashed subvalue", p_l = 2^4), (0000 0000, "Empty", p_l =
0), (0000 0001, "Reserved for compact encoding",) :}\\

</div>

</div>

<div class="paragraph">

If the value of \\p_l\\ is equal to the maximum possible value the bits
can hold, such as 63 (\\2^6-1\\) in case of the \\01\\ variant, then the
value of the next 8 bits (\\N_2\\) are added the the length. This
process is repeated for every \\N_n\\ where \\N_n = 2^8-1\\. Any value
smaller than the maximum possible value of \\N_n\\ implies that the next
value of \\N\_(n+1)\\ should not be added to the length. The hashed
subvalue for variants \\001\\ and \\0001\\ is described in [Definition
28](#defn-hashed-subvalue).

</div>

<div class="paragraph">

Formally, the length of the partial key, \\"pk"\_N^l\\, is defined as:

</div>

<div class="stemblock">

<div class="content">

\\"pk"\_N^l = p_l + N_n + N\_(n+x) + ... + N\_(n+x+y)\\

</div>

</div>

<div class="paragraph">

as long as \\p_l = m\\, \\N\_(n+x) = 2^8-1\\ and \\N\_(n+x+y) \<
2^8-1\\, where \\m\\ is the maximum possible value that \\p_l\\ can
hold.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-merkl-proof" class="anchor"></a><a href="#sect-merkl-proof" class="link">2.4.4. Merkle Proof</a>

<div class="paragraph">

To prove the consistency of the state storage across the network and its
modifications both efficiently and effectively, the trie implements a
Merkle tree structure. The hash value corresponding to each node needs
to be computed rigorously to make the inter-implementation data
integrity possible.

</div>

<div class="paragraph">

The Merkle value of each node should depend on the Merkle value of all
its children as well as on its corresponding data in the state storage.
This recursive dependency is encompassed into the subvalue part of the
node value which recursively depends on the Merkle value of its
children. Additionally, as [Section 2.5.1](#sect-child-trie-structure)
clarifies, the Merkle proof of each **child trie** must be updated first
before the final Polkadot state root can be calculated.

</div>

<div class="paragraph">

We use the auxiliary function introduced in [Definition
26](#defn-children-bitmap) to encode and decode information stored in a
branch node.

</div>

<div id="defn-children-bitmap" class="exampleblock">

<div class="title">

Definition 26. [Children Bitmap](#defn-children-bitmap)

</div>

<div class="content">

<div class="paragraph">

Suppose \\N_b, N_c in cc N\\ and \\N_c\\ is a child of \\N_b\\. We
define bit \\b_i : = 1\\ if and only if \\N_b\\ has a child with index
\\i\\, therefore we define **ChildrenBitmap** functions as follows:

</div>

<div class="stemblock">

<div class="content">

\\"ChildrenBitmap:"\\ \\cc N_b -\> bbb B_2\\ \\N_b -\> (b\_(15),
...,b_8,b_7,...,b_0)\_2\\

</div>

</div>

<div class="paragraph">

where

</div>

<div class="stemblock">

<div class="content">

\\b_i := {(1, EE N_c in cc N: k\_(N_c) = k\_(N_b)\|\|i\|\|pk\_(N_c)),(0,
"otherwise"):}\\

</div>

</div>

</div>

</div>

<div id="defn-node-subvalue" class="exampleblock">

<div class="title">

Definition 27. [Subvalue](#defn-node-subvalue)

</div>

<div class="content">

<div class="paragraph">

For a given node \\N\\, the **subvalue** of \\N\\, formally referred to
as \\sv_N\\, is determined as follows:

</div>

<div class="stemblock">

<div class="content">

\\sv_N :=
{("StoredValue"\_("SC")),("Enc"\_("SC")("ChildrenBitmap"(N)\|\|"StoredValue"\_("SC")\|\|"Enc"\_("SC")(H(N\_(C_1))),...,"Enc"\_("SC")(H(N\_(C_n))))):}\\

</div>

</div>

<div class="paragraph">

where the first variant is a leaf node and the second variant is a
branch node.

</div>

<div class="stemblock">

<div class="content">

\\"StoredValue"\_("SC") := {("Enc"\_("SC")("StoredValue"(k_N)),"if
StoredValue"(k_N) = v),(phi,"if StoredValue"(k_N) = phi):}\\

</div>

</div>

<div class="paragraph">

\\N\_(C_1) ... N\_(C_n)\\ with \\n \<= 16\\ are the children nodes of
the branch node \\N\\.

</div>

<div class="ulist">

- \\"Enc"\_("SC")\\ is defined in [Section A.2.2](#sect-scale-codec).

- \\"StoredValue"\\, where \\v\\ can be empty, is defined in [Definition
  16](#defn-stored-value).

- \\H\\ is defined in [Definition 29](#defn-merkle-value).

- \\"ChildrenBitmap"(N)\\ is defined in [Definition
  26](#defn-children-bitmap).

</div>

<div class="paragraph">

The trie deviates from a traditional Merkle tree in that the node value
([Definition 24](#defn-node-value)), \\v_N\\, is presented instead of
its hash if it occupies less space than its hash.

</div>

</div>

</div>

<div id="defn-hashed-subvalue" class="exampleblock">

<div class="title">

Definition 28. [Hashed Subvalue](#defn-hashed-subvalue)

</div>

<div class="content">

<div class="paragraph">

To increase performance, a merkle proof can be generated by inserting
the hash of a value into the trie rather than the value itself (which
can be quite large). If merkle proof computation with node hashing is
explicitly executed via the Host API ([Section
B.2.8.2](#sect-ext-storage-root-version-2)), then any value larger than
32 bytes is hashed, resulting in that hash being used as the subvalue
([Definition 27](#defn-node-subvalue)) under the corresponding key. The
node header must specify the variant \\001\\ and \\0001\\ respectively
for leaves containing a hash as their subvalue and for branches
containing a hash as their subvalue ([Definition
25](#defn-node-header)).

</div>

</div>

</div>

<div id="defn-merkle-value" class="exampleblock">

<div class="title">

Definition 29. [Merkle Value](#defn-merkle-value)

</div>

<div class="content">

<div class="paragraph">

For a given node \\N\\, the **Merkle value** of \\N\\, denoted by
\\H(N)\\ is defined as follows:

</div>

<div class="stemblock">

<div class="content">

\\H: bbb B -\> U\_(i -\> 0)^(32) bbb B_32\\ \\H(N): {(v_N,\|\|v_N\|\| \<
32 " and " N != R),("Blake2b"(v_n),\|\|v_N\|\| \>= 32 " or " N = R):}\\

</div>

</div>

<div class="paragraph">

Where \\v_N\\ is the node value of \\N\\ ([Definition
24](#defn-node-value)) and \\R\\ is the root of the trie. The **Merkle
hash** of the trie is defined to be \\H(R)\\.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-managing-multiple-states" class="anchor"></a><a href="#sect-managing-multiple-states" class="link">2.4.5. Managing
Multiple Variants of State</a>

<div class="paragraph">

Unless a node is committed to only update its state according to the
finalized block ([Definition 90](#defn-finalized-block)), it is
inevitable for the node to store multiple variants of the state (one for
each block). This is, for example, necessary for nodes participating in
the block production and finalization.

</div>

<div class="paragraph">

While the state trie structure ([Section
2.4.3](#sect-state-storage-trie-structure)) facilitates and optimizes
storing and switching between multiple variants of the state storage,
the Polkadot Host does not specify how a node is required to accomplish
this task. Instead, the Polkadot Host is required to implement
\\"Set-State-At"\\ ([Definition 30](#defn-set-state-at)):

</div>

<div id="defn-set-state-at" class="exampleblock">

<div class="title">

Definition 30. [Set State At Block](#defn-set-state-at)

</div>

<div class="content">

<div class="paragraph">

The function:

</div>

<div class="stemblock">

<div class="content">

\\"Set-State-At"(B)\\

</div>

</div>

<div class="paragraph">

in which \\B\\ is a block in the block tree ([Definition
4](#defn-block-tree)), sets the content of state storage equal to the
resulting state of executing all extrinsics contained in the branch of
the block tree from genesis till block B including those recorded in
Block \\B\\.

</div>

<div class="paragraph">

For the definition of the state storage see [Section
2.4](#sect-state-storage).

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-child-storages" class="anchor"></a><a href="#sect-child-storages" class="link">2.5. Child Storage</a>

<div class="paragraph">

As clarified in [Section 2.4](#sect-state-storage), the Polkadot state
storage implements a hash table for inserting and reading key-value
entries. The child storage works the same way but is stored in a
separate and isolated environment. Entries in the child storage are not
directly accessible via querying the main state storage.

</div>

<div class="paragraph">

The Polkadot Host supports as many child storages as required by Runtime
and identifies each separate child storage by its unique identifying
key. Child storages are usually used in situations where Runtime deals
with multiple instances of a certain type of objects such as Parachains
or Smart Contracts. In such cases, the execution of the Runtime
entrypoint might result in generating repeated keys across multiple
instances of certain objects. Even with repeated keys, all such
instances of key-value pairs must be able to be stored within the
Polkadot state.

</div>

<div class="paragraph">

In these situations, the child storage can be used to provide the
isolation necessary to prevent any undesired interference between the
state of separated instances. The Polkadot Host makes no assumptions
about how child storages are used, but provides the functionality for it
via the Host API ([Section B.3](#sect-child-storage-api)).

</div>

<div class="sect3">

#### <a href="#sect-child-trie-structure" class="anchor"></a><a href="#sect-child-trie-structure" class="link">2.5.1. Child Tries</a>

<div class="paragraph">

The child trie specification is the same as the one described in
[Section 2.4.3](#sect-state-storage-trie-structure). Child tries have
their own isolated environment. Nonetheless, the main Polkadot state
trie depends on them by storing a node (\\K_N, V_N\\) which corresponds
to an individual child trie. Here, \\K_N\\ is the child storage key
associated to the child trie, and \\V_N\\ is the Merkle value of its
corresponding child trie computed according to the procedure described
in [Section 2.4.4](#sect-merkl-proof).

</div>

<div class="paragraph">

The Polkadot Host API ([Section B.3](#sect-child-storage-api)) allows
the Runtime to provide the key \\K_N\\ in order to identify the child
trie, followed by a second key in order to identify the value within
that child trie. Every time a child trie is modified, the Merkle proof
\\V_N\\ of the child trie stored in the Polkadot state must be updated
first. After that, the final Merkle proof of the Polkadot state can be
computed. This mechanism provides a proof of the full Polkadot state
including all its child states.

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-runtime-interaction" class="anchor"></a><a href="#sect-runtime-interaction" class="link">2.6. Runtime
Interactions</a>

<div class="paragraph">

Like any transaction-based transition system, Polkadot’s state is
changed by executing an ordered set of instructions. These instructions
are known as *extrinsics*. In Polkadot, the execution logic of the state
transition function is encapsulated in a Runtime ([Definition
1](#defn-state-machine)). For easy upgradability this Runtime is
presented as a Wasm blob. Nonetheless, the Polkadot Host needs to be in
constant interaction with the Runtime ([Section
2.6.1](#sect-entrypoints-into-runtime)).

</div>

<div class="paragraph">

In [Section 2.3](#sect-extrinsics), we specify the procedure of the
process where the extrinsics are submitted, pre-processed and validated
by Runtime and queued to be applied to the current state.

</div>

<div class="paragraph">

To make state replication feasible, Polkadot journals and batches series
of its extrinsics together into a structure known as a *block*, before
propagating them to other nodes, similar to most other prominent
distributed ledger systems. The specification of the Polkadot block as
well as the process of verifying its validity are both explained in
[Section 2.2](#sect-state-replication).

</div>

<div class="sect3">

#### <a href="#sect-entrypoints-into-runtime" class="anchor"></a><a href="#sect-entrypoints-into-runtime" class="link">2.6.1. Interacting
with the Runtime</a>

<div class="paragraph">

The Runtime ([Definition 1](#defn-state-machine)) is the code
implementing the logic of the chain. This code is decoupled from the
Polkadot Host to make the the logic of the chain easily upgradable
without the need to upgrade the Polkadot Host itself. The general
procedure to interact with the Runtime is described by
[Interact-With-Runtime](#algo-runtime-interaction).

</div>

<div class="sidebarblock">

<div class="content">

\require \$F, H_b(B),(A_1,\ldots,A_n)\$ \state \$\mathcal{S}\_B
\leftarrow\$ \call{Set-State-At}{\$H_b(B)\$} \state \$A \leftarrow
Enc\_{SC}((A_1, \ldots, A_n))\$ \state
\call{Call-Runtime-Entrypoint}{\$R_B, \mathcal{RE}\_B, F, A, A\_{len}\$}

<div class="dlist">

where  
<div class="ulist">

- \\F\\ is the runtime entrypoint call.

- \\H_b(B)\\ is the block hash indicating the state at the end of \\B\\.

- \\A_1,...,A_n\\ are arguments to be passed to the runtime entrypoint.

</div>

</div>

</div>

</div>

<div class="paragraph">

In this section, we describe the details upon which the Polkadot Host is
interacting with the Runtime. In particular, \\"Set-State-At"\\ and
\\"Call-Runtime-Entrypoint"\\ procedures called by
[Interact-With-Runtime](#algo-runtime-interaction) are explained in
[Definition 32](#defn-call-into-runtime) and [Definition
30](#defn-set-state-at) respectively. \\R_B\\ is the Runtime code loaded
from \\S_B\\, as described in [Definition
31](#defn-runtime-code-at-state), and \\RE_B\\ is the Polkadot Host API,
as described in [Definition 201](#defn-host-api-at-state).

</div>

</div>

<div class="sect3">

#### <a href="#sect-loading-runtime-code" class="anchor"></a><a href="#sect-loading-runtime-code" class="link">2.6.2. Loading the
Runtime Code</a>

<div class="paragraph">

The Polkadot Host expects to receive the code for the Runtime of the
chain as a compiled WebAssembly (Wasm) Blob. The current runtime is
stored in the state database under the key represented as a byte array:

</div>

<div class="stemblock">

<div class="content">

\\b := "3A,63,6F,64,65"\\

</div>

</div>

<div class="paragraph">

which is the ASCII byte representation of the string `:code` ([Section
A.3](#chapter-genesis)). As a result of storing the Runtime as part of
the state, the Runtime code itself becomes state sensitive and calls to
Runtime can change the Runtime code itself. Therefore the Polkadot Host
needs to always make sure to provide the Runtime corresponding to the
state in which the entrypoint has been called. Accordingly, we define
\\R_B\\ ([Definition 31](#defn-runtime-code-at-state)).

</div>

<div class="paragraph">

The initial Runtime code of the chain is provided as part of the genesis
state ([Section A.3](#chapter-genesis)) and subsequent calls to the
Runtime have the ability to, in turn, upgrade the Runtime by replacing
this Wasm blob with the help of the storage API ([Section
B.2](#sect-storage-api)). Therefore, the executor **must always** load
the latest Runtime from storage - or preferably detect Runtime upgrades
([Definition 11](#defn-digest)) - either based on the parent block when
importing blocks or the best/highest block when creating new blocks.

</div>

<div id="defn-runtime-code-at-state" class="exampleblock">

<div class="title">

Definition 31. [Runtime Code at State](#defn-runtime-code-at-state)

</div>

<div class="content">

<div class="paragraph">

By \\R_B\\, we refer to the Runtime code stored in the state storage at
the end of the execution of block \\B\\.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-code-executor" class="anchor"></a><a href="#sect-code-executor" class="link">2.6.3. Code Executor</a>

<div class="paragraph">

The Polkadot Host executes the calls of Runtime entrypoints inside a
Wasm Virtual Machine (VM), which in turn provides the Runtime with
access to the Polkadot Host API. This part of the Polkadot Host is
referred to as the *Executor*.

</div>

<div class="paragraph">

[Definition 32](#defn-call-into-runtime) introduces the notation for
calling the runtime entrypoint which is used whenever an algorithm of
the Polkadot Host needs to access the runtime.

</div>

<div class="paragraph">

It is acceptable behavior that the Runtime panics during execution of a
function in order to indicate an error. The Polkadot Host must be able
to catch that panic and recover from it.

</div>

<div class="paragraph">

In this section, we specify the general setup for an Executor that calls
into the Runtime. In [Appendix C](#chap-runtime-api) we specify the
parameters and return values for each Runtime entrypoint separately.

</div>

<div id="defn-call-into-runtime" class="exampleblock">

<div class="title">

Definition 32. [Call Runtime Entrypoint](#defn-call-into-runtime)

</div>

<div class="content">

<div class="paragraph">

By

</div>

<div class="stemblock">

<div class="content">

\\"Call-Runtime-Entrypoint"(R,RE,"Runtime-Entrypoint",A,A_len)\\

</div>

</div>

<div class="paragraph">

we refer to the task using the executor to invoke the while passing an
\\A_1, ..., A_n\\ argument to it and using the encoding described in
[Section 2.6.3.2](#sect-runtime-send-args-to-runtime-enteries).

</div>

</div>

</div>

<div class="sect4">

##### <a href="#sect-memory-management" class="anchor"></a><a href="#sect-memory-management" class="link">2.6.3.1. Memory
Management</a>

<div class="paragraph">

The Polkadot Host is responsible for managing the WASM heap memory
starting at the exported symbol as a part of implementing the allocator
Host API ([Section B.9](#sect-allocator-api)) and the same allocator
should be used for any other heap allocation to be used by the Polkadot
Runtime.

</div>

<div class="paragraph">

The size of the provided WASM memory should be based on the value of the
storage key (an unsigned 64-bit integer), where each page has the size
of 64KB. This memory should be made available to the Polkadot Runtime
for import under the symbol name `memory`.

</div>

</div>

<div class="sect4">

##### <a href="#sect-runtime-send-args-to-runtime-enteries"
class="anchor"></a><a href="#sect-runtime-send-args-to-runtime-enteries"
class="link">2.6.3.2. Sending Data to a Runtime Entrypoint</a>

<div class="paragraph">

In general, all data exchanged between the Polkadot Host and the Runtime
is encoded using SCALE codec described in [Section
A.2.2](#sect-scale-codec). Therefore all runtime entrypoints have the
following identical Wasm function signatures:

</div>

<div class="listingblock">

<div class="content">

``` rouge
(func $runtime_entrypoint (param $data i32) (param $len i32) (result i64))
```

</div>

</div>

<div class="paragraph">

In each invocation of a Runtime entrypoints, the argument(s) which are
supposed to be sent to the entrypoint, need to be SCALE encoded into a
byte array \\B\\ ([Section A.2.2](#sect-scale-codec)) and copied into a
section of Wasm shared memory managed by the shared allocator described
in [Section 2.6.3.1](#sect-memory-management).

</div>

<div class="paragraph">

When the Wasm method, corresponding to the entrypoint, is invoked, two
integers are passed as arguments. The first argument is set to the
memory address of the byte array \\B\\ in Wasm memory. The second
argument sets the length of the encoded data stored in \\B\\.

</div>

</div>

<div class="sect4">

##### <a href="#sect-runtime-return-value" class="anchor"></a><a href="#sect-runtime-return-value" class="link">2.6.3.3. Receiving
Data from a Runtime Entrypoint</a>

<div class="paragraph">

The value which is returned from the invocation is an integer,
representing two consecutive integers in which the least significant one
indicates the pointer to the offset of the result returned by the
entrypoint encoded in SCALE codec in the memory buffer. The most
significant one provides the size of the blob.

</div>

</div>

<div class="sect4">

##### <a href="#sect-runtime-version-custom-section" class="anchor"></a><a href="#sect-runtime-version-custom-section" class="link">2.6.3.4.
Runtime Version Custom Section</a>

<div class="paragraph">

For newer Runtimes, the Runtime version ([Section
C.4.1](#defn-rt-core-version)) can be read directly from the [Wasm
custom
section](https://webassembly.github.io/spec/core/appendix/custom.html)
with the name `runtime_version`. The content is a SCALE encoded
structure as described in [Section C.4.1](#defn-rt-core-version).

</div>

<div class="paragraph">

Retrieving the Runtime version this way is preferred over calling the
`Core_version` entrypoint since it involves significantly less overhead.

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#chap-sync" class="anchor"></a><a href="#chap-sync" class="link">3. Synchronization</a>

<div class="sectionbody">

<div class="paragraph">

Many applications that interact with the Polkadot network to some extent
must be able to retrieve certain information about the network.
Depending on the utility, this includes validators that interact with
Polkadot’s consensus and need access to the full state, either from the
past or just the most up-to-date state, or light clients that are only
interest in the minimum information required in order to verify some
claims about the state of the network, such as the balance of a specific
account. To allow implemenations to quickly retrieve the required
information, different types of synchronization protocols are available,
respectivel Full, Fast and Warp sync suited for different needs.

</div>

<div class="paragraph">

The associated network messages are specified in [Section
4.8](#sect-network-messages).

</div>

<div class="sect2">

### <a href="#sect-sync-warp" class="anchor"></a><a href="#sect-sync-warp" class="link">3.1. Warp Sync</a>

<div class="paragraph">

Warp sync ([Section 4.8.4](#sect-msg-warp-sync)) only downloads the
block headers where authority set changes occurred, so called fragments
([Definition 41](#defn-warp-sync-proof)), and by verifying the GRANDPA
justifications ([Definition 45](#defn-grandpa-justifications-compact)).
This protocols allows nodes to arrive at the desired state much faster
than fast sync.

</div>

</div>

<div class="sect2">

### <a href="#sect-sync-fast" class="anchor"></a><a href="#sect-sync-fast" class="link">3.2. Fast Sync</a>

<div class="paragraph">

Fast sync works by downloading the block header history and validating
the auhtority set changes ([Section 3.3.1](#sect-authority-set)) in
order to arrive at a specific (usually the most recent) header. After
the desired header has been reached and verified, the state can be
downloaded and imported ([Section 4.8.3](#sect-msg-state-request)). Once
this process has been completed, the node can proceed with a full sync.

</div>

</div>

<div class="sect2">

### <a href="#id-full-sync" class="anchor"></a><a href="#id-full-sync" class="link">3.3. Full Sync</a>

<div class="paragraph">

The full sync protocols is the "default" protocol that’s suited for many
types of implementations, such as archive nodes (nodes that store
everything), validators that participate in Polkadots consensus and
light clients that only verify claims about the state of the network.
Full sync works by listening to announced blocks ([Section
4.8.1](#sect-msg-block-announce)) and requesting the blocks from the
announcing peers, or just the block headers in case of light clients.

</div>

<div class="paragraph">

The full sync protocol usually downloads the entire chain, but no such
requirements must be met. If an implemenation only wants the latest,
finalized state, it can combine it with protocols such as fast sync
([Section 3.2](#sect-sync-fast)) and/or warp sync ([Section
3.1](#sect-sync-warp)) to make synchronization as fast as possible.

</div>

<div class="sect3">

#### <a href="#sect-authority-set" class="anchor"></a><a href="#sect-authority-set" class="link">3.3.1. Consensus Authority
Set</a>

<div class="paragraph">

Because Polkadot is a proof-of-stake protocol, each of its consensus
engines has its own set of nodes represented by known public keys, which
have the authority to influence the protocol in pre-defined ways
explained in this Section. To verify the validity of each block, the
Polkadot node must track the current list of authorities ([Definition
33](#defn-authority-list)) for that block.

</div>

<div id="defn-authority-list" class="exampleblock">

<div class="title">

Definition 33. [Authority List](#defn-authority-list)

</div>

<div class="content">

<div class="paragraph">

The **authority list** of block \\B\\ for consensus engine \\C\\ noted
as \\"Auth"\_C(B)\\ is an array that contains the following pair of
types for each of its authorities \\A in "Auth"\_C(B)\\:

</div>

<div class="stemblock">

<div class="content">

\\(pk_A,w_A)\\

</div>

</div>

<div class="paragraph">

\\pk_A\\ is the session public key ([Definition 180](#defn-session-key))
of authority \\A\\. And \\w_A\\ is an unsigned 64-bit integer indicating
the authority weight. The value of \\"Auth"\_C(B)\\ is part of the
Polkadot state. The value for \\"Auth"\_C(B_0)\\ is set in the genesis
state ([Section A.3](#chapter-genesis)) and can be retrieved using a
runtime entrypoint corresponding to consensus engine \\C\\.

</div>

<div class="paragraph">

The authorities and their corresponding weights can be retrieved from
the Runtime ([Section C.10.1](#sect-rte-grandpa-auth)).

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-consensus-message-digest" class="anchor"></a><a href="#sect-consensus-message-digest" class="link">3.3.2.
Runtime-to-Consensus Engine Message</a>

<div class="paragraph">

The authority list ([Definition 33](#defn-authority-list)) is part of
the Polkadot state and the Runtime has the authority to update this list
in the course of any state transitions. The Runtime informs the
corresponding consensus engine about the changes in the authority set by
adding the appropriate consensus message in the form of a digest item
([Definition 11](#defn-digest)) to the block header of block \\B\\ which
caused the transition in the authority set.

</div>

<div class="paragraph">

The Polkadot Host must inspect the digest header of each block and
delegate consensus messages to their consensus engines. The BABE and
GRANDPA consensus engine must react based on the type of consensus
messages it receives. The active GRANDPA authorities can only vote for
blocks that occurred after the finalized block in which they were
selected. Any votes for blocks before the came into effect would get
rejected.

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-block-validation" class="anchor"></a><a href="#sect-block-validation" class="link">3.4. Importing and
Validating Block</a>

<div class="paragraph">

Block validation is the process by which a node asserts that a block is
fit to be added to the blockchain. This means that the block is
consistent with the current state of the system and transitions to a new
valid state.

</div>

<div class="paragraph">

New blocks can be received by the Polkadot Host via other peers
([Section 4.8.2](#sect-msg-block-request)) or from the Host’s own
consensus engine ([Chapter 5](#sect-block-production)). Both the Runtime
and the Polkadot Host then need to work together to assure block
validity. A block is deemed valid if the block author had authorship
rights for the slot in which the block was produce as well as if the
transactions in the block constitute a valid transition of states. The
former criterion is validated by the Polkadot Host according to the
block production consensus protocol. The latter can be verified by the
Polkadot Host invoking entry into the Runtime as ([Section
C.4.2](#sect-rte-core-execute-block)) as a part of the validation
process. Any state changes created by this function on successful
execution are persisted.

</div>

<div class="paragraph">

The Polkadot Host implements
[Import-and-Validate-Block](#algo-import-and-validate-block) to assure
the validity of the block.

</div>

<div class="sidebarblock">

<div class="content">

\require \$B, \text{Just}(B)\$ \state
\call{Set-Storage-State-At}{\$P(B)\$} \if{\$\text{Just}(B) \neq
\emptyset\$} \state \call{Verify-Block-Justification}{\$B,
\text{Just}(B)\$}
\if{\$B~\textbf{is}~\text{Finalized}~\textbf{and}~P(B)~\textbf{is
not}~\text{Finalized}\$} \state \call{Mark-as-Final}{\$P(B)\$} \endif
\endif \if{\$H_p(B) \notin PBT\$} \return \endif \state
\call{Verify-Authorship-Right}{\$\text{Head}(B)\$} \state \$B
\leftarrow\$ \call{Remove-Seal}{\$B\$} \state \$R \leftarrow\$
\call{Call-Runtime-Entry}{\$\texttt{Core\\execute\\block}, B\$} \state
\$B \leftarrow\$ \call{Add-Seal}{\$B\$} \if{\$R =\$ \textsc{True}}
\state \call{Persist-State}{} \endif

<div class="dlist">

where  
<div class="ulist">

- \\"Remove-Seal"\\ removes the Seal digest from the block ([Definition
  11](#defn-digest)) before submitting it to the Runtime.

- \\"Add-Seal"\\ adds the Seal digest back to the block ([Definition
  11](#defn-digest)) for later propagation.

- \\"Persist-State"\\ implies the persistence of any state changes
  created by \\tt "Core_execute_block"\\ ([Section
  C.4.2](#sect-rte-core-execute-block)) on successful execution.

- \\"PBT"\\ is the pruned block tree ([Definition 4](#defn-block-tree)).

- \\"Verify-Authorship-Right"\\ is part of the block production
  consensus protocol and is described in
  [Verify-Authorship-Right](#algo-verify-authorship-right).

- *Finalized block* and *finality* are defined in [Chapter
  6](#sect-finality).

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#chap-networking" class="anchor"></a><a href="#chap-networking" class="link">4. Networking</a>

<div class="sectionbody">

<div class="admonitionblock note">

|     |                                                                                                                                                                                                                                                                                                                                              |
|-----|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This chapter in its current form is incomplete and considered work in progress. Authors appreciate receiving request for clarification or any reports regarding deviation from the current Polkadot network protocol. This can be done through filing an issue in [Polkadot Specification repository](https://github.com/w3f/polkadot-spec). |

</div>

<div class="sect2">

### <a href="#id-introduction-2" class="anchor"></a><a href="#id-introduction-2" class="link">4.1. Introduction</a>

<div class="paragraph">

The Polkadot network is decentralized and does not rely on any central
authority or entity for achieving its fullest potential of provided
functionality. The networking protocol is based on a family of open
protocols, including protocol implemented *libp2p* e.g. the distributed
Kademlia hash table which is used for peer discovery.

</div>

<div class="paragraph">

This chapter walks through the behavior of the networking implementation
of the Polkadot Host and defines the network messages. The
implementation details of the *libp2p* protocols used are specified in
external sources as described in [Section
4.2](#sect-networking-external-docs)

</div>

</div>

<div class="sect2">

### <a href="#sect-networking-external-docs" class="anchor"></a><a href="#sect-networking-external-docs" class="link">4.2. External
Documentation</a>

<div class="paragraph">

Complete specification of the Polkadot networking protocol relies on the
following external protocols:

</div>

<div class="ulist">

- [libp2p](https://github.com/libp2p/specs) - *libp2p* is a modular
  peer-to-peer networking stack composed of many modules and different
  parts. includes the multiplexing protocols and .

- [libp2p addressing](https://docs.libp2p.io/concepts/addressing/) - The
  Polkadot Host uses the *libp2p* addressing system to identify and
  connect to peers.

- [Kademlia](https://en.wikipedia.org/wiki/Kademlia) - *Kademlia* is a
  distributed hash table for decentralized peer-to-peer networks. The
  Polkadot Host uses Kademlia for peer discovery.

- [Noise](https://noiseprotocol.org/) - The *Noise* protocol is a
  framework for building cryptographic protocols. The Polkadot Host uses
  Noise to establish the encryption layer to remote peers.

- [yamux](https://docs.libp2p.io/concepts/stream-multiplexing/#yamux) -
  *yamux* is a multiplexing protocol developed by HashiCorp. It is the
  de-facto standard for the Polkadot Host. [Section
  4.7](#sect-protocols-substreams) describes the subprotocol in more
  detail.

- [Protocol
  Buffers](https://developers.google.com/protocol-buffers/docs/reference/proto3-spec) -
  Protocol Buffers is a language-neutral, platform-neutral mechanism for
  serializing structured data and is developed by Google. The Polkadot
  Host uses Protocol Buffers to serialize specific messages, as
  clarified in [Section 4.8](#sect-network-messages).

</div>

</div>

<div class="sect2">

### <a href="#id-node-identities" class="anchor"></a><a href="#id-node-identities" class="link">4.3. Node Identities</a>

<div class="paragraph">

Each Polkadot Host node maintains an ED25519 key pair which is used to
identify the node. The public key is shared with the rest of the network
allowing the nodes to establish secure communication channels.

</div>

<div class="paragraph">

Each node must have its own unique ED25519 key pair. If two or more
nodes use the same key, the network will interpret those nodes as a
single node, which will result in unspecified behavior. Furthermore, the
node’s *PeerId* as defined in [Definition 34](#defn-peer-id) is derived
from its public key. *PeerId* is used to identify each node when they
are discovered in the course of the discovery mechanism described in
[Section 4.4](#sect-discovery-mechanism).

</div>

<div id="defn-peer-id" class="exampleblock">

<div class="title">

Definition 34. [PeerId](#defn-peer-id)

</div>

<div class="content">

<div class="paragraph">

The Polkadot node’s PeerId, formally referred to as \\P\_(id)\\, is
derived from the ED25519 public key and is structured based on the
[libp2p specification](https://docs.libp2p.io/concepts/peer-id/), but
does not fully conform to the specification. Specifically, it does not
support [CID](https://github.com/multiformats/cid) and the only
supported key type is ED25519.

</div>

<div class="paragraph">

The byte representation of the PeerId is always of the following bytes
in this exact order:

</div>

<div class="stemblock">

<div class="content">

\\b_0 = 0\\ \\b_1 = 36\\ \\b_2 = 8\\ \\b_3 = 1\\ \\b_4 = 18\\ \\b_5 =
32\\ \\b\_(6..37) = ...\\

</div>

</div>

<div class="paragraph">

where

</div>

<div class="ulist">

- \\b_0\\ is the [multihash
  prefix](https://github.com/multiformats/multihash#multihash) of value
  \\0\\ (implying no hashing is used).

- \\b_1\\ the length of the PeerId (remaining bytes).

- \\b_2\\ and \\b_3\\ are a protobuf encoded field-value pair
  [indicating the used key
  type](https://github.com/libp2p/specs/blob/master/peer-ids/peer-ids.md#keys)
  (field \\1\\ of value \\1\\ implies *ED25519*).

- \\b_4\\, \\b_5\\ and \\b\_(6..37)\\ are a protobuf encoded field-value
  pair where \\b_5\\ indicates the length of the public key followed by
  the the raw ED25519 public key itself, which varies for each Polkadot
  Host and is always 32 bytes (field \\2\\ contains the public key,
  which has a field value length prefix).

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-discovery-mechanism" class="anchor"></a><a href="#sect-discovery-mechanism" class="link">4.4. Discovery
mechanism</a>

<div class="paragraph">

The Polkadot Host uses various mechanisms to find peers within the
network, to establish and maintain a list of peers and to share that
list with other peers from the network as follows:

</div>

<div class="ulist">

- **Bootstrap nodes** are hard-coded node identities and addresses
  provided by the genesis state ([Section A.3](#chapter-genesis)).

- **mDNS** is a protocol that performs a broadcast to the local network.
  Nodes that might be listening can respond to the broadcast. [The
  libp2p mDNS
  specification](https://github.com/libp2p/specs/blob/master/discovery/mdns.md)
  defines this process in more detail. This protocol is an optional
  implementation detail for Polkadot Host implementers and is not
  required to participate in the Polkadot network.

- **Kademlia requests** invoking Kademlia requests, where nodes respond
  with their list of available peers. Kademlia requests are performed on
  a specific substream as described in [Section
  4.7](#sect-protocols-substreams).

</div>

</div>

<div class="sect2">

### <a href="#sect-connection-establishment" class="anchor"></a><a href="#sect-connection-establishment" class="link">4.5. Connection
establishment</a>

<div class="paragraph">

Polkadot nodes connect to peers by establishing a TCP connection. Once
established, the node initiates a handshake with the remote peers on the
encryption layer. An additional layer on top of the encryption layer,
known as the multiplexing layer, allows a connection to be split into
substreams, as described by the [yamux
specification](https://docs.libp2p.io/concepts/stream-multiplexing/#yamux),
either by the local or remote node.

</div>

<div class="paragraph">

The Polkadot node supports two types of substream protocols. [Section
4.7](#sect-protocols-substreams) describes the usage of each type in
more detail:

</div>

<div class="ulist">

- **Request-Response substreams**: After the protocol is negotiated by
  the multiplexing layer, the initiator sends a single message
  containing a request. The responder then sends a response, after which
  the substream is then immediately closed. The requests and responses
  are prefixed with their [LEB128](https://en.wikipedia.org/wiki/LEB128)
  encoded length.

- **Notification substreams**. After the protocol is negotiated, the
  initiator sends a single handshake message. The responder can then
  either accept the substream by sending its own handshake or reject it
  by closing the substream. After the substream has been accepted, the
  initiator can send an unbound number of individual messages. The
  responder keeps its sending side of the substream open, despite not
  sending anything anymore, and can later close it in order to signal to
  the initiator that it no longer wishes to communicate.

  <div class="paragraph">

  Handshakes and messages are prefixed with their
  [LEB128](https://en.wikipedia.org/wiki/LEB128) encoded lengths. A
  handshake can be empty, in which case the length prefix would be *0*.

  </div>

</div>

<div class="paragraph">

Connections are established by using the following protocols:

</div>

<div class="ulist">

- `/noise` - a protocol that is announced when a connection to a peer is
  established.

- `/multistream/1.0.0` - a protocol that is announced when negotiating
  an encryption protocol or a substream.

- `/yamux/1.0.0` - a protocol used during *yamux* negotiation. See
  [Section 4.7](#sect-protocols-substreams) for more information.

</div>

<div class="paragraph">

The Polkadot Host can establish a connection with any peer of which it
knows the address. The Polkadot Host supports multiple networking
protocols:

</div>

<div class="ulist">

- **TCP/IP** with addresses in the form of `/ip4/1.2.3.4/tcp/30333` to
  establish a TCP connection and negotiate encryption and a multiplexing
  layer.

- **WebSocket** with addresses in the form of
  `/ip4/1.2.3.4/tcp/30333/ws` to establish a TCP connection and
  negotiate the WebSocket protocol within the connection. Additionally,
  encryption and multiplexing layer is negotiated within the WebSocket
  connection.

- **DNS** addresses in form of `/dns/example.com/tcp/30333` and
  `/dns/example.com/tcp/30333/ws`.

</div>

<div class="paragraph">

The addressing system is described in the [libp2p
addressing](https://docs.libp2p.io/concepts/addressing/) specification.
After a base-layer protocol is established, the Polkadot Host will apply
the Noise protocol to establish the encryption layer as described in
[Section 4.6](#sect-encryption-layer).

</div>

</div>

<div class="sect2">

### <a href="#sect-encryption-layer" class="anchor"></a><a href="#sect-encryption-layer" class="link">4.6. Encryption Layer</a>

<div class="paragraph">

Polkadot protocol uses the *libp2p* Noise framework to build an
encryption protocol. The Noise protocol is a framework for building
encryption protocols. *libp2p* utilizes that protocol for establishing
encrypted communication channels. Refer to the [libp2p Secure Channel
Handshake](https://github.com/libp2p/specs/tree/master/noise)
specification for a detailed description.

</div>

<div class="paragraph">

Polkadot nodes use the [XX handshake
pattern](https://noiseexplorer.com/patterns/XX/) to establish a
connection between peers. The three following steps are required to
complete the handshake process:

</div>

<div class="olist arabic">

1.  The initiator generates a keypair and sends the public key to the
    responder. The [Noise
    specification](https://github.com/libp2p/specs/tree/master/noise)
    and the [libp2p PeerId
    specification](https://github.com/libp2p/specs/blob/master/peer-ids/peer-ids.md)
    describe keypairs in more detail.

2.  The responder generates its own key pair and sends its public key
    back to the initiator. After that, the responder derives a shared
    secret and uses it to encrypt all further communication. The
    responder now sends its static Noise public key (which may change
    anytime and does not need to be persisted on disk), its *libp2p*
    public key and a signature of the static Noise public key signed
    with the *libp2p* public key.

3.  The initiator derives a shared secret and uses it to encrypt all
    further communication. It also sends its static Noise public key,
    *libp2p* public key and signature to the responder.

</div>

<div class="paragraph">

After these three steps, both the initiator and responder derive a new
shared secret using the static and session-defined Noise keys, which are
used to encrypt all further communication.

</div>

</div>

<div class="sect2">

### <a href="#sect-protocols-substreams" class="anchor"></a><a href="#sect-protocols-substreams" class="link">4.7. Protocols and
Substreams</a>

<div class="paragraph">

After the node establishes a connection with a peer, the use of
multiplexing allows the Polkadot Host to open substreams. *libp2p* uses
the [*yamux
protocol*](https://docs.libp2p.io/concepts/stream-multiplexing/#yamux)
to manage substreams and to allow the negotiation of
*application-specific protocols*, where each protocol serves a specific
utility.

</div>

<div class="paragraph">

The Polkadot Host uses multiple substreams whose usage depends on a
specific purpose. Each substream is either a *Request-Response
substream* or a *Notification substream*, as described in [Section
4.5](#sect-connection-establishment).

</div>

<div class="admonitionblock note">

|     |                                                                                                                                                                                                                                                                                           |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | The prefixes on those substreams are known as protocol identifiers and are used to segregate communications to specific networks. This prevents any interference with other networks. `dot` is used exclusively for Polkadot. Kusama, for example, uses the protocol identifier `ksmcc3`. |

</div>

<div class="ulist">

- `/ipfs/ping/1.0.0` - Open a standardized substream *libp2p* to a peer
  and initialize a ping to verify if a connection is still alive. If the
  peer does not respond, the connection is dropped. This is a
  *Request-Response substream*.

  <div class="paragraph">

  Further specification and reference implementation are available in
  the [libp2p
  documentation](https://docs.libp2p.io/concepts/protocols/#ping).

  </div>

- `/ipfs/id/1.0.0` - Open a standardized *libp2p* substream to a peer to
  ask for information about that peer. This is a *Request-Response
  substream*, but the initiator does **not** send any message to the
  responder and only waits for the response.

  <div class="paragraph">

  Further specification and reference implementation are available in
  the [libp2p
  documentation](https://docs.libp2p.io/concepts/protocols/#identify).

  </div>

- `/dot/kad` - Open a standardized substream for Kademlia `FIND_NODE`
  requests. This is a *Request-Response substream*, as defined by the
  *libp2p* standard.

  <div class="paragraph">

  Further specification and reference implementation are available on
  [Wikipedia](https://en.wikipedia.org/wiki/Kademlia) respectively the
  [golang Github
  repository](https://github.com/libp2p/go-libp2p-kad-dht).

  </div>

- `/91b171bb158e2d3848fa23a9f1c25182fb8e20313b2c1eb49219da7a70ce90c3/light/2` -
  a request and response protocol that allows a light client to request
  information about the state. This is a *Request-Response substream*.

  <div class="paragraph">

  The messages are specified in [Section 7.4](#sect-light-msg).

  </div>

  <div class="admonitionblock note">

  |     |                                                                                                   |
  |-----|---------------------------------------------------------------------------------------------------|
  |     | For backwards compatibility reasons, `/dot/light/2` is also a valid substream for those messages. |

  </div>

- `/91b171bb158e2d3848fa23a9f1c25182fb8e20313b2c1eb49219da7a70ce90c3/block-announces/1` -
  a substream/notification protocol which sends blocks to connected
  peers. This is a *Notification substream*.

  <div class="paragraph">

  The messages are specified in [Section
  4.8.1](#sect-msg-block-announce).

  </div>

  <div class="admonitionblock note">

  |     |                                                                                                             |
  |-----|-------------------------------------------------------------------------------------------------------------|
  |     | For backwards compatibility reasons, `/dot/block-announces/1` is also a valid substream for those messages. |

  </div>

- `/91b171bb158e2d3848fa23a9f1c25182fb8e20313b2c1eb49219da7a70ce90c3/sync/2` -
  a request and response protocol that allows the Polkadot Host to
  request information about blocks. This is a *Request-Response
  substream*.

  <div class="paragraph">

  The messages are specified in [Section
  4.8.2](#sect-msg-block-request).

  </div>

  <div class="admonitionblock note">

  |     |                                                                                                  |
  |-----|--------------------------------------------------------------------------------------------------|
  |     | For backwards compatibility reasons, `/dot/sync/2` is also a valid substream for those messages. |

  </div>

- `/91b171bb158e2d3848fa23a9f1c25182fb8e20313b2c1eb49219da7a70ce90c3/sync/warp` -
  a request and response protocol that allows the Polkadot Host to
  perform a warp sync request. This is a *Request-Response substream*.

  <div class="paragraph">

  The messages are specified in [Section 4.8.4](#sect-msg-warp-sync).

  </div>

  <div class="admonitionblock note">

  |     |                                                                                                     |
  |-----|-----------------------------------------------------------------------------------------------------|
  |     | For backwards compatibility reasons, `/dot/sync/warp` is also a valid substream for those messages. |

  </div>

- `/91b171bb158e2d3848fa23a9f1c25182fb8e20313b2c1eb49219da7a70ce90c3/transactions/1` -
  a substream/notification protocol which sends transactions to
  connected peers. This is a *Notification substream*.

  <div class="paragraph">

  The messages are specified in [Section 4.8.5](#sect-msg-transactions).

  </div>

  <div class="admonitionblock note">

  |     |                                                                                                          |
  |-----|----------------------------------------------------------------------------------------------------------|
  |     | For backwards compatibility reasons, `/dot/transactions/1` is also a valid substream for those messages. |

  </div>

- `/91b171bb158e2d3848fa23a9f1c25182fb8e20313b2c1eb49219da7a70ce90c3/grandpa/1` -
  a substream/notification protocol that sends GRANDPA votes to
  connected peers. This is a *Notification substream*.

  <div class="paragraph">

  The messages are specified in [Section 4.8.6](#sect-msg-grandpa).

  </div>

  <div class="admonitionblock note">

  |     |                                                                                                            |
  |-----|------------------------------------------------------------------------------------------------------------|
  |     | For backwards compatibility reasons, `/paritytech/grandpa/1` is also a valid substream for those messages. |

  </div>

- `/91b171bb158e2d3848fa23a9f1c25182fb8e20313b2c1eb49219da7a70ce90c3/beefy/1` -
  a substream/notification protocol which sends signed BEEFY statements,
  as described in [Section 6.7](#sect-grandpa-beefy), to connected
  peers. This is a *Notification* substream.

  <div class="paragraph">

  The messages are specified in [Section
  4.8.7](#sect-msg-grandpa-beefy).

  </div>

  <div class="admonitionblock note">

  |     |                                                                                                          |
  |-----|----------------------------------------------------------------------------------------------------------|
  |     | For backwards compatibility reasons, `/paritytech/beefy/1` is also a valid substream for those messages. |

  </div>

</div>

</div>

<div class="sect2">

### <a href="#sect-network-messages" class="anchor"></a><a href="#sect-network-messages" class="link">4.8. Network Messages</a>

<div class="paragraph">

The Polkadot Host must actively communicate with the network in order to
participate in the validation process or act as a full node.

</div>

<div class="admonitionblock note">

|     |                                                                                                                                                                                                                                                                                                       |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | The Polkadot network originally only used SCALE encoding for all message formats. Meanwhile, Protobuf has been adopted for certain messages. The encoding of each listed message is always SCALE encoded unless Protobuf is explicitly mentioned. Encoding and message formats are subject to change. |

</div>

<div class="sect3">

#### <a href="#sect-msg-block-announce" class="anchor"></a><a href="#sect-msg-block-announce" class="link">4.8.1. Announcing
blocks</a>

<div class="paragraph">

When the node creates or receives a new block, it must be announced to
the network. Other nodes within the network will track this announcement
and can request information about this block. The mechanism for tracking
announcements and requesting the required data is
implementation-specific.

</div>

<div class="paragraph">

Block announcements, requests and responses are sent over the substream
as described in [Definition 35](#defn-block-announce-handshake).

</div>

<div id="defn-block-announce-handshake" class="exampleblock">

<div class="title">

Definition 35. [Block Announce
Handshake](#defn-block-announce-handshake)

</div>

<div class="content">

<div class="paragraph">

The `BlockAnnounceHandshake` initializes a substream to a remote peer.
Once established, all `BlockAnounce` messages ([Definition
36](#defn-block-announce)) created by the node are sent to the
`/dot/block-announces/1` substream.

</div>

<div class="paragraph">

The `BlockAnnounceHandshake` is a structure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\BA_h = "Enc"\_("SC")(R, N_B, h_B, h_G)\\

</div>

</div>

<div class="paragraph">

where:

</div>

<div class="stemblock">

<div class="content">

\\R = {(1,"The node is a full node"),(2,"The node is a light
client"),(4,"The node is a validator"):}\\ \\N_B = "Best block number
according to the node"\\ \\h_B = "Best block hash according to the
node"\\ \\h_G = "Genesis block hash according to the node"\\

</div>

</div>

</div>

</div>

<div id="defn-block-announce" class="exampleblock">

<div class="title">

Definition 36. [Block Announce](#defn-block-announce)

</div>

<div class="content">

<div class="paragraph">

The `BlockAnnounce` message is sent to the specified substream and
indicates to remote peers that the node has either created or received a
new block.

</div>

<div class="paragraph">

The message is a structure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\BA = "Enc"\_("SC")("Head"(B),b)\\

</div>

</div>

<div class="paragraph">

where:

</div>

<div class="stemblock">

<div class="content">

\\"Head"(B) = "Header of the announced block"\\ \\b = {(0,"Is not part
of the best chain"),(1,"Is the best block according to the node"):}\\

</div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-msg-block-request" class="anchor"></a><a href="#sect-msg-block-request" class="link">4.8.2. Requesting
Blocks</a>

<div class="paragraph">

Block requests can be used to retrieve a range of blocks from peers.
Those messages are sent over the `/dot/sync/2` substream.

</div>

<div id="defn-msg-block-request" class="exampleblock">

<div class="title">

Definition 37. [Block Request](#defn-msg-block-request)

</div>

<div class="content">

<div class="paragraph">

The `BlockRequest` message is a Protobuf serialized structure of the
following format:

</div>

| Type        | Id  | Description                                                       | Value   |
|-------------|-----|-------------------------------------------------------------------|---------|
| `uint32`    | 1   | Bits of block data to request                                     | \\B_f\\ |
| `oneof`     |     | Start from this block                                             | \\B_s\\ |
| *Direction* | 5   | Sequence direction, interpreted as Id *0* (ascending) if missing. |         |
| `uint32`    | 6   | Maximum amount (*optional*)                                       | \\B_m\\ |

<div class="dlist">

where  
<div class="ulist">

- \\B_f\\ indicates all the fields that should be included in the
  request. its **big-endian** encoded bitmask that applies to all
  desired fields with bitwise OR operations. For example, the \\B_f\\
  value to request *Header* and *Justification* is *0001 0001* (17).

  | Field         | Value     |
  |---------------|-----------|
  | Header        | 0000 0001 |
  | Body          | 0000 0010 |
  | Justification | 0001 0000 |

- \\B_s\\ is a Protobuf structure indicating a varying data type (enum)
  of the following values:

  | Type    | Id  | Description      |
  |---------|-----|------------------|
  | `bytes` | 2   | The block hash   |
  | `bytes` | 3   | The block number |

- *Direction* is a Protobuf structure indicating the sequence direction
  of the requested blocks. The structure is a varying data type (enum)
  of the following format:

  | Id  | Description                                                    |
  |-----|----------------------------------------------------------------|
  | 0   | Enumerate in ascending order (from child to parent)            |
  | 1   | Enumerate in descending order (from parent to canonical child) |

- \\B_m\\ is the number of blocks to be returned. An implementation
  defined maximum is used when unspecified.

</div>

</div>

</div>

</div>

<div id="defn-msg-block-response" class="exampleblock">

<div class="title">

Definition 38. [Block Response](#defn-msg-block-response)

</div>

<div class="content">

<div class="paragraph">

The `BlockResponse` message is received after sending a `BlockRequest`
message to a peer. The message is a Protobuf serialized structure of the
following format:

</div>

| Type                 | Id  | Description                           |
|----------------------|-----|---------------------------------------|
| Repeated *BlockData* | 1   | Block data for the requested sequence |

<div class="paragraph">

where *BlockData* is a Protobuf structure containing the requested
blocks. Do note that the optional values are either present or absent
depending on the requested fields (bitmask value). The structure has the
following format:

</div>

| Type             | Id  | Description                                                           | Value                                        |
|------------------|-----|-----------------------------------------------------------------------|----------------------------------------------|
| `bytes`          | 1   | Block header hash                                                     | [Definition 12](#defn-block-header-hash)     |
| `bytes`          | 2   | Block header (optional)                                               | [Definition 10](#defn-block-header)          |
| repeated `bytes` | 3   | Block body (optional)                                                 | [Definition 13](#defn-block-body)            |
| `bytes`          | 4   | Block receipt (optional)                                              |                                              |
| `bytes`          | 5   | Block message queue (optional)                                        |                                              |
| `bytes`          | 6   | Justification (optional)                                              | [Definition 78](#defn-grandpa-justification) |
| `bool`           | 7   | Indicates whether the justification is empty (i.e. should be ignored) |                                              |

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-msg-state-request" class="anchor"></a><a href="#sect-msg-state-request" class="link">4.8.3. Requesting
States</a>

<div class="paragraph">

The Polkadot Host can request the state in form of a key/value list at a
specified block.

</div>

<div class="paragraph">

When receiving state entries from the state response messages
([Definition 40](#defn-msg-state-response)), the node can verify the
entries with the entry proof (id *1* in *KeyValueStorage*) against the
merkle root in the block header (of the block specified in [Definition
39](#defn-msg-state-request)). Once the state response message claims
that all entries have been sent (id *3* in *KeyValueStorage*), the node
can use all collected entry proofs and validate it against the merkle
root to confirm that claim.

</div>

<div class="paragraph">

See the the synchronization chapter for more information ([Chapter
3](#chap-sync)).

</div>

<div id="defn-msg-state-request" class="exampleblock">

<div class="title">

Definition 39. [State Request](#defn-msg-state-request)

</div>

<div class="content">

<div class="paragraph">

A **state request** is sent to a peer to request the state at a
specified block. The message is a single 32-byte Blake2 hash which
indicates the block from which the sync should start.

</div>

<div class="paragraph">

Depending on what substream is used, he remote peer either sends back a
state response ([Definition 40](#defn-msg-state-response)) on the
`/dot/sync/2` substream or a warp sync proof ([Definition
41](#defn-warp-sync-proof)) on the `/dot/sync/warp`.

</div>

</div>

</div>

<div id="defn-msg-state-response" class="exampleblock">

<div class="title">

Definition 40. [State Response](#defn-msg-state-response)

</div>

<div class="content">

<div class="paragraph">

The **state response** is sent to the peer that initialized the state
request ([Definition 39](#defn-msg-state-request)) and contains a list
of key/value entries with an associated proof. This response is sent
continuously until all key/value pairs have been submitted.

</div>

| Type                          | Id  | Description   |
|-------------------------------|-----|---------------|
| `repeated KeyValueStateEntry` | 1   | State entries |
| `bytes`                       | 2   | State proof   |

<div class="paragraph">

where *KeyValueStateEntry* is of the following format:

</div>

| Type                  | Id  | Description                                       |
|-----------------------|-----|---------------------------------------------------|
| `bytes`               | 1   | Root of the entry, empty if top level             |
| `repeated StateEntry` | 2   | Collection of key/values                          |
| `bool`                | 3   | Equal 'true' if there are no more keys to return. |

<div class="paragraph">

and *StateEntry*:

</div>

| Type    | Id  | Description            |
|---------|-----|------------------------|
| `bytes` | 1   | The key of the entry   |
| `bytes` | 2   | The value of the entry |

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-msg-warp-sync" class="anchor"></a><a href="#sect-msg-warp-sync" class="link">4.8.4. Warp Sync</a>

<div class="paragraph">

The warp sync protocols allows nodes to retrieve blocks from remote
peers where authority set changes occurred. This can be used to speed up
synchronization to the latest state.

</div>

<div class="paragraph">

See the the synchronization chapter for more information ([Chapter
3](#chap-sync)).

</div>

<div id="defn-warp-sync-proof" class="exampleblock">

<div class="title">

Definition 41. [Warp Sync Proof](#defn-warp-sync-proof)

</div>

<div class="content">

<div class="paragraph">

The **warp sync proof** message, \\P\\, is sent to the peer that
initialized the state request ([Definition 39](#defn-msg-state-request))
on the `/dot/sync/warp` substream and contains accumulated proof of
multiple authority set changes ([Section
3.3.2](#sect-consensus-message-digest)). It’s a datastructure of the
following format:

</div>

<div class="stemblock">

<div class="content">

\\P = (f_x...f_y, c)\\

</div>

</div>

<div class="paragraph">

\\f_x...f_y\\ is an array consisting of warp sync fragments of the
following format:

</div>

<div class="stemblock">

<div class="content">

\\f_x = (B_h, J^(r,"stage")(B))\\

</div>

</div>

<div class="paragraph">

where \\B_h\\ is the last block header containing a digest item
([Definition 11](#defn-digest)) signaling an authority set change from
which the next authority set change can be fetched from.
\\J^(r,"stage")(B)\\ is the GRANDPA justification ([Definition
78](#defn-grandpa-justification)) and \\c\\ is a boolean that indicates
whether the warp sync has been completed.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-msg-transactions" class="anchor"></a><a href="#sect-msg-transactions" class="link">4.8.5. Transactions</a>

<div class="paragraph">

Transactions ([Section 2.3](#sect-extrinsics)) are sent directly to
peers with which the Polkadot Host has an open transaction substream
([Definition 42](#defn-transactions-message)). Polkadot Host
implementers should implement a mechanism that only sends a transaction
once to each peer and avoids sending duplicates. Sending duplicate
transactions might result in undefined consequences such as being
blocked for bad behavior by peers.

</div>

<div class="paragraph">

The mechanism for managing transactions is further described in Section
[Section 2.3](#sect-extrinsics).

</div>

<div id="defn-transactions-message" class="exampleblock">

<div class="title">

Definition 42. [Transaction Message](#defn-transactions-message)

</div>

<div class="content">

<div class="paragraph">

The **transactions message** is the structure of how the transactions
are sent over the network. It is represented by \\M_T\\ and is defined
as follows:

</div>

<div class="stemblock">

<div class="content">

\\M_T := "Enc"\_("SC")(C_1,...,C_n)\\

</div>

</div>

<div class="paragraph">

in which:

</div>

<div class="stemblock">

<div class="content">

\\C_i := "Enc"\_("SC")(E_i)\\

</div>

</div>

<div class="paragraph">

Where each \\E_i\\ is a byte array and represents a separate extrinsic.
The Polkadot Host is agnostic about the content of an extrinsic and
treats it as a blob of data.

</div>

<div class="paragraph">

Transactions are sent over the `/dot/transactions/1` substream.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-msg-grandpa" class="anchor"></a><a href="#sect-msg-grandpa" class="link">4.8.6. GRANDPA Messages</a>

<div class="paragraph">

The exchange of GRANDPA messages is conducted on the substream. The
process for the creation and distributing these messages is described in
[Chapter 6](#sect-finality). The underlying messages are specified in
this section.

</div>

<div id="defn-gossip-message" class="exampleblock">

<div class="title">

Definition 43. [Grandpa Gossip Message](#defn-gossip-message)

</div>

<div class="content">

<div class="paragraph">

A **GRANDPA gossip message**, \\M\\, is a varying datatype ([Definition
188](#defn-varrying-data-type)) which identifies the message type that
is cast by a voter followed by the message itself.

</div>

<div class="stemblock">

<div class="content">

\\M = {(0,"Vote message", V_m),(1,"Commit message", C_m),(2,"Neighbor
message", N_m),(3,"Catch-up request message",R_m),(4,"Catch-up
message",U_m):}\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\V_m\\ is defined in [Definition 44](#defn-grandpa-vote-msg).

- \\C_m\\ is defined in [Definition 46](#defn-grandpa-commit-msg).

- \\N_m\\ is defined in [Definition 47](#defn-grandpa-neighbor-msg).

- \\R_m\\ is defined in [Definition
  48](#defn-grandpa-catchup-request-msg).

- \\U_M\\ is defined in [Definition
  49](#defn-grandpa-catchup-response-msg).

</div>

</div>

</div>

</div>

<div id="defn-grandpa-vote-msg" class="exampleblock">

<div class="title">

Definition 44. [GRANDPA Vote Messages](#defn-grandpa-vote-msg)

</div>

<div class="content">

<div class="paragraph">

A **GRANDPA vote message** by voter \\v\\, \\M_v^(r,"stage")\\, is
gossip to the network by voter \\v\\ with the following structure:

</div>

<div class="stemblock">

<div class="content">

\\M_v^(r,"stage")(B) := "Enc"\_("SC")(r,"id"\_(bbb V),"SigMsg")\\
\\"SigMsg" := ("msg","Sig"\_(v_i)^(r,"stage"),v\_("id"))\\ \\"msg" :=
"Enc"\_("SC")("stage",V_v^(r,"stage")(B))\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\r\\ is an unsigned 64-bit integer indicating the Grandpa round
  number ([Definition 76](#defn-voting-rounds)).

- \\"id"\_(bbb V)\\ is an unsigned 64-bit integer indicating the
  authority Set Id ([Definition 33](#defn-authority-list)).

- \\"Sig"\_(v_i)^(r,"stage")\\ is a 512-bit byte array containing the
  signature of the authority ([Definition 77](#defn-sign-round-vote)).

- \\v\_(id)\\ is a 256-bit byte array containing the *ed25519* public
  key of the authority.

- \\"stage"\\ is a 8-bit integer of value *0* if it’s a pre-vote
  sub-round, *1* if it’s a pre-commit sub-round or *2* if it’s a primary
  proposal message.

- \\V_v^(r,"stage")(B)\\ is the GRANDPA vote for block \\B\\
  ([Definition 76](#defn-voting-rounds)).

</div>

</div>

<div class="paragraph">

This message is the sub-component of the GRANDPA gossip message
([Definition 43](#defn-gossip-message)) of type Id 0.

</div>

</div>

</div>

<div id="defn-grandpa-justifications-compact" class="exampleblock">

<div class="title">

Definition 45. [GRANDPA Compact Justification
Format](#defn-grandpa-justifications-compact)

</div>

<div class="content">

<div class="paragraph">

The **GRANDPA compact justification format** is an optimized data
structure to store a collection of pre-commits and their signatures to
be submitted as part of a commit message. Instead of storing an array of
justifications, it uses the following format:

</div>

<div class="stemblock">

<div class="content">

\\J\_(v\_(0,...n))^(r,"comp") := ({V\_(v_0)^(r,pc),...
V\_(v_n)^(r,pc)},{("Sig"\_(v_0)^(r,pc),v\_("id"\_0)), ...
("Sig"\_(v_n)^(r,pc),v\_("id"\_n))})\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\V\_(v_i)^(r,pc)\\ is a 256-bit byte array containing the pre-commit
  vote of authority \\v_i\\ ([Definition 76](#defn-voting-rounds)).

- \\"Sig"\_(v_i)^(r,pc)\\ is a 512-bit byte array containing the
  pre-commit signature of authority \\v_i\\ ([Definition
  77](#defn-sign-round-vote)).

- \\v\_("id"\_n)\\ is a 256-bit byte array containing the public key of
  authority \\v_i\\.

</div>

</div>

</div>

</div>

<div id="defn-grandpa-commit-msg" class="exampleblock">

<div class="title">

Definition 46. [GRANDPA Commit Message](#defn-grandpa-commit-msg)

</div>

<div class="content">

<div class="paragraph">

A **GRANDPA commit message** for block \\B\\ in round \\r\\,
\\M_v^(r,"Fin")(B)\\, is a message broadcasted by voter \\v\\ to the
network indicating that voter \\v\\ has finalized block \\B\\ in round
\\r\\. It has the following structure:

</div>

<div class="stemblock">

<div class="content">

\\M_v^(r,"Fin")(B) := "Enc"\_("SC")(r,"id"\_(bbb
V),V_v^r(B),J\_(v\_(0,...n))^(r,"comp"))\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\r\\ is an unsigned 64-bit integer indicating the round number
  ([Definition 76](#defn-voting-rounds)).

- \\id\_(bbb V)\\ is the authority set Id ([Definition
  33](#defn-authority-list)).

- \\V_v^r(B)\\ is a 256-bit array containing the GRANDPA vote for block
  \\B\\ ([Definition 75](#defn-vote)).

- \\J\_(v\_(0,...n))^(r,"comp")\\ is the compacted GRANDPA justification
  containing observed pre-commit of authorities \\v_0\\ to \\v_n\\
  ([Definition 45](#defn-grandpa-justifications-compact)).

</div>

</div>

<div class="paragraph">

This message is the sub-component of the GRANDPA gossip message
([Definition 43](#defn-gossip-message)) of type Id *1*.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#sect-grandpa-neighbor-msg" class="anchor"></a><a href="#sect-grandpa-neighbor-msg" class="link">4.8.6.1. GRANDPA
Neighbor Messages</a>

<div class="paragraph">

Neighbor messages are sent to all connected peers but they are not
repropagated on reception. A message should be send whenever the
messages values change and at least every 5 minutes. The sender should
take the recipients state into account and avoid sending messages to
peers that are using a different voter sets or are in a different round.
Messages received from a future voter set or round can be dropped and
ignored.

</div>

<div id="defn-grandpa-neighbor-msg" class="exampleblock">

<div class="title">

Definition 47. [GRANDPA Neighbor Message](#defn-grandpa-neighbor-msg)

</div>

<div class="content">

<div class="paragraph">

A **GRANDPA Neighbor Message** is defined as:

</div>

<div class="stemblock">

<div class="content">

\\M^("neigh") := "Enc"\_("SC")(v,r,"id"\_(bbb V),H_i(B\_("last")))\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\v\\ is an unsigned 8-bit integer indicating the version of the
  neighbor message, currently *1*.

- \\r\\ is an unsigned 64-bit integer indicating the round number
  ([Definition 76](#defn-voting-rounds)).

- \\"id"\_(bbb V)\\ is an unsigned 64-bit integer indicating the
  authority Id ([Definition 33](#defn-authority-list)).

- \\H_i(B\_("last"))\\ is an unsigned 32-bit integer indicating the
  block number of the last finalized block \\B\_("last")\\.

</div>

</div>

<div class="paragraph">

This message is the sub-component of the GRANDPA gossip message
([Definition 43](#defn-gossip-message)) of type Id *2*.

</div>

</div>

</div>

</div>

<div class="sect4">

##### <a href="#sect-grandpa-catchup-messages" class="anchor"></a><a href="#sect-grandpa-catchup-messages" class="link">4.8.6.2. GRANDPA
Catch-up Messages</a>

<div class="paragraph">

Whenever a Polkadot node detects that it is lagging behind the finality
procedure, it needs to initiate a *catch-up* procedure. GRANDPA Neighbor
messages ([Definition 47](#defn-grandpa-neighbor-msg)) reveal the round
number for the last finalized GRANDPA round which the node’s peers have
observed. This provides the means to identify a discrepancy in the
latest finalized round number observed among the peers. If such a
discrepancy is observed, the node needs to initiate the catch-up
procedure explained in [Section 6.6.1](#sect-grandpa-catchup)).

</div>

<div class="paragraph">

In particular, this procedure involves sending a *catch-up request* and
processing *catch-up response* messages.

</div>

<div id="defn-grandpa-catchup-request-msg" class="exampleblock">

<div class="title">

Definition 48. [Catch-Up Request
Message](#defn-grandpa-catchup-request-msg)

</div>

<div class="content">

<div class="paragraph">

A **GRANDPA catch-up request message** for round \\r\\,
\\M\_(i,v)^("Cat"-q)("id"\_(bbb V),r)\\, is a message sent from node
\\i\\ to its voting peer node \\v\\ requesting the latest status of a
GRANDPA round \\r' \>r\\ of the authority set \\bbb V\_("id")\\ along
with the justification of the status and has the following structure:

</div>

<div class="stemblock">

<div class="content">

\\M\_(i,v)^(r,"Cat"-q) := "Enc"\_("SC")(r,"id"\_(bbb V))\\

</div>

</div>

<div class="paragraph">

This message is the sub-component of the GRANDPA Gossip message
([Definition 43](#defn-gossip-message)) of type Id *3*.

</div>

</div>

</div>

<div id="defn-grandpa-catchup-response-msg" class="exampleblock">

<div class="title">

Definition 49. [Catch-Up Response
Message](#defn-grandpa-catchup-response-msg)

</div>

<div class="content">

<div class="paragraph">

A **GRANDPA catch-up response message** for round \\r\\,
\\M\_(v,i)^("Cat"-s)("id"\_(bbb V),r)\\, is a message sent by a node
\\v\\ to node \\i\\ in response of a catch-up request
\\M\_(v,i)^("Cat"-q)("id"\_(bbb V),r')\\ in which \\r \>= r'\\ is the
latest GRANDPA round which v has prove of its finalization and has the
following structure:

</div>

<div class="stemblock">

<div class="content">

\\M\_(v,i)^("Cat"-s) := "Enc"\_("SC")("id"\_(bbb V), r,
J\_(0,...n)^(r,"pv")(B), J\_(0,...m)^(r,"pc")(B),H_h(B'),H_i(B'))\\

</div>

</div>

<div class="paragraph">

Where \\B\\ is the highest block which \\v\\ believes to be finalized in
round \\r\\ ([Definition 76](#defn-voting-rounds)). \\B'\\ is the
highest ancestor of all blocks voted on in the arrays of justifications
\\J\_(0,...n)^(r,"pv")(B)\\ and \\J\_(0,...m)^(r,"pc")(B)\\ ([Definition
78](#defn-grandpa-justification)) with the exception of the equivocatory
votes.

</div>

<div class="paragraph">

This message is the sub-component of the GRANDPA Gossip message
([Definition 43](#defn-gossip-message)) of type Id *4*.

</div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-msg-grandpa-beefy" class="anchor"></a><a href="#sect-msg-grandpa-beefy" class="link">4.8.7. GRANDPA BEEFY</a>

<div class="admonitionblock warning">

|     |                                                                             |
|-----|-----------------------------------------------------------------------------|
|     | The BEEFY protocol is currently in early development and subject to change. |

</div>

<div class="paragraph">

This section defines the messages required for the GRANDPA BEEFY
protocol ([Section 6.7](#sect-grandpa-beefy)). Those messages are sent
over the `/paritytech/beefy/1` substream.

</div>

<div id="defn-grandpa-beefy-commitment" class="exampleblock">

<div class="title">

Definition 50. [Commitment](#defn-grandpa-beefy-commitment)

</div>

<div class="content">

<div class="paragraph">

A **commitment**, \\C\\, contains the information extracted from the
finalized block at height \\H_i(B\_("last"))\\ as specified in the
message body and a datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\C = (R_h,H_i(B\_("last")),"id"\_(bbb V))\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\R_h\\ is the MMR root of all the block header hashes leading up to
  the latest, finalized block.

- \\H_i(B\_("last"))\\ is the block number this commitment is for.
  Namely the latest, finalized block.

- \\"id"\_(bbb V)\\ is the current authority set Id ([Definition
  73](#defn-authority-set-id)).

</div>

</div>

</div>

</div>

<div id="defn-msg-beefy-gossip" class="exampleblock">

<div class="title">

Definition 51. [Vote Message](#defn-msg-beefy-gossip)

</div>

<div class="content">

<div class="paragraph">

A **vote message**, \\M_v\\, is direct vote created by the Polkadot Host
on every BEEFY round and is gossiped to its peers. The message is a
datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\M_v = "Enc"\_("SC")(C,A\_("id")^("bfy"),A\_("sig"))\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\C\\ is the BEEFY commitment ([Definition
  50](#defn-grandpa-beefy-commitment)).

- \\A\_("id")^("bfy")\\ is the ECDSA public key of the Polkadot Host.

- \\A\_("sig")\\ is the signature created with \\A\_("id")^("bfy")\\ by
  signing the statement \\R_h\\ in \\C\\.

</div>

</div>

</div>

</div>

<div id="defn-grandpa-beefy-signed-commitment" class="exampleblock">

<div class="title">

Definition 52. [Signed
Commitment](#defn-grandpa-beefy-signed-commitment)

</div>

<div class="content">

<div class="paragraph">

A **signed commitment**, \\M\_("sc")\\, is a datastructure of the
following format:

</div>

<div class="stemblock">

<div class="content">

\\M\_("SC") = "Enc"\_("SC")(C,S_n)\\ \\S_n = (A_0^("sig"),...
A_n^("sig"))\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\C\\ is the BEEFY commitment ([Definition
  50](#defn-grandpa-beefy-commitment)).

- \\S_n\\ is an array where its exact size matches the number of
  validators in the current authority set as specified by \\"id"\_(bbb
  V)\\ ([Definition 73](#defn-authority-set-id)) in \\C\\. Individual
  items are of the type *Option* ([Definition 190](#defn-option-type))
  which can contain a signature of a validator which signed the same
  statement (\\R_h\\ in \\C\\) and is active in the current authority
  set. It’s critical that the signatures are sorted based on their
  corresponding public key entry in the authority set.

  <div class="paragraph">

  For example, the signature of the validator at index 3 in the
  authority set must be placed at index *3* in \\S_n\\. If not signature
  is available for that validator, then the *Option* variant is *None*
  inserted ([Definition 190](#defn-option-type)). This sorting allows
  clients to map public keys to their corresponding signatures.

  </div>

</div>

</div>

</div>

</div>

<div id="defn-grandpa-beefy-signed-commitment-witness"
class="exampleblock">

<div class="title">

Definition 53. [Signed Commitment
Witness](#defn-grandpa-beefy-signed-commitment-witness)

</div>

<div class="content">

<div class="paragraph">

A **signed commitment witness**, \\M\_("SC")^w\\, is a light version of
the signed BEEFY commitment ([Definition
52](#defn-grandpa-beefy-signed-commitment)). Instead of containing the
entire list of signatures, it only claims which validator signed the
statement.

</div>

<div class="paragraph">

The message is a datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\M\_("SC")^w = "Enc"\_("SC")(C,V\_(0,... n), R\_("sig"))\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\C\\ is the BEEFY commitment ([Definition
  50](#defn-grandpa-beefy-commitment)).

- \\V\_(0,... n)\\ is an array where its exact size matches the number
  of validators in the current authority set as specified by
  \\"id"\_(bbb V)\\ in \\C\\. Individual items are booleans which
  indicate whether the validator has signed the statement (*true*) or
  not (*false*). It’s critical that the boolean indicators are sorted
  based on their corresponding public key entry in the authority set.

  <div class="paragraph">

  For example, the boolean indicator of the validator at index 3 in the
  authority set must be placed at index *3* in \\V_n\\. This sorting
  allows clients to map public keys to their corresponding boolean
  indicators.

  </div>

- \\R\_("sig")\\ is the MMR root of the signatures in the original
  signed BEEFY commitment ([Definition
  52](#defn-grandpa-beefy-signed-commitment)).

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#sect-block-production" class="anchor"></a><a href="#sect-block-production" class="link">5. Block Production</a>

<div class="sectionbody">

<div class="sect2">

### <a href="#id-introduction-3" class="anchor"></a><a href="#id-introduction-3" class="link">5.1. Introduction</a>

<div class="paragraph">

The Polkadot Host uses BABE protocol for block production. It is
designed based on Ouroboros praos . BABE execution happens in sequential
non-overlapping phases known as an ***epoch***. Each epoch on its turn
is divided into a predefined number of slots. All slots in each epoch
are sequentially indexed starting from 0. At the beginning of each
epoch, the BABE node needs to run
[Block-Production-Lottery](#algo-block-production-lottery) to find out
in which slots it should produce a block and gossip to the other block
producers. In turn, the block producer node should keep a copy of the
block tree and grow it as it receives valid blocks from other block
producers. A block producer prunes the tree in parallel by eliminating
branches that do not include the most recent finalized blocks
([Definition 5](#defn-pruned-tree)).

</div>

<div class="sect3">

#### <a href="#id-block-producer" class="anchor"></a><a href="#id-block-producer" class="link">5.1.1. Block Producer</a>

<div class="paragraph">

A **block producer**, noted by \\cc P_j\\, is a node running the
Polkadot Host which is authorized to keep a transaction queue and which
it gets a turn in producing blocks.

</div>

</div>

<div class="sect3">

#### <a href="#id-block-authoring-session-key-pair" class="anchor"></a><a href="#id-block-authoring-session-key-pair" class="link">5.1.2. Block
Authoring Session Key Pair</a>

<div class="paragraph">

**Block authoring session key pair** \\(sk_j^s,pk_j^s)\\ is an SR25519
key pair which the block producer \\cc P_j\\ signs by their account key
([Definition 177](#defn-account-key)) and is used to sign the produced
block as well as to compute its lottery values in
[Block-Production-Lottery](#algo-block-production-lottery).

</div>

<div id="defn-epoch-slot" class="exampleblock">

<div class="title">

Definition 54. [Epoch and Slot](#defn-epoch-slot)

</div>

<div class="content">

<div class="paragraph">

A block production **epoch**, formally referred to as \\cc E\\, is a
period with a pre-known starting time and fixed-length during which the
set of block producers stays constant. Epochs are indexed sequentially,
and we refer to the \\n^(th)\\ epoch since genesis by \\cc E_n\\. Each
epoch is divided into equal-length periods known as block production
**slots**, sequentially indexed in each epoch. The index of each slot is
called a **slot number**. The equal length duration of each slot is
called the **slot duration** and indicated by \\cc T\\. Each slot is
awarded to a subset of block producers during which they are allowed to
generate a block.

</div>

<div class="admonitionblock note">

|     |                                                                                                                                       |
|-----|---------------------------------------------------------------------------------------------------------------------------------------|
|     | Substrate refers to an epoch as "session" in some places, however, epoch should be the preferred and official name for these periods. |

</div>

</div>

</div>

<div id="defn-epoch-duration" class="exampleblock">

<div class="title">

Definition 55. [Epoch and Slot Duration](#defn-epoch-duration)

</div>

<div class="content">

<div class="paragraph">

We refer to the number of slots in epoch \\cc E_n\\ by \\sc_n\\.
\\sc_n\\ is set to the `duration` field in the returned data from the
call of the Runtime entry `BabeApi_configuration` ([Section
C.11.1](#sect-rte-babeapi-epoch)) at genesis. For a given block \\B\\,
we use the notation **\\s_B\\** to refer to the slot during which \\B\\
has been produced. Conversely, for slot \\s\\, \\cc B_c\\ is the set of
Blocks generated at slot \\s\\.

</div>

<div class="paragraph">

[Definition 56](#defn-epoch-subchain) provides an iterator over the
blocks produced during a specific epoch.

</div>

</div>

</div>

<div id="defn-epoch-subchain" class="exampleblock">

<div class="title">

Definition 56. [Epoch Subchain](#defn-epoch-subchain)

</div>

<div class="content">

<div class="paragraph">

By \\"SubChain"(cc E_n\\) for epoch \\cc E_n\\, we refer to the path
graph of \\BT\\ containing all the blocks generated during the slots of
epoch \\cc E_n\\. When there is more than one block generated at a slot,
we choose the one which is also on \\"Longest-Chain"(BT)\\.

</div>

</div>

</div>

<div id="defn-equivovation" class="exampleblock">

<div class="title">

Definition 57. [Equivocation](#defn-equivocation)

</div>

<div class="content">

<div class="paragraph">

A block producer **equivocates** if they produce more than one block at
the same slot. The proof of equivocation are the given distinct headers
that were signed by the validator and which include the slot number.

</div>

<div class="paragraph">

The Polkadot Host must detect equivocations committed by other
validators and submit those to the Runtime as described in [Section
C.11.6](#sect-babeapi_submit_report_equivocation_unsigned_extrinsic).

</div>

</div>

</div>

<div id="defn-consensus-message-babe" class="exampleblock">

<div class="title">

Definition 58. [BABE Consensus Message](#defn-consensus-message-babe)

</div>

<div class="content">

<div class="paragraph">

\\"CM"\_b\\, the consensus message for BABE, is of the following format:

</div>

<div class="stemblock">

<div class="content">

\\"CM"\_b = {(1,("Auth"\_C, r)),(2,A_i),(3,D):}\\

</div>

</div>

<div class="dlist">

where

</div>

<div class="hdlist">

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td class="hdlist1">1</td>
<td class="hdlist2"><p>implies <strong>next epoch data</strong>: The
Runtime issues this message on every first block of an epoch. The
supplied authority set (<a href="#defn-authority-list">Definition
33</a>), \$"Auth"_C\$, and randomness (<a
href="#defn-epoch-randomness">Definition 71</a>), \$r\$, are used in the
next epoch \$cc E_n + 1\$.</p></td>
</tr>
<tr class="even">
<td class="hdlist1">2</td>
<td class="hdlist2"><p>implies <strong>on disabled</strong>: A 32-bit
integer, \$A_i\$, indicating the individual authority in the current
authority list that should be immediately disabled until the next
authority set changes. This message initial intension was to cause an
immediate suspension of all authority functionality with the specified
authority.</p></td>
</tr>
<tr class="odd">
<td class="hdlist1">3</td>
<td class="hdlist2"><p>implies <strong>next epoch descriptor</strong>:
These messages are only issued on configuration change and in the first
block of an epoch. The supplied configuration data are intended to be
used from the next epoch onwards.</p>
<div class="ulist">
<ul>
<li><p>\$D\$ is a varying datatype of the following format:</p>
<div class="stemblock">
<div class="content">
\$D = {(1, (c,2_("nd"))):}\$
</div>
</div>
<div class="paragraph">
<p>where \$c\$ is the probability that a slot will not be empty (<a
href="#defn-babe-constant">Definition 59</a>). It is encoded as a tuple
of two unsigned 64-bit integers \$(c_("nominator"),c_("denominator"))\$
which are used to compute the rational \$c =
c_("nominator")/c_("denominator")\$.</p>
</div></li>
<li><p>\$2_("nd")\$ describes what secondary slot (<a
href="#defn-babe-secondary-slots">Definition 61</a>), if any, is to be
used. It is encoded as one-byte varying datatype:</p>
<div class="stemblock">
<div class="content">
\$s_"2nd" = { (0,-&gt;,"no secondary slot"), (1,-&gt;,"plain secondary
slot"), (2,-&gt;,"secondary slot with VRF output") :}\$
</div>
</div></li>
</ul>
</div></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-block-production-lottery" class="anchor"></a><a href="#sect-block-production-lottery" class="link">5.2. Block
Production Lottery</a>

<div class="paragraph">

The babe constant ([Definition 59](#defn-babe-constant)) is initialized
at genesis to the value returned by calling `BabeApi_configuration`
([Section C.11.1](#sect-rte-babeapi-epoch)). For efficiency reasons, it
is generally updated by the Runtime through the *next config data*
consensus message in the digest ([Definition 11](#defn-digest)) of the
first block of an epoch for the next epoch.

</div>

<div class="paragraph">

A block producer aiming to produce a block during \\cc E_n\\ should run
\<algo-block-production-lottery\>\> to identify the slots it is awarded.
These are the slots during which the block producer is allowed to build
a block. The \\sk\\ is the block producer lottery secret key and \\n\\
is the index of the epoch for whose slots the block producer is running
the lottery.

</div>

<div class="paragraph">

In order to ensure consistent block production, BABE uses secondary
slots in case no authority won the (primary) block production lottery.
Unlike the lottery, secondary slot assignees are know upfront publically
([Definition 61](#defn-babe-secondary-slots)). The Runtime provides
information on how or if secondary slots are executed ([Section
C.11.1](#sect-rte-babeapi-epoch)), explained further in [Definition
61](#defn-babe-secondary-slots).

</div>

<div id="defn-babe-constant" class="exampleblock">

<div class="title">

Definition 59. [BABE Constant](#defn-babe-constant)

</div>

<div class="content">

<div class="paragraph">

The **BABE constant** is the probability that a slot will not be empty
and used in the winning threshold calculation ([Definition
60](#defn-winning-threshold)). It’s expressed as a rational, \\(x, y)\\,
where \\x\\ is the numerator and \\y\\ is the denominator.

</div>

</div>

</div>

<div id="defn-winning-threshold" class="exampleblock">

<div class="title">

Definition 60. [Winning Threshold](#defn-winning-threshold)

</div>

<div class="content">

<div class="paragraph">

The **Winning threshold** denoted by \\T\_(cc E_n)\\ is the threshold
that is used alongside the result of
[Block-Production-Lottery](#algo-block-production-lottery) to decide if
a block producer is the winner of a specific slot. \\T\_(cc E_n)\\ is
calculated as follows:

</div>

<div class="stemblock">

<div class="content">

\\A_w =sum\_(n=1)^(\|"Auth"\_C(B)\|)(w_A in "Auth"\_C(B)\_n)\\ \\T\_(cc
E_n) := 1 - (1 - c)^(w_a/A_w)\\

</div>

</div>

<div class="paragraph">

where \\A_w\\ is the total sum of all authority weights in the authority
set ([Definition 33](#defn-authority-list)) for epoch \\cc E_n\\,
\\w_a\\ is the weight of the block author and \\c in (0, 1)\\ is the
BABE constant ([Definition 59](#defn-babe-constant)).

</div>

<div class="paragraph">

The numbers should be treated as 64-bit rational numbers.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-primary-block-production-lottery" class="anchor"></a><a href="#id-primary-block-production-lottery" class="link">5.2.1.
Primary Block Production Lottery</a>

<div class="paragraph">

A block producer aiming to produce a block during \\cc E_n\\ should run
the \\"Block-Production-Lottery"\\ algorithm to identify the slots it is
awarded. These are the slots during which the block producer is allowed
to build a block. The session secret key, \\sk\\, is the block producer
lottery secret key and \\n\\ is the index of the epoch for whose slots
the block producer is running the lottery.

</div>

<div class="sidebarblock">

<div class="content">

\require sk \state \$r \leftarrow\$ \call{Epoch-Randomness}{\$n\$}
\for{\$i := 1 ~\textbf{to}~ sc_n\$} \state \$(\pi, d) \leftarrow\$
\call{VRF}{\$r, i, sk\$} \state \$A\[i\] \leftarrow (d, \pi)\$ \endfor
\return{A}

<div class="paragraph">

where \\"Epoch-Randomness"\\ is defined in ([Definition
71](#defn-epoch-randomness)), \\sc_n\\ is defined in [Definition
55](#defn-epoch-duration) , \\"VRF"\\ creates the BABE VRF transcript
([Definition 62](#defn-babe-vrf-transcript)) and \\e_i\\ is the epoch
index, retrieved from the Runtime ([Section
C.11.1](#sect-rte-babeapi-epoch)). \\s_k\\ and \\p_k\\ is the secret key
respectively the public key of the authority. For any slot \\s\\ in
epoch \\n\\ where \\o \< T\_(cc E_n)\\ ([Definition
60](#defn-winning-threshold)), the block producer is required to produce
a block.

</div>

</div>

</div>

<div class="admonitionblock note">

|     |                                                                                                                                                                                                                           |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | the secondary slots ([Definition 61](#defn-babe-secondary-slots)) are running along side the primary block production lottery and mainly serve as a fallback to in case no authority was selected in the primary lottery. |

</div>

<div id="defn-babe-secondary-slots" class="exampleblock">

<div class="title">

Definition 61. [Secondary Slots](#defn-babe-secondary-slots)

</div>

<div class="content">

<div class="paragraph">

**Secondary slots** work along side primary slot to ensure consistent
block production, as described in [Section
5.2](#sect-block-production-lottery). The secondary assignee of a block
is determined by calculating a specific value, \\i_d\\, which indicates
the index in the authority set ([Definition 33](#defn-authority-list)).
The corresponding authority in that set has the right to author a
secondary block. This calculation is done for every slot in the epoch,
\\s in sc_n\\ ([Definition 55](#defn-epoch-duration)).

</div>

<div class="stemblock">

<div class="content">

\\p larr h("Enc"\_"SC"(r,s))\\ \\i_d larr p mod A_l\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\r\\ is the Epoch randomness ([Definition
  71](#defn-epoch-randomness)).

- \\s\\ is the slot number ([Definition 54](#defn-epoch-slot)).

- \\"Enc"\_"SC"(...)\\ encodes its inner value to the corresponding
  SCALE value.

- \\h(...)\\ creates a 256-bit Blake2 hash from its inner value.

- \\A_l\\ is the lengths of the authority list ([Definition
  33](#defn-authority-list)).

</div>

</div>

<div class="paragraph">

If \\i_d\\ points to the authority, that authority must claim the
secondary slot by creating a BABE VRF transcript ([Definition
62](#defn-babe-vrf-transcript)). The resulting values \\o\\ and \\p\\
are then used in the Pre-Digest item ([Definition
69](#defn-babe-header)). In case of secondary slots with plain outputs,
respectively the Pre-Digest being of value *2*, the transcript
respectively the VRF is skipped.

</div>

</div>

</div>

<div id="defn-babe-vrf-transcript" class="exampleblock">

<div class="title">

Definition 62. [BABE Slot VRF transcript](#defn-babe-vrf-transcript)

</div>

<div class="content">

<div class="paragraph">

The BABE block production lottery requires a specific transcript
structure ([Definition 175](#defn-vrf-transcript)). That structure is
used by both primary slots
([Block-Production-Lottery](#algo-block-production-lottery)) and
secondary slots ([Definition 61](#defn-babe-secondary-slots)).

</div>

<div class="stemblock">

<div class="content">

\\t_1 larr "Transcript"("'BABE'")\\ \\t_2 larr "append"(t_1, "'slot
number'", s)\\ \\t_3 larr "append"(t_2, "'current epoch'", e_i)\\ \\t_4
larr "append"(t_3, "'chain randomness'", r)\\ \\t_5 larr "append"(t_4,
"'vrf-nm-pk'", p_k)\\ \\t_6 larr "meta-ad"(t_5, "'VRFHash'", "False")\\
\\t_7 larr "meta-ad"(t_6, 64\_"le", "True")\\ \\h larr "prf"(t_7,
"False")\\ \\o = s_k \* h\\ \\p larr "dleq_prove"(t_7, h)\\

</div>

</div>

<div class="paragraph">

The operators are defined in [Definition 176](#defn-strobe-operations),
\\"dleq_prove"\\ in [Definition 172](#defn-vrf-dleq-prove). The computed
outputs, \\o\\ and \\p\\, are included in the block Pre-Digest
([Definition 69](#defn-babe-header)).

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-slot-number-calculation" class="anchor"></a><a href="#sect-slot-number-calculation" class="link">5.3. Slot Number
Calculation</a>

<div class="paragraph">

It is imperative for the security of the network that each block
producer correctly determines the current slot numbers at a given time
by regularly estimating the local clock offset in relation to the
network ([Definition 64](#defn-relative-synchronization)).

</div>

<div class="sidebarblock">

<div class="content">

<div class="admonitionblock important">

|     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | **The calculation described in this section is still to be implemented and deployed**: For now, each block producer is required to synchronize its local clock using NTP instead. The current slot \\s\\ is then calculated by \\s = t\_"unix"/cc T\\ where \\cc T\\ is defined in [Definition 54](#defn-epoch-slot) and \\t\_"unix"\\ is defined in [Definition 181](#defn-unix-time). That also entails that slot numbers are currently not reset at the beginning of each epoch. |

</div>

</div>

</div>

<div class="paragraph">

Polkadot does this synchronization without relying on any external clock
source (e.g. through the or the ). To stay in synchronization, each
producer is therefore required to periodically estimate its local clock
offset in relation to the rest of the network.

</div>

<div class="paragraph">

This estimation depends on the two fixed parameters \\k\\ ([Definition
65](#defn-prunned-best)) and \\s\_(cq)\\ ([Definition
66](#defn-chain-quality)). These are chosen based on the results of a
[formal security
analysis](https://research.web3.foundation/en/latest/polkadot/block-production/Babe.html#-5.-security-analysis),
currently assuming a \\1 s\\ clock drift per day and targeting a
probability lower than \\0.5%\\ for an adversary to break BABE in 3
years with resistance against a network delay up to \\1 / 3\\ of the
slot time and a Babe constant ([Definition 59](#defn-babe-constant)) of
\\c = 0.38\\.

</div>

<div class="paragraph">

All validators are then required to run
[Median-Algorithm](#algo-slot-time) at the beginning of each sync period
([Definition 68](#defn-sync-period)) to update their synchronization
using all block arrival times of the previous period. The algorithm
should only be run once all the blocks in this period have been
finalized, even if only probabilistically ([Definition
65](#defn-prunned-best)). The target slot to which to synchronize should
be the first slot in the new sync period.

</div>

<div id="defn-slot-offset" class="exampleblock">

<div class="title">

Definition 63. [Slot Offset](#defn-slot-offset)

</div>

<div class="content">

<div class="paragraph">

Let \\s_i\\ and \\s_j\\ be two slots belonging to epochs \\cc E_k\\ and
\\cc E_l\\. By **Slot-Offset**\\(s_i,s_j)\\ we refer to the function
whose value is equal to the number of slots between \\s_i\\ and \\s_j\\
(counting \\s_j\\) on the time continuum. As such, we have
**Slot-Offset**\\(s_i, s_i) = 0\\.

</div>

</div>

</div>

<div class="paragraph">

It is imperative for the security of the network that each block
producer correctly determines the current slot numbers at a given time
by regularly estimating the local clock offset in relation to the
network ([Definition 64](#defn-relative-synchronization)).

</div>

<div id="defn-relative-synchronization" class="exampleblock">

<div class="title">

Definition 64. [Relative Time
Synchronization](#defn-relative-synchronization)

</div>

<div class="content">

<div class="paragraph">

The **relative time synchronization** is a tuple of a slot number and a
local clock timestamp \\(s\_"sync",t\_"sync")\\ describing the last
point at which the slot numbers have been synchronized with the local
clock.

</div>

</div>

</div>

<div class="sidebarblock">

<div class="content">

\require \$s\$ \return{\$t\_\text{sync} +
\$\call{Slot-Offset}{\$s\_{sync}, s\$}\$ \times \mathcal{T}\$}

<div class="paragraph">

where \\s\\ is the slot number.

</div>

</div>

</div>

<div class="sidebarblock">

<div class="content">

\require \$\mathfrak{E}, s\_{sync}\$ \state \$T_s \leftarrow \\ \\\$
\for{\$B ~\textbf{in}~ \mathfrak{E}\_j\$} \state \$t\_{est}^{B}
\leftarrow T_B + \$\call{Slot-Offset}{\$s_B, s\_{sync}\$}\$ \times
\mathcal{T}\$ \state \$T_s \leftarrow T_s \cup t\_{est}^{B}\$ \endfor
\return \call{Median}{\$T_s\$}

<div class="dlist">

where  
<div class="ulist">

- \\\mathfrak{E}\\ is the sync period used for the estimate.

- \\s\_"sync"\\ is the slot time to estimate.

- \\"Slot-Offset"\\ is defined in [Slot-Time](#algo-slot-offset).

- \\\mathcal{T}\\ is the slot duration defined in [Definition
  54](#defn-epoch-slot).

</div>

</div>

</div>

</div>

<div id="defn-prunned-best" class="exampleblock">

<div class="title">

Definition 65. [Pruned Best Chain](#defn-prunned-best)

</div>

<div class="content">

<div class="paragraph">

The **pruned best chain** \\C^(r^k)\\ is the longest selected chain
([Definition 7](#defn-longest-chain)) with the last \\k\\ Blocks pruned.
We chose \\k= 140\\. The **last (probabilistic) finalized block**
describes the last block in this pruned best chain.

</div>

</div>

</div>

<div id="defn-chain-quality" class="exampleblock">

<div class="title">

Definition 66. [Chain Quality](#defn-chain-quality)

</div>

<div class="content">

<div class="paragraph">

The **chain quality** \\s\_(cq)\\ represents the number of slots that
are used to estimate the local clock offset. Currently, it is set to
\\s\_(cq) = 3000\\.

</div>

<div class="paragraph">

The prerequisite for such a calculation is that each producer stores the
arrival time of each block ([Definition 67](#defn-block-time)) measured
by a clock that is otherwise not adjusted by any external protocol.

</div>

</div>

</div>

<div id="defn-block-time" class="exampleblock">

<div class="title">

Definition 67. [Block Arrival Time](#defn-block-time)

</div>

<div class="content">

<div class="paragraph">

The **block arrival time** of block \\B\\ for node \\j\\ formally
represented by \\T_B^j\\ is the local time of node \\j\\ when node \\j\\
has received block \\B\\ for the first time. If the node \\j\\ itself is
the producer of \\B\\, \\T_B^j\\ is set equal to the time that the block
is produced. The index \\j\\ in \\T_B^j\\ notation may be dropped and
B’s arrival time is referred to by \\T_B\\ when there is no ambiguity
about the underlying node.

</div>

</div>

</div>

<div id="defn-sync-period" class="exampleblock">

<div class="title">

Definition 68. [Sync Period](#defn-sync-period)

</div>

<div class="content">

<div class="paragraph">

A is an interval at which each validator (re-)evaluates its local clock
offsets. The first sync period \\fr E_1\\ starts just after the genesis
block is released. Consequently, each sync period \\fr E_i\\ starts
after \\fr E\_(i - 1)\\. The length of the sync period ([Definition
66](#defn-chain-quality)) is equal to \\s\_(qc)\\and expressed in the
number of slots.

</div>

</div>

</div>

<div class="imageblock">

<div class="content">

<img
src="data:image/svg+xml;base64,PHN2ZyB2ZXJzaW9uPSIxLjEiIGlkPSJzdmcyIiB4bWw6c3BhY2U9InByZXNlcnZlIiB3aWR0aD0iMTA5Ny4zMzMzIiBoZWlnaHQ9IjYzNi44OTMzMSIgdmlld2JveD0iMCAwIDEwOTcuMzMzMyA2MzYuODkzMzEiIHNvZGlwb2RpOmRvY25hbWU9ImMwMS1zMDVfYmFiZS10aW1lLXN5bmMuZXBzIiB4bWxuczppbmtzY2FwZT0iaHR0cDovL3d3dy5pbmtzY2FwZS5vcmcvbmFtZXNwYWNlcy9pbmtzY2FwZSIgeG1sbnM6c29kaXBvZGk9Imh0dHA6Ly9zb2RpcG9kaS5zb3VyY2Vmb3JnZS5uZXQvRFREL3NvZGlwb2RpLTAuZHRkIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnN2Zz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPjxkZWZzIGlkPSJkZWZzNiI+PC9kZWZzPjxuYW1lZHZpZXcgaWQ9Im5hbWVkdmlldzQiIHBhZ2Vjb2xvcj0iI2ZmZmZmZiIgYm9yZGVyY29sb3I9IiM2NjY2NjYiIGJvcmRlcm9wYWNpdHk9IjEuMCIgaW5rc2NhcGU6cGFnZXNoYWRvdz0iMiIgaW5rc2NhcGU6cGFnZW9wYWNpdHk9IjAuMCIgaW5rc2NhcGU6cGFnZWNoZWNrZXJib2FyZD0iMCI+PC9uYW1lZHZpZXc+PGcgaWQ9Imc4IiBpbmtzY2FwZTpncm91cG1vZGU9ImxheWVyIiBpbmtzY2FwZTpsYWJlbD0iaW5rX2V4dF9YWFhYWFgiIHRyYW5zZm9ybT0ibWF0cml4KDEuMzMzMzMzMywwLDAsLTEuMzMzMzMzMywwLDYzNi44OTMzMykiPjxnIGlkPSJnMTAiIHRyYW5zZm9ybT0ic2NhbGUoMC4xKSI+PHBhdGggZD0iTSAxOTcxLjAyLDM2NjguMTIgViAyMjMyLjI1IiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoyLjU7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoMTIiPjwvcGF0aD48cGF0aCBkPSJNIDI1MDUsMzY2OC4xMiBWIDIyMzIuMjUiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjIuNTtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgxNCI+PC9wYXRoPjxwYXRoIGQ9Ik0gMzE1MC4xNywzNjY4LjEyIFYgMjIzMi4yNSIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6Mi41O3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDE2Ij48L3BhdGg+PHBhdGggZD0iTSAzNTgxLjc4LDM2NjguMTIgViAyMjMyLjI1IiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoyLjU7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoMTgiPjwvcGF0aD48cGF0aCBkPSJNIDQxMzcuNDUsMzY2OC4xMiBWIDIyMzIuMjUiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjIuNTtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgyMCI+PC9wYXRoPjxwYXRoIGQ9Ik0gNDQ5NS42LDM2NjguMTIgViAyMjMyLjI1IiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoyLjU7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoMjIiPjwvcGF0aD48cGF0aCBkPSJNIDUxOTAuNjUsMzY2OC4xMiBWIDIyMzIuMjUiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjIuNTtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgyNCI+PC9wYXRoPjxwYXRoIGQ9Ik0gNTkzNi43NCwzNjY4LjEyIFYgMjIzMi4yNSIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6Mi41O3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDI2Ij48L3BhdGg+PHBhdGggZD0iTSA2MzI0LjMsMzY2OC4xMiBWIDIyMzIuMjUiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjIuNTtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgyOCI+PC9wYXRoPjxwYXRoIGQ9Im0gNzIzMS40MiwxODguNjkxIGggLTMxNC41NSB2IDQyMi40NTcgaCAzMTQuNTUgViAxODguNjkxIiBzdHlsZT0iZmlsbDojZmFjZDA4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDMwIj48L3BhdGg+PHBhdGggZD0ibSAxOTcwLjg5LDM2MTIuMyA2ODguNDIsNDg5Ljc5IEggNjQ4Ni4yIiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojZmFjZDA4O3N0cm9rZS13aWR0aDoyMDtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgzMiI+PC9wYXRoPjxwYXRoIGQ9Im0gMjY1OS4zMSw0MTAyLjA5IDE0Ni40NSw0OTYuOTYgaCAyNjEwLjQ3IiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojZmFjZDA4O3N0cm9rZS13aWR0aDoyMDtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgzNCI+PC9wYXRoPjxwYXRoIGQ9Ik0gMTk3MC44OSwzNjEyLjMgSCA2OTYwLjEyIiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojZmFjZDA4O3N0cm9rZS13aWR0aDoyMDtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgzNiI+PC9wYXRoPjxwYXRoIGQ9Im0gMzE1MC4wNSwzNjEyLjMgMTQyLjQ0LC00ODkuNzkgaCAyNDUyLjQ2IiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojZmFjZDA4O3N0cm9rZS13aWR0aDoyMDtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgzOCI+PC9wYXRoPjxwYXRoIGQ9Ik0gNjMyNC4xOSwzNjEyLjMgNzQ5Mi4yMywyNjMyLjcyIiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojZmFjZDA4O3N0cm9rZS13aWR0aDoyMDtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGg0MCI+PC9wYXRoPjxwYXRoIGQ9Ik0gNjE0MC41NCw0MTAyLjA5IDY5MTEuMSw0NjEzLjQiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiNmYWNkMDg7c3Ryb2tlLXdpZHRoOjIwO3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDQyIj48L3BhdGg+PHBhdGggZD0ibSAxOTE1LjA3LDM0NTQuMDQgYyAtNTYuNDgsMCAtMTAyLjQ0LDQ1Ljk1IC0xMDIuNDQsMTAyLjQzIHYgMTExLjY1IGMgMCw1Ni40OSA0NS45NiwxMDIuNDQgMTAyLjQ0LDEwMi40NCBoIDExMS42NSBjIDU2LjQ4LDAgMTAyLjQ0LC00NS45NSAxMDIuNDQsLTEwMi40NCB2IC0xMTEuNjUgYyAwLC01Ni40OCAtNDUuOTYsLTEwMi40MyAtMTAyLjQ0LC0xMDIuNDMgaCAtMTExLjY1IiBzdHlsZT0iZmlsbDojZmZmZmZmO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQ0Ij48L3BhdGg+PHBhdGggZD0ibSAyMDI2LjcyLDM3NzUuNTYgYyAtMjAuNDcsMCAtOTEuMTgsMCAtMTExLjY1LDAgLTU5LjM0LDAgLTEwNy40NCwtNDguMSAtMTA3LjQ0LC0xMDcuNDQgMCwtMjAuNDcgMCwtOTEuMTcgMCwtMTExLjY1IDAsLTU5LjMzIDQ4LjEsLTEwNy40MyAxMDcuNDQsLTEwNy40MyAyMC40NywwIDkxLjE4LDAgMTExLjY1LDAgNTkuMzQsMCAxMDcuNDQsNDguMSAxMDcuNDQsMTA3LjQzIDAsMjAuNDggMCw5MS4xOCAwLDExMS42NSAwLDU5LjM0IC00OC4xLDEwNy40NCAtMTA3LjQ0LDEwNy40NCB6IG0gMCwtMTAgYyA1My43MywwIDk3LjQ0LC00My43MSA5Ny40NCwtOTcuNDQgdiAtMTExLjY1IGMgMCwtNTMuNzIgLTQzLjcxLC05Ny40MyAtOTcuNDQsLTk3LjQzIGggLTExMS42NSBjIC01My43MywwIC05Ny40NCw0My43MSAtOTcuNDQsOTcuNDMgdiAxMTEuNjUgYyAwLDUzLjczIDQzLjcxLDk3LjQ0IDk3LjQ0LDk3LjQ0IGggMTExLjY1IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQ2Ij48L3BhdGg+PHBhdGggZD0ibSAyNDQ5LjA1LDM0NTQuMDQgYyAtNTYuNDksMCAtMTAyLjQ0LDQ1Ljk1IC0xMDIuNDQsMTAyLjQzIHYgMTExLjY1IGMgMCw1Ni40OSA0NS45NSwxMDIuNDQgMTAyLjQ0LDEwMi40NCBoIDExMS42NSBjIDU2LjQ4LDAgMTAyLjQ0LC00NS45NSAxMDIuNDQsLTEwMi40NCB2IC0xMTEuNjUgYyAwLC01Ni40OCAtNDUuOTYsLTEwMi40MyAtMTAyLjQ0LC0xMDIuNDMgaCAtMTExLjY1IiBzdHlsZT0iZmlsbDojZmZmZmZmO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQ4Ij48L3BhdGg+PHBhdGggZD0ibSAyNTYwLjcsMzc3NS41NiBjIC0yMC40NywwIC05MS4xOCwwIC0xMTEuNjUsMCAtNTkuMzQsMCAtMTA3LjQ0LC00OC4xIC0xMDcuNDQsLTEwNy40NCAwLC0yMC40NyAwLC05MS4xNyAwLC0xMTEuNjUgMCwtNTkuMzMgNDguMSwtMTA3LjQzIDEwNy40NCwtMTA3LjQzIDIwLjQ3LDAgOTEuMTgsMCAxMTEuNjUsMCA1OS4zNCwwIDEwNy40NCw0OC4xIDEwNy40NCwxMDcuNDMgMCwyMC40OCAwLDkxLjE4IDAsMTExLjY1IDAsNTkuMzQgLTQ4LjEsMTA3LjQ0IC0xMDcuNDQsMTA3LjQ0IHogbSAwLC0xMCBjIDUzLjczLDAgOTcuNDQsLTQzLjcxIDk3LjQ0LC05Ny40NCB2IC0xMTEuNjUgYyAwLC01My43MiAtNDMuNzEsLTk3LjQzIC05Ny40NCwtOTcuNDMgaCAtMTExLjY1IGMgLTUzLjczLDAgLTk3LjQ0LDQzLjcxIC05Ny40NCw5Ny40MyB2IDExMS42NSBjIDAsNTMuNzMgNDMuNzEsOTcuNDQgOTcuNDQsOTcuNDQgaCAxMTEuNjUiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTAiPjwvcGF0aD48cGF0aCBkPSJtIDI1MDQuODcsNDE1Ny45MiBjIDAsNTkuMzMgNDguMSwxMDcuNDMgMTA3LjQ1LDEwNy40MyAyMC40NywwIDkxLjE3LDAgMTExLjY0LDAgNTkuMzQsMCAxMDcuNDQsLTQ4LjEgMTA3LjQ0LC0xMDcuNDMgMCwtMjAuNDggMCwtOTEuMTkgMCwtMTExLjY1IDAsLTU5LjM0IC00OC4xLC0xMDcuNDUgLTEwNy40NCwtMTA3LjQ1IC0yMC40NywwIC05MS4xNywwIC0xMTEuNjQsMCAtNTkuMzUsMCAtMTA3LjQ1LDQ4LjExIC0xMDcuNDUsMTA3LjQ1IDAsMjAuNDYgMCw5MS4xNyAwLDExMS42NSIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1MiI+PC9wYXRoPjxwYXRoIGQ9Im0gMjY0Mi41LDQ2NTQuODggYyAwLDU5LjM0IDQ4LjEsMTA3LjQzIDEwNy40MywxMDcuNDMgMjAuNDgsMCA5MS4xOCwwIDExMS42NSwwIDU5LjM0LDAgMTA3LjQ0LC00OC4wOSAxMDcuNDQsLTEwNy40MyAwLC0yMC40OCAwLC05MS4xOCAwLC0xMTEuNjUgMCwtNTkuMzQgLTQ4LjEsLTEwNy40NCAtMTA3LjQ0LC0xMDcuNDQgLTIwLjQ3LDAgLTkxLjE3LDAgLTExMS42NSwwIC01OS4zMywwIC0xMDcuNDMsNDguMSAtMTA3LjQzLDEwNy40NCAwLDIwLjQ3IDAsOTEuMTcgMCwxMTEuNjUiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTQiPjwvcGF0aD48cGF0aCBkPSJtIDQ4NzYuMzIsNDY1NC44OCBjIDAsNTkuMzQgNDguMTEsMTA3LjQzIDEwNy40NSwxMDcuNDMgMjAuNDcsMCA5MS4xNywwIDExMS42NSwwIDU5LjMzLDAgMTA3LjQ0LC00OC4wOSAxMDcuNDQsLTEwNy40MyAwLC0yMC40OCAwLC05MS4xOCAwLC0xMTEuNjUgMCwtNTkuMzQgLTQ4LjExLC0xMDcuNDQgLTEwNy40NCwtMTA3LjQ0IC0yMC40OCwwIC05MS4xOCwwIC0xMTEuNjUsMCAtNTkuMzQsMCAtMTA3LjQ1LDQ4LjEgLTEwNy40NSwxMDcuNDQgMCwyMC40NyAwLDkxLjE3IDAsMTExLjY1IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDU2Ij48L3BhdGg+PHBhdGggZD0ibSA1MjUyLjk3LDQ2NTQuODggYyAwLDU5LjM0IDQ4LjEsMTA3LjQzIDEwNy40NCwxMDcuNDMgMjAuNDcsMCA5MS4xNywwIDExMS42NSwwIDU5LjMzLDAgMTA3LjQzLC00OC4wOSAxMDcuNDMsLTEwNy40MyAwLC0yMC40OCAwLC05MS4xOCAwLC0xMTEuNjUgMCwtNTkuMzQgLTQ4LjEsLTEwNy40NCAtMTA3LjQzLC0xMDcuNDQgLTIwLjQ4LDAgLTkxLjE4LDAgLTExMS42NSwwIC01OS4zNCwwIC0xMDcuNDQsNDguMSAtMTA3LjQ0LDEwNy40NCAwLDIwLjQ3IDAsOTEuMTcgMCwxMTEuNjUiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTgiPjwvcGF0aD48cGF0aCBkPSJtIDI4ODguOTMsNDE1Ny45MiBjIDAsNTkuMzMgNDguMSwxMDcuNDMgMTA3LjQ0LDEwNy40MyAyMC40NywwIDkxLjE4LDAgMTExLjY1LDAgNTkuMzMsMCAxMDcuNDQsLTQ4LjEgMTA3LjQ0LC0xMDcuNDMgMCwtMjAuNDggMCwtOTEuMTkgMCwtMTExLjY1IDAsLTU5LjM0IC00OC4xMSwtMTA3LjQ1IC0xMDcuNDQsLTEwNy40NSAtMjAuNDcsMCAtOTEuMTgsMCAtMTExLjY1LDAgLTU5LjM0LDAgLTEwNy40NCw0OC4xMSAtMTA3LjQ0LDEwNy40NSAwLDIwLjQ2IDAsOTEuMTcgMCwxMTEuNjUiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjAiPjwvcGF0aD48cGF0aCBkPSJtIDQ0OTUuNDcsNDE1Ny45MiBjIDAsNTkuMzMgNDguMTEsMTA3LjQzIDEwNy40NSwxMDcuNDMgMjAuNDcsMCA5MS4xNywwIDExMS42NSwwIDU5LjMzLDAgMTA3LjQzLC00OC4xIDEwNy40MywtMTA3LjQzIDAsLTIwLjQ4IDAsLTkxLjE5IDAsLTExMS42NSAwLC01OS4zNCAtNDguMSwtMTA3LjQ1IC0xMDcuNDMsLTEwNy40NSAtMjAuNDgsMCAtOTEuMTgsMCAtMTExLjY1LDAgLTU5LjM0LDAgLTEwNy40NSw0OC4xMSAtMTA3LjQ1LDEwNy40NSAwLDIwLjQ2IDAsOTEuMTcgMCwxMTEuNjUiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjIiPjwvcGF0aD48cGF0aCBkPSJtIDU5NzcuMjgsNDE1Ny45MiBjIDAsNTkuMzMgNDguMTEsMTA3LjQzIDEwNy40NCwxMDcuNDMgMjAuNDcsMCA5MS4xNywwIDExMS42NSwwIDU5LjM0LDAgMTA3LjQ0LC00OC4xIDEwNy40NCwtMTA3LjQzIDAsLTIwLjQ4IDAsLTkxLjE5IDAsLTExMS42NSAwLC01OS4zNCAtNDguMSwtMTA3LjQ1IC0xMDcuNDQsLTEwNy40NSAtMjAuNDgsMCAtOTEuMTgsMCAtMTExLjY1LDAgLTU5LjMzLDAgLTEwNy40NCw0OC4xMSAtMTA3LjQ0LDEwNy40NSAwLDIwLjQ2IDAsOTEuMTcgMCwxMTEuNjUiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjQiPjwvcGF0aD48cGF0aCBkPSJtIDYzMjIuOTQsNDE1Ny45MiBjIDAsNTkuMzMgNDguMDksMTA3LjQzIDEwNy40MywxMDcuNDMgMjAuNDgsMCA5MS4xOCwwIDExMS42NSwwIDU5LjMzLDAgMTA3LjQ0LC00OC4xIDEwNy40NCwtMTA3LjQzIDAsLTIwLjQ4IDAsLTkxLjE5IDAsLTExMS42NSAwLC01OS4zNCAtNDguMTEsLTEwNy40NSAtMTA3LjQ0LC0xMDcuNDUgLTIwLjQ3LDAgLTkxLjE3LDAgLTExMS42NSwwIC01OS4zNCwwIC0xMDcuNDMsNDguMTEgLTEwNy40MywxMDcuNDUgMCwyMC40NiAwLDkxLjE3IDAsMTExLjY1IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY2Ij48L3BhdGg+PHBhdGggZD0ibSAzMDk0LjIyLDM0NTQuMDQgYyAtNTYuNDgsMCAtMTAyLjQ0LDQ1Ljk1IC0xMDIuNDQsMTAyLjQzIHYgMTExLjY1IGMgMCw1Ni40OSA0NS45NiwxMDIuNDQgMTAyLjQ0LDEwMi40NCBoIDExMS42NSBjIDU2LjQ4LDAgMTAyLjQ0LC00NS45NSAxMDIuNDQsLTEwMi40NCB2IC0xMTEuNjUgYyAwLC01Ni40OCAtNDUuOTYsLTEwMi40MyAtMTAyLjQ0LC0xMDIuNDMgaCAtMTExLjY1IiBzdHlsZT0iZmlsbDojZmZmZmZmO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY4Ij48L3BhdGg+PHBhdGggZD0ibSAzMjA1Ljg3LDM3NzUuNTYgYyAtMjAuNDcsMCAtOTEuMTgsMCAtMTExLjY1LDAgLTU5LjM0LDAgLTEwNy40NCwtNDguMSAtMTA3LjQ0LC0xMDcuNDQgMCwtMjAuNDcgMCwtOTEuMTcgMCwtMTExLjY1IDAsLTU5LjMzIDQ4LjEsLTEwNy40MyAxMDcuNDQsLTEwNy40MyAyMC40NywwIDkxLjE4LDAgMTExLjY1LDAgNTkuMzQsMCAxMDcuNDQsNDguMSAxMDcuNDQsMTA3LjQzIDAsMjAuNDggMCw5MS4xOCAwLDExMS42NSAwLDU5LjM0IC00OC4xLDEwNy40NCAtMTA3LjQ0LDEwNy40NCB6IG0gMCwtMTAgYyA1My43MywwIDk3LjQ0LC00My43MSA5Ny40NCwtOTcuNDQgdiAtMTExLjY1IGMgMCwtNTMuNzIgLTQzLjcxLC05Ny40MyAtOTcuNDQsLTk3LjQzIGggLTExMS42NSBjIC01My43MywwIC05Ny40NCw0My43MSAtOTcuNDQsOTcuNDMgdiAxMTEuNjUgYyAwLDUzLjczIDQzLjcxLDk3LjQ0IDk3LjQ0LDk3LjQ0IGggMTExLjY1IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDcwIj48L3BhdGg+PHBhdGggZD0ibSAzNTI1LjgzLDM0NTQuMDQgYyAtNTYuNDgsMCAtMTAyLjQ0LDQ1Ljk1IC0xMDIuNDQsMTAyLjQzIHYgMTExLjY1IGMgMCw1Ni40OSA0NS45NiwxMDIuNDQgMTAyLjQ0LDEwMi40NCBoIDExMS42NSBjIDU2LjQ5LDAgMTAyLjQ0LC00NS45NSAxMDIuNDQsLTEwMi40NCB2IC0xMTEuNjUgYyAwLC01Ni40OCAtNDUuOTUsLTEwMi40MyAtMTAyLjQ0LC0xMDIuNDMgaCAtMTExLjY1IiBzdHlsZT0iZmlsbDojZmZmZmZmO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDcyIj48L3BhdGg+PHBhdGggZD0ibSAzNjM3LjQ4LDM3NzUuNTYgYyAtMjAuNDcsMCAtOTEuMTgsMCAtMTExLjY1LDAgLTU5LjMzLDAgLTEwNy40NCwtNDguMSAtMTA3LjQ0LC0xMDcuNDQgMCwtMjAuNDcgMCwtOTEuMTcgMCwtMTExLjY1IDAsLTU5LjMzIDQ4LjExLC0xMDcuNDMgMTA3LjQ0LC0xMDcuNDMgMjAuNDcsMCA5MS4xOCwwIDExMS42NSwwIDU5LjM0LDAgMTA3LjQ0LDQ4LjEgMTA3LjQ0LDEwNy40MyAwLDIwLjQ4IDAsOTEuMTggMCwxMTEuNjUgMCw1OS4zNCAtNDguMSwxMDcuNDQgLTEwNy40NCwxMDcuNDQgeiBtIDAsLTEwIGMgNTMuNzMsMCA5Ny40NCwtNDMuNzEgOTcuNDQsLTk3LjQ0IHYgLTExMS42NSBjIDAsLTUzLjcyIC00My43MSwtOTcuNDMgLTk3LjQ0LC05Ny40MyBoIC0xMTEuNjUgYyAtNTMuNzMsMCAtOTcuNDQsNDMuNzEgLTk3LjQ0LDk3LjQzIHYgMTExLjY1IGMgMCw1My43MyA0My43MSw5Ny40NCA5Ny40NCw5Ny40NCBoIDExMS42NSIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3NCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzEyOS4yMywzMTc4LjM0IGMgMCw1OS4zMyA0OC4xLDEwNy40NCAxMDcuNDQsMTA3LjQ0IDIwLjQ3LDAgOTEuMTcsMCAxMTEuNjUsMCA1OS4zMywwIDEwNy40MywtNDguMTEgMTA3LjQzLC0xMDcuNDQgMCwtMjAuNDggMCwtOTEuMTcgMCwtMTExLjY1IDAsLTU5LjM0IC00OC4xLC0xMDcuNDQgLTEwNy40MywtMTA3LjQ0IC0yMC40OCwwIC05MS4xOCwwIC0xMTEuNjUsMCAtNTkuMzQsMCAtMTA3LjQ0LDQ4LjEgLTEwNy40NCwxMDcuNDQgMCwyMC40OCAwLDkxLjE3IDAsMTExLjY1IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDc2Ij48L3BhdGg+PHBhdGggZD0ibSAzNTI5LjI4LDMxNzguMzQgYyAwLDU5LjMzIDQ4LjExLDEwNy40NCAxMDcuNDQsMTA3LjQ0IDIwLjQ4LDAgOTEuMTgsMCAxMTEuNjYsMCA1OS4zMywwIDEwNy40MywtNDguMTEgMTA3LjQzLC0xMDcuNDQgMCwtMjAuNDggMCwtOTEuMTcgMCwtMTExLjY1IDAsLTU5LjM0IC00OC4xLC0xMDcuNDQgLTEwNy40MywtMTA3LjQ0IC0yMC40OCwwIC05MS4xOCwwIC0xMTEuNjYsMCAtNTkuMzMsMCAtMTA3LjQ0LDQ4LjEgLTEwNy40NCwxMDcuNDQgMCwyMC40OCAwLDkxLjE3IDAsMTExLjY1IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDc4Ij48L3BhdGg+PHBhdGggZD0ibSA0NzY0LjU4LDMxNzguMzQgYyAwLDU5LjMzIDQ4LjEsMTA3LjQ0IDEwNy40NCwxMDcuNDQgMjAuNDcsMCA5MS4xNywwIDExMS42NSwwIDU5LjMzLDAgMTA3LjQ0LC00OC4xMSAxMDcuNDQsLTEwNy40NCAwLC0yMC40OCAwLC05MS4xNyAwLC0xMTEuNjUgMCwtNTkuMzQgLTQ4LjExLC0xMDcuNDQgLTEwNy40NCwtMTA3LjQ0IC0yMC40OCwwIC05MS4xOCwwIC0xMTEuNjUsMCAtNTkuMzQsMCAtMTA3LjQ0LDQ4LjEgLTEwNy40NCwxMDcuNDQgMCwyMC40OCAwLDkxLjE3IDAsMTExLjY1IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDgwIj48L3BhdGg+PHBhdGggZD0ibSA1NTc1LjkxLDMxNzguMzQgYyAwLDU5LjMzIDQ4LjExLDEwNy40NCAxMDcuNDUsMTA3LjQ0IDIwLjQ2LDAgOTEuMTcsMCAxMTEuNjUsMCA1OS4zMywwIDEwNy40MywtNDguMTEgMTA3LjQzLC0xMDcuNDQgMCwtMjAuNDggMCwtOTEuMTcgMCwtMTExLjY1IDAsLTU5LjM0IC00OC4xLC0xMDcuNDQgLTEwNy40MywtMTA3LjQ0IC0yMC40OCwwIC05MS4xOSwwIC0xMTEuNjUsMCAtNTkuMzQsMCAtMTA3LjQ1LDQ4LjEgLTEwNy40NSwxMDcuNDQgMCwyMC40OCAwLDkxLjE3IDAsMTExLjY1IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDgyIj48L3BhdGg+PHBhdGggZD0ibSA0MDgxLjUxLDM0NTQuMDQgYyAtNTYuNDksMCAtMTAyLjQ0LDQ1Ljk1IC0xMDIuNDQsMTAyLjQzIHYgMTExLjY1IGMgMCw1Ni40OSA0NS45NSwxMDIuNDQgMTAyLjQ0LDEwMi40NCBoIDExMS42NCBjIDU2LjQ5LDAgMTAyLjQ0LC00NS45NSAxMDIuNDQsLTEwMi40NCB2IC0xMTEuNjUgYyAwLC01Ni40OCAtNDUuOTUsLTEwMi40MyAtMTAyLjQ0LC0xMDIuNDMgaCAtMTExLjY0IiBzdHlsZT0iZmlsbDojZmZmZmZmO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDg0Ij48L3BhdGg+PHBhdGggZD0ibSA0MTkzLjE1LDM3NzUuNTYgYyAtMjAuNDcsMCAtOTEuMTcsMCAtMTExLjY0LDAgLTU5LjM0LDAgLTEwNy40NCwtNDguMSAtMTA3LjQ0LC0xMDcuNDQgMCwtMjAuNDcgMCwtOTEuMTcgMCwtMTExLjY1IDAsLTU5LjMzIDQ4LjEsLTEwNy40MyAxMDcuNDQsLTEwNy40MyAyMC40NywwIDkxLjE3LDAgMTExLjY0LDAgNTkuMzUsMCAxMDcuNDQsNDguMSAxMDcuNDQsMTA3LjQzIDAsMjAuNDggMCw5MS4xOCAwLDExMS42NSAwLDU5LjM0IC00OC4wOSwxMDcuNDQgLTEwNy40NCwxMDcuNDQgeiBtIDAsLTEwIGMgNTMuNzMsMCA5Ny40NCwtNDMuNzEgOTcuNDQsLTk3LjQ0IHYgLTExMS42NSBjIDAsLTUzLjcyIC00My43MSwtOTcuNDMgLTk3LjQ0LC05Ny40MyBoIC0xMTEuNjQgYyAtNTMuNzMsMCAtOTcuNDQsNDMuNzEgLTk3LjQ0LDk3LjQzIHYgMTExLjY1IGMgMCw1My43MyA0My43MSw5Ny40NCA5Ny40NCw5Ny40NCBoIDExMS42NCIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4NiI+PC9wYXRoPjxwYXRoIGQ9Im0gNDQzOS42NSwzNDU0LjA0IGMgLTU2LjQ4LDAgLTEwMi40NCw0NS45NSAtMTAyLjQ0LDEwMi40MyB2IDExMS42NSBjIDAsNTYuNDkgNDUuOTYsMTAyLjQ0IDEwMi40NCwxMDIuNDQgaCAxMTEuNjUgYyA1Ni40OCwwIDEwMi40NCwtNDUuOTUgMTAyLjQ0LC0xMDIuNDQgdiAtMTExLjY1IGMgMCwtNTYuNDggLTQ1Ljk2LC0xMDIuNDMgLTEwMi40NCwtMTAyLjQzIGggLTExMS42NSIgc3R5bGU9ImZpbGw6I2ZmZmZmZjtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNDU1MS4zLDM3NzUuNTYgYyAtMjAuNDcsMCAtOTEuMTgsMCAtMTExLjY2LDAgLTU5LjMzLDAgLTEwNy40MywtNDguMSAtMTA3LjQzLC0xMDcuNDQgMCwtMjAuNDcgMCwtOTEuMTcgMCwtMTExLjY1IDAsLTU5LjMzIDQ4LjEsLTEwNy40MyAxMDcuNDMsLTEwNy40MyAyMC40OCwwIDkxLjE5LDAgMTExLjY2LDAgNTkuMzQsMCAxMDcuNDQsNDguMSAxMDcuNDQsMTA3LjQzIDAsMjAuNDggMCw5MS4xOCAwLDExMS42NSAwLDU5LjM0IC00OC4xLDEwNy40NCAtMTA3LjQ0LDEwNy40NCB6IG0gMCwtMTAgYyA1My43MywwIDk3LjQ0LC00My43MSA5Ny40NCwtOTcuNDQgdiAtMTExLjY1IGMgMCwtNTMuNzIgLTQzLjcxLC05Ny40MyAtOTcuNDQsLTk3LjQzIGggLTExMS42NiBjIC01My43MiwwIC05Ny40Myw0My43MSAtOTcuNDMsOTcuNDMgdiAxMTEuNjUgYyAwLDUzLjczIDQzLjcxLDk3LjQ0IDk3LjQzLDk3LjQ0IGggMTExLjY2IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDkwIj48L3BhdGg+PHBhdGggZD0ibSA1MTM0LjcsMzQ1NC4wNCBjIC01Ni40OCwwIC0xMDIuNDMsNDUuOTUgLTEwMi40MywxMDIuNDMgdiAxMTEuNjUgYyAwLDU2LjQ5IDQ1Ljk1LDEwMi40NCAxMDIuNDMsMTAyLjQ0IGggMTExLjY1IGMgNTYuNDksMCAxMDIuNDUsLTQ1Ljk1IDEwMi40NSwtMTAyLjQ0IHYgLTExMS42NSBjIDAsLTU2LjQ4IC00NS45NiwtMTAyLjQzIC0xMDIuNDUsLTEwMi40MyBIIDUxMzQuNyIgc3R5bGU9ImZpbGw6I2ZmZmZmZjtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg5MiI+PC9wYXRoPjxwYXRoIGQ9Im0gNTI0Ni4zNSwzNzc1LjU2IGMgLTIwLjQ2LDAgLTkxLjE3LDAgLTExMS42NSwwIC01OS4zMywwIC0xMDcuNDMsLTQ4LjEgLTEwNy40MywtMTA3LjQ0IDAsLTIwLjQ3IDAsLTkxLjE3IDAsLTExMS42NSAwLC01OS4zMyA0OC4xLC0xMDcuNDMgMTA3LjQzLC0xMDcuNDMgMjAuNDgsMCA5MS4xOSwwIDExMS42NSwwIDU5LjM0LDAgMTA3LjQ1LDQ4LjEgMTA3LjQ1LDEwNy40MyAwLDIwLjQ4IDAsOTEuMTggMCwxMTEuNjUgMCw1OS4zNCAtNDguMTEsMTA3LjQ0IC0xMDcuNDUsMTA3LjQ0IHogbSAwLC0xMCBjIDUzLjczLDAgOTcuNDUsLTQzLjcxIDk3LjQ1LC05Ny40NCB2IC0xMTEuNjUgYyAwLC01My43MiAtNDMuNzIsLTk3LjQzIC05Ny40NSwtOTcuNDMgSCA1MTM0LjcgYyAtNTMuNzIsMCAtOTcuNDMsNDMuNzEgLTk3LjQzLDk3LjQzIHYgMTExLjY1IGMgMCw1My43MyA0My43MSw5Ny40NCA5Ny40Myw5Ny40NCBoIDExMS42NSIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg5NCI+PC9wYXRoPjxwYXRoIGQ9Ik0gMTk3MS4wMiwyMDExLjQyIFYgMTgxMy45OCIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6Mi41O3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDk2Ij48L3BhdGg+PHBhdGggZD0iTSAyNTA1LDIwMTEuNDIgViAxODEzLjk4IiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoyLjU7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoOTgiPjwvcGF0aD48cGF0aCBkPSJNIDMxNTAuMTcsMjAxMS40MiBWIDE4MTMuOTgiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjIuNTtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgxMDAiPjwvcGF0aD48cGF0aCBkPSJNIDM1ODEuNzgsMjAxMS40MiBWIDE4MTMuOTgiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjIuNTtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgxMDIiPjwvcGF0aD48cGF0aCBkPSJNIDQxMzcuNDYsMjAxMS40MiBWIDE4MTMuOTgiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjIuNTtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgxMDQiPjwvcGF0aD48cGF0aCBkPSJNIDQ0OTUuNiwyMDExLjQyIFYgMTgxMy45OCIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6Mi41O3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDEwNiI+PC9wYXRoPjxwYXRoIGQ9Ik0gNTE5MC42NiwyMDExLjQyIFYgMTgxMy45OCIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6Mi41O3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDEwOCI+PC9wYXRoPjxwYXRoIGQ9Ik0gMjU4LjE1MiwyMjMyLjI1IEggODIzMC4wMSIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6MTA7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoMTEwIj48L3BhdGg+PHBhdGggZD0iTSA3MjMxLjQyLDYxMS4xNDggViAxNTY5LjUyIiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoxMDtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgxMTIiPjwvcGF0aD48cGF0aCBkPSJtIDE5MzUuODUsMjIzMi4yNSBjIDAsMTguMTkgMTQuNzMsMzIuOTIgMzIuOTIsMzIuOTIgMTguMTcsMCAzMi45MSwtMTQuNzMgMzIuOTEsLTMyLjkyIDAsLTE4LjE3IC0xNC43NCwtMzIuOTEgLTMyLjkxLC0zMi45MSAtMTguMTksMCAtMzIuOTIsMTQuNzQgLTMyLjkyLDMyLjkxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDExNCI+PC9wYXRoPjxwYXRoIGQ9Im0gMjQ3NC4zMywyMjMyLjI1IGMgMCwxOC4xOSAxNC43NCwzMi45MiAzMi45MiwzMi45MiAxOC4xOSwwIDMyLjkyLC0xNC43MyAzMi45MiwtMzIuOTIgMCwtMTguMTcgLTE0LjczLC0zMi45MSAtMzIuOTIsLTMyLjkxIC0xOC4xOCwwIC0zMi45MiwxNC43NCAtMzIuOTIsMzIuOTEiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMTE2Ij48L3BhdGg+PHBhdGggZD0ibSAyNjM1LjM0LDIyMzIuMjUgYyAwLDE4LjE5IDE0Ljc0LDMyLjkyIDMyLjkyLDMyLjkyIDE4LjE4LDAgMzIuOTIsLTE0LjczIDMyLjkyLC0zMi45MiAwLC0xOC4xNyAtMTQuNzQsLTMyLjkxIC0zMi45MiwtMzIuOTEgLTE4LjE4LDAgLTMyLjkyLDE0Ljc0IC0zMi45MiwzMi45MSIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgxMTgiPjwvcGF0aD48cGF0aCBkPSJtIDI3NzUuMjIsMjIzMi4yNSBjIDAsMTguMTkgMTQuNzQsMzIuOTIgMzIuOTIsMzIuOTIgMTguMTcsMCAzMi45MiwtMTQuNzMgMzIuOTIsLTMyLjkyIDAsLTE4LjE3IC0xNC43NSwtMzIuOTEgLTMyLjkyLC0zMi45MSAtMTguMTgsMCAtMzIuOTIsMTQuNzQgLTMyLjkyLDMyLjkxIiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDEyMCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzAyMS42NSwyMjMyLjI1IGMgMCwxOC4xOSAxNC43NCwzMi45MiAzMi45MiwzMi45MiAxOC4xOCwwIDMyLjkyLC0xNC43MyAzMi45MiwtMzIuOTIgMCwtMTguMTcgLTE0Ljc0LC0zMi45MSAtMzIuOTIsLTMyLjkxIC0xOC4xOCwwIC0zMi45MiwxNC43NCAtMzIuOTIsMzIuOTEiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMTIyIj48L3BhdGg+PHBhdGggZD0ibSAzMTE5LjUsMjIzMi4yNSBjIDAsMTguMTkgMTQuNzQsMzIuOTIgMzIuOTIsMzIuOTIgMTguMTgsMCAzMi45MiwtMTQuNzMgMzIuOTIsLTMyLjkyIDAsLTE4LjE3IC0xNC43NCwtMzIuOTEgLTMyLjkyLC0zMi45MSAtMTguMTgsMCAtMzIuOTIsMTQuNzQgLTMyLjkyLDMyLjkxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDEyNCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzI2MS45NSwyMjMyLjI1IGMgMCwxOC4xOSAxNC43NCwzMi45MiAzMi45MiwzMi45MiAxOC4xOCwwIDMyLjkyLC0xNC43MyAzMi45MiwtMzIuOTIgMCwtMTguMTcgLTE0Ljc0LC0zMi45MSAtMzIuOTIsLTMyLjkxIC0xOC4xOCwwIC0zMi45MiwxNC43NCAtMzIuOTIsMzIuOTEiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMTI2Ij48L3BhdGg+PHBhdGggZD0ibSAzNTUxLjExLDIyMzIuMjUgYyAwLDE4LjE5IDE0Ljc0LDMyLjkyIDMyLjkyLDMyLjkyIDE4LjE4LDAgMzIuOTIsLTE0LjczIDMyLjkyLC0zMi45MiAwLC0xOC4xNyAtMTQuNzQsLTMyLjkxIC0zMi45MiwtMzIuOTEgLTE4LjE4LDAgLTMyLjkyLDE0Ljc0IC0zMi45MiwzMi45MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgxMjgiPjwvcGF0aD48cGF0aCBkPSJtIDM2NjIuMDEsMjIzMi4yNSBjIDAsMTguMTkgMTQuNzMsMzIuOTIgMzIuOTIsMzIuOTIgMTguMTgsMCAzMi45MSwtMTQuNzMgMzIuOTEsLTMyLjkyIDAsLTE4LjE3IC0xNC43MywtMzIuOTEgLTMyLjkxLC0zMi45MSAtMTguMTksMCAtMzIuOTIsMTQuNzQgLTMyLjkyLDMyLjkxIiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDEzMCI+PC9wYXRoPjxwYXRoIGQ9Im0gNDEwNi43OSwyMjMyLjI1IGMgMCwxOC4xOSAxNC43NCwzMi45MiAzMi45MiwzMi45MiAxOC4xOCwwIDMyLjkxLC0xNC43MyAzMi45MSwtMzIuOTIgMCwtMTguMTcgLTE0LjczLC0zMi45MSAtMzIuOTEsLTMyLjkxIC0xOC4xOCwwIC0zMi45MiwxNC43NCAtMzIuOTIsMzIuOTEiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMTMyIj48L3BhdGg+PHBhdGggZD0ibSA0NDY0Ljk0LDIyMzIuMjUgYyAwLDE4LjE5IDE0LjczLDMyLjkyIDMyLjkxLDMyLjkyIDE4LjE4LDAgMzIuOTIsLTE0LjczIDMyLjkyLC0zMi45MiAwLC0xOC4xNyAtMTQuNzQsLTMyLjkxIC0zMi45MiwtMzIuOTEgLTE4LjE4LDAgLTMyLjkxLDE0Ljc0IC0zMi45MSwzMi45MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgxMzQiPjwvcGF0aD48cGF0aCBkPSJtIDQ2MjUuODIsMjIzMi4yNSBjIDAsMTguMTkgMTQuNzMsMzIuOTIgMzIuOTIsMzIuOTIgMTguMTgsMCAzMi45MiwtMTQuNzMgMzIuOTIsLTMyLjkyIDAsLTE4LjE3IC0xNC43NCwtMzIuOTEgLTMyLjkyLC0zMi45MSAtMTguMTksMCAtMzIuOTIsMTQuNzQgLTMyLjkyLDMyLjkxIiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDEzNiI+PC9wYXRoPjxwYXRoIGQ9Im0gNDg5NC45MiwyMjMyLjI1IGMgMCwxOC4xOSAxNC43NCwzMi45MiAzMi45MiwzMi45MiAxOC4xOCwwIDMyLjkyLC0xNC43MyAzMi45MiwtMzIuOTIgMCwtMTguMTcgLTE0Ljc0LC0zMi45MSAtMzIuOTIsLTMyLjkxIC0xOC4xOCwwIC0zMi45MiwxNC43NCAtMzIuOTIsMzIuOTEiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMTM4Ij48L3BhdGg+PHBhdGggZD0ibSA1MDA2LjY4LDIyMzIuMjUgYyAwLDE4LjE5IDE0LjczLDMyLjkyIDMyLjkyLDMyLjkyIDE4LjE3LDAgMzIuOTEsLTE0LjczIDMyLjkxLC0zMi45MiAwLC0xOC4xNyAtMTQuNzQsLTMyLjkxIC0zMi45MSwtMzIuOTEgLTE4LjE5LDAgLTMyLjkyLDE0Ljc0IC0zMi45MiwzMi45MSIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgxNDAiPjwvcGF0aD48cGF0aCBkPSJtIDUxNTkuOTksMjIzMi4yNSBjIDAsMTguMTkgMTQuNzQsMzIuOTIgMzIuOTIsMzIuOTIgMTguMTgsMCAzMi45MiwtMTQuNzMgMzIuOTIsLTMyLjkyIDAsLTE4LjE3IC0xNC43NCwtMzIuOTEgLTMyLjkyLC0zMi45MSAtMTguMTgsMCAtMzIuOTIsMTQuNzQgLTMyLjkyLDMyLjkxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDE0MiI+PC9wYXRoPjxwYXRoIGQ9Im0gNzE5OC41LDE1NjkuNTIgYyAwLDE4LjE4IDE0Ljc0LDMyLjkyIDMyLjkyLDMyLjkyIDE4LjE4LDAgMzIuOTEsLTE0Ljc0IDMyLjkxLC0zMi45MiAwLC0xOC4xNyAtMTQuNzMsLTMyLjkyIC0zMi45MSwtMzIuOTIgLTE4LjE4LDAgLTMyLjkyLDE0Ljc1IC0zMi45MiwzMi45MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgxNDQiPjwvcGF0aD48cGF0aCBkPSJtIDUzODMuMzEsMjIzMi4yNSBjIDAsMTguMTkgMTQuNzQsMzIuOTIgMzIuOTIsMzIuOTIgMTguMTgsMCAzMi45MiwtMTQuNzMgMzIuOTIsLTMyLjkyIDAsLTE4LjE3IC0xNC43NCwtMzIuOTEgLTMyLjkyLC0zMi45MSAtMTguMTgsMCAtMzIuOTIsMTQuNzQgLTMyLjkyLDMyLjkxIiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDE0NiI+PC9wYXRoPjxwYXRoIGQ9Im0gNTcwNi4yNiwyMjMyLjI1IGMgMCwxOC4xOSAxNC43NCwzMi45MiAzMi45MiwzMi45MiAxOC4xOCwwIDMyLjkyLC0xNC43MyAzMi45MiwtMzIuOTIgMCwtMTguMTcgLTE0Ljc0LC0zMi45MSAtMzIuOTIsLTMyLjkxIC0xOC4xOCwwIC0zMi45MiwxNC43NCAtMzIuOTIsMzIuOTEiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMTQ4Ij48L3BhdGg+PHBhdGggZD0ibSA1OTA2LjA4LDIyMzIuMjUgYyAwLDE4LjE5IDE0Ljc0LDMyLjkyIDMyLjkxLDMyLjkyIDE4LjE4LDAgMzIuOTIsLTE0LjczIDMyLjkyLC0zMi45MiAwLC0xOC4xNyAtMTQuNzQsLTMyLjkxIC0zMi45MiwtMzIuOTEgLTE4LjE3LDAgLTMyLjkxLDE0Ljc0IC0zMi45MSwzMi45MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgxNTAiPjwvcGF0aD48cGF0aCBkPSJtIDYxMDcuNjIsMjIzMi4yNSBjIDAsMTguMTkgMTQuNzUsMzIuOTIgMzIuOTIsMzIuOTIgMTguMTksMCAzMi45MiwtMTQuNzMgMzIuOTIsLTMyLjkyIDAsLTE4LjE3IC0xNC43MywtMzIuOTEgLTMyLjkyLC0zMi45MSAtMTguMTcsMCAtMzIuOTIsMTQuNzQgLTMyLjkyLDMyLjkxIiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDE1MiI+PC9wYXRoPjxwYXRoIGQ9Im0gNzQ1OS4zMSwyMjMyLjI1IGMgMCwxOC4xOSAxNC43NCwzMi45MiAzMi45MiwzMi45MiAxOC4xOSwwIDMyLjkyLC0xNC43MyAzMi45MiwtMzIuOTIgMCwtMTguMTcgLTE0LjczLC0zMi45MSAtMzIuOTIsLTMyLjkxIC0xOC4xOCwwIC0zMi45MiwxNC43NCAtMzIuOTIsMzIuOTEiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMTU0Ij48L3BhdGg+PHBhdGggZD0ibSA2MjkyLDIyMzIuMjUgYyAwLDE4LjE5IDE0LjczLDMyLjkyIDMyLjkyLDMyLjkyIDE4LjE3LDAgMzIuOTEsLTE0LjczIDMyLjkxLC0zMi45MiAwLC0xOC4xNyAtMTQuNzQsLTMyLjkxIC0zMi45MSwtMzIuOTEgLTE4LjE5LDAgLTMyLjkyLDE0Ljc0IC0zMi45MiwzMi45MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgxNTYiPjwvcGF0aD48cGF0aCBkPSJtIDY0NTMuMjgsMjIzMi4yNSBjIDAsMTguMTkgMTQuNzMsMzIuOTIgMzIuOTIsMzIuOTIgMTguMTcsMCAzMi45MiwtMTQuNzMgMzIuOTIsLTMyLjkyIDAsLTE4LjE3IC0xNC43NSwtMzIuOTEgLTMyLjkyLC0zMi45MSAtMTguMTksMCAtMzIuOTIsMTQuNzQgLTMyLjkyLDMyLjkxIiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDE1OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNjc2My40LDIyMzIuMjUgYyAwLDE4LjE5IDE0Ljc0LDMyLjkyIDMyLjkyLDMyLjkyIDE4LjE5LDAgMzIuOTIsLTE0LjczIDMyLjkyLC0zMi45MiAwLC0xOC4xNyAtMTQuNzMsLTMyLjkxIC0zMi45MiwtMzIuOTEgLTE4LjE4LDAgLTMyLjkyLDE0Ljc0IC0zMi45MiwzMi45MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgxNjAiPjwvcGF0aD48cGF0aCBkPSJNIDE5NzAuNjIsNTA3LjY5OSBWIDQ0MS4yODEiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjIuNTtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgxNjIiPjwvcGF0aD48cGF0aCBkPSJNIDIzODIuOCw1MDcuNjk5IFYgNDQxLjI4MSIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6Mi41O3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDE2NCI+PC9wYXRoPjxwYXRoIGQ9Ik0gMTk3MC42Miw0NzQuNDg4IEggMjM4Mi44IiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoyLjU7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoMTY2Ij48L3BhdGg+PHBhdGggZD0ibSAyMTUwLjY1LDM3MS44MDEgdiA5LjU1OCBoIDUyLjU3IHYgLTkuNTU4IGggLTIwLjU2IHYgLTU1LjgzMiBoIC0xMS40NSB2IDU1LjgzMiBoIC0yMC41NiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgxNjgiPjwvcGF0aD48cGF0aCBkPSJtIDE5NjkuOTgsMjEzNS4zNyBjIC05LjM4LDAgLTE0Ljc5LC05LjExIC0xNC43OSwtMjUuNjIgMCwtMTYuNSA1LjQxLC0yNS42IDE0Ljc5LC0yNS42IDkuNDcsMCAxNC44OCw5LjEgMTQuODgsMjUuNiAwLDE2LjUxIC01LjQxLDI1LjYyIC0xNC44OCwyNS42MiB6IG0gMCw4LjIgYyAxNy41LDAgMjYuMDYsLTEzLjggMjYuMDYsLTMzLjgyIDAsLTIwLjEgLTguNTYsLTMzLjkgLTI2LjA2LC0zMy45IC0xNy40MSwwIC0yNS45NywxMy44IC0yNS45NywzMy45IDAsMjAuMDIgOC41NiwzMy44MiAyNS45NywzMy44MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgxNzAiPjwvcGF0aD48cGF0aCBkPSJtIDI0OTguMDEsMjEyNi44IGggLTE0LjYxIHYgNy40IGMgOS40NywwLjI2IDE0LjA3LDEuMDcgMTcuNCw4LjIgaCA3Ljk0IHYgLTY1LjM4IGggLTEwLjczIHYgNDkuNzgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMTcyIj48L3BhdGg+PHBhdGggZD0ibSAyNjYyLjA4LDIwODYuMzkgaCAzNC4yNyB2IC05LjM3IGggLTQ3LjYxIHYgOC44NCBjIDIxLjgyLDE3LjA0IDM0Ljg5LDI4LjU4IDM0Ljg5LDM5LjUgMCw2LjMxIC00LjE0LDEwLjAxIC0xMC41NSwxMC4wMSAtNi4yMiwwIC0xMi4xNywtMy43IC0xMi4xNywtMTMuODkgaCAtMTAuNzMgYyAtMC4xOCwxMy4xNyA5LjAyLDIyLjA5IDIzLjM2LDIyLjA5IDEyLjA4LDAgMjEuMjgsLTYuMjIgMjEuMjgsLTE3LjMxIDAsLTEzLjUzIC0xMi45OSwtMjYuMTUgLTMyLjc0LC0zOS44NyIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgxNzQiPjwvcGF0aD48cGF0aCBkPSJtIDMxNDUuMDIsMjA4Ni4zOSBoIDM0LjI3IHYgLTkuMzcgaCAtNDcuNjEgdiA4Ljg0IGMgMjEuODIsMTcuMDQgMzQuODksMjguNTggMzQuODksMzkuNSAwLDYuMzEgLTQuMTQsMTAuMDEgLTEwLjU1LDEwLjAxIC02LjIyLDAgLTEyLjE3LC0zLjcgLTEyLjE3LC0xMy44OSBoIC0xMC43MyBjIC0wLjE4LDEzLjE3IDkuMDIsMjIuMDkgMjMuMzYsMjIuMDkgMTIuMDgsMCAyMS4yOCwtNi4yMiAyMS4yOCwtMTcuMzEgMCwtMTMuNTMgLTEyLjk5LC0yNi4xNSAtMzIuNzQsLTM5Ljg3IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDE3NiI+PC9wYXRoPjxwYXRoIGQ9Im0gMjgwOS44MSwyMTA2LjY5IGggLTMuMTUgdiA4LjkyIGggMi43IGMgMTAuMTksMCAxNS4xNSwzLjM0IDE1LjE1LDEwLjExIDAsNi41OCAtNS4zMiw5LjY1IC0xMS4zNiw5LjY1IC03Ljk0LDAgLTEyLjM2LC00Ljc5IC0xMy4zNSwtMTIuNDUgaCAtMTAuNDYgYyAwLjk5LDEyLjQ1IDkuOTIsMjAuNjUgMjQuNDQsMjAuNjUgMTAuOTEsMCAyMS43MywtNC45NiAyMS43MywtMTcuMjIgMCwtNi41IC0zLjc5LC0xMS45MSAtOS41NiwtMTQuNyA3Ljg1LC0yLjg4IDExLjI3LC05LjI5IDExLjI3LC0xNS45NiAwLC0xMy4zNSAtMTEuNDUsLTE5Ljg0IC0yNC41MiwtMTkuODQgLTE1LjE1LDAgLTIzLjM2LDkuOTIgLTI0LjE3LDIxLjQ2IGggMTAuNDYgYyAxLjA4LC03LjIxIDUuMzIsLTEzLjE2IDEzLjg5LC0xMy4xNiA3LjU3LDAgMTMuMjUsNC4xNCAxMy4yNSwxMS4yNyAwLDguMzkgLTYuNjcsMTEuMjcgLTE2LjMyLDExLjI3IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDE3OCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzA1Ni4yNSwyMTA2LjY5IGggLTMuMTYgdiA4LjkyIGggMi43MSBjIDEwLjE5LDAgMTUuMTQsMy4zNCAxNS4xNCwxMC4xMSAwLDYuNTggLTUuMzEsOS42NSAtMTEuMzYsOS42NSAtNy45MywwIC0xMi4zNSwtNC43OSAtMTMuMzQsLTEyLjQ1IGggLTEwLjQ2IGMgMC45OSwxMi40NSA5LjkxLDIwLjY1IDI0LjQ0LDIwLjY1IDEwLjksMCAyMS43MywtNC45NiAyMS43MywtMTcuMjIgMCwtNi41IC0zLjc5LC0xMS45MSAtOS41NiwtMTQuNyA3Ljg1LC0yLjg4IDExLjI3LC05LjI5IDExLjI3LC0xNS45NiAwLC0xMy4zNSAtMTEuNDUsLTE5Ljg0IC0yNC41MywtMTkuODQgLTE1LjE1LDAgLTIzLjM1LDkuOTIgLTI0LjE3LDIxLjQ2IGggMTAuNDcgYyAxLjA4LC03LjIxIDUuMzEsLTEzLjE2IDEzLjg4LC0xMy4xNiA3LjU4LDAgMTMuMjYsNC4xNCAxMy4yNiwxMS4yNyAwLDguMzkgLTYuNjgsMTEuMjcgLTE2LjMyLDExLjI3IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDE4MCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzI5OC44LDIxMDYuNjkgaCAtMy4xNiB2IDguOTIgaCAyLjcxIGMgMTAuMTksMCAxNS4xNCwzLjM0IDE1LjE0LDEwLjExIDAsNi41OCAtNS4zMSw5LjY1IC0xMS4zNiw5LjY1IC03LjkzLDAgLTEyLjM1LC00Ljc5IC0xMy4zNCwtMTIuNDUgaCAtMTAuNDYgYyAwLjk5LDEyLjQ1IDkuOTEsMjAuNjUgMjQuNDMsMjAuNjUgMTAuOTEsMCAyMS43NCwtNC45NiAyMS43NCwtMTcuMjIgMCwtNi41IC0zLjc5LC0xMS45MSAtOS41NiwtMTQuNyA3Ljg0LC0yLjg4IDExLjI3LC05LjI5IDExLjI3LC0xNS45NiAwLC0xMy4zNSAtMTEuNDUsLTE5Ljg0IC0yNC41MywtMTkuODQgLTE1LjE1LDAgLTIzLjM1LDkuOTIgLTI0LjE3LDIxLjQ2IGggMTAuNDYgYyAxLjA4LC03LjIxIDUuMzIsLTEzLjE2IDEzLjg5LC0xMy4xNiA3LjU3LDAgMTMuMjYsNC4xNCAxMy4yNiwxMS4yNyAwLDguMzkgLTYuNjgsMTEuMjcgLTE2LjMyLDExLjI3IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDE4MiI+PC9wYXRoPjxwYXRoIGQ9Im0gMzU5NS40NSwyMTAxLjY0IHYgMjYuNzkgbCAtMjAuNTYsLTI2Ljc5IHogbSAxMC43MywtOS4yOSB2IC0xNS4zMyBoIC0xMC43MyB2IDE1LjMzIGggLTMyLjI4IHYgOC45MyBsIDMyLjM3LDQxLjEyIGggMTAuNjQgdiAtNDAuNzYgaCAxMS41NCB2IC05LjI5IGggLTExLjU0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDE4NCI+PC9wYXRoPjxwYXRoIGQ9Im0gNTA0NC45NiwyMTAxLjY0IHYgMjYuNzkgbCAtMjAuNTcsLTI2Ljc5IHogbSAxMC43MywtOS4yOSB2IC0xNS4zMyBoIC0xMC43MyB2IDE1LjMzIGggLTMyLjI5IHYgOC45MyBsIDMyLjM4LDQxLjEyIGggMTAuNjQgdiAtNDAuNzYgaCAxMS41NCB2IC05LjI5IGggLTExLjU0IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDE4NiI+PC9wYXRoPjxwYXRoIGQ9Im0gNDE0Ni45NiwyMTEyLjM3IGMgLTYuMDQsMCAtMTAuNDUsLTMuMDcgLTExLjgxLC02Ljg1IGwgLTEwLjEsMC41MyA0LjMzLDM2LjM1IGggMzkuMTMgdiAtOS40NyBoIC0zMC4yOSBsIC0yLjA4LC0xNi40MSBjIDMuMTYsMi41MiA3LjY3LDQuMDUgMTMuNTMsNC4wNSAxMS4xOCwwIDIxLjU1LC03LjY2IDIxLjU1LC0yMi4zNiAwLC0xNC42MSAtMTEuMTgsLTIyLjM2IC0yNC4xNiwtMjIuMzYgLTE1LjI0LDAgLTIzLDkuOTIgLTIzLjgxLDIxLjE5IGggMTAuMzcgYyAwLjksLTcuNTggNS4wNSwtMTIuODkgMTMuNjIsLTEyLjg5IDcuMjEsMCAxMi44OSw1LjE0IDEyLjg5LDEzLjg5IDAsOS43MyAtNi42NywxNC4zMyAtMTMuMTcsMTQuMzMiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMTg4Ij48L3BhdGg+PHBhdGggZD0ibSAzNzIyLjMsMjE0Mi40IHYgLTkuNDcgYyAtMTYuNjgsLTE1Ljc4IC0yNS42MSwtMzEuOTMgLTI3LjA1LC01NS45MSBoIC0xMi4xOCBjIDEuMTcsMjMgMTIuNjMsNDIuMDIgMjcuODcsNTUuOTEgaCAtMzUuNjIgdiA5LjQ3IGggNDYuOTgiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMTkwIj48L3BhdGg+PHBhdGggZD0ibSA0OTE2LjgyLDIxMjUuNDUgYyAwLC02LjIyIDQuNzksLTEwLjM3IDExLjgyLC0xMC4zNyA3LjEzLDAgMTEuNzMsNC4xNSAxMS43MywxMC4zNyAwLDYuMjIgLTQuNiw5LjkyIC0xMS43Myw5LjkyIC03LjAzLDAgLTExLjgyLC0zLjcgLTExLjgyLC05LjkyIHogbSAxMS44MiwtNDEuMyBjIDguMDMsMCAxMy4xNiw0LjQxIDEzLjE2LDExLjgxIDAsNy4zIC01LjEzLDExLjgxIC0xMy4xNiwxMS44MSAtOC4wMywwIC0xMy4xNywtNC41MSAtMTMuMTcsLTExLjgxIDAsLTcuNCA1LjE0LC0xMS44MSAxMy4xNywtMTEuODEgeiBtIDEzLjk3LDI3Ljc3IGMgNy43NywtMy45NyAxMC4zNywtMTAuMTkgMTAuMzcsLTE2LjMzIDAsLTEyLjg5IC0xMC42MywtMTkuNzQgLTI0LjM0LC0xOS43NCAtMTMuNzEsMCAtMjQuMzUsNi44NSAtMjQuMzUsMTkuNzQgMCw2LjE0IDIuNjIsMTIuNDYgMTAuMzcsMTYuMzMgLTUuNzcsMy4yNCAtOC4zOCw5LjI5IC04LjM4LDE0Ljg4IDAsOS43NCA4LjY1LDE2Ljc3IDIyLjM2LDE2Ljc3IDEzLjYxLDAgMjIuMzYsLTcuMDMgMjIuMzYsLTE2Ljc3IDAsLTUuNTkgLTIuNDMsLTExLjM2IC04LjM5LC0xNC44OCIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgxOTIiPjwvcGF0aD48cGF0aCBkPSJtIDQ1MTQuODQsMjA5OC4wNCBjIDAsOC41NiAtNS4zMiwxMy45NyAtMTIuNzEsMTMuOTcgLTcuNCwwIC0xMi44MSwtNS40MSAtMTIuODEsLTEzLjk3IDAsLTguNjcgNS4zMiwtMTMuODkgMTIuNzIsLTEzLjg5IDcuNDgsMCAxMi44LDUuMjIgMTIuOCwxMy44OSB6IG0gLTEwLjYzLDIyLjQ1IGMgMTIuMDgsMCAyMS43MiwtOC42NyAyMS43MiwtMjIuMjggMCwtMTMuMDcgLTkuNzMsLTIyLjM2IC0yMy44LC0yMi4zNiAtMTYuOTYsMCAtMjQuNTQsMTIuOCAtMjQuNTQsMzEuOTIgMCwxOC44NSA2Ljg2LDM1LjggMjUuOTgsMzUuOCAxMy43LDAgMjAuMiwtOC44NCAyMS4xLC0xNy41OSBoIC0xMC45MSBjIC0wLjczLDYuMzIgLTUuMTQsOS4zOSAtMTEsOS4zOSAtOC44NCwwIC0xNC4wNywtOC45NCAtMTQuMjUsLTIyLjM2IDIuODgsNC4xNCA4LjIxLDcuNDggMTUuNyw3LjQ4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDE5NCI+PC9wYXRoPjxwYXRoIGQ9Im0gNDY0Ni4yMywyMTIxLjM5IGMgMCwtOC41NyA1LjMxLC0xMy45OCAxMi43MSwtMTMuOTggNy4zMSwwIDEyLjgsNS40MSAxMi44LDEzLjk4IDAsOC43NSAtNS40MSwxMy45OCAtMTIuNzEsMTMuOTggLTcuNDksMCAtMTIuOCwtNS4yMyAtMTIuOCwtMTMuOTggeiBtIDEwLjYzLC0yMi40NiBjIC0xMi4wOCwwIC0yMS43Myw4LjY2IC0yMS43MywyMi4zNyAwLDEyLjk5IDkuNzQsMjIuMjcgMjMuODEsMjIuMjcgMTYuOTUsMCAyNC41MiwtMTIuOCAyNC41MiwtMzEuOTIgMCwtMTguODUgLTYuOTQsLTM1LjggLTI2LjA1LC0zNS44IC0xMy42MiwwIC0yMC4xMiw4Ljg0IC0yMS4wMiwxNy41OSBoIDEwLjkxIGMgMC43MiwtNi4zMiA1LjE1LC05LjI5IDExLjAxLC05LjI5IDguODMsMCAxNC4wNyw4LjkyIDE0LjI0LDIyLjI2IC0yLjg4LC00LjE0IC04LjIsLTcuNDggLTE1LjY5LC03LjQ4IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDE5NiI+PC9wYXRoPjxwYXRoIGQ9Im0gNTIyMC4yNywyMTQyLjQgdiAtOS40NyBjIC0xNi42OCwtMTUuNzggLTI1LjYxLC0zMS45MyAtMjcuMDUsLTU1LjkxIGggLTEyLjE4IGMgMS4xNywyMyAxMi42Myw0Mi4wMiAyNy44Nyw1NS45MSBoIC0zNS42MiB2IDkuNDcgaCA0Ni45OCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgxOTgiPjwvcGF0aD48cGF0aCBkPSJtIDE5NzYuMDksMTc0My44OSBjIC05LjM3LDAgLTE0Ljc5LC05LjEyIC0xNC43OSwtMjUuNjIgMCwtMTYuNSA1LjQyLC0yNS42MSAxNC43OSwtMjUuNjEgOS40NywwIDE0Ljg4LDkuMTEgMTQuODgsMjUuNjEgMCwxNi41IC01LjQxLDI1LjYyIC0xNC44OCwyNS42MiB6IG0gMCw4LjIgYyAxNy41LDAgMjYuMDYsLTEzLjggMjYuMDYsLTMzLjgyIDAsLTIwLjExIC04LjU2LC0zMy45MSAtMjYuMDYsLTMzLjkxIC0xNy40LDAgLTI1Ljk3LDEzLjggLTI1Ljk3LDMzLjkxIDAsMjAuMDIgOC41NywzMy44MiAyNS45NywzMy44MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyMDAiPjwvcGF0aD48cGF0aCBkPSJtIDIwMjkuNTgsMTcwNC44MyBoIC0xOS45NCB2IDkuNjUgaCAxOS45NCB2IDE5LjQgaCA5LjkxIHYgLTE5LjQgaCAxOS44NCB2IC05LjY1IGggLTE5Ljg0IHYgLTE5LjI5IGggLTkuOTEgdiAxOS4yOSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyMDIiPjwvcGF0aD48cGF0aCBkPSJtIDIwNzcuODIsMTczNS4zMSBoIC0xNC42MSB2IDcuNCBjIDkuNDcsMC4yNyAxNC4wNywxLjA4IDE3LjQsOC4yMSBoIDcuOTQgdiAtNjUuMzggaCAtMTAuNzMgdiA0OS43NyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyMDQiPjwvcGF0aD48cGF0aCBkPSJtIDIxMDguOTMsMTY5NC45MSBoIDM0LjI3IHYgLTkuMzcgaCAtNDcuNjEgdiA4LjgzIGMgMjEuODIsMTcuMDQgMzQuODksMjguNTkgMzQuODksMzkuNTEgMCw2LjMgLTQuMTQsMTAuMDEgLTEwLjU1LDEwLjAxIC02LjIyLDAgLTEyLjE3LC0zLjcxIC0xMi4xNywtMTMuODkgaCAtMTAuNzMgYyAtMC4xOCwxMy4xNiA5LjAyLDIyLjA5IDIzLjM2LDIyLjA5IDEyLjA4LDAgMjEuMjgsLTYuMjIgMjEuMjgsLTE3LjMyIDAsLTEzLjUyIC0xMi45OSwtMjYuMTUgLTMyLjc0LC0zOS44NiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyMDYiPjwvcGF0aD48cGF0aCBkPSJtIDIxNDQuMDEsMTc0MS4zNiB2IDkuNTYgaCA1Mi41OCB2IC05LjU2IGggLTIwLjU2IHYgLTU1LjgyIGggLTExLjQ2IHYgNTUuODIgaCAtMjAuNTYiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMjA4Ij48L3BhdGg+PHBhdGggZD0ibSAyNTAzLjI5LDE3MzUuMzEgaCAtMTQuNjEgdiA3LjQgYyA5LjQ3LDAuMjcgMTQuMDcsMS4wOCAxNy40MSw4LjIxIGggNy45MyB2IC02NS4zOCBoIC0xMC43MyB2IDQ5Ljc3IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDIxMCI+PC9wYXRoPjxwYXRoIGQ9Im0gMjU0NC42OSwxNzA0LjgzIGggLTE5LjkzIHYgOS42NSBoIDE5LjkzIHYgMTkuNCBoIDkuOTIgdiAtMTkuNCBoIDE5LjgzIHYgLTkuNjUgaCAtMTkuODMgdiAtMTkuMjkgaCAtOS45MiB2IDE5LjI5IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDIxMiI+PC9wYXRoPjxwYXRoIGQ9Im0gMjU5Mi45MywxNzM1LjMxIGggLTE0LjYxIHYgNy40IGMgOS40NywwLjI3IDE0LjA3LDEuMDggMTcuNCw4LjIxIGggNy45NCB2IC02NS4zOCBoIC0xMC43MyB2IDQ5Ljc3IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDIxNCI+PC9wYXRoPjxwYXRoIGQ9Im0gMjYyNS40LDE3MzUuMzEgaCAtMTQuNjEgdiA3LjQgYyA5LjQ3LDAuMjcgMTQuMDYsMS4wOCAxNy40LDguMjEgaCA3Ljk0IHYgLTY1LjM4IGggLTEwLjczIHYgNDkuNzciIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMjE2Ij48L3BhdGg+PHBhdGggZD0ibSAyNjQxLjUzLDE3NDEuMzYgdiA5LjU2IGggNTIuNTggdiAtOS41NiBoIC0yMC41NiB2IC01NS44MiBoIC0xMS40NSB2IDU1LjgyIGggLTIwLjU3IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDIxOCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzE0OC4xMywxNjk0LjkxIGggMzQuMjYgdiAtOS4zNyBoIC00Ny42MSB2IDguODMgYyAyMS44MiwxNy4wNCAzNC45LDI4LjU5IDM0LjksMzkuNTEgMCw2LjMgLTQuMTUsMTAuMDEgLTEwLjU1LDEwLjAxIC02LjIyLDAgLTEyLjE4LC0zLjcxIC0xMi4xOCwtMTMuODkgaCAtMTAuNzMgYyAtMC4xOCwxMy4xNiA5LjAyLDIyLjA5IDIzLjM2LDIyLjA5IDEyLjA5LDAgMjEuMjgsLTYuMjIgMjEuMjgsLTE3LjMyIDAsLTEzLjUyIC0xMi45OCwtMjYuMTUgLTMyLjczLC0zOS44NiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyMjAiPjwvcGF0aD48cGF0aCBkPSJtIDMyMDguNDYsMTcwNC44MyBoIC0xOS45MyB2IDkuNjUgaCAxOS45MyB2IDE5LjQgaCA5LjkyIHYgLTE5LjQgaCAxOS44NCB2IC05LjY1IGggLTE5Ljg0IHYgLTE5LjI5IGggLTkuOTIgdiAxOS4yOSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyMjIiPjwvcGF0aD48cGF0aCBkPSJtIDMyNTYuNzEsMTczNS4zMSBoIC0xNC42MSB2IDcuNCBjIDkuNDYsMC4yNyAxNC4wNiwxLjA4IDE3LjQsOC4yMSBoIDcuOTQgdiAtNjUuMzggaCAtMTAuNzMgdiA0OS43NyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyMjQiPjwvcGF0aD48cGF0aCBkPSJtIDMzMDEuOTgsMTc0My44OSBjIC05LjM4LDAgLTE0Ljc5LC05LjEyIC0xNC43OSwtMjUuNjIgMCwtMTYuNSA1LjQxLC0yNS42MSAxNC43OSwtMjUuNjEgOS40NywwIDE0Ljg4LDkuMTEgMTQuODgsMjUuNjEgMCwxNi41IC01LjQxLDI1LjYyIC0xNC44OCwyNS42MiB6IG0gMCw4LjIgYyAxNy40OSwwIDI2LjA2LC0xMy44IDI2LjA2LC0zMy44MiAwLC0yMC4xMSAtOC41NywtMzMuOTEgLTI2LjA2LC0zMy45MSAtMTcuNDEsMCAtMjUuOTcsMTMuOCAtMjUuOTcsMzMuOTEgMCwyMC4wMiA4LjU2LDMzLjgyIDI1Ljk3LDMzLjgyIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDIyNiI+PC9wYXRoPjxwYXRoIGQ9Im0gMzMzMC4yLDE3NDEuMzYgdiA5LjU2IGggNTIuNTggdiAtOS41NiBoIC0yMC41NiB2IC01NS44MiBoIC0xMS40NiB2IDU1LjgyIGggLTIwLjU2IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDIyOCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzU5NC4wMiwxNzA5LjAzIHYgMjYuNzkgbCAtMjAuNTYsLTI2Ljc5IHogbSAxMC43MywtOS4yOSB2IC0xNS4zMyBoIC0xMC43MyB2IDE1LjMzIGggLTMyLjI4IHYgOC45MyBsIDMyLjM3LDQxLjEyIGggMTAuNjQgdiAtNDAuNzYgaCAxMS41NSB2IC05LjI5IGggLTExLjU1IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDIzMCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzY0MC44MywxNzAzLjcxIGggLTE5LjkzIHYgOS42NSBoIDE5LjkzIHYgMTkuMzkgaCA5LjkyIHYgLTE5LjM5IGggMTkuODQgdiAtOS42NSBoIC0xOS44NCB2IC0xOS4zIGggLTkuOTIgdiAxOS4zIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDIzMiI+PC9wYXRoPjxwYXRoIGQ9Im0gMzY5MS4xNSwxNzMyLjg0IGMgMCwtNi4yMiA0Ljc4LC0xMC4zNyAxMS44MSwtMTAuMzcgNy4xMiwwIDExLjcyLDQuMTUgMTEuNzIsMTAuMzcgMCw2LjIyIC00LjYsOS45MiAtMTEuNzIsOS45MiAtNy4wMywwIC0xMS44MSwtMy43IC0xMS44MSwtOS45MiB6IG0gMTEuODEsLTQxLjMgYyA4LjAzLDAgMTMuMTcsNC40MiAxMy4xNywxMS44MSAwLDcuMyAtNS4xNCwxMS44MSAtMTMuMTcsMTEuODEgLTguMDMsMCAtMTMuMTYsLTQuNTEgLTEzLjE2LC0xMS44MSAwLC03LjM5IDUuMTMsLTExLjgxIDEzLjE2LC0xMS44MSB6IG0gMTMuOTgsMjcuNzcgYyA3Ljc1LC0zLjk3IDEwLjM3LC0xMC4xOSAxMC4zNywtMTYuMzIgMCwtMTIuODkgLTEwLjY0LC0xOS43NSAtMjQuMzUsLTE5Ljc1IC0xMy43MSwwIC0yNC4zNSw2Ljg2IC0yNC4zNSwxOS43NSAwLDYuMTMgMi42MiwxMi40NSAxMC4zNywxNi4zMiAtNS43NywzLjI1IC04LjM4LDkuMjkgLTguMzgsMTQuODggMCw5Ljc0IDguNjUsMTYuNzggMjIuMzYsMTYuNzggMTMuNjIsMCAyMi4zNiwtNy4wNCAyMi4zNiwtMTYuNzggMCwtNS41OSAtMi40MywtMTEuMzYgLTguMzgsLTE0Ljg4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDIzNCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzczMC4yOSwxNzQwLjIzIHYgOS41NiBoIDUyLjU4IHYgLTkuNTYgaCAtMjAuNTYgdiAtNTUuODIgaCAtMTEuNDYgdiA1NS44MiBoIC0yMC41NiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyMzYiPjwvcGF0aD48cGF0aCBkPSJtIDQxNDIuOTksMTcxOS43OCBjIC02LjA0LDAgLTEwLjQ2LC0zLjA2IC0xMS44MSwtNi44NSBsIC0xMC4xLDAuNTQgNC4zMywzNi4zNCBoIDM5LjEzIHYgLTkuNDcgaCAtMzAuMyBsIC0yLjA3LC0xNi40MSBjIDMuMTUsMi41MiA3LjY3LDQuMDYgMTMuNTIsNC4wNiAxMS4xOCwwIDIxLjU1LC03LjY3IDIxLjU1LC0yMi4zNyAwLC0xNC42MSAtMTEuMTgsLTIyLjM2IC0yNC4xNiwtMjIuMzYgLTE1LjI0LDAgLTIzLDkuOTIgLTIzLjgxLDIxLjE5IGggMTAuMzcgYyAwLjkxLC03LjU4IDUuMDUsLTEyLjg5IDEzLjYyLC0xMi44OSA3LjIxLDAgMTIuOSw1LjE0IDEyLjksMTMuODkgMCw5LjczIC02LjY4LDE0LjMzIC0xMy4xNywxNC4zMyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyMzgiPjwvcGF0aD48cGF0aCBkPSJtIDQxOTQuNzYsMTcwMy43MyBoIC0xOS45MyB2IDkuNjUgaCAxOS45MyB2IDE5LjM5IGggOS45MSB2IC0xOS4zOSBoIDE5Ljg1IHYgLTkuNjUgaCAtMTkuODUgdiAtMTkuMyBoIC05LjkxIHYgMTkuMyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyNDAiPjwvcGF0aD48cGF0aCBkPSJtIDQyNzUuMSwxNzQ5LjgxIHYgLTkuNDcgYyAtMTYuNjgsLTE1Ljc4IC0yNS42LC0zMS45MiAtMjcuMDUsLTU1LjkxIGggLTEyLjE3IGMgMS4xNywyMyAxMi42Miw0Mi4wMiAyNy44Nyw1NS45MSBoIC0zNS42MyB2IDkuNDcgaCA0Ni45OCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyNDIiPjwvcGF0aD48cGF0aCBkPSJtIDQyNzEuOTUsMTc0MC4yNSB2IDkuNTYgaCA1Mi41OCB2IC05LjU2IGggLTIwLjU3IHYgLTU1LjgyIGggLTExLjQ0IHYgNTUuODIgaCAtMjAuNTciIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMjQ0Ij48L3BhdGg+PHBhdGggZD0ibSA0NTE0Ljg1LDE3MDYuNTUgYyAwLDguNTcgLTUuMzIsMTMuOTggLTEyLjcxLDEzLjk4IC03LjQsMCAtMTIuODEsLTUuNDEgLTEyLjgxLC0xMy45OCAwLC04LjY2IDUuMzIsLTEzLjg5IDEyLjcyLC0xMy44OSA3LjQ4LDAgMTIuOCw1LjIzIDEyLjgsMTMuODkgeiBtIC0xMC42MywyMi40NSBjIDEyLjA4LDAgMjEuNzIsLTguNjYgMjEuNzIsLTIyLjI3IDAsLTEzLjA4IC05LjczLC0yMi4zNyAtMjMuOCwtMjIuMzcgLTE2Ljk2LDAgLTI0LjU0LDEyLjgxIC0yNC41NCwzMS45MyAwLDE4Ljg1IDYuODYsMzUuOCAyNS45OCwzNS44IDEzLjcxLDAgMjAuMiwtOC44NCAyMS4xLC0xNy41OSBoIC0xMC45MSBjIC0wLjczLDYuMzIgLTUuMTQsOS4zOSAtMTEsOS4zOSAtOC44NCwwIC0xNC4wNywtOC45NCAtMTQuMjUsLTIyLjM3IDIuODgsNC4xNCA4LjIsNy40OCAxNS43LDcuNDgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMjQ2Ij48L3BhdGg+PHBhdGggZD0ibSA0NTUzLjU0LDE3MDQuODMgaCAtMTkuOTMgdiA5LjY1IGggMTkuOTMgdiAxOS40IGggOS45MiB2IC0xOS40IGggMTkuODQgdiAtOS42NSBoIC0xOS44NCB2IC0xOS4yOSBoIC05LjkyIHYgMTkuMjkiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMjQ4Ij48L3BhdGg+PHBhdGggZD0ibSA0NjI4LjAzLDE3MDYuNTUgYyAwLDguNTcgLTUuMzIsMTMuOTggLTEyLjcxLDEzLjk4IC03LjM5LDAgLTEyLjgsLTUuNDEgLTEyLjgsLTEzLjk4IDAsLTguNjYgNS4zMiwtMTMuODkgMTIuNzEsLTEzLjg5IDcuNDgsMCAxMi44LDUuMjMgMTIuOCwxMy44OSB6IE0gNDYxNy40LDE3MjkgYyAxMi4wOCwwIDIxLjczLC04LjY2IDIxLjczLC0yMi4yNyAwLC0xMy4wOCAtOS43NCwtMjIuMzcgLTIzLjgxLC0yMi4zNyAtMTYuOTUsMCAtMjQuNTMsMTIuODEgLTI0LjUzLDMxLjkzIDAsMTguODUgNi44NSwzNS44IDI1Ljk3LDM1LjggMTMuNzEsMCAyMC4yLC04Ljg0IDIxLjExLC0xNy41OSBoIC0xMC45MiBjIC0wLjcyLDYuMzIgLTUuMTQsOS4zOSAtMTEsOS4zOSAtOC44MywwIC0xNC4wNywtOC45NCAtMTQuMjQsLTIyLjM3IDIuODgsNC4xNCA4LjIsNy40OCAxNS42OSw3LjQ4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDI1MCI+PC9wYXRoPjxwYXRoIGQ9Im0gNDY0MS40NywxNzQxLjM2IHYgOS41NiBoIDUyLjU4IHYgLTkuNTYgaCAtMjAuNTcgdiAtNTUuODIgaCAtMTEuNDQgdiA1NS44MiBoIC0yMC41NyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyNTIiPjwvcGF0aD48cGF0aCBkPSJtIDUyMjAuMjcsMTc1MC45MiB2IC05LjQ4IGMgLTE2LjY4LC0xNS43OCAtMjUuNjEsLTMxLjkyIC0yNy4wNSwtNTUuOSBoIC0xMi4xOCBjIDEuMTcsMjIuOTkgMTIuNjMsNDIuMDIgMjcuODcsNTUuOSBoIC0zNS42MiB2IDkuNDggaCA0Ni45OCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyNTQiPjwvcGF0aD48cGF0aCBkPSJtIDUyNDIuMzcsMTcwNC44MyBoIC0xOS45MyB2IDkuNjUgaCAxOS45MyB2IDE5LjQgaCA5LjkyIHYgLTE5LjQgaCAxOS44NCB2IC05LjY1IGggLTE5Ljg0IHYgLTE5LjI5IGggLTkuOTIgdiAxOS4yOSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyNTYiPjwvcGF0aD48cGF0aCBkPSJtIDUzMDIuNjEsMTcyMC44OSBjIC02LjA0LDAgLTEwLjQ2LC0zLjA3IC0xMS44MSwtNi44NiBsIC0xMC4xLDAuNTQgNC4zMywzNi4zNSBoIDM5LjE0IHYgLTkuNDggaCAtMzAuMzEgbCAtMi4wNywtMTYuNCBjIDMuMTYsMi41MiA3LjY3LDQuMDUgMTMuNTMsNC4wNSAxMS4xOCwwIDIxLjU1LC03LjY3IDIxLjU1LC0yMi4zNiAwLC0xNC42MSAtMTEuMTgsLTIyLjM3IC0yNC4xNywtMjIuMzcgLTE1LjIzLDAgLTIyLjk5LDkuOTMgLTIzLjgxLDIxLjE5IGggMTAuMzcgYyAwLjkxLC03LjU3IDUuMDYsLTEyLjg5IDEzLjYzLC0xMi44OSA3LjIxLDAgMTIuODksNS4xNCAxMi44OSwxMy44OSAwLDkuNzQgLTYuNjcsMTQuMzQgLTEzLjE3LDE0LjM0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDI1OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNTMyOS4xMywxNzQxLjM2IHYgOS41NiBoIDUyLjU4IHYgLTkuNTYgaCAtMjAuNTcgdiAtNTUuODIgaCAtMTEuNDUgdiA1NS44MiBoIC0yMC41NiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyNjAiPjwvcGF0aD48cGF0aCBkPSJNIDU5MzcuMjgsMjAxMS40MiBWIDE4MTMuOTgiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjIuNTtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGgyNjIiPjwvcGF0aD48cGF0aCBkPSJtIDU5MjIuNzQsMTczMy45NiBjIDAsLTYuMjIgNC43OSwtMTAuMzcgMTEuODIsLTEwLjM3IDcuMTMsMCAxMS43Myw0LjE1IDExLjczLDEwLjM3IDAsNi4yMiAtNC42LDkuOTMgLTExLjczLDkuOTMgLTcuMDMsMCAtMTEuODIsLTMuNzEgLTExLjgyLC05LjkzIHogbSAxMS44MiwtNDEuMyBjIDguMDIsMCAxMy4xNiw0LjQyIDEzLjE2LDExLjgxIDAsNy4zMSAtNS4xNCwxMS44MiAtMTMuMTYsMTEuODIgLTguMDMsMCAtMTMuMTcsLTQuNTEgLTEzLjE3LC0xMS44MiAwLC03LjM5IDUuMTQsLTExLjgxIDEzLjE3LC0xMS44MSB6IG0gMTMuOTcsMjcuNzggYyA3Ljc3LC0zLjk4IDEwLjM3LC0xMC4yIDEwLjM3LC0xNi4zMyAwLC0xMi44OSAtMTAuNjMsLTE5Ljc1IC0yNC4zNCwtMTkuNzUgLTEzLjcxLDAgLTI0LjM1LDYuODYgLTI0LjM1LDE5Ljc1IDAsNi4xMyAyLjYyLDEyLjQ1IDEwLjM3LDE2LjMzIC01Ljc3LDMuMjQgLTguMzksOS4yOCAtOC4zOSwxNC44NyAwLDkuNzUgOC42NiwxNi43OCAyMi4zNywxNi43OCAxMy42MSwwIDIyLjM2LC03LjAzIDIyLjM2LC0xNi43OCAwLC01LjU5IC0yLjQzLC0xMS4zNiAtOC4zOSwtMTQuODciIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMjY0Ij48L3BhdGg+PHBhdGggZD0ibSA1OTg3LjE0LDE3MDQuODMgaCAtMTkuOTQgdiA5LjY1IGggMTkuOTQgdiAxOS40IGggOS45MiB2IC0xOS40IGggMTkuODMgdiAtOS42NSBoIC0xOS44MyB2IC0xOS4yOSBoIC05LjkyIHYgMTkuMjkiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMjY2Ij48L3BhdGg+PHBhdGggZD0ibSA2MDUzLjc5LDE3MTAuMTUgdiAyNi43OSBsIC0yMC41NywtMjYuNzkgeiBtIDEwLjczLC05LjI4IHYgLTE1LjMzIGggLTEwLjczIHYgMTUuMzMgaCAtMzIuMjkgdiA4LjkyIGwgMzIuMzcsNDEuMTMgaCAxMC42NSB2IC00MC43NyBoIDExLjU0IHYgLTkuMjggaCAtMTEuNTQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMjY4Ij48L3BhdGg+PHBhdGggZD0ibSA2MDc1LjM0LDE3NDEuMzYgdiA5LjU2IGggNTIuNTggdiAtOS41NiBoIC0yMC41NyB2IC01NS44MiBoIC0xMS40NSB2IDU1LjgyIGggLTIwLjU2IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDI3MCI+PC9wYXRoPjxwYXRoIGQ9Ik0gNjMyMy4yLDIwMTEuNDIgViAxODEzLjk4IiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoyLjU7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoMjcyIj48L3BhdGg+PHBhdGggZD0ibSA2MzA1LjM3LDE3MzUuMzEgaCAtMTQuNjEgdiA3LjQgYyA5LjQ3LDAuMjcgMTQuMDcsMS4wOCAxNy40LDguMjEgaCA3Ljk0IHYgLTY1LjM4IGggLTEwLjczIHYgNDkuNzciIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMjc0Ij48L3BhdGg+PHBhdGggZD0ibSA2MzUwLjYzLDE3NDMuODkgYyAtOS4zNywwIC0xNC43OSwtOS4xMiAtMTQuNzksLTI1LjYyIDAsLTE2LjUgNS40MiwtMjUuNjEgMTQuNzksLTI1LjYxIDkuNDYsMCAxNC44OCw5LjExIDE0Ljg4LDI1LjYxIDAsMTYuNSAtNS40MiwyNS42MiAtMTQuODgsMjUuNjIgeiBtIDAsOC4yIGMgMTcuNDksMCAyNi4wNywtMTMuOCAyNi4wNywtMzMuODIgMCwtMjAuMTEgLTguNTgsLTMzLjkxIC0yNi4wNywtMzMuOTEgLTE3LjQsMCAtMjUuOTgsMTMuOCAtMjUuOTgsMzMuOTEgMCwyMC4wMiA4LjU4LDMzLjgyIDI1Ljk4LDMzLjgyIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDI3NiI+PC9wYXRoPjxwYXRoIGQ9Im0gNjQwNC4xMiwxNzA0LjgzIGggLTE5LjkzIHYgOS42NSBoIDE5LjkzIHYgMTkuNCBoIDkuOTIgdiAtMTkuNCBoIDE5LjgzIHYgLTkuNjUgaCAtMTkuODMgdiAtMTkuMjkgaCAtOS45MiB2IDE5LjI5IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDI3OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNjQ1My4xNywxNjk0LjkxIGggMzQuMjcgdiAtOS4zNyBoIC00Ny42MiB2IDguODMgYyAyMS44MywxNy4wNCAzNC45LDI4LjU5IDM0LjksMzkuNTEgMCw2LjMgLTQuMTUsMTAuMDEgLTEwLjU0LDEwLjAxIC02LjIyLDAgLTEyLjE4LC0zLjcxIC0xMi4xOCwtMTMuODkgaCAtMTAuNzMgYyAtMC4xOCwxMy4xNiA5LjAyLDIyLjA5IDIzLjM2LDIyLjA5IDEyLjA4LDAgMjEuMjcsLTYuMjIgMjEuMjcsLTE3LjMyIDAsLTEzLjUyIC0xMi45OCwtMjYuMTUgLTMyLjczLC0zOS44NiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyODAiPjwvcGF0aD48cGF0aCBkPSJtIDY0ODguMjUsMTc0MS4zNiB2IDkuNTYgaCA1Mi41OCB2IC05LjU2IGggLTIwLjU3IHYgLTU1LjgyIGggLTExLjQ1IHYgNTUuODIgaCAtMjAuNTYiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMjgyIj48L3BhdGg+PHBhdGggZD0ibSA3MDk2LjY3LDE3MzQuNyB2IC01Mi45NCBoIC0xMS4xOSB2IDY1LjM4IGggMTcuNzcgbCAxNS44OCwtNTIuMTMgMTUuNzgsNTIuMTMgaCAxNy43NiB2IC02NS4zOCBoIC0xMS4xOCB2IDUyLjk0IGwgLTE2LjU5LC01Mi45NCBoIC0xMS42NCBsIC0xNi41OSw1Mi45NCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyODQiPjwvcGF0aD48cGF0aCBkPSJtIDcxOTYuNCwxNzEwLjc5IGMgLTAuMjYsNy41OCAtNi4wMywxMi4xOCAtMTIuMzUsMTIuMTggLTUuMDUsMCAtMTEuOTksLTIuOTggLTEyLjg5LC0xMi4xOCB6IG0gLTEyLjA4LC0yMS4yOCBjIDUuNTksMCAxMC4wMSwyLjI2IDExLjkxLDYuNzcgaCAxMC41NCBjIC0yLjI1LC03Ljc2IC05LjQ2LC0xNS43IC0yMiwtMTUuNyAtMTUuNiwwIC0yNC41MywxMS45MSAtMjQuNTMsMjUuOCAwLDE0LjYgMTAuMDEsMjQuOTggMjMuODEsMjQuOTggMTQuODgsMCAyNC4xNywtMTIuMDggMjMuMjcsLTI4LjQxIGggLTM2LjE2IGMgMC43MiwtOS4wMiA3LjAzLC0xMy40NCAxMy4xNiwtMTMuNDQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMjg2Ij48L3BhdGg+PHBhdGggZD0ibSA3MjIyLjc0LDE3MDYuMDEgYyAwLC0xMC4yOCA1LjE0LC0xNi42OCAxMi4yNywtMTYuNjggNy4wMywwIDEyLjU0LDUuNSAxMi41NCwxNi42OCAwLDExLjE5IC01LjUxLDE2LjYgLTEyLjU0LDE2LjYgLTcuMTMsMCAtMTIuMjcsLTYuNCAtMTIuMjcsLTE2LjYgeiBtIDM1LjA4LDQxLjEzIHYgLTY1LjM4IGggLTEwLjczIHYgNi40IGMgLTIuODgsLTQuNzggLTcuOTMsLTcuNTggLTE0LjQzLC03LjU4IC0xMS40NSwwIC0yMS4xLDkuODMgLTIxLjEsMjUuNDMgMCwxNS41MSA5LjY1LDI1LjM1IDIxLjEsMjUuMzUgNi41LDAgMTEuNTUsLTIuOCAxNC40MywtNy41OCB2IDIzLjM2IGggMTAuNzMiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMjg4Ij48L3BhdGg+PHBhdGggZD0ibSA3Mjc4LjgzLDE2ODEuNzYgaCAtMTAuNzMgdiA0OC41MSBoIDEwLjczIHogbSAwLDU0LjU2IGggLTEwLjczIHYgMTAuODIgaCAxMC43MyB2IC0xMC44MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyOTAiPjwvcGF0aD48cGF0aCBkPSJtIDcyOTcuNTgsMTY5NS4zNyBjIDAsLTQuMjQgMy41MiwtNi43NiA4LjkzLC02Ljc2IDcuOTQsMCAxMi42Myw0LjA1IDEyLjYzLDEyLjI3IHYgMy42OSBjIC0xNS4zNCwtMS40NCAtMjEuNTYsLTMuNiAtMjEuNTYsLTkuMiB6IG0gMjEuMjgsMTYuNjkgdiAwLjkgYyAwLDguMyAtNC43NywxMC44MiAtMTAuMDksMTAuODIgLTUuNDEsMCAtOS40OCwtMi44OCAtOS43NSwtOC43NSBoIC0xMC41NSBjIDAuNzMsOS45MiA4LjkzLDE2LjY5IDIwLjY2LDE2LjY5IDExLjYzLDAgMjAuNzQsLTUuMzMgMjAuNDcsLTIwLjgzIDAsLTIuNDQgLTAuMTksLTguMTIgLTAuMTksLTEyLjU0IDAsLTYuMTMgMC41NSwtMTIuNTMgMS40NSwtMTYuNTkgaCAtOS44MyBjIC0wLjM2LDIuMDcgLTAuNzIsMy4yNCAtMC45MSw2LjU4IC0zLjA2LC01LjIzIC04LjgzLC03Ljc2IC0xNS45NSwtNy43NiAtMTAuNTYsMCAtMTcuOTUsNS42OSAtMTcuOTUsMTQuNTMgMCwxMi4wOCAxNC44OCwxNS4xNCAzMi42NCwxNi45NSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgyOTIiPjwvcGF0aD48cGF0aCBkPSJtIDczNjQuMDYsMTczMS4zNiBjIDExLjcyLDAgMTYuNSwtNy41OCAxNi41LC0xOS4xMyB2IC0zMC40NyBoIC0xMC43MyB2IDI3Ljg2IGMgMCw2LjU5IC0xLDEyLjk5IC05LjIsMTIuOTkgLTguMiwwIC0xMS4yNywtNi4zMSAtMTEuMjcsLTE1LjA2IHYgLTI1Ljc5IGggLTEwLjczIHYgNDguNTEgaCAxMC43MyB2IC02Ljc2IGMgMi43OSw1LjA1IDcuOTMsNy44NSAxNC43LDcuODUiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMjk0Ij48L3BhdGg+PHBhdGggZD0ibSA3MDA3Ljc3LDM2OC41MTIgYyAtMTkuMTIsMCAtMzAuMjIsMTMuNjE3IC0zMC4yMiwzNC4wOTcgMCwyMC41NTEgMTEuODIsMzMuNjI5IDMwLjc2LDMzLjYyOSAxNC41MiwwIDI0Ljg5LC04LjI5NyAyNy41MSwtMjIuOTEgaCAtMTEuMDEgYyAtMS45OCw4Ljg0IC04LjM5LDEzLjUzMSAtMTYuODYsMTMuNTMxIC0xMC4zOCwwIC0xOC41OCwtOC40NjggLTE4LjU4LC0yNC4yNSAwLC0xNS44NzkgOC4wMywtMjQuNzE4IDE4LjQ5LC0yNC43MTggOC44NCwwIDE1LjE0LDQuNTk3IDE3LjE0LDEzLjUxOSBoIDEwLjk5IGMgLTIuNywtMTQuNjAxIC0xMy4xNiwtMjIuODk4IC0yOC4yMiwtMjIuODk4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDI5NiI+PC9wYXRoPjxwYXRoIGQ9Im0gNzA0My4zMSwzNjkuNjkxIHYgNjUuMzc5IGggMTAuNzMgdiAtNjUuMzc5IGggLTEwLjczIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDI5OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNzA5Ny43OCwzOTMuODU5IGMgMCwxMS4xOCAtNi4wNSwxNi42OCAtMTIuODEsMTYuNjggLTYuNzYsMCAtMTIuODEsLTUuNSAtMTIuODEsLTE2LjY4IDAsLTExLjE4NyA2LjA1LC0xNi41OTcgMTIuODEsLTE2LjU5NyA2Ljc2LDAgMTIuODEsNS40MSAxMi44MSwxNi41OTcgeiBtIC0xMi44MSwtMjUuMzQ3IGMgLTExLjgxLDAgLTIzLjksNy44NDcgLTIzLjksMjUuMzQ3IDAsMTcuNDkzIDEyLjA5LDI1LjQzIDIzLjksMjUuNDMgMTEuODEsMCAyMy44OSwtNy45MzcgMjMuODksLTI1LjQzIDAsLTE3LjUgLTEyLjA4LC0yNS4zNDcgLTIzLjg5LC0yNS4zNDciIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzAwIj48L3BhdGg+PHBhdGggZD0ibSA3MTQ4LjE4LDQwMS42MDkgYyAtMC45LDUuMTQxIC01LjQxLDguNzUgLTExLjI3LDguNzUgLTYuNjcsMCAtMTIuNzEsLTQuOTYxIC0xMi43MSwtMTYuNDE4IDAsLTExLjU0MyA2LjEzLC0xNi41IDEyLjQ0LC0xNi41IDUuMjMsMCAxMC41NSwyLjM0IDExLjksOC44NCBIIDcxNTkgYyAtMi4xNiwtMTEuMzYzIC0xMi4xNywtMTcuNzY5IC0yMi41NCwtMTcuNzY5IC0xNC4wNywwIC0yMy4zNiwxMC45MDYgLTIzLjM2LDI1LjM0NyAwLDE0LjQyMiA5LjM4LDI1LjQzIDIzLjgxLDI1LjQzIDEwLjU1LDAgMTkuOTMsLTYuODU5IDIxLjczLC0xNy42OCBoIC0xMC40NiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzMDIiPjwvcGF0aD48cGF0aCBkPSJtIDcxNzYuMjMsMzk4LjcxOSAxNy45NCwxOS40OCBoIDEyLjkgbCAtMTguNTksLTE5LjkyOSAyMC42NiwtMjguNTc5IGggLTEyLjUzIGwgLTE1LjI1LDIxLjAwOCAtNS4xMywtNS41MDggdiAtMTUuNSBoIC0xMC43NCB2IDY1LjM3OSBoIDEwLjc0IHYgLTM2LjM1MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzMDQiPjwvcGF0aD48cGF0aCBkPSJtIDcyODMuNjQsMzkzLjc3IC05LjkyLDI4LjAzMSAtOS44NCwtMjguMDMxIHogbSAtMy40Myw0MS4zIDI0LjUyLC02NS4zNzkgaCAtMTIuNTMgbCAtNS4xNCwxNC41MiBoIC0yNi41MSBsIC01LjA2LC0xNC41MiBoIC0xMS43MSBsIDI0LjM0LDY1LjM3OSBoIDEyLjA5IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDMwNiI+PC9wYXRoPjxwYXRoIGQ9Im0gNzMxNi4zNywzOTMuOTQxIGMgMCwtMTAuMjgxIDUuMTQsLTE2LjY3OSAxMi4yNywtMTYuNjc5IDcuMDMsMCAxMi41NCw1LjQ5NiAxMi41NCwxNi42NzkgMCwxMS4xODggLTUuNTEsMTYuNTk4IC0xMi41NCwxNi41OTggLTcuMTMsMCAtMTIuMjcsLTYuMzk4IC0xMi4yNywtMTYuNTk4IHogbSAzNS4wOCw0MS4xMjkgdiAtNjUuMzc5IGggLTEwLjczIHYgNi4zOTkgYyAtMi44OCwtNC43ODEgLTcuOTMsLTcuNTc4IC0xNC40MiwtNy41NzggLTExLjQ2LDAgLTIxLjExLDkuODI4IC0yMS4xMSwyNS40MjkgMCwxNS41MDggOS42NSwyNS4zNDggMjEuMTEsMjUuMzQ4IDYuNDksMCAxMS41NCwtMi44MDEgMTQuNDIsLTcuNTc4IHYgMjMuMzU5IGggMTAuNzMiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzA4Ij48L3BhdGg+PHBhdGggZD0ibSA3MzcyLjQ4LDQyNC4yNSBoIC0xMC43NCB2IDEwLjgyIGggMTAuNzQgeiBtIDAsLTYuMDUxIHYgLTQ5LjIzOCBjIDAsLTEyLjE3MiAtMy4wNywtMTUuMDYzIC0xNC4wOCwtMTUuMDYzIGggLTMuNiB2IDguMzEzIGggMS45OCBjIDQuNDIsMCA0Ljk2LDEuMTY4IDQuOTYsNi4zMDEgdiA0OS42ODcgaCAxMC43NCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzMTAiPjwvcGF0aD48cGF0aCBkPSJtIDczOTguMzUsMzY4LjUxMiBjIC0xMS41NSwwIC0xNi4yMyw3LjU3OCAtMTYuMjMsMTkuMTI5IHYgMzAuNTU4IGggMTAuNzMgdiAtMjcuOTYxIGMgMCwtNi41NzggMC45LC0xMi45NzYgOC45MiwtMTIuOTc2IDguMDMsMCAxMC45Miw2LjMwOCAxMC45MiwxNS4wNTggdiAyNS44NzkgaCAxMC43MiB2IC00OC41MDggaCAtMTAuNzIgdiA2LjY2OCBjIC0yLjgsLTUuMDUgLTcuNzYsLTcuODQ3IC0xNC4zNCwtNy44NDciIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzEyIj48L3BhdGg+PHBhdGggZD0ibSA3NDUwLjc0LDQxMS4wNzggYyAtNC42OSwwIC05LjAyLC0yLjA3OCAtOS4wMiwtNS4zMTYgMCwtMy4yNSAyLjM1LC00Ljk2MSA2LjQ5LC01Ljc3NCBsIDYuODUsLTEuMzU5IGMgOS44NCwtMS44OTEgMTcuMzIsLTQuOTYxIDE3LjMyLC0xNC40MTggMCwtMTAuMTA5IC05LjU2LC0xNS42OTkgLTIwLjU2LC0xNS42OTkgLTExLjksMCAtMTkuODQsNi43NjkgLTIxLjAxLDE1Ljk1NyBoIDEwLjQ2IGMgMC45OSwtNC45NDkgNC42LC03Ljg0IDEwLjkxLC03Ljg0IDUuNTksMCA5Ljc0LDIuMzQgOS43NCw2LjMxMiAwLDMuOTY5IC0zLjYsNS43NyAtOC4zOSw2LjY4IGwgLTcuMywxLjQzOCBjIC04LjIxLDEuNjIxIC0xNC42MSw1LjMyIC0xNC42MSwxNC4xNTIgMCw4LjU3OCA5LjIsMTQuMDc4IDE5Ljc1LDE0LjA3OCA5LjQ3LDAgMTguMTMsLTQuNTk4IDIwLjExLC0xNC4zNCBoIC0xMC4xIGMgLTEuMTcsNC40MSAtNS4yMyw2LjEyOSAtMTAuNjQsNi4xMjkiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzE0Ij48L3BhdGg+PHBhdGggZD0ibSA3NDkyLjIzLDQzMSB2IC0xMi44MDEgaCA5Ljc0IHYgLTcuNzUgaCAtOS43NCBWIDM4NC4wMiBjIDAsLTQuOTYxIDEuMTcsLTYuMTI5IDUuNzcsLTYuMTI5IGggMy44OCB2IC04LjIgaCAtNy45NCBjIC0xMC4zNywwIC0xMi40NCwyLjc4OSAtMTIuNDQsMTIuNzA3IHYgMjguMDUxIGggLTcuMjIgdiA3Ljc1IGggNy4yMiBWIDQzMSBoIDEwLjczIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDMxNiI+PC9wYXRoPjxwYXRoIGQ9Im0gNzUwOC44MiwzNjkuNjkxIHYgNDguNTA4IGggMTAuNzQgdiAtNi43NTggYyAyLjc5LDUuMDQ3IDcuNTcsNy44NDggMTQuMDYsNy44NDggNy40OSwwIDExLjksLTMuMTYgMTQuMTYsLTguNTcgNC4xNSw2LjEzMyA5LjgyLDguNTcgMTUuNzgsOC41NyAxMS40NiwwIDE1Ljg3LC03LjU3OCAxNS44NywtMTkuMTI5IHYgLTMwLjQ2OSBoIC0xMC43MyB2IDI3Ljg2IGMgMCw2LjU5IC0wLjYzLDEyLjk4OCAtOC41NywxMi45ODggLTcuOTQsMCAtMTAuNjQsLTYuMzA5IC0xMC42NCwtMTUuMDU5IHYgLTI1Ljc4OSBoIC0xMC43MiB2IDI3Ljg2IGMgMCw2LjU5IC0wLjY0LDEyLjk4OCAtOC41OCwxMi45ODggLTcuOTMsMCAtMTAuNjMsLTYuMzA5IC0xMC42MywtMTUuMDU5IHYgLTI1Ljc4OSBoIC0xMC43NCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzMTgiPjwvcGF0aD48cGF0aCBkPSJtIDc2MjEuNzIsMzk4LjcxOSBjIC0wLjI2LDcuNTgyIC02LjAzLDEyLjE3OSAtMTIuMzUsMTIuMTc5IC01LjA1LDAgLTExLjk5LC0yLjk3NiAtMTIuODksLTEyLjE3OSB6IG0gLTEyLjA4LC0yMS4yNzggYyA1LjU5LDAgMTAuMDEsMi4yNTggMTEuOTEsNi43NyBoIDEwLjU1IGMgLTIuMjYsLTcuNzYyIC05LjQ3LC0xNS42OTkgLTIyLjAxLC0xNS42OTkgLTE1LjYsMCAtMjQuNTMsMTEuOTEgLTI0LjUzLDI1Ljc4OSAwLDE0LjYwOSAxMC4wMSwyNC45ODggMjMuODEsMjQuOTg4IDE0Ljg4LDAgMjQuMTcsLTEyLjA3OCAyMy4yNywtMjguNDEgaCAtMzYuMTYgYyAwLjcxLC05LjAyIDcuMDMsLTEzLjQzOCAxMy4xNiwtMTMuNDM4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDMyMCI+PC9wYXRoPjxwYXRoIGQ9Im0gNzY2NS4xMSw0MTkuMjg5IGMgMTEuNzIsMCAxNi41MSwtNy41NzggMTYuNTEsLTE5LjEyOSB2IC0zMC40NjkgaCAtMTAuNzMgdiAyNy44NiBjIDAsNi41OSAtMSwxMi45ODggLTkuMiwxMi45ODggLTguMjEsMCAtMTEuMjcsLTYuMzA5IC0xMS4yNywtMTUuMDU5IHYgLTI1Ljc4OSBoIC0xMC43NCB2IDQ4LjUwOCBoIDEwLjc0IHYgLTYuNzU4IGMgMi43OSw1LjA0NyA3LjkzLDcuODQ4IDE0LjY5LDcuODQ4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDMyMiI+PC9wYXRoPjxwYXRoIGQ9Im0gNzcwMy4yNiw0MzEgdiAtMTIuODAxIGggOS43MyB2IC03Ljc1IGggLTkuNzMgViAzODQuMDIgYyAwLC00Ljk2MSAxLjE3LC02LjEyOSA1Ljc3LC02LjEyOSBoIDMuODggdiAtOC4yIGggLTcuOTQgYyAtMTAuMzcsMCAtMTIuNDQsMi43ODkgLTEyLjQ0LDEyLjcwNyB2IDI4LjA1MSBoIC03LjIyIHYgNy43NSBoIDcuMjIgViA0MzEgaCAxMC43MyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzMjQiPjwvcGF0aD48cGF0aCBkPSJtIDU0MzAuMTUsMjA5OC4wNCBjIDAsOC41NiAtNS4zMiwxMy45NyAtMTIuNzEsMTMuOTcgLTcuMzksMCAtMTIuOCwtNS40MSAtMTIuOCwtMTMuOTcgMCwtOC42NyA1LjMyLC0xMy44OSAxMi43MSwtMTMuODkgNy40OCwwIDEyLjgsNS4yMiAxMi44LDEzLjg5IHogbSAtMTAuNjMsMjIuNDUgYyAxMi4wOCwwIDIxLjczLC04LjY3IDIxLjczLC0yMi4yOCAwLC0xMy4wNyAtOS43NCwtMjIuMzYgLTIzLjgxLC0yMi4zNiAtMTYuOTYsMCAtMjQuNTMsMTIuOCAtMjQuNTMsMzEuOTIgMCwxOC44NSA2Ljg1LDM1LjggMjUuOTcsMzUuOCAxMy43LDAgMjAuMiwtOC44NCAyMS4xMSwtMTcuNTkgaCAtMTAuOTIgYyAtMC43Miw2LjMyIC01LjE0LDkuMzkgLTExLDkuMzkgLTguODQsMCAtMTQuMDcsLTguOTQgLTE0LjI1LC0yMi4zNiAyLjg5LDQuMTQgOC4yMSw3LjQ4IDE1LjcsNy40OCIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzMjYiPjwvcGF0aD48cGF0aCBkPSJtIDU3MDkuOTUsMjEyNi44IGggLTE0LjYxIHYgNy40IGMgOS40NywwLjI2IDE0LjA3LDEuMDcgMTcuNCw4LjIgaCA3Ljk0IHYgLTY1LjM4IGggLTEwLjczIHYgNDkuNzgiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzI4Ij48L3BhdGg+PHBhdGggZD0ibSA1NzU1LjIyLDIxMzUuMzcgYyAtOS4zNywwIC0xNC43OSwtOS4xMSAtMTQuNzksLTI1LjYyIDAsLTE2LjUgNS40MiwtMjUuNiAxNC43OSwtMjUuNiA5LjQ2LDAgMTQuODgsOS4xIDE0Ljg4LDI1LjYgMCwxNi41MSAtNS40MiwyNS42MiAtMTQuODgsMjUuNjIgeiBtIDAsOC4yIGMgMTcuNDksMCAyNi4wNywtMTMuOCAyNi4wNywtMzMuODIgMCwtMjAuMSAtOC41OCwtMzMuOSAtMjYuMDcsLTMzLjkgLTE3LjQsMCAtMjUuOTgsMTMuOCAtMjUuOTgsMzMuOSAwLDIwLjAyIDguNTgsMzMuODIgMjUuOTgsMzMuODIiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzMwIj48L3BhdGg+PHBhdGggZD0ibSA2MTExLjMsMjEyNi44IGggLTE0LjYgdiA3LjQgYyA5LjQ3LDAuMjYgMTQuMDcsMS4wNyAxNy40LDguMiBoIDcuOTQgdiAtNjUuMzggaCAtMTAuNzQgdiA0OS43OCIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzMzIiPjwvcGF0aD48cGF0aCBkPSJtIDYxNTYuNTcsMjEzNS4zNyBjIC05LjM4LDAgLTE0LjgsLTkuMTEgLTE0LjgsLTI1LjYyIDAsLTE2LjUgNS40MiwtMjUuNiAxNC44LC0yNS42IDkuNDYsMCAxNC44OCw5LjEgMTQuODgsMjUuNiAwLDE2LjUxIC01LjQyLDI1LjYyIC0xNC44OCwyNS42MiB6IG0gMCw4LjIgYyAxNy40OSwwIDI2LjA2LC0xMy44IDI2LjA2LC0zMy44MiAwLC0yMC4xIC04LjU3LC0zMy45IC0yNi4wNiwtMzMuOSAtMTcuNCwwIC0yNS45OCwxMy44IC0yNS45OCwzMy45IDAsMjAuMDIgOC41OCwzMy44MiAyNS45OCwzMy44MiIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzMzQiPjwvcGF0aD48cGF0aCBkPSJtIDU5MjMuOCwyMTI1LjQ1IGMgMCwtNi4yMiA0Ljc4LC0xMC4zNyAxMS44MSwtMTAuMzcgNy4xMywwIDExLjczLDQuMTUgMTEuNzMsMTAuMzcgMCw2LjIyIC00LjYsOS45MiAtMTEuNzMsOS45MiAtNy4wMywwIC0xMS44MSwtMy43IC0xMS44MSwtOS45MiB6IG0gMTEuODEsLTQxLjMgYyA4LjAzLDAgMTMuMTcsNC40MSAxMy4xNywxMS44MSAwLDcuMyAtNS4xNCwxMS44MSAtMTMuMTcsMTEuODEgLTguMDMsMCAtMTMuMTYsLTQuNTEgLTEzLjE2LC0xMS44MSAwLC03LjQgNS4xMywtMTEuODEgMTMuMTYsLTExLjgxIHogbSAxMy45OCwyNy43NyBjIDcuNzYsLTMuOTcgMTAuMzcsLTEwLjE5IDEwLjM3LC0xNi4zMyAwLC0xMi44OSAtMTAuNjQsLTE5Ljc0IC0yNC4zNSwtMTkuNzQgLTEzLjcxLDAgLTI0LjM0LDYuODUgLTI0LjM0LDE5Ljc0IDAsNi4xNCAyLjYxLDEyLjQ2IDEwLjM3LDE2LjMzIC01Ljc3LDMuMjQgLTguMzksOS4yOSAtOC4zOSwxNC44OCAwLDkuNzQgOC42NSwxNi43NyAyMi4zNiwxNi43NyAxMy42MSwwIDIyLjM2LC03LjAzIDIyLjM2LC0xNi43NyAwLC01LjU5IC0yLjQzLC0xMS4zNiAtOC4zOCwtMTQuODgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzM2Ij48L3BhdGg+PHBhdGggZD0ibSA2NDU5LjQ0LDIxMjYuOCBoIC0xNC42MSB2IDcuNCBjIDkuNDcsMC4yNiAxNC4wNywxLjA3IDE3LjQsOC4yIGggNy45NCB2IC02NS4zOCBoIC0xMC43MyB2IDQ5Ljc4IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDMzOCI+PC9wYXRoPjxwYXRoIGQ9Im0gNjQ5OC4zOSwyMTA2LjY5IGggLTMuMTUgdiA4LjkyIGggMi43MSBjIDEwLjE5LDAgMTUuMTUsMy4zNCAxNS4xNSwxMC4xMSAwLDYuNTggLTUuMzIsOS42NSAtMTEuMzcsOS42NSAtNy45MywwIC0xMi4zNSwtNC43OSAtMTMuMzQsLTEyLjQ1IGggLTEwLjQ2IGMgMC45OSwxMi40NSA5LjkyLDIwLjY1IDI0LjQ0LDIwLjY1IDEwLjkxLDAgMjEuNzMsLTQuOTYgMjEuNzMsLTE3LjIyIDAsLTYuNSAtMy43OSwtMTEuOTEgLTkuNTYsLTE0LjcgNy44NSwtMi44OCAxMS4yOCwtOS4yOSAxMS4yOCwtMTUuOTYgMCwtMTMuMzUgLTExLjQ2LC0xOS44NCAtMjQuNTMsLTE5Ljg0IC0xNS4xNSwwIC0yMy4zNiw5LjkyIC0yNC4xNywyMS40NiBoIDEwLjQ1IGMgMS4wOSwtNy4yMSA1LjMzLC0xMy4xNiAxMy44OSwtMTMuMTYgNy41OCwwIDEzLjI2LDQuMTQgMTMuMjYsMTEuMjcgMCw4LjM5IC02LjY3LDExLjI3IC0xNi4zMywxMS4yNyIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzNDAiPjwvcGF0aD48cGF0aCBkPSJtIDYzMDUuMzcsMjEyNi44IGggLTE0LjYxIHYgNy40IGMgOS40NywwLjI2IDE0LjA3LDEuMDcgMTcuNCw4LjIgaCA3Ljk0IHYgLTY1LjM4IGggLTEwLjczIHYgNDkuNzgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzQyIj48L3BhdGg+PHBhdGggZD0ibSA2MzUwLjYzLDIxMzUuMzcgYyAtOS4zNywwIC0xNC43OSwtOS4xMSAtMTQuNzksLTI1LjYyIDAsLTE2LjUgNS40MiwtMjUuNiAxNC43OSwtMjUuNiA5LjQ2LDAgMTQuODgsOS4xIDE0Ljg4LDI1LjYgMCwxNi41MSAtNS40MiwyNS42MiAtMTQuODgsMjUuNjIgeiBtIDAsOC4yIGMgMTcuNDksMCAyNi4wNywtMTMuOCAyNi4wNywtMzMuODIgMCwtMjAuMSAtOC41OCwtMzMuOSAtMjYuMDcsLTMzLjkgLTE3LjQsMCAtMjUuOTgsMTMuOCAtMjUuOTgsMzMuOSAwLDIwLjAyIDguNTgsMzMuODIgMjUuOTgsMzMuODIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzQ0Ij48L3BhdGg+PHBhdGggZD0ibSA2Nzc4LDIxMjYuOCBoIC0xNC42MSB2IDcuNCBjIDkuNDgsMC4yNiAxNC4wOCwxLjA3IDE3LjQxLDguMiBoIDcuOTQgdiAtNjUuMzggSCA2Nzc4IHYgNDkuNzgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzQ2Ij48L3BhdGg+PHBhdGggZD0ibSA2ODEwLjQ3LDIxMjYuOCBoIC0xNC42MSB2IDcuNCBjIDkuNDcsMC4yNiAxNC4wNywxLjA3IDE3LjQsOC4yIGggNy45NCB2IC02NS4zOCBoIC0xMC43MyB2IDQ5Ljc4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDM0OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNzQ2NC43NiwyMTI2LjggaCAtMTQuNjEgdiA3LjQgYyA5LjQ4LDAuMjYgMTQuMDcsMS4wNyAxNy40LDguMiBoIDcuOTQgdiAtNjUuMzggaCAtMTAuNzMgdiA0OS43OCIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzNTAiPjwvcGF0aD48cGF0aCBkPSJtIDc1MjEuMywyMDk4LjA0IGMgMCw4LjU2IC01LjMzLDEzLjk3IC0xMi43MiwxMy45NyAtNy4zOSwwIC0xMi44LC01LjQxIC0xMi44LC0xMy45NyAwLC04LjY3IDUuMzIsLTEzLjg5IDEyLjcxLC0xMy44OSA3LjQ4LDAgMTIuODEsNS4yMiAxMi44MSwxMy44OSB6IG0gLTEwLjY0LDIyLjQ1IGMgMTIuMDgsMCAyMS43MywtOC42NyAyMS43MywtMjIuMjggMCwtMTMuMDcgLTkuNzQsLTIyLjM2IC0yMy44MSwtMjIuMzYgLTE2Ljk1LDAgLTI0LjUzLDEyLjggLTI0LjUzLDMxLjkyIDAsMTguODUgNi44NSwzNS44IDI1Ljk4LDM1LjggMTMuNzEsMCAyMC4xOSwtOC44NCAyMS4xLC0xNy41OSBoIC0xMC45MiBjIC0wLjcyLDYuMzIgLTUuMTQsOS4zOSAtMTAuOTksOS4zOSAtOC44NCwwIC0xNC4wOCwtOC45NCAtMTQuMjUsLTIyLjM2IDIuODgsNC4xNCA4LjIsNy40OCAxNS42OSw3LjQ4IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDM1MiI+PC9wYXRoPjxwYXRoIGQ9Im0gNjg4My42LDIyMzIuMjUgYyAwLDE4LjE5IDE0Ljc0LDMyLjkyIDMyLjkyLDMyLjkyIDE4LjE3LDAgMzIuOTEsLTE0LjczIDMyLjkxLC0zMi45MiAwLC0xOC4xNyAtMTQuNzQsLTMyLjkxIC0zMi45MSwtMzIuOTEgLTE4LjE4LDAgLTMyLjkyLDE0Ljc0IC0zMi45MiwzMi45MSIgc3R5bGU9ImZpbGw6I2I2YjZiODtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzNTQiPjwvcGF0aD48cGF0aCBkPSJtIDY4ODkuMjUsMjEyNi44IGggLTE0LjYxIHYgNy40IGMgOS40OCwwLjI2IDE0LjA4LDEuMDcgMTcuNDEsOC4yIGggNy45NCB2IC02NS4zOCBoIC0xMC43NCB2IDQ5Ljc4IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDM1NiI+PC9wYXRoPjxwYXRoIGQ9Im0gNjkyMC4zNiwyMDg2LjM5IGggMzQuMjcgdiAtOS4zNyBoIC00Ny42MiB2IDguODQgYyAyMS44MiwxNy4wNCAzNC45LDI4LjU4IDM0LjksMzkuNSAwLDYuMzEgLTQuMTUsMTAuMDEgLTEwLjU1LDEwLjAxIC02LjIyLDAgLTEyLjE3LC0zLjcgLTEyLjE3LC0xMy44OSBoIC0xMC43NCBjIC0wLjE3LDEzLjE3IDkuMDMsMjIuMDkgMjMuMzYsMjIuMDkgMTIuMDgsMCAyMS4yOCwtNi4yMiAyMS4yOCwtMTcuMzEgMCwtMTMuNTMgLTEyLjk5LC0yNi4xNSAtMzIuNzMsLTM5Ljg3IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDM1OCI+PC9wYXRoPjxwYXRoIGQ9Im0gMjUwMi41NywzNjM5Ljk5IGggLTIzLjM4IHYgMTEuODMgYyAxNS4xNiwwLjQ0IDIyLjUyLDEuNzQgMjcuODYsMTMuMTQgaCAxMi43IHYgLTEwNC42NSBoIC0xNy4xOCB2IDc5LjY4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDM2MCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzEzMy4yNSwzNTc1LjMyIGggNTQuODUgdiAtMTUuMDEgaCAtNzYuMjEgdiAxNC4xNSBjIDM0LjkzLDI3LjI4IDU1Ljg2LDQ1Ljc1IDU1Ljg2LDYzLjIyIDAsMTAuMSAtNi42NCwxNi4wMiAtMTYuODksMTYuMDIgLTkuOTYsMCAtMTkuNDksLTUuOTIgLTE5LjQ5LC0yMi4yMyBoIC0xNy4xNyBjIC0wLjI5LDIxLjA4IDE0LjQzLDM1LjM3IDM3LjM4LDM1LjM3IDE5LjM0LDAgMzQuMDcsLTkuOTYgMzQuMDcsLTI3LjcxIDAsLTIxLjY2IC0yMC43OSwtNDEuODcgLTUyLjQsLTYzLjgxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDM2MiI+PC9wYXRoPjxwYXRoIGQ9Im0gMzI4MC42LDMxMTMuNDcgaCAtNS4wNSB2IDE0LjI5IGggNC4zMyBjIDE2LjMxLDAgMjQuMjUsNS4zNCAyNC4yNSwxNi4xNyAwLDEwLjU0IC04LjUxLDE1LjQ0IC0xOC4xOSwxNS40NCAtMTIuNywwIC0xOS43NywtNy42NCAtMjEuMzYsLTE5LjkxIGggLTE2Ljc1IGMgMS42LDE5LjkxIDE1Ljg4LDMzLjA2IDM5LjEyLDMzLjA2IDE3LjQ3LDAgMzQuNzksLTcuOTQgMzQuNzksLTI3LjU4IDAsLTEwLjM5IC02LjA2LC0xOS4wNSAtMTUuMywtMjMuNTMgMTIuNTYsLTQuNjEgMTguMDQsLTE0Ljg2IDE4LjA0LC0yNS41NCAwLC0yMS4zNyAtMTguMzMsLTMxLjc2IC0zOS4yNiwtMzEuNzYgLTI0LjI1LDAgLTM3LjM5LDE1Ljg4IC0zOC42OSwzNC4zNSBoIDE2Ljc1IGMgMS43MywtMTEuNTUgOC41MiwtMjEuMDcgMjIuMjMsLTIxLjA3IDEyLjEyLDAgMjEuMjIsNi42NCAyMS4yMiwxOC4wNCAwLDEzLjQzIC0xMC42OCwxOC4wNCAtMjYuMTMsMTguMDQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzY0Ij48L3BhdGg+PHBhdGggZD0ibSAzNzM1LjAxLDMxNzAuNjMgdiAtMTUuMTUgYyAtMjYuNzEsLTI1LjI2IC00MSwtNTEuMSAtNDMuMywtODkuNSBoIC0xOS40OSBjIDEuODcsMzYuODEgMjAuMiw2Ny4yNyA0NC42LDg5LjUgaCAtNTcuMDIgdiAxNS4xNSBoIDc1LjIxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDM2NiI+PC9wYXRoPjxwYXRoIGQ9Im0gNDkwOC43OSwzMTQzLjUgYyAwLC05Ljk2IDcuNjQsLTE2LjYgMTguOSwtMTYuNiAxMS40MSwwIDE4Ljc2LDYuNjQgMTguNzYsMTYuNiAwLDkuOTYgLTcuMzUsMTUuODcgLTE4Ljc2LDE1Ljg3IC0xMS4yNiwwIC0xOC45LC01LjkxIC0xOC45LC0xNS44NyB6IG0gMTguOSwtNjYuMTEgYyAxMi44NCwwIDIxLjA4LDcuMDcgMjEuMDgsMTguOTEgMCwxMS42OSAtOC4yNCwxOC45IC0yMS4wOCwxOC45IC0xMi44NSwwIC0yMS4wNywtNy4yMSAtMjEuMDcsLTE4LjkgMCwtMTEuODQgOC4yMiwtMTguOTEgMjEuMDcsLTE4LjkxIHogbSAyMi4zNyw0NC40NSBjIDEyLjQyLC02LjM0IDE2LjYxLC0xNi4zIDE2LjYxLC0yNi4xMiAwLC0yMC42NCAtMTcuMDMsLTMxLjYxIC0zOC45OCwtMzEuNjEgLTIxLjk0LDAgLTM4Ljk3LDEwLjk3IC0zOC45NywzMS42MSAwLDkuODIgNC4xOSwxOS45MiAxNi42LDI2LjEyIC05LjI0LDUuMiAtMTMuNDMsMTQuODggLTEzLjQzLDIzLjgyIDAsMTUuNiAxMy44NiwyNi44NiAzNS44LDI2Ljg2IDIxLjgsMCAzNS44LC0xMS4yNiAzNS44LC0yNi44NiAwLC04Ljk0IC0zLjg5LC0xOC4xOCAtMTMuNDMsLTIzLjgyIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDM2OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNTY5Mi40MywzMTQ1LjY2IGggLTIzLjM5IHYgMTEuODQgYyAxNS4xNiwwLjQ0IDIyLjUyLDEuNzQgMjcuODYsMTMuMTMgaCAxMi43MSB2IC0xMDQuNjUgaCAtMTcuMTggdiA3OS42OCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzNzAiPjwvcGF0aD48cGF0aCBkPSJtIDU3NjQuODYsMzE1OS4zNyBjIC0xNS4wMSwwIC0yMy42NywtMTQuNTcgLTIzLjY3LC00MC45OCAwLC0yNi40MiA4LjY2LC00MSAyMy42NywtNDEgMTUuMTYsMCAyMy44MiwxNC41OCAyMy44Miw0MSAwLDI2LjQxIC04LjY2LDQwLjk4IC0yMy44Miw0MC45OCB6IG0gMCwxMy4xNSBjIDI4LjAxLDAgNDEuNzIsLTIyLjA5IDQxLjcyLC01NC4xMyAwLC0zMi4yIC0xMy43MSwtNTQuMjggLTQxLjcyLC01NC4yOCAtMjcuODYsMCAtNDEuNTcsMjIuMDggLTQxLjU3LDU0LjI4IDAsMzIuMDQgMTMuNzEsNTQuMTMgNDEuNTcsNTQuMTMiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzcyIj48L3BhdGg+PHBhdGggZD0ibSAyNjQyLjUxLDQwNjQuOTQgaCA1NC44NSB2IC0xNS4wMSBoIC03Ni4yMiB2IDE0LjE1IGMgMzQuOTQsMjcuMjggNTUuODcsNDUuNzUgNTUuODcsNjMuMjIgMCwxMC4xIC02LjY0LDE2LjAyIC0xNi44OSwxNi4wMiAtOS45NiwwIC0xOS40OSwtNS45MiAtMTkuNDksLTIyLjIzIGggLTE3LjE4IGMgLTAuMjgsMjEuMDcgMTQuNDQsMzUuMzcgMzcuMzksMzUuMzcgMTkuMzQsMCAzNC4wNiwtOS45NiAzNC4wNiwtMjcuNzEgMCwtMjEuNjYgLTIwLjc4LC00MS44NyAtNTIuMzksLTYzLjgxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDM3NCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzA0Ni4wNiw0MDk3LjQyIGggLTUuMDUgdiAxNC4yOSBoIDQuMzMgYyAxNi4zMSwwIDI0LjI1LDUuMzQgMjQuMjUsMTYuMTcgMCwxMC41MyAtOC41MSwxNS40NCAtMTguMTksMTUuNDQgLTEyLjcsMCAtMTkuNzcsLTcuNjUgLTIxLjM2LC0xOS45MSBoIC0xNi43NSBjIDEuNTksMTkuOTEgMTUuODgsMzMuMDUgMzkuMTIsMzMuMDUgMTcuNDcsMCAzNC43OSwtNy45NCAzNC43OSwtMjcuNTcgMCwtMTAuNCAtNi4wNiwtMTkuMDYgLTE1LjMsLTIzLjUzIDEyLjU2LC00LjYyIDE4LjA0LC0xNC44NiAxOC4wNCwtMjUuNTUgMCwtMjEuMzYgLTE4LjMzLC0zMS43NiAtMzkuMjYsLTMxLjc2IC0yNC4yNSwwIC0zNy4zOSwxNS44OCAtMzguNjksMzQuMzYgaCAxNi43NSBjIDEuNzMsLTExLjU1IDguNTIsLTIxLjA3IDIyLjIzLC0yMS4wNyAxMi4xMiwwIDIxLjIyLDYuNjQgMjEuMjIsMTguMDMgMCwxMy40MyAtMTAuNjgsMTguMDUgLTI2LjEzLDE4LjA1IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDM3NiI+PC9wYXRoPjxwYXRoIGQ9Im0gNDYzNy4zMSw0MTIwLjk1IGMgMCwtMTMuNzIgOC41MiwtMjIuMzggMjAuMzUsLTIyLjM4IDExLjY5LDAgMjAuNSw4LjY2IDIwLjUsMjIuMzggMCwxNCAtOC42NiwyMi4zNyAtMjAuMzUsMjIuMzcgLTExLjk4LDAgLTIwLjUsLTguMzcgLTIwLjUsLTIyLjM3IHogbSAxNy4wMywtMzUuOTQgYyAtMTkuMzQsMCAtMzQuNzgsMTMuODUgLTM0Ljc4LDM1LjggMCwyMC43OCAxNS41OCwzNS42NSAzOC4xLDM1LjY1IDI3LjE0LDAgMzkuMjcsLTIwLjUgMzkuMjcsLTUxLjEgMCwtMzAuMTcgLTExLjEyLC01Ny4zMSAtNDEuNzIsLTU3LjMxIC0yMS44LDAgLTMyLjE5LDE0LjE1IC0zMy42MywyOC4xNSBoIDE3LjQ2IGMgMS4xNiwtMTAuMSA4LjIzLC0xNC44NiAxNy42MiwtMTQuODYgMTQuMTQsMCAyMi41MSwxNC4yOCAyMi44LDM1LjY1IC00LjYyLC02LjY0IC0xMy4xNCwtMTEuOTggLTI1LjEyLC0xMS45OCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzNzgiPjwvcGF0aD48cGF0aCBkPSJtIDYwOTIuMzYsNDEyOS42MSBoIC0yMy4zOSB2IDExLjg0IGMgMTUuMTYsMC40MyAyMi41MiwxLjczIDI3Ljg2LDEzLjEzIGggMTIuNzEgdiAtMTA0LjY1IGggLTE3LjE4IHYgNzkuNjgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzgwIj48L3BhdGg+PHBhdGggZD0ibSA2MTY0Ljc5LDQxNDMuMzIgYyAtMTUuMDEsMCAtMjMuNjcsLTE0LjU3IC0yMy42NywtNDAuOTkgMCwtMjYuNDIgOC42NiwtNDAuOTkgMjMuNjcsLTQwLjk5IDE1LjE2LDAgMjMuODIsMTQuNTcgMjMuODIsNDAuOTkgMCwyNi40MiAtOC42Niw0MC45OSAtMjMuODIsNDAuOTkgeiBtIDAsMTMuMTQgYyAyOC4wMSwwIDQxLjcyLC0yMi4wOSA0MS43MiwtNTQuMTMgMCwtMzIuMTkgLTEzLjcxLC01NC4yOCAtNDEuNzIsLTU0LjI4IC0yNy44NiwwIC00MS41NywyMi4wOSAtNDEuNTcsNTQuMjggMCwzMi4wNCAxMy43MSw1NC4xMyA0MS41Nyw1NC4xMyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzODIiPjwvcGF0aD48cGF0aCBkPSJtIDY0NDEuOTgsNDEyOS42MSBoIC0yMy4zOSB2IDExLjg0IGMgMTUuMTYsMC40MyAyMi41MiwxLjczIDI3Ljg2LDEzLjEzIGggMTIuNzEgdiAtMTA0LjY1IGggLTE3LjE4IHYgNzkuNjgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzg0Ij48L3BhdGg+PHBhdGggZD0ibSA2NTA0LjMxLDQwOTcuNDIgaCAtNS4wNiB2IDE0LjI5IGggNC4zNCBjIDE2LjMxLDAgMjQuMjUsNS4zNCAyNC4yNSwxNi4xNyAwLDEwLjUzIC04LjUyLDE1LjQ0IC0xOC4yLDE1LjQ0IC0xMi42OSwwIC0xOS43NywtNy42NSAtMjEuMzUsLTE5LjkxIGggLTE2Ljc1IGMgMS41OSwxOS45MSAxNS44OCwzMy4wNSAzOS4xMiwzMy4wNSAxNy40NiwwIDM0Ljc5LC03Ljk0IDM0Ljc5LC0yNy41NyAwLC0xMC40IC02LjA3LC0xOS4wNiAtMTUuMzEsLTIzLjUzIDEyLjU2LC00LjYyIDE4LjA1LC0xNC44NiAxOC4wNSwtMjUuNTUgMCwtMjEuMzYgLTE4LjMzLC0zMS43NiAtMzkuMjYsLTMxLjc2IC0yNC4yNiwwIC0zNy4zOSwxNS44OCAtMzguNjksMzQuMzYgaCAxNi43NSBjIDEuNzMsLTExLjU1IDguNTEsLTIxLjA3IDIyLjIzLC0yMS4wNyAxMi4xMiwwIDIxLjIyLDYuNjQgMjEuMjIsMTguMDMgMCwxMy40MyAtMTAuNjksMTguMDUgLTI2LjEzLDE4LjA1IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDM4NiI+PC9wYXRoPjxwYXRoIGQ9Im0gMjc5OS42NCw0NTk0LjIzIGggLTUuMDYgdiAxNC4yOSBoIDQuMzMgYyAxNi4zMiwwIDI0LjI2LDUuMzQgMjQuMjYsMTYuMTcgMCwxMC41MyAtOC41MiwxNS40NCAtMTguMTksMTUuNDQgLTEyLjcxLDAgLTE5Ljc4LC03LjY1IC0yMS4zNywtMTkuOTIgaCAtMTYuNzQgYyAxLjU5LDE5LjkyIDE1Ljg4LDMzLjA2IDM5LjEyLDMzLjA2IDE3LjQ2LDAgMzQuNzgsLTcuOTQgMzQuNzgsLTI3LjU4IDAsLTEwLjM5IC02LjA2LC0xOS4wNSAtMTUuMywtMjMuNTMgMTIuNTYsLTQuNjEgMTguMDUsLTE0Ljg2IDE4LjA1LC0yNS41NCAwLC0yMS4zNyAtMTguMzMsLTMxLjc2IC0zOS4yNywtMzEuNzYgLTI0LjI0LDAgLTM3LjM4LDE1Ljg4IC0zOC42OCwzNC4zNiBoIDE2Ljc1IGMgMS43MiwtMTEuNTYgOC41MSwtMjEuMDggMjIuMjIsLTIxLjA4IDEyLjEzLDAgMjEuMjIsNi42NCAyMS4yMiwxOC4wNCAwLDEzLjQzIC0xMC42OCwxOC4wNSAtMjYuMTIsMTguMDUiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzg4Ij48L3BhdGg+PHBhdGggZD0ibSA1MDQ4LjE5LDQ1ODYuMTQgdiA0Mi44NyBsIC0zMi45MSwtNDIuODcgeiBtIDE3LjE4LC0xNC44NiB2IC0yNC41NSBoIC0xNy4xOCB2IDI0LjU1IGggLTUxLjY4IHYgMTQuMjkgbCA1MS44Myw2NS44MiBoIDE3LjAzIHYgLTY1LjI1IGggMTguNDcgdiAtMTQuODYgaCAtMTguNDciIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoMzkwIj48L3BhdGg+PHBhdGggZD0ibSA1NDI5LjU0LDQ1ODAuMzcgYyAwLDEzLjcxIC04LjUyLDIyLjM3IC0yMC4zNSwyMi4zNyAtMTEuODQsMCAtMjAuNSwtOC42NiAtMjAuNSwtMjIuMzcgMCwtMTMuODYgOC41MSwtMjIuMjMgMjAuMzUsLTIyLjIzIDExLjk4LDAgMjAuNSw4LjM3IDIwLjUsMjIuMjMgeiBtIC0xNy4wMywzNS45NSBjIDE5LjMzLDAgMzQuNzgsLTEzLjg2IDM0Ljc4LC0zNS42NiAwLC0yMC45MyAtMTUuNTgsLTM1LjggLTM4LjEsLTM1LjggLTI3LjE0LDAgLTM5LjI3LDIwLjUgLTM5LjI3LDUxLjA5IDAsMzAuMTggMTAuOTcsNTcuMzIgNDEuNTcsNTcuMzIgMjEuOTQsMCAzMi4zMywtMTQuMTUgMzMuNzgsLTI4LjE2IGggLTE3LjQ2IGMgLTEuMTYsMTAuMTEgLTguMjMsMTUuMDIgLTE3LjYyLDE1LjAyIC0xNC4xNCwwIC0yMi41MiwtMTQuMjkgLTIyLjgsLTM1LjggNC42Miw2LjY1IDEzLjEzLDExLjk5IDI1LjEyLDExLjk5IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDM5MiI+PC9wYXRoPjxwYXRoIGQ9Im0gMzU4NC4xOCwzNTk5LjcxIHYgNDIuODggbCAtMzIuOTEsLTQyLjg4IHogbSAxNy4xNywtMTQuODYgdiAtMjQuNTQgaCAtMTcuMTcgdiAyNC41NCBoIC01MS42OCB2IDE0LjI5IGwgNTEuODIsNjUuODIgaCAxNy4wMyB2IC02NS4yNSBoIDE4LjQ4IHYgLTE0Ljg2IGggLTE4LjQ4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDM5NCI+PC9wYXRoPjxwYXRoIGQ9Im0gNDEzMy45NCwzNjE2Ljg5IGMgLTkuNjcsMCAtMTYuNzQsLTQuOSAtMTguOTEsLTEwLjk2IGwgLTE2LjE3LDAuODcgNi45Myw1OC4xNiBoIDYyLjY0IHYgLTE1LjE2IGggLTQ4LjQ5IGwgLTMuMzIsLTI2LjI3IGMgNS4wNSw0LjA1IDEyLjI3LDYuNSAyMS42NSw2LjUgMTcuOSwwIDM0LjUsLTEyLjI3IDM0LjUsLTM1Ljc5IDAsLTIzLjM5IC0xNy45LC0zNS44IC0zOC42OCwtMzUuOCAtMjQuNCwwIC0zNi44MSwxNS44NyAtMzguMTEsMzMuOTEgaCAxNi42IGMgMS40NCwtMTIuMTIgOC4wOCwtMjAuNjMgMjEuOCwtMjAuNjMgMTEuNTQsMCAyMC42NCw4LjIyIDIwLjY0LDIyLjIyIDAsMTUuNTkgLTEwLjY5LDIyLjk1IC0yMS4wOCwyMi45NSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzOTYiPjwvcGF0aD48cGF0aCBkPSJtIDQ1MDkuNjcsMzU5My45NCBjIDAsMTMuNzEgLTguNTEsMjIuMzggLTIwLjM1LDIyLjM4IC0xMS44MywwIC0yMC41LC04LjY3IC0yMC41LC0yMi4zOCAwLC0xMy44NSA4LjUyLC0yMi4yMiAyMC4zNiwtMjIuMjIgMTEuOTgsMCAyMC40OSw4LjM3IDIwLjQ5LDIyLjIyIHogbSAtMTcuMDMsMzUuOTUgYyAxOS4zNCwwIDM0Ljc5LC0xMy44NiAzNC43OSwtMzUuNjUgMCwtMjAuOTQgLTE1LjU5LC0zNS44IC0zOC4xMSwtMzUuOCAtMjcuMTQsMCAtMzkuMjcsMjAuNDkgLTM5LjI3LDUxLjA5IDAsMzAuMTggMTAuOTgsNTcuMzEgNDEuNTgsNTcuMzEgMjEuOTQsMCAzMi4zMywtMTQuMTUgMzMuNzgsLTI4LjE1IGggLTE3LjQ2IGMgLTEuMTcsMTAuMTEgLTguMjQsMTUuMDEgLTE3LjYyLDE1LjAxIC0xNC4xNCwwIC0yMi41MiwtMTQuMjkgLTIyLjgsLTM1Ljc5IDQuNjEsNi42NCAxMy4xMywxMS45OCAyNS4xMSwxMS45OCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGgzOTgiPjwvcGF0aD48cGF0aCBkPSJtIDUyMjkuMzYsMzY2NC45NiB2IC0xNS4xNiBjIC0yNi43MSwtMjUuMjUgLTQwLjk5LC01MS4wOSAtNDMuMzEsLTg5LjQ5IGggLTE5LjQ4IGMgMS44NywzNi44MSAyMC4yLDY3LjI3IDQ0LjYsODkuNDkgaCAtNTcuMDEgdiAxNS4xNiBoIDc1LjIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNDAwIj48L3BhdGg+PHBhdGggZD0ibSA3MzI4Ljk3LDI2ODguNTQgYyAwLDU5LjM0IDQ4LjExLDEwNy40NCAxMDcuNDQsMTA3LjQ0IDIwLjQ3LDAgOTEuMTcsMCAxMTEuNjUsMCA1OS4zNCwwIDEwNy40MywtNDguMSAxMDcuNDMsLTEwNy40NCAwLC0yMC40NyAwLC05MS4xNyAwLC0xMTEuNjQgMCwtNTkuMzQgLTQ4LjA5LC0xMDcuNDQgLTEwNy40MywtMTA3LjQ0IC0yMC40OCwwIC05MS4xOCwwIC0xMTEuNjUsMCAtNTkuMzMsMCAtMTA3LjQ0LDQ4LjEgLTEwNy40NCwxMDcuNDQgMCwyMC40NyAwLDkxLjE3IDAsMTExLjY0IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQwMiI+PC9wYXRoPjxwYXRoIGQ9Im0gNjc1My4yNSw0NjY5LjIyIGMgMCw1OS4zNCA0OC4xLDEwNy40NCAxMDcuNDQsMTA3LjQ0IDIwLjQ4LDAgOTEuMTcsMCAxMTEuNjUsMCA1OS4zNCwwIDEwNy40NCwtNDguMSAxMDcuNDQsLTEwNy40NCAwLC0yMC40NyAwLC05MS4xNyAwLC0xMTEuNjUgMCwtNTkuMzMgLTQ4LjEsLTEwNy40MyAtMTA3LjQ0LC0xMDcuNDMgLTIwLjQ4LDAgLTkxLjE3LDAgLTExMS42NSwwIC01OS4zNCwwIC0xMDcuNDQsNDguMSAtMTA3LjQ0LDEwNy40MyAwLDIwLjQ4IDAsOTEuMTggMCwxMTEuNjUiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNDA0Ij48L3BhdGg+PHBhdGggZD0ibSA2MjY4LjM2LDM0NTQuMDQgYyAtNTYuNDksMCAtMTAyLjQ0LDQ1Ljk1IC0xMDIuNDQsMTAyLjQzIHYgMTExLjY1IGMgMCw1Ni40OSA0NS45NSwxMDIuNDQgMTAyLjQ0LDEwMi40NCBoIDExMS42NSBjIDU2LjQ4LDAgMTAyLjQ0LC00NS45NSAxMDIuNDQsLTEwMi40NCB2IC0xMTEuNjUgYyAwLC01Ni40OCAtNDUuOTYsLTEwMi40MyAtMTAyLjQ0LC0xMDIuNDMgaCAtMTExLjY1IiBzdHlsZT0iZmlsbDojZmZmZmZmO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQwNiI+PC9wYXRoPjxwYXRoIGQ9Im0gNjM4MC4wMSwzNzc1LjU2IGMgLTIwLjQ3LDAgLTkxLjE4LDAgLTExMS42NSwwIC01OS4zNCwwIC0xMDcuNDQsLTQ4LjEgLTEwNy40NCwtMTA3LjQ0IDAsLTIwLjQ3IDAsLTkxLjE3IDAsLTExMS42NSAwLC01OS4zMyA0OC4xLC0xMDcuNDMgMTA3LjQ0LC0xMDcuNDMgMjAuNDcsMCA5MS4xOCwwIDExMS42NSwwIDU5LjMzLDAgMTA3LjQ0LDQ4LjEgMTA3LjQ0LDEwNy40MyAwLDIwLjQ4IDAsOTEuMTggMCwxMTEuNjUgMCw1OS4zNCAtNDguMTEsMTA3LjQ0IC0xMDcuNDQsMTA3LjQ0IHogbSAwLC0xMCBjIDUzLjczLDAgOTcuNDQsLTQzLjcxIDk3LjQ0LC05Ny40NCB2IC0xMTEuNjUgYyAwLC01My43MiAtNDMuNzEsLTk3LjQzIC05Ny40NCwtOTcuNDMgaCAtMTExLjY1IGMgLTUzLjcyLDAgLTk3LjQ0LDQzLjcxIC05Ny40NCw5Ny40MyB2IDExMS42NSBjIDAsNTMuNzMgNDMuNzIsOTcuNDQgOTcuNDQsOTcuNDQgaCAxMTEuNjUiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNDA4Ij48L3BhdGg+PHBhdGggZD0ibSA2Mjc1Ljk5LDM2MzkuOTkgaCAtMjMuMzkgdiAxMS44MyBjIDE1LjE2LDAuNDQgMjIuNTIsMS43NCAyNy44NywxMy4xNCBoIDEyLjcgdiAtMTA0LjY1IGggLTE3LjE4IHYgNzkuNjgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNDEwIj48L3BhdGg+PHBhdGggZD0ibSA2MzQ4LjQyLDM2NTMuNyBjIC0xNS4wMSwwIC0yMy42NywtMTQuNTcgLTIzLjY3LC00MC45OSAwLC0yNi40MSA4LjY2LC00MC45OSAyMy42NywtNDAuOTkgMTUuMTYsMCAyMy44MiwxNC41OCAyMy44Miw0MC45OSAwLDI2LjQyIC04LjY2LDQwLjk5IC0yMy44Miw0MC45OSB6IG0gMCwxMy4xNCBjIDI4LjAxLDAgNDEuNzIsLTIyLjA5IDQxLjcyLC01NC4xMyAwLC0zMi4xOSAtMTMuNzEsLTU0LjI3IC00MS43MiwtNTQuMjcgLTI3Ljg2LDAgLTQxLjU3LDIyLjA4IC00MS41Nyw1NC4yNyAwLDMyLjA0IDEzLjcxLDU0LjEzIDQxLjU3LDU0LjEzIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQxMiI+PC9wYXRoPjxwYXRoIGQ9Im0gNzQ0OC4zLDI2NTguNiBoIC0yMy4zOSB2IDExLjg0IGMgMTUuMTUsMC40NCAyMi41MiwxLjc0IDI3Ljg2LDEzLjEzIGggMTIuNyB2IC0xMDQuNjUgaCAtMTcuMTcgdiA3OS42OCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg0MTQiPjwvcGF0aD48cGF0aCBkPSJtIDc1MzguNzgsMjYxMi41NiBjIDAsMTMuNzEgLTguNTIsMjIuMzcgLTIwLjM2LDIyLjM3IC0xMS44MywwIC0yMC40OSwtOC42NiAtMjAuNDksLTIyLjM3IDAsLTEzLjg2IDguNTEsLTIyLjIzIDIwLjM1LC0yMi4yMyAxMS45OCwwIDIwLjUsOC4zNyAyMC41LDIyLjIzIHogbSAtMTcuMDQsMzUuOTQgYyAxOS4zNCwwIDM0Ljc5LC0xMy44NSAzNC43OSwtMzUuNjUgMCwtMjAuOTQgLTE1LjU5LC0zNS44IC0zOC4xMSwtMzUuOCAtMjcuMTMsMCAtMzkuMjYsMjAuNSAtMzkuMjYsNTEuMDkgMCwzMC4xOCAxMC45Nyw1Ny4zMiA0MS41Nyw1Ny4zMiAyMS45NCwwIDMyLjMzLC0xNC4xNSAzMy43OCwtMjguMTYgaCAtMTcuNDYgYyAtMS4xNiwxMC4xMSAtOC4yNCwxNS4wMSAtMTcuNjIsMTUuMDEgLTE0LjE0LDAgLTIyLjUyLC0xNC4yOCAtMjIuOCwtMzUuNzkgNC42Miw2LjY0IDEzLjEzLDExLjk4IDI1LjExLDExLjk4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQxNiI+PC9wYXRoPjxwYXRoIGQ9Im0gNjg2OS42LDQ2MzkuMjggaCAtMjMuMzkgdiAxMS44MyBjIDE1LjE1LDAuNDQgMjIuNTIsMS43NCAyNy44NiwxMy4xNCBoIDEyLjcgViA0NTU5LjYgaCAtMTcuMTcgdiA3OS42OCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg0MTgiPjwvcGF0aD48cGF0aCBkPSJtIDY5MTkuMzcsNDU3NC42MSBoIDU0Ljg1IFYgNDU1OS42IEggNjg5OCB2IDE0LjE1IGMgMzQuOTQsMjcuMjcgNTUuODYsNDUuNzUgNTUuODYsNjMuMjIgMCwxMC4xIC02LjY0LDE2LjAxIC0xNi44OCwxNi4wMSAtOS45NiwwIC0xOS40OSwtNS45MSAtMTkuNDksLTIyLjIyIGggLTE3LjE4IGMgLTAuMjgsMjEuMDcgMTQuNDQsMzUuMzcgMzcuMzksMzUuMzcgMTkuMzQsMCAzNC4wNiwtOS45NiAzNC4wNiwtMjcuNzIgMCwtMjEuNjUgLTIwLjc4LC00MS44NiAtNTIuMzksLTYzLjgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNDIwIj48L3BhdGg+PHBhdGggZD0ibSA2NzM4LjEyLDM0NTQuMDQgYyAtNTYuNDgsMCAtMTAyLjQ0LDQ1Ljk1IC0xMDIuNDQsMTAyLjQzIHYgMTExLjY1IGMgMCw1Ni40OSA0NS45NiwxMDIuNDQgMTAyLjQ0LDEwMi40NCBoIDExMS42NSBjIDU2LjQ5LDAgMTAyLjQ0LC00NS45NSAxMDIuNDQsLTEwMi40NCB2IC0xMTEuNjUgYyAwLC01Ni40OCAtNDUuOTUsLTEwMi40MyAtMTAyLjQ0LC0xMDIuNDMgaCAtMTExLjY1IiBzdHlsZT0iZmlsbDojZmZmZmZmO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQyMiI+PC9wYXRoPjxwYXRoIGQ9Im0gNjg0OS43NywzNzc1LjU2IGMgLTIwLjQ4LDAgLTkxLjE3LDAgLTExMS42NSwwIC01OS4zMywwIC0xMDcuNDQsLTQ4LjEgLTEwNy40NCwtMTA3LjQ0IDAsLTIwLjQ3IDAsLTkxLjE3IDAsLTExMS42NSAwLC01OS4zMyA0OC4xMSwtMTA3LjQzIDEwNy40NCwtMTA3LjQzIDIwLjQ4LDAgOTEuMTcsMCAxMTEuNjUsMCA1OS4zNCwwIDEwNy40NCw0OC4xIDEwNy40NCwxMDcuNDMgMCwyMC40OCAwLDkxLjE4IDAsMTExLjY1IDAsNTkuMzQgLTQ4LjEsMTA3LjQ0IC0xMDcuNDQsMTA3LjQ0IHogbSAwLC0xMCBjIDUzLjczLDAgOTcuNDQsLTQzLjcxIDk3LjQ0LC05Ny40NCB2IC0xMTEuNjUgYyAwLC01My43MiAtNDMuNzEsLTk3LjQzIC05Ny40NCwtOTcuNDMgaCAtMTExLjY1IGMgLTUzLjczLDAgLTk3LjQ0LDQzLjcxIC05Ny40NCw5Ny40MyB2IDExMS42NSBjIDAsNTMuNzMgNDMuNzEsOTcuNDQgOTcuNDQsOTcuNDQgaCAxMTEuNjUiIHN0eWxlPSJmaWxsOiNiNmI2Yjg7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNDI0Ij48L3BhdGg+PHBhdGggZD0ibSA2NzY1LjY3LDM2MzkuOTkgaCAtMjMuMzkgdiAxMS44MyBjIDE1LjE2LDAuNDQgMjIuNTIsMS43NCAyNy44NiwxMy4xNCBoIDEyLjcxIHYgLTEwNC42NSBoIC0xNy4xOCB2IDc5LjY4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQyNiI+PC9wYXRoPjxwYXRoIGQ9Im0gNjgxNy42LDM2MzkuOTkgaCAtMjMuMzggdiAxMS44MyBjIDE1LjE1LDAuNDQgMjIuNTEsMS43NCAyNy44NiwxMy4xNCBoIDEyLjcgdiAtMTA0LjY1IGggLTE3LjE4IHYgNzkuNjgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNDI4Ij48L3BhdGg+PHBhdGggZD0ibSA1ODgwLjc5LDM0NTQuMDQgYyAtNTYuNDksMCAtMTAyLjQzLDQ1Ljk1IC0xMDIuNDMsMTAyLjQzIHYgMTExLjY1IGMgMCw1Ni40OSA0NS45NCwxMDIuNDQgMTAyLjQzLDEwMi40NCBoIDExMS42NSBjIDU2LjQ4LDAgMTAyLjQ0LC00NS45NSAxMDIuNDQsLTEwMi40NCB2IC0xMTEuNjUgYyAwLC01Ni40OCAtNDUuOTYsLTEwMi40MyAtMTAyLjQ0LC0xMDIuNDMgaCAtMTExLjY1IiBzdHlsZT0iZmlsbDojZmZmZmZmO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQzMCI+PC9wYXRoPjxwYXRoIGQ9Im0gNTk5Mi40NCwzNzc1LjU2IGMgLTIwLjQ3LDAgLTkxLjE3LDAgLTExMS42NSwwIC01OS4zNCwwIC0xMDcuNDMsLTQ4LjEgLTEwNy40MywtMTA3LjQ0IDAsLTIwLjQ3IDAsLTkxLjE3IDAsLTExMS42NSAwLC01OS4zMyA0OC4wOSwtMTA3LjQzIDEwNy40MywtMTA3LjQzIDIwLjQ4LDAgOTEuMTgsMCAxMTEuNjUsMCA1OS4zMywwIDEwNy40NCw0OC4xIDEwNy40NCwxMDcuNDMgMCwyMC40OCAwLDkxLjE4IDAsMTExLjY1IDAsNTkuMzQgLTQ4LjExLDEwNy40NCAtMTA3LjQ0LDEwNy40NCB6IG0gMCwtMTAgYyA1My43MywwIDk3LjQ0LC00My43MSA5Ny40NCwtOTcuNDQgdiAtMTExLjY1IGMgMCwtNTMuNzIgLTQzLjcxLC05Ny40MyAtOTcuNDQsLTk3LjQzIGggLTExMS42NSBjIC01My43MiwwIC05Ny40Myw0My43MSAtOTcuNDMsOTcuNDMgdiAxMTEuNjUgYyAwLDUzLjczIDQzLjcxLDk3LjQ0IDk3LjQzLDk3LjQ0IGggMTExLjY1IiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQzMiI+PC9wYXRoPjxwYXRoIGQ9Im0gNTkxMS4yNSwzNjM3LjgzIGMgMCwtOS45NiA3LjY0LC0xNi42IDE4LjksLTE2LjYgMTEuNDEsMCAxOC43Niw2LjY0IDE4Ljc2LDE2LjYgMCw5Ljk1IC03LjM1LDE1Ljg3IC0xOC43NiwxNS44NyAtMTEuMjYsMCAtMTguOSwtNS45MiAtMTguOSwtMTUuODcgeiBtIDE4LjksLTY2LjExIGMgMTIuODQsMCAyMS4wOCw3LjA3IDIxLjA4LDE4LjkgMCwxMS42OSAtOC4yNCwxOC45MSAtMjEuMDgsMTguOTEgLTEyLjg1LDAgLTIxLjA3LC03LjIyIC0yMS4wNywtMTguOTEgMCwtMTEuODMgOC4yMiwtMTguOSAyMS4wNywtMTguOSB6IG0gMjIuMzgsNDQuNDUgYyAxMi40MSwtNi4zNSAxNi42LC0xNi4zMSAxNi42LC0yNi4xMiAwLC0yMC42NSAtMTcuMDMsLTMxLjYxIC0zOC45OCwtMzEuNjEgLTIxLjk0LDAgLTM4Ljk3LDEwLjk2IC0zOC45NywzMS42MSAwLDkuODEgNC4xOSwxOS45MiAxNi42LDI2LjEyIC05LjI0LDUuMiAtMTMuNDMsMTQuODcgLTEzLjQzLDIzLjgyIDAsMTUuNTkgMTMuODYsMjYuODUgMzUuOCwyNi44NSAyMS44LDAgMzUuOCwtMTEuMjYgMzUuOCwtMjYuODUgMCwtOC45NSAtMy44OSwtMTguMTkgLTEzLjQyLC0yMy44MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg0MzQiPjwvcGF0aD48cGF0aCBkPSJNIDE5NzAuNjIsNjQ0LjM1OSBWIDU3Ny45MyIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6MTA7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoNDM2Ij48L3BhdGg+PHBhdGggZD0iTSAyMzgyLjgsNjQ0LjM1OSBWIDU3Ny45MyIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6MTA7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoNDM4Ij48L3BhdGg+PHBhdGggZD0iTSAyNzk0Ljk5LDY0NC4zNTkgViA1NzcuOTMiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjEwO3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDQ0MCI+PC9wYXRoPjxwYXRoIGQ9Ik0gMzIwNy4xOCw2NDQuMzU5IFYgNTc3LjkzIiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoxMDtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGg0NDIiPjwvcGF0aD48cGF0aCBkPSJNIDM2MTkuMzcsNjQ0LjM1OSBWIDU3Ny45MyIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6MTA7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoNDQ0Ij48L3BhdGg+PHBhdGggZD0iTSA0MDMxLjU2LDY0NC4zNTkgViA1NzcuOTMiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjEwO3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDQ0NiI+PC9wYXRoPjxwYXRoIGQ9Ik0gNDQ0My43NSw2NDQuMzU5IFYgNTc3LjkzIiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoxMDtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGg0NDgiPjwvcGF0aD48cGF0aCBkPSJNIDQ4NTUuOTMsNjQ0LjM1OSBWIDU3Ny45MyIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6MTA7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoNDUwIj48L3BhdGg+PHBhdGggZD0iTSA1MjY4LjEyLDY0NC4zNTkgViA1NzcuOTMiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjEwO3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDQ1MiI+PC9wYXRoPjxwYXRoIGQ9Ik0gNTY4MC4zMSw2NDQuMzU5IFYgNTc3LjkzIiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoxMDtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGg0NTQiPjwvcGF0aD48cGF0aCBkPSJNIDYwOTIuNSw2NDQuMzU5IFYgNTc3LjkzIiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoxMDtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGg0NTYiPjwvcGF0aD48cGF0aCBkPSJNIDY1MDQuNjgsNjQ0LjM1OSBWIDU3Ny45MyIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6MTA7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoNDU4Ij48L3BhdGg+PHBhdGggZD0iTSA2OTE2Ljg3LDY0NC4zNTkgViA1NzcuOTMiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjEwO3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDQ2MCI+PC9wYXRoPjxwYXRoIGQ9Ik0gNzMyOS4wNiw2NDQuMzU5IFYgNTc3LjkzIiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoxMDtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGg0NjIiPjwvcGF0aD48cGF0aCBkPSJNIDc3NDEuMjUsNjQ0LjM1OSBWIDU3Ny45MyIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6MTA7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoNDY0Ij48L3BhdGg+PHBhdGggZD0iTSA4MTUzLjQzLDY0NC4zNTkgViA1NzcuOTMiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjEwO3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDQ2NiI+PC9wYXRoPjxwYXRoIGQ9Ik0gMjU4LjE1Niw2MTEuMTQ4IEggODIzMC4wMSIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6MTA7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoNDY4Ij48L3BhdGg+PHBhdGggZD0ibSAxOTc5LjEyLDc4My4zNCBjIC05LjM4LDAgLTE0Ljc5LC05LjExIC0xNC43OSwtMjUuNjIxIDAsLTE2LjUgNS40MSwtMjUuNTk4IDE0Ljc5LC0yNS41OTggOS40NywwIDE0Ljg4LDkuMDk4IDE0Ljg4LDI1LjU5OCAwLDE2LjUxMSAtNS40MSwyNS42MjEgLTE0Ljg4LDI1LjYyMSB6IG0gMCw4LjE5OSBjIDE3LjUsMCAyNi4wNiwtMTMuODAxIDI2LjA2LC0zMy44MiAwLC0yMC4wOTggLTguNTYsLTMzLjg5OSAtMjYuMDYsLTMzLjg5OSAtMTcuNCwwIC0yNS45NywxMy44MDEgLTI1Ljk3LDMzLjg5OSAwLDIwLjAxOSA4LjU3LDMzLjgyIDI1Ljk3LDMzLjgyIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQ3MCI+PC9wYXRoPjxwYXRoIGQ9Im0gMjM3NS42OSw3NzQuNzYyIGggLTE0LjYgdiA3LjQwNiBjIDkuNDYsMC4yNjIgMTQuMDYsMS4wNyAxNy40LDguMjAzIGggNy45NCB2IC02NS4zODMgaCAtMTAuNzQgdiA0OS43NzQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNDcyIj48L3BhdGg+PHBhdGggZD0ibSAyNzg0Ljg0LDczNC4zNTkgaCAzNC4yNiB2IC05LjM3MSBoIC00Ny42MSB2IDguODQgYyAyMS44MiwxNy4wNDMgMzQuOSwyOC41ODIgMzQuOSwzOS41IDAsNi4zMTMgLTQuMTUsMTAuMDEyIC0xMC41NSwxMC4wMTIgLTYuMjIsMCAtMTIuMTgsLTMuNjk5IC0xMi4xOCwtMTMuODkxIGggLTEwLjczIGMgLTAuMTgsMTMuMTcyIDkuMDIsMjIuMDkgMjMuMzYsMjIuMDkgMTIuMDksMCAyMS4yOCwtNi4yMTkgMjEuMjgsLTE3LjMwOSAwLC0xMy41MzEgLTEyLjk4LC0yNi4xNiAtMzIuNzMsLTM5Ljg3MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg0NzQiPjwvcGF0aD48cGF0aCBkPSJtIDMyMDQuODcsNzU0LjY2IGggLTMuMTUgdiA4LjkxOCBoIDIuNyBjIDEwLjE5LDAgMTUuMTUsMy4zNCAxNS4xNSwxMC4xMTMgMCw2LjU3OSAtNS4zMiw5LjY0OSAtMTEuMzcsOS42NDkgLTcuOTMsMCAtMTIuMzUsLTQuNzg5IC0xMy4zNCwtMTIuNDQ5IGggLTEwLjQ2IGMgMC45OSwxMi40NDkgOS45MiwyMC42NDggMjQuNDQsMjAuNjQ4IDEwLjkxLDAgMjEuNzMsLTQuOTYxIDIxLjczLC0xNy4yMyAwLC02LjQ4OSAtMy43OSwtMTEuODk5IC05LjU2LC0xNC42ODggNy44NSwtMi44ODMgMTEuMjcsLTkuMjkzIDExLjI3LC0xNS45NjEgMCwtMTMuMzUxIC0xMS40NSwtMTkuODQgLTI0LjUyLC0xOS44NCAtMTUuMTYsMCAtMjMuMzYsOS45MTggLTI0LjE3LDIxLjQ2MSBoIDEwLjQ2IGMgMS4wOCwtNy4yMjIgNS4zMiwtMTMuMTYgMTMuODksLTEzLjE2IDcuNTcsMCAxMy4yNSw0LjEzNyAxMy4yNSwxMS4yNyAwLDguMzkgLTYuNjcsMTEuMjY5IC0xNi4zMiwxMS4yNjkiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNDc2Ij48L3BhdGg+PHBhdGggZD0ibSAzNjI2LjgsNzQ5LjYwOSB2IDI2Ljc4MiBsIC0yMC41NiwtMjYuNzgyIHogbSAxMC43MywtOS4yODkgdiAtMTUuMzMyIGggLTEwLjczIHYgMTUuMzMyIGggLTMyLjI5IHYgOC45MyBsIDMyLjM4LDQxLjEyMSBoIDEwLjY0IHYgLTQwLjc2MiBoIDExLjU0IHYgLTkuMjg5IGggLTExLjU0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQ3OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNDAzMi41OCw3NjAuMzQgYyAtNi4wNCwwIC0xMC40NiwtMy4wNyAtMTEuODEsLTYuODYgbCAtMTAuMSwwLjU0IDQuMzMsMzYuMzUxIGggMzkuMTMgdiAtOS40NzMgaCAtMzAuMyBsIC0yLjA3LC0xNi40MSBjIDMuMTUsMi41MjQgNy42Nyw0LjA1MSAxMy41Miw0LjA1MSAxMS4xOSwwIDIxLjU2LC03LjY2IDIxLjU2LC0yMi4zNTkgMCwtMTQuNjEgLTExLjE4LC0yMi4zNiAtMjQuMTcsLTIyLjM2IC0xNS4yNCwwIC0yMyw5LjkxOCAtMjMuODEsMjEuMTg4IGggMTAuMzcgYyAwLjkxLC03LjU3OCA1LjA1LC0xMi44ODcgMTMuNjIsLTEyLjg4NyA3LjIxLDAgMTIuOSw1LjEyOSAxMi45LDEzLjg3OSAwLDkuNzM4IC02LjY4LDE0LjM0IC0xMy4xNywxNC4zNCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg0ODAiPjwvcGF0aD48cGF0aCBkPSJtIDQ0NTksNzQ2IGMgMCw4LjU3IC01LjMyLDEzLjk4IC0xMi43MSwxMy45OCAtNy40LDAgLTEyLjgxLC01LjQxIC0xMi44MSwtMTMuOTggMCwtOC42NiA1LjMyLC0xMy44NzkgMTIuNzIsLTEzLjg3OSA3LjQ4LDAgMTIuOCw1LjIxOSAxMi44LDEzLjg3OSB6IG0gLTEwLjYzLDIyLjQ2MSBjIDEyLjA4LDAgMjEuNzIsLTguNjcyIDIxLjcyLC0yMi4yODEgMCwtMTMuMDc4IC05LjczLC0yMi4zNiAtMjMuOCwtMjIuMzYgLTE2Ljk2LDAgLTI0LjU0LDEyLjgwMSAtMjQuNTQsMzEuOTE4IDAsMTguODUyIDYuODYsMzUuODAxIDI1Ljk4LDM1LjgwMSAxMy43LDAgMjAuMiwtOC44NCAyMS4xLC0xNy41OSBoIC0xMC45MSBjIC0wLjczLDYuMzIxIC01LjE0LDkuMzkxIC0xMSw5LjM5MSAtOC44NCwwIC0xNC4wNywtOC45NDIgLTE0LjI1LC0yMi4zNzEgMi44OCw0LjE1MiA4LjIxLDcuNDkyIDE1LjcsNy40OTIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNDgyIj48L3BhdGg+PHBhdGggZD0ibSA0ODcyLjU0LDc5MC4zNzEgdiAtOS40NzMgYyAtMTYuNjgsLTE1Ljc3NyAtMjUuNjEsLTMxLjkyOSAtMjcuMDYsLTU1LjkxIGggLTEyLjE3IGMgMS4xNywyMyAxMi42Miw0Mi4wMjQgMjcuODcsNTUuOTEgaCAtMzUuNjMgdiA5LjQ3MyBoIDQ2Ljk5IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQ4NCI+PC9wYXRoPjxwYXRoIGQ9Im0gNTI1NC42OSw3NzMuNDE4IGMgMCwtNi4yMTkgNC43OSwtMTAuMzY3IDExLjgyLC0xMC4zNjcgNy4xMywwIDExLjczLDQuMTQ4IDExLjczLDEwLjM2NyAwLDYuMjIzIC00LjYsOS45MjIgLTExLjczLDkuOTIyIC03LjAzLDAgLTExLjgyLC0zLjY5OSAtMTEuODIsLTkuOTIyIHogbSAxMS44MiwtNDEuMjk3IGMgOC4wMywwIDEzLjE2LDQuNDEgMTMuMTYsMTEuODAxIDAsNy4zMDggLTUuMTMsMTEuODE2IC0xMy4xNiwxMS44MTYgLTguMDMsMCAtMTMuMTYsLTQuNTA4IC0xMy4xNiwtMTEuODE2IDAsLTcuMzkxIDUuMTMsLTExLjgwMSAxMy4xNiwtMTEuODAxIHogbSAxMy45NywyNy43NyBjIDcuNzcsLTMuOTczIDEwLjM4LC0xMC4xOTIgMTAuMzgsLTE2LjMzMiAwLC0xMi44OTEgLTEwLjY0LC0xOS43MzkgLTI0LjM1LC0xOS43MzkgLTEzLjcxLDAgLTI0LjM1LDYuODQ4IC0yNC4zNSwxOS43MzkgMCw2LjE0IDIuNjIsMTIuNDUzIDEwLjM4LDE2LjMzMiAtNS43OCwzLjIzOCAtOC4zOSw5LjI4OSAtOC4zOSwxNC44NzEgMCw5Ljc1IDguNjUsMTYuNzc3IDIyLjM2LDE2Ljc3NyAxMy42MSwwIDIyLjM2LC03LjAyNyAyMi4zNiwtMTYuNzc3IDAsLTUuNTgyIC0yLjQzLC0xMS4zNTIgLTguMzksLTE0Ljg3MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg0ODYiPjwvcGF0aD48cGF0aCBkPSJtIDU2NjQuMjcsNzY5LjM1MiBjIDAsLTguNTYzIDUuMzIsLTEzLjk3MyAxMi43MiwtMTMuOTczIDcuMywwIDEyLjgsNS40MSAxMi44LDEzLjk3MyAwLDguNzUgLTUuNDEsMTMuOTg4IC0xMi43MSwxMy45ODggLTcuNDksMCAtMTIuODEsLTUuMjM4IC0xMi44MSwtMTMuOTg4IHogbSAxMC42NCwtMjIuNDU0IGMgLTEyLjA4LDAgLTIxLjczLDguNjUzIC0yMS43MywyMi4zNzIgMCwxMi45OCA5Ljc0LDIyLjI2OSAyMy44MSwyMi4yNjkgMTYuOTUsMCAyNC41MiwtMTIuODAxIDI0LjUyLC0zMS45MTggMCwtMTguODUxIC02Ljk0LC0zNS44MDEgLTI2LjA1LC0zNS44MDEgLTEzLjYzLDAgLTIwLjEyLDguODI4IC0yMS4wMiwxNy41NzggaCAxMC45MSBjIDAuNzIsLTYuMzA4IDUuMTQsLTkuMjc3IDExLC05LjI3NyA4Ljg0LDAgMTQuMDgsOC45MTggMTQuMjUsMjIuMjU4IC0yLjg4LC00LjE0MSAtOC4yLC03LjQ4MSAtMTUuNjksLTcuNDgxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQ4OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNjA3Ny4wMSw3NzQuNzYyIGggLTE0LjYxIHYgNy40MDYgYyA5LjQ3LDAuMjYyIDE0LjA3LDEuMDcgMTcuNCw4LjIwMyBoIDcuOTQgdiAtNjUuMzgzIGggLTEwLjczIHYgNDkuNzc0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQ5MCI+PC9wYXRoPjxwYXRoIGQ9Im0gNjEyMi4yNyw3ODMuMzQgYyAtOS4zNywwIC0xNC43OSwtOS4xMSAtMTQuNzksLTI1LjYyMSAwLC0xNi41IDUuNDIsLTI1LjU5OCAxNC43OSwtMjUuNTk4IDkuNDYsMCAxNC44OCw5LjA5OCAxNC44OCwyNS41OTggMCwxNi41MTEgLTUuNDIsMjUuNjIxIC0xNC44OCwyNS42MjEgeiBtIDAsOC4xOTkgYyAxNy40OSwwIDI2LjA3LC0xMy44MDEgMjYuMDcsLTMzLjgyIDAsLTIwLjA5OCAtOC41OCwtMzMuODk5IC0yNi4wNywtMzMuODk5IC0xNy40LDAgLTI1Ljk3LDEzLjgwMSAtMjUuOTcsMzMuODk5IDAsMjAuMDE5IDguNTcsMzMuODIgMjUuOTcsMzMuODIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNDkyIj48L3BhdGg+PHBhdGggZD0ibSA2NDg5LjIsNzc0Ljc2MiBoIC0xNC42MSB2IDcuNDA2IGMgOS40NywwLjI2MiAxNC4wNywxLjA3IDE3LjQsOC4yMDMgaCA3Ljk0IHYgLTY1LjM4MyBoIC0xMC43MyB2IDQ5Ljc3NCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg0OTQiPjwvcGF0aD48cGF0aCBkPSJtIDY1MjEuNjYsNzc0Ljc2MiBoIC0xNC42MSB2IDcuNDA2IGMgOS40NywwLjI2MiAxNC4wNywxLjA3IDE3LjQsOC4yMDMgaCA3Ljk0IHYgLTY1LjM4MyBoIC0xMC43MyB2IDQ5Ljc3NCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg0OTYiPjwvcGF0aD48cGF0aCBkPSJtIDY4OTkuNCw3NzQuNzYyIGggLTE0LjYxIHYgNy40MDYgYyA5LjQ3LDAuMjYyIDE0LjA3LDEuMDcgMTcuNCw4LjIwMyBoIDcuOTQgdiAtNjUuMzgzIGggLTEwLjczIHYgNDkuNzc0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDQ5OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNjkzMC41MSw3MzQuMzU5IGggMzQuMjcgdiAtOS4zNzEgaCAtNDcuNjIgdiA4Ljg0IGMgMjEuODMsMTcuMDQzIDM0LjkxLDI4LjU4MiAzNC45MSwzOS41IDAsNi4zMTMgLTQuMTUsMTAuMDEyIC0xMC41NSwxMC4wMTIgLTYuMjIsMCAtMTIuMTgsLTMuNjk5IC0xMi4xOCwtMTMuODkxIGggLTEwLjczIGMgLTAuMTgsMTMuMTcyIDkuMDIsMjIuMDkgMjMuMzYsMjIuMDkgMTIuMDgsMCAyMS4yOCwtNi4yMTkgMjEuMjgsLTE3LjMwOSAwLC0xMy41MzEgLTEyLjk5LC0yNi4xNiAtMzIuNzQsLTM5Ljg3MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1MDAiPjwvcGF0aD48cGF0aCBkPSJtIDczMTAuMDcsNzc0Ljc2MiBoIC0xNC42IHYgNy40MDYgYyA5LjQ3LDAuMjYyIDE0LjA3LDEuMDcgMTcuNCw4LjIwMyBoIDcuOTQgdiAtNjUuMzgzIGggLTEwLjc0IHYgNDkuNzc0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDUwMiI+PC9wYXRoPjxwYXRoIGQ9Im0gNzM0OS4wMiw3NTQuNjYgaCAtMy4xNSB2IDguOTE4IGggMi43IGMgMTAuMiwwIDE1LjE2LDMuMzQgMTUuMTYsMTAuMTEzIDAsNi41NzkgLTUuMzMsOS42NDkgLTExLjM3LDkuNjQ5IC03LjkzLDAgLTEyLjM1LC00Ljc4OSAtMTMuMzUsLTEyLjQ0OSBoIC0xMC40NiBjIDEsMTIuNDQ5IDkuOTIsMjAuNjQ4IDI0LjQ0LDIwLjY0OCAxMC45MSwwIDIxLjczLC00Ljk2MSAyMS43MywtMTcuMjMgMCwtNi40ODkgLTMuNzksLTExLjg5OSAtOS41NiwtMTQuNjg4IDcuODUsLTIuODgzIDExLjI4LC05LjI5MyAxMS4yOCwtMTUuOTYxIDAsLTEzLjM1MSAtMTEuNDUsLTE5Ljg0IC0yNC41MywtMTkuODQgLTE1LjE1LDAgLTIzLjM2LDkuOTE4IC0yNC4xNywyMS40NjEgaCAxMC40NiBjIDEuMDgsLTcuMjIyIDUuMzIsLTEzLjE2IDEzLjg5LC0xMy4xNiA3LjU3LDAgMTMuMjYsNC4xMzcgMTMuMjYsMTEuMjcgMCw4LjM5IC02LjY3LDExLjI2OSAtMTYuMzMsMTEuMjY5IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDUwNCI+PC9wYXRoPjxwYXRoIGQ9Im0gNzcwOS44MSw3NzQuNzYyIGggLTE0LjYxIHYgNy40MDYgYyA5LjQ3LDAuMjYyIDE0LjA3LDEuMDcgMTcuNCw4LjIwMyBoIDcuOTQgdiAtNjUuMzgzIGggLTEwLjczIHYgNDkuNzc0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDUwNiI+PC9wYXRoPjxwYXRoIGQ9Im0gNzc1OC41MSw3NDkuNjA5IHYgMjYuNzgyIGwgLTIwLjU2LC0yNi43ODIgeiBtIDEwLjczLC05LjI4OSB2IC0xNS4zMzIgaCAtMTAuNzMgdiAxNS4zMzIgaCAtMzIuMjggdiA4LjkzIGwgMzIuMzcsNDEuMTIxIGggMTAuNjQgdiAtNDAuNzYyIGggMTEuNTUgdiAtOS4yODkgaCAtMTEuNTUiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTA4Ij48L3BhdGg+PHBhdGggZD0ibSA4MTMyLjE5LDc3NC43NjIgaCAtMTQuNjEgdiA3LjQwNiBjIDkuNDgsMC4yNjIgMTQuMDgsMS4wNyAxNy40MSw4LjIwMyBoIDcuOTQgdiAtNjUuMzgzIGggLTEwLjc0IHYgNDkuNzc0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDUxMCI+PC9wYXRoPjxwYXRoIGQ9Im0gODE3NC40OSw3NjAuMzQgYyAtNi4wNSwwIC0xMC40NiwtMy4wNyAtMTEuODIsLTYuODYgbCAtMTAuMSwwLjU0IDQuMzMsMzYuMzUxIGggMzkuMTQgdiAtOS40NzMgaCAtMzAuMyBsIC0yLjA3LC0xNi40MSBjIDMuMTUsMi41MjQgNy42Niw0LjA1MSAxMy41Miw0LjA1MSAxMS4xOSwwIDIxLjU2LC03LjY2IDIxLjU2LC0yMi4zNTkgMCwtMTQuNjEgLTExLjE5LC0yMi4zNiAtMjQuMTcsLTIyLjM2IC0xNS4yNCwwIC0yMi45OSw5LjkxOCAtMjMuODEsMjEuMTg4IGggMTAuMzcgYyAwLjkxLC03LjU3OCA1LjA2LC0xMi44ODcgMTMuNjIsLTEyLjg4NyA3LjIyLDAgMTIuODksNS4xMjkgMTIuODksMTMuODc5IDAsOS43MzggLTYuNjcsMTQuMzQgLTEzLjE2LDE0LjM0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDUxMiI+PC9wYXRoPjxwYXRoIGQ9Im0gMzA1Ljk2OSw2NTUuODk4IGMgLTI2Ljc1NCwwIC00Mi4yNzgsMTkuMDUxIC00Mi4yNzgsNDcuNjkyIDAsMjguNzgxIDE2LjUzNiw0Ny4wNyA0My4wMzYsNDcuMDcgMjAuMzE2LDAgMzQuODI4LC0xMS42MDEgMzguNDg0LC0zMi4wNTEgaCAtMTUuMzk1IGMgLTIuNzczLDEyLjM3MSAtMTEuNzM0LDE4LjkzIC0yMy41OTcsMTguOTMgLTE0LjUxNiwwIC0yNS45OTIsLTExLjg1OSAtMjUuOTkyLC0zMy45NDkgMCwtMjIuMTk5IDExLjIzLC0zNC41NyAyNS44NjcsLTM0LjU3IDEyLjM2MywwIDIxLjE5NSw2LjQ0MSAyMy45NzYsMTguOTI5IGggMTUuMzk1IGMgLTMuNzg1LC0yMC40MzcgLTE4LjQyMiwtMzIuMDUxIC0zOS40OTYsLTMyLjA1MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1MTQiPjwvcGF0aD48cGF0aCBkPSJtIDM3OC43MjMsNjU1Ljg5OCBjIC0xNi4xNTMsMCAtMjIuNzE1LDEwLjU5IC0yMi43MTUsMjYuNzQzIHYgNDIuNzg5IGggMTUuMDE1IHYgLTM5LjEyMSBjIDAsLTkuMjA3IDEuMjU4LC0xOC4xOCAxMi40OTMsLTE4LjE4IDExLjIzLDAgMTUuMjY5LDguODQgMTUuMjY5LDIxLjA4MiB2IDM2LjIxOSBoIDE1LjAxNiB2IC02Ny44OTEgaCAtMTUuMDE2IHYgOS4zMzIgYyAtMy45MSwtNy4wNjIgLTEwLjg1NSwtMTAuOTczIC0yMC4wNjIsLTEwLjk3MyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1MTYiPjwvcGF0aD48cGF0aCBkPSJtIDQ1OC4wNTksNzEwLjUzOSBjIC05LjQ2OSwwIC0xNC44OTUsLTMuNzc3IC0xNC44OTUsLTE3LjQxOCB2IC0zNS41ODIgaCAtMTUuMDEyIHYgNjcuODkxIGggMTQuNzU4IHYgLTEyLjEyMSBjIDMuNjY0LDcuNTgyIDEwLjIyNywxMi4xMjEgMTguNDI2LDEyLjI0MiAxLjEzNywwIDIuNzc3LC0wLjEyMSAzLjkxNCwtMC4yNSB2IC0xNS4xNTMgYyAtMi41MjMsMC4yNjIgLTQuOTIyLDAuMzkxIC03LjE5MSwwLjM5MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1MTgiPjwvcGF0aD48cGF0aCBkPSJtIDUwMi4wNjMsNzEwLjUzOSBjIC05LjQ2NSwwIC0xNC44ODcsLTMuNzc3IC0xNC44ODcsLTE3LjQxOCBWIDY1Ny41MzkgSCA0NzIuMTYgdiA2Ny44OTEgaCAxNC43NjIgdiAtMTIuMTIxIGMgMy42Niw3LjU4MiAxMC4yMjMsMTIuMTIxIDE4LjQyMiwxMi4yNDIgMS4xMzYsMCAyLjc3NywtMC4xMjEgMy45MTQsLTAuMjUgdiAtMTUuMTUzIGMgLTIuNTI0LDAuMjYyIC00LjkyMiwwLjM5MSAtNy4xOTUsMC4zOTEiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTIwIj48L3BhdGg+PHBhdGggZD0ibSA1NjAuNzE1LDY5OC4xNjggYyAtMC4zNzUsMTAuNjAyIC04LjQ1MywxNy4wMzEgLTE3LjI4NSwxNy4wMzEgLTcuMDY3LDAgLTE2Ljc4MiwtNC4xNiAtMTguMDQ3LC0xNy4wMzEgeiBtIC0xNi45MSwtMjkuNzc3IGMgNy44MjgsMCAxNC4wMDgsMy4xNDggMTYuNjYsOS40NjEgSCA1NzUuMjMgQyA1NzIuMDcsNjY3IDU2MS45OCw2NTUuODk4IDU0NC40NDEsNjU1Ljg5OCBjIC0yMS44MzIsMCAtMzQuMzI4LDE2LjY2MSAtMzQuMzI4LDM2LjA5IDAsMjAuNDQyIDE0LjAwOCwzNC45NTMgMzMuMzE3LDM0Ljk1MyAyMC44MiwwIDMzLjgxNiwtMTYuOTAyIDMyLjU1OCwtMzkuNzQyIGggLTUwLjYwNSBjIDEuMDEyLC0xMi42MjkgOS44NDQsLTE4LjgwOCAxOC40MjIsLTE4LjgwOCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1MjIiPjwvcGF0aD48cGF0aCBkPSJtIDYyMS4zNjcsNzI2Ljk0MSBjIDE2LjQwNiwwIDIzLjA5OCwtMTAuNTg5IDIzLjA5OCwtMjYuNzUgdiAtNDIuNjUyIGggLTE1LjAyIHYgMzguOTkyIGMgMCw5LjIwNyAtMS4zODYsMTguMTggLTEyLjg3MSwxOC4xOCAtMTEuNDgsMCAtMTUuNzczLC04Ljg0IC0xNS43NzMsLTIxLjA4MiB2IC0zNi4wOSBoIC0xNS4wMTYgdiA2Ny44OTEgaCAxNS4wMTYgdiAtOS40NjEgYyAzLjkxNCw3LjA2MiAxMS4xMDUsMTAuOTcyIDIwLjU2NiwxMC45NzIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTI0Ij48L3BhdGg+PHBhdGggZD0iTSA2NzQuNzA3LDc0My4zNTIgViA3MjUuNDMgaCAxMy42MjkgdiAtMTAuODUyIGggLTEzLjYyOSB2IC0zNi45NjkgYyAwLC02Ljk0OSAxLjY0MSwtOC41ODkgOC4wNzgsLTguNTg5IGggNS40MyB2IC0xMS40ODEgaCAtMTEuMTEgYyAtMTQuNTExLDAgLTE3LjQxLDMuOTEgLTE3LjQxLDE3Ljc4OSB2IDM5LjI1IGggLTEwLjA5NyB2IDEwLjg1MiBoIDEwLjA5NyB2IDE3LjkyMiBoIDE1LjAxMiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1MjYiPjwvcGF0aD48cGF0aCBkPSJtIDc2My43NTgsNjU1Ljg5OCBjIC0yNi43NTQsMCAtNDIuMjc4LDE5LjA1MSAtNDIuMjc4LDQ3LjY5MiAwLDI4Ljc4MSAxNi41MzYsNDcuMDcgNDMuMDMyLDQ3LjA3IDIwLjMxNiwwIDM0LjgzMiwtMTEuNjAxIDM4LjQ4OCwtMzIuMDUxIGggLTE1LjM5NSBjIC0yLjc3NywxMi4zNzEgLTExLjczNCwxOC45MyAtMjMuNjAxLDE4LjkzIC0xNC41MTIsMCAtMjUuOTg4LC0xMS44NTkgLTI1Ljk4OCwtMzMuOTQ5IDAsLTIyLjE5OSAxMS4yMjYsLTM0LjU3IDI1Ljg2NywtMzQuNTcgMTIuMzYzLDAgMjEuMTk1LDYuNDQxIDIzLjk3NiwxOC45MjkgaCAxNS4zOTUgYyAtMy43ODUsLTIwLjQzNyAtMTguNDI2LC0zMi4wNTEgLTM5LjQ5NiwtMzIuMDUxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDUyOCI+PC9wYXRoPjxwYXRoIGQ9Im0gODEzLjQyNiw2NTcuNTM5IHYgOTEuNDgxIGggMTUuMDEyIHYgLTkxLjQ4MSBoIC0xNS4wMTIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTMwIj48L3BhdGg+PHBhdGggZD0ibSA4ODkuNjIxLDY5MS4zNTkgYyAwLDE1LjY0MSAtOC40NTcsMjMuMzUyIC0xNy45MjIsMjMuMzUyIC05LjQ2NSwwIC0xNy45MTgsLTcuNzExIC0xNy45MTgsLTIzLjM1MiAwLC0xNS42NDggOC40NTMsLTIzLjIzIDE3LjkxOCwtMjMuMjMgOS40NjUsMCAxNy45MjIsNy41ODIgMTcuOTIyLDIzLjIzIHogbSAtMTcuOTIyLC0zNS40NjEgYyAtMTYuNTMxLDAgLTMzLjQ0MSwxMC45NzMgLTMzLjQ0MSwzNS40NjEgMCwyNC40ODEgMTYuOTEsMzUuNTgyIDMzLjQ0MSwzNS41ODIgMTYuNTMxLDAgMzMuNDM4LC0xMS4xMDEgMzMuNDM4LC0zNS41ODIgMCwtMjQuNDg4IC0xNi45MDcsLTM1LjQ2MSAtMzMuNDM4LC0zNS40NjEiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTMyIj48L3BhdGg+PHBhdGggZD0ibSA5NjAuMTE3LDcwMi4yMTEgYyAtMS4yNjIsNy4xODcgLTcuNTcsMTIuMjM4IC0xNS43NzMsMTIuMjM4IC05LjMzNiwwIC0xNy43OTMsLTYuOTQxIC0xNy43OTMsLTIyLjk2OSAwLC0xNi4xNTIgOC41NzgsLTIzLjA4OSAxNy40MTQsLTIzLjA4OSA3LjMxNiwwIDE0Ljc2MiwzLjI4MSAxNi42NTYsMTIuMzcxIGggMTQuNjQxIGMgLTMuMDI4LC0xNS45MSAtMTcuMDM5LC0yNC44NjQgLTMxLjU1MSwtMjQuODY0IC0xOS42ODgsMCAtMzIuNjg0LDE1LjI3IC0zMi42ODQsMzUuNDYxIDAsMjAuMTkyIDEzLjEyNSwzNS41ODIgMzMuMzE3LDM1LjU4MiAxNC43NjUsMCAyNy44OSwtOS41ODkgMzAuNDEsLTI0LjczIGggLTE0LjYzNyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1MzQiPjwvcGF0aD48cGF0aCBkPSJtIDk5OS4zMTYsNjk4LjE2OCAyNS4xMTQsMjcuMjYyIGggMTguMDQgbCAtMjUuOTksLTI3Ljg5MSAyOC45LC00MCBoIC0xNy41NCBsIC0yMS4zMywyOS40MDIgLTcuMTk0LC03LjY5MSB2IC0yMS43MTEgaCAtMTUuMDExIHYgOTEuNDgxIGggMTUuMDExIHYgLTUwLjg1MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1MzYiPjwvcGF0aD48cGF0aCBkPSJNIDc2NDMuNjEsMjIxLjg5OCBWIDE1NS40OCIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6MTA7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoNTM4Ij48L3BhdGg+PHBhdGggZD0iTSA3MjMxLjQyLDIyMS44OTggViAxNTUuNDgiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjEwO3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDU0MCI+PC9wYXRoPjxwYXRoIGQ9Ik0gODA1NS44LDIyMS44OTggViAxNTUuNDgiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjEwO3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDU0MiI+PC9wYXRoPjxwYXRoIGQ9Ik0gMjU4LjE1NiwxODguNjkxIEggODIzMC4wMSIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6MTA7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoNTQ0Ij48L3BhdGg+PHBhdGggZD0ibSA3MjA2LjY1LDUwLjk0OTIgaCAtMTQuNjEgdiA3LjQwMjQgYyA5LjQ3LDAuMjU3OCAxNC4wNywxLjA2NjQgMTcuNCw4LjE5OTIgaCA3Ljk0IFYgMS4xNjc5NyBoIC0xMC43MyBWIDUwLjk0OTIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTQ2Ij48L3BhdGg+PHBhdGggZD0ibSA3MjM3Ljc2LDEwLjU1MDggaCAzNC4yNyBWIDEuMTY3OTcgaCAtNDcuNjIgdiA4Ljg0MzczIGMgMjEuODMsMTcuMDM5MSAzNC45LDI4LjU3ODEgMzQuOSwzOS41IDAsNi4zMDg2IC00LjE1LDEwLjAwNzggLTEwLjU0LDEwLjAwNzggLTYuMjIsMCAtMTIuMTgsLTMuNjk5MiAtMTIuMTgsLTEzLjg5MDYgaCAtMTAuNzMgYyAtMC4xOCwxMy4xNzE5IDkuMDIsMjIuMDg5OSAyMy4zNiwyMi4wODk5IDEyLjA4LDAgMjEuMjcsLTYuMjE4OCAyMS4yNywtMTcuMzA4NiAwLC0xMy41MzEzIC0xMi45OCwtMjYuMTQ4NSAtMzIuNzMsLTM5Ljg1OTQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTQ4Ij48L3BhdGg+PHBhdGggZD0ibSA3NjEzLjc0LDUwLjk0OTIgaCAtMTQuNjEgdiA3LjQwMjQgYyA5LjQ3LDAuMjU3OCAxNC4wNywxLjA2NjQgMTcuNCw4LjE5OTIgaCA3Ljk0IFYgMS4xNjc5NyBoIC0xMC43MyBWIDUwLjk0OTIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTUwIj48L3BhdGg+PHBhdGggZD0ibSA3NjUyLjY5LDMwLjgzOTggaCAtMy4xNSB2IDguOTIxOSBoIDIuNyBjIDEwLjIsMCAxNS4xNiwzLjMzOTkgMTUuMTYsMTAuMTA5NCAwLDYuNTc4MSAtNS4zMiw5LjY0ODQgLTExLjM3LDkuNjQ4NCAtNy45MywwIC0xMi4zNSwtNC43ODkgLTEzLjM1LC0xMi40NDkyIGggLTEwLjQ2IGMgMSwxMi40NDkyIDkuOTIsMjAuNjQ4NSAyNC40NSwyMC42NDg1IDEwLjksMCAyMS43MiwtNC45NjEgMjEuNzIsLTE3LjIxODggMCwtNi41IC0zLjc4LC0xMS45MTAyIC05LjU2LC0xNC42OTkyIDcuODYsLTIuODkwNiAxMS4yOCwtOS4yOTMgMTEuMjgsLTE1Ljk2MSBDIDc2ODAuMTEsNi40ODgyOCA3NjY4LjY2LDAgNzY1NS41OCwwIGMgLTE1LjE0LDAgLTIzLjM2LDkuOTE3OTcgLTI0LjE3LDIxLjQ2MDkgaCAxMC40NiBjIDEuMDksLTcuMjEwOSA1LjMyLC0xMy4xNjAxMiAxMy44OSwtMTMuMTYwMTIgNy41OCwwIDEzLjI2LDQuMTQwNjIgMTMuMjYsMTEuMjY5NTIgMCw4LjM5MDYgLTYuNjcsMTEuMjY5NSAtMTYuMzMsMTEuMjY5NSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1NTIiPjwvcGF0aD48cGF0aCBkPSJtIDgwMjcuMDIsNTAuOTQ5MiBoIC0xNC42MSB2IDcuNDAyNCBjIDkuNDcsMC4yNTc4IDE0LjA3LDEuMDY2NCAxNy40LDguMTk5MiBoIDcuOTQgViAxLjE2Nzk3IGggLTEwLjczIFYgNTAuOTQ5MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1NTQiPjwvcGF0aD48cGF0aCBkPSJtIDgwNzUuNzIsMjUuNzg5MSB2IDI2Ljc4OSBsIC0yMC41NywtMjYuNzg5IHogTSA4MDg2LjQ1LDE2LjUgViAxLjE2Nzk3IGggLTEwLjczIFYgMTYuNSBoIC0zMi4yOSB2IDguOTI5NyBsIDMyLjM4LDQxLjEyMTEgaCAxMC42NCBWIDI1Ljc4OTEgaCAxMS41NCBWIDE2LjUgaCAtMTEuNTQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTU2Ij48L3BhdGg+PHBhdGggZD0iTSAyODIuODcxLDMwOC4xNDggViAyMzUuMDkgaCAtMTUuNTE2IHYgOTEuNDggaCAyMS40NSBsIDM4Ljc0MiwtNzMuMDU4IHYgNzMuMDU4IGggMTUuNTE5IHYgLTkxLjQ4IGggLTIxLjQ1MyBsIC0zOC43NDIsNzMuMDU4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDU1OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNDA0LjIxMSwyNzUuNzE5IGMgLTAuMzc1LDEwLjYwMSAtOC40NTMsMTcuMDMxIC0xNy4yODUsMTcuMDMxIC03LjA2NywwIC0xNi43ODEsLTQuMTYgLTE4LjA0NywtMTcuMDMxIHogbSAtMTYuOTEsLTI5Ljc3OCBjIDcuODI4LDAgMTQuMDA4LDMuMTQ5IDE2LjY2LDkuNDU3IGggMTQuNzY2IGMgLTMuMTYxLC0xMC44NDcgLTEzLjI1LC0yMS45NDkgLTMwLjc4OSwtMjEuOTQ5IC0yMS44MzMsMCAtMzQuMzI5LDE2LjY2IC0zNC4zMjksMzYuMDkgMCwyMC40NDEgMTQuMDA4LDM0Ljk0OSAzMy4zMTcsMzQuOTQ5IDIwLjgyLDAgMzMuODE2LC0xNi45MSAzMi41NTgsLTM5Ljc1IGggLTUwLjYwNSBjIDEuMDEyLC0xMi42MTcgOS44NDQsLTE4Ljc5NyAxOC40MjIsLTE4Ljc5NyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1NjAiPjwvcGF0aD48cGF0aCBkPSJtIDQ3NC4zMzYsMzAyLjk4IDExLjczOCwtNDguMjEgOS45NjUsNDguMjEgaCAxNi4yODEgbCAtMTguMDQ3LC02Ny44OSBoIC0xNC4yNTcgbCAtMTMuMzc1LDUwLjIxOSAtMTMuMzc5LC01MC4yMTkgaCAtMTQuMjU4IGwgLTE4LjA0Nyw2Ny44OSBoIDE2LjI4MSBsIDkuOTY5LC00OC4yMSAxMS42MDksNDguMjEgaCAxNS41MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1NjIiPjwvcGF0aD48cGF0aCBkPSJtIDU4NC42ODQsMjMzLjQ0OSBjIC0yNi43NTQsMCAtNDIuMjc0LDE5LjA1MSAtNDIuMjc0LDQ3LjY5MiAwLDI4Ljc3NyAxNi41MzEsNDcuMDcgNDMuMDMxLDQ3LjA3IDIwLjMxNywwIDM0LjgyOSwtMTEuNjAyIDM4LjQ4NSwtMzIuMDUxIGggLTE1LjM5NSBjIC0yLjc3MywxMi4zNzEgLTExLjczNCwxOC45MyAtMjMuNTk3LDE4LjkzIC0xNC41MTIsMCAtMjUuOTkzLC0xMS44NiAtMjUuOTkzLC0zMy45NDkgMCwtMjIuMjExIDExLjIzMSwtMzQuNTcxIDI1Ljg3MiwtMzQuNTcxIDEyLjM2MywwIDIxLjE5NSw2LjQ0MiAyMy45NzIsMTguOTMgaCAxNS4zOTUgYyAtMy43ODIsLTIwLjQ0MSAtMTguNDIyLC0zMi4wNTEgLTM5LjQ5NiwtMzIuMDUxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDU2NCI+PC9wYXRoPjxwYXRoIGQ9Im0gNjM0LjM0OCwyMzUuMDkgdiA5MS40OCBoIDE1LjAxNSB2IC05MS40OCBoIC0xNS4wMTUiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTY2Ij48L3BhdGg+PHBhdGggZD0ibSA3MTAuNTQ3LDI2OC44OTggYyAwLDE1LjY1MyAtOC40NTcsMjMuMzUyIC0xNy45MTgsMjMuMzUyIC05LjQ2OSwwIC0xNy45MjIsLTcuNjk5IC0xNy45MjIsLTIzLjM1MiAwLC0xNS42MzYgOC40NTMsLTIzLjIxOCAxNy45MjIsLTIzLjIxOCA5LjQ2MSwwIDE3LjkxOCw3LjU4MiAxNy45MTgsMjMuMjE4IHogbSAtMTcuOTE4LC0zNS40NDkgYyAtMTYuNTM1LDAgLTMzLjQ0MSwxMC45NjkgLTMzLjQ0MSwzNS40NDkgMCwyNC40OTMgMTYuOTA2LDM1LjU5IDMzLjQ0MSwzNS41OSAxNi41MjcsMCAzMy40MzcsLTExLjA5NyAzMy40MzcsLTM1LjU5IDAsLTI0LjQ4IC0xNi45MSwtMzUuNDQ5IC0zMy40MzcsLTM1LjQ0OSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1NjgiPjwvcGF0aD48cGF0aCBkPSJtIDc4MS4wNDMsMjc5Ljc1IGMgLTEuMjY2LDcuMTk5IC03LjU3NCwxMi4yNSAtMTUuNzc3LDEyLjI1IC05LjMzNiwwIC0xNy43OTMsLTYuOTQxIC0xNy43OTMsLTIyLjk2OSAwLC0xNi4xNTIgOC41NzgsLTIzLjA5IDE3LjQxOCwtMjMuMDkgNy4zMTIsMCAxNC43NTcsMy4yNzggMTYuNjUyLDEyLjM2OCBoIDE0LjY0MSBjIC0zLjAyOCwtMTUuOTExIC0xNy4wMzYsLTI0Ljg2IC0zMS41NDcsLTI0Ljg2IC0xOS42ODgsMCAtMzIuNjg4LDE1LjI3IC0zMi42ODgsMzUuNDQ5IDAsMjAuMjA0IDEzLjEyNSwzNS41OSAzMy4zMTcsMzUuNTkgMTQuNzY1LDAgMjcuODksLTkuNTkgMzAuNDEsLTI0LjczOCBoIC0xNC42MzMiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTcwIj48L3BhdGg+PHBhdGggZD0ibSA4MjAuMjQyLDI3NS43MTkgMjUuMTEsMjcuMjYxIGggMTguMDQ2IGwgLTI1Ljk5NiwtMjcuODkgMjguODk5LC00MCBoIC0xNy41MzkgbCAtMjEuMzI4LDI5LjM5OCAtNy4xOTIsLTcuNjg3IFYgMjM1LjA5IGggLTE1LjAxNSB2IDkxLjQ4IGggMTUuMDE1IHYgLTUwLjg1MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1NzIiPjwvcGF0aD48cGF0aCBkPSJtIDI2My45NDUsMjM0Ni4wMyBjIDAsMTcuMTcgMTcuNzkzLDI1Ljc1IDM0LjU3OCwyNS43NSAxOC4wNDcsMCAzMi4xNzYsLTguMjEgMzUuODQsLTI3LjI2IEggMzE4Ljg0IGMgLTIuNjUyLDEwLjk4IC0xMi4yNDIsMTQuMTMgLTIxLjIwMywxNC4xMyAtNy4wNjMsMCAtMTcuNTM5LC0zLjE1IC0xNy41MzksLTEyLjExIDAsLTcuMDcgNS44MDgsLTEwLjU5IDEzLjYyOSwtMTIuMTIgbCAxMS4yMywtMi4xNCBjIDE2LjAyNywtMy4xNSAzMS4yOTMsLTguOTYgMzEuMjkzLC0yNy4zOCAwLC0xOC40MyAtMTguMjk3LC0yNy44OSAtMzYuMzQsLTI3Ljg5IC0yMS43MDcsMCAtMzYuNTk0LDExLjg3IC0zOC40ODgsMzEuOTIgaCAxNS43NzMgYyAyLjc3OCwtMTIuNDkgMTAuODUyLC0xOC44IDIzLjQ2OSwtMTguOCAxMC44NTYsMCAxOS41NjMsNC45MyAxOS41NjMsMTMuNzUgMCw5LjM1IC0xMC4wOTQsMTIuNSAtMTguODA1LDE0LjE1IGwgLTExLjEwMiwyLjEzIGMgLTE0LjM4NiwyLjkgLTI2LjM3NSwxMC4zNiAtMjYuMzc1LDI1Ljg3IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDU3NCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzYyLjk1MywyMzY0LjQ2IHYgLTE3LjkyIGggMTMuNjI5IHYgLTEwLjg1IGggLTEzLjYyOSB2IC0zNi45NyBjIDAsLTYuOTQgMS42NDUsLTguNTkgOC4wNzgsLTguNTkgaCA1LjQzIHYgLTExLjQ4IGggLTExLjEwOSBjIC0xNC41MTIsMCAtMTcuNDExLDMuOTIgLTE3LjQxMSwxNy43OSB2IDM5LjI1IGggLTEwLjA5NyB2IDEwLjg1IGggMTAuMDk3IHYgMTcuOTIgaCAxNS4wMTIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTc2Ij48L3BhdGg+PHBhdGggZD0ibSA0MzIuOTc3LDIzMTIuNDcgYyAwLDE1LjY0IC04LjQ1NywyMy4zNSAtMTcuOTIyLDIzLjM1IC05LjQ2OSwwIC0xNy45MTgsLTcuNzEgLTE3LjkxOCwtMjMuMzUgMCwtMTUuNjUgOC40NDksLTIzLjIyIDE3LjkxOCwtMjMuMjIgOS40NjUsMCAxNy45MjIsNy41NyAxNy45MjIsMjMuMjIgeiBtIC0xNy45MjIsLTM1LjQ2IGMgLTE2LjUzMiwwIC0zMy40NDIsMTAuOTggLTMzLjQ0MiwzNS40NiAwLDI0LjQ4IDE2LjkxLDM1LjU4IDMzLjQ0MiwzNS41OCAxNi41MjcsMCAzMy40MzcsLTExLjEgMzMuNDM3LC0zNS41OCAwLC0yNC40OCAtMTYuOTEsLTM1LjQ2IC0zMy40MzcsLTM1LjQ2IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDU3OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNDg4LjE5NSwyMzMxLjY1IGMgLTkuNDY1LDAgLTE0Ljg4NiwtMy43OCAtMTQuODg2LC0xNy40MSB2IC0zNS41OSBoIC0xNS4wMTYgdiA2Ny44OSBoIDE0Ljc2MiB2IC0xMi4xMiBjIDMuNjYsNy41OCAxMC4yMjIsMTIuMTIgMTguNDIyLDEyLjI1IDEuMTM2LDAgMi43NzcsLTAuMTMgMy45MTQsLTAuMjYgdiAtMTUuMTQgYyAtMi41MjQsMC4yNSAtNC45MjIsMC4zOCAtNy4xOTYsMC4zOCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1ODAiPjwvcGF0aD48cGF0aCBkPSJtIDU0Ni44NDgsMjMxOS4yOSBjIC0wLjM3NSwxMC41OSAtOC40NTMsMTcuMDMgLTE3LjI4NSwxNy4wMyAtNy4wNjcsMCAtMTYuNzgyLC00LjE2IC0xOC4wNDcsLTE3LjAzIHogbSAtMTYuOTEsLTI5Ljc5IGMgNy44MjgsMCAxNC4wMDcsMy4xNSAxNi42Niw5LjQ2IGggMTQuNzY1IGMgLTMuMTYsLTEwLjg1IC0xMy4yNSwtMjEuOTUgLTMwLjc4OSwtMjEuOTUgLTIxLjgzMiwwIC0zNC4zMjgsMTYuNjYgLTM0LjMyOCwzNi4wOSAwLDIwLjQ0IDE0LjAwOCwzNC45NSAzMy4zMTcsMzQuOTUgMjAuODIsMCAzMy44MTYsLTE2LjkgMzIuNTU4LC0zOS43NCBoIC01MC42MDUgYyAxLjAxMSwtMTIuNjMgOS44NDMsLTE4LjgxIDE4LjQyMiwtMTguODEiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTgyIj48L3BhdGg+PHBhdGggZD0ibSA1ODMuNjUyLDIzMTIuNiBjIDAsLTE0LjM5IDcuMTk2LC0yMy4zNSAxNy4xNjQsLTIzLjM1IDkuODQsMCAxNy41MzksNy43IDE3LjUzOSwyMy4zNSAwLDE1LjY0IC03LjY5OSwyMy4yMiAtMTcuNTM5LDIzLjIyIC05Ljk2OCwwIC0xNy4xNjQsLTguOTcgLTE3LjE2NCwtMjMuMjIgeiBtIDQ5LjA5LDU3LjUzIHYgLTkxLjQ4IGggLTE1LjAxNSB2IDguOTYgYyAtNC4wMzksLTYuNjggLTExLjEwNiwtMTAuNiAtMjAuMTkyLC0xMC42IC0xNi4wMjMsMCAtMjkuNTMxLDEzLjc1IC0yOS41MzEsMzUuNTkgMCwyMS43IDEzLjUwOCwzNS40NSAyOS41MzEsMzUuNDUgOS4wODYsMCAxNi4xNTMsLTMuOTEgMjAuMTkyLC0xMC41OSB2IDMyLjY3IGggMTUuMDE1IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDU4NCI+PC9wYXRoPjxwYXRoIGQ9Im0gNzIwLjg4NywyMzEyLjM0IC0xMy44ODMsMzkuMjUgLTEzLjc1OCwtMzkuMjUgeiBtIC00Ljc5Nyw1Ny43OSAzNC4zMiwtOTEuNDggaCAtMTcuNTM5IGwgLTcuMTkxLDIwLjMxIGggLTM3LjEwMiBsIC03LjA2MiwtMjAuMzEgaCAtMTYuNDA3IGwgMzQuMDcxLDkxLjQ4IGggMTYuOTEiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTg2Ij48L3BhdGg+PHBhdGggZD0ibSA3ODYuMjAzLDIzMzEuNjUgYyAtOS40NjksMCAtMTQuODk0LC0zLjc4IC0xNC44OTQsLTE3LjQxIHYgLTM1LjU5IGggLTE1LjAxMiB2IDY3Ljg5IGggMTQuNzU4IHYgLTEyLjEyIGMgMy42NjQsNy41OCAxMC4yMjYsMTIuMTIgMTguNDI1LDEyLjI1IDEuMTM3LDAgMi43NzgsLTAuMTMgMy45MTUsLTAuMjYgdiAtMTUuMTQgYyAtMi41MjQsMC4yNSAtNC45MjIsMC4zOCAtNy4xOTIsMC4zOCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1ODgiPjwvcGF0aD48cGF0aCBkPSJtIDgzMC4yMTUsMjMzMS42NSBjIC05LjQ2OSwwIC0xNC44OTEsLTMuNzggLTE0Ljg5MSwtMTcuNDEgdiAtMzUuNTkgaCAtMTUuMDE1IHYgNjcuODkgaCAxNC43NjEgdiAtMTIuMTIgYyAzLjY2LDcuNTggMTAuMjIzLDEyLjEyIDE4LjQyMiwxMi4yNSAxLjEzNywwIDIuNzc4LC0wLjEzIDMuOTE4LC0wLjI2IHYgLTE1LjE0IGMgLTIuNTI3LDAuMjUgLTQuOTIyLDAuMzggLTcuMTk1LDAuMzgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNTkwIj48L3BhdGg+PHBhdGggZD0ibSA4NTkuMzMyLDIyNzguNjUgaCAtMTUuMDE2IHYgNjcuODkgaCAxNS4wMTYgeiBtIDAsNzYuMzUgaCAtMTUuMDE2IHYgMTUuMTMgaCAxNS4wMTYgViAyMzU1IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDU5MiI+PC9wYXRoPjxwYXRoIGQ9Im0gOTEyLjk0NSwyMzQ2LjU0IGggMTUuNjQ5IGwgLTI0LjQ4MSwtNjcuODkgaCAtMTQuMTM2IGwgLTI0LjczMSw2Ny44OSBoIDE2LjUzMSBsIDE1LjY0NSwtNDguNDYgMTUuNTIzLDQ4LjQ2IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDU5NCI+PC9wYXRoPjxwYXRoIGQ9Im0gOTQzLjE5OSwyMjk3LjcgYyAwLC01LjkyIDQuOTIyLC05LjQ2IDEyLjQ5MiwtOS40NiAxMS4xMDYsMCAxNy42NjgsNS42OCAxNy42NjgsMTcuMTYgdiA1LjE3IGMgLTIxLjQ1MywtMi4wMiAtMzAuMTYsLTUuMDQgLTMwLjE2LC0xMi44NyB6IG0gMjkuNzgxLDIzLjM1IHYgMS4yNiBjIDAsMTEuNjEgLTYuNjkxLDE1LjE1IC0xNC4xMzYsMTUuMTUgLTcuNTY3LDAgLTEzLjI0NiwtNC4wNCAtMTMuNjI5LC0xMi4yNSBoIC0xNC43NjIgYyAxLjAwOCwxMy44OSAxMi40OTIsMjMuMzUgMjguODk5LDIzLjM1IDE2LjI4MSwwIDI5LjAyMywtNy40NSAyOC42NCwtMjkuMTUgMCwtMy40MSAtMC4yNDYsLTExLjM2IC0wLjI0NiwtMTcuNTQgMCwtOC41OCAwLjc1OCwtMTcuNTUgMi4wMTYsLTIzLjIyIGggLTEzLjc1NCBjIC0wLjUwNCwyLjkgLTEuMDEyLDQuNTQgLTEuMjYyLDkuMjEgLTQuMjkzLC03LjMxIC0xMi4zNjcsLTEwLjg1IC0yMi4zMzYsLTEwLjg1IC0xNC43NjIsMCAtMjUuMTA5LDcuOTUgLTI1LjEwOSwyMC4zMSAwLDE2LjkyIDIwLjgyLDIxLjIgNDUuNjc5LDIzLjczIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDU5NiI+PC9wYXRoPjxwYXRoIGQ9Im0gMTAwMC41OCwyMjc4LjY1IHYgOTEuNDggaCAxNS4wMSB2IC05MS40OCBoIC0xNS4wMSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg1OTgiPjwvcGF0aD48cGF0aCBkPSJtIDEwNDguNjEsMjM1Ni43NyB2IDEzLjM2IGggNzMuNTcgdiAtMTMuMzYgaCAtMjguNzcgdiAtNzguMTIgaCAtMTYuMDMgdiA3OC4xMiBoIC0yOC43NyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2MDAiPjwvcGF0aD48cGF0aCBkPSJtIDExNDMuNzIsMjI3OC42NSBoIC0xNS4wMiB2IDY3Ljg5IGggMTUuMDIgeiBtIDAsNzYuMzUgaCAtMTUuMDIgdiAxNS4xMyBoIDE1LjAyIFYgMjM1NSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2MDIiPjwvcGF0aD48cGF0aCBkPSJtIDExNTguMDgsMjI3OC42NSB2IDY3Ljg5IGggMTUuMDIgdiAtOS40NiBjIDMuOTEsNy4wNiAxMC42LDEwLjk3IDE5LjY4LDEwLjk3IDEwLjQ4LDAgMTYuNjYsLTQuNDEgMTkuODEsLTExLjk5IDUuODEsOC41OSAxMy43NiwxMS45OSAyMi4wOSwxMS45OSAxNi4wMiwwIDIyLjIxLC0xMC41OSAyMi4yMSwtMjYuNzQgdiAtNDIuNjYgaCAtMTUuMDIgdiAzOC45OSBjIDAsOS4yMSAtMC44OCwxOC4xOCAtMTEuOTksMTguMTggLTExLjEsMCAtMTQuODksLTguODQgLTE0Ljg5LC0yMS4wOCB2IC0zNi4wOSBoIC0xNS4wMSB2IDM4Ljk5IGMgMCw5LjIxIC0wLjg5LDE4LjE4IC0xMS45OSwxOC4xOCAtMTEuMTEsMCAtMTQuODksLTguODQgLTE0Ljg5LC0yMS4wOCB2IC0zNi4wOSBoIC0xNS4wMiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2MDQiPjwvcGF0aD48cGF0aCBkPSJtIDEzMTYuMDEsMjMxOS4yOSBjIC0wLjM4LDEwLjU5IC04LjQ2LDE3LjAzIC0xNy4yOSwxNy4wMyAtNy4wNiwwIC0xNi43OCwtNC4xNiAtMTguMDQsLTE3LjAzIHogbSAtMTYuOTEsLTI5Ljc5IGMgNy44MywwIDE0LjAxLDMuMTUgMTYuNjYsOS40NiBoIDE0Ljc2IGMgLTMuMTYsLTEwLjg1IC0xMy4yNSwtMjEuOTUgLTMwLjc5LC0yMS45NSAtMjEuODMsMCAtMzQuMzIsMTYuNjYgLTM0LjMyLDM2LjA5IDAsMjAuNDQgMTQuMDEsMzQuOTUgMzMuMzEsMzQuOTUgMjAuODIsMCAzMy44MiwtMTYuOSAzMi41NiwtMzkuNzQgaCAtNTAuNiBjIDEuMDEsLTEyLjYzIDkuODQsLTE4LjgxIDE4LjQyLC0xOC44MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2MDYiPjwvcGF0aD48cGF0aCBkPSJtIDEzNjUuMTgsMjMzNi41NyBjIC02LjU3LDAgLTEyLjYyLC0yLjkgLTEyLjYyLC03LjQ0IDAsLTQuNTQgMy4yOCwtNi45NCA5LjA4LC04LjA4IGwgOS41OSwtMS44OSBjIDEzLjc2LC0yLjY1IDI0LjIzLC02Ljk1IDI0LjIzLC0yMC4yIDAsLTE0LjEzIC0xMy4zNywtMjEuOTUgLTI4Ljc3LC0yMS45NSAtMTYuNjUsMCAtMjcuNzYsOS40NiAtMjkuNCwyMi4zMyBoIDE0LjY0IGMgMS4zOSwtNi45NCA2LjQzLC0xMC45NyAxNS4yNywtMTAuOTcgNy44MiwwIDEzLjYzLDMuMjggMTMuNjMsOC44NCAwLDUuNTQgLTUuMDUsOC4wNyAtMTEuNzQsOS4zMyBsIC0xMC4yMiwyLjAxIGMgLTExLjQ5LDIuMjggLTIwLjQ1LDcuNDUgLTIwLjQ1LDE5LjgyIDAsMTEuOTkgMTIuODgsMTkuNjggMjcuNjQsMTkuNjggMTMuMjUsMCAyNS4zNywtNi40MyAyOC4xNCwtMjAuMDYgaCAtMTQuMTMgYyAtMS42NCw2LjE5IC03LjMyLDguNTggLTE0Ljg5LDguNTgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjA4Ij48L3BhdGg+PHBhdGggZD0ibSAxOTY3LjQ1LDM2NTMuNyBjIC0xNS4wMSwwIC0yMy42NywtMTQuNTcgLTIzLjY3LC00MC45OSAwLC0yNi40MSA4LjY2LC00MC45OSAyMy42NywtNDAuOTkgMTUuMTYsMCAyMy44MiwxNC41OCAyMy44Miw0MC45OSAwLDI2LjQyIC04LjY2LDQwLjk5IC0yMy44Miw0MC45OSB6IG0gMCwxMy4xNCBjIDI4LjAxLDAgNDEuNzIsLTIyLjA5IDQxLjcyLC01NC4xMyAwLC0zMi4xOSAtMTMuNzEsLTU0LjI3IC00MS43MiwtNTQuMjcgLTI3Ljg2LDAgLTQxLjU3LDIyLjA4IC00MS41Nyw1NC4yNyAwLDMyLjA0IDEzLjcxLDU0LjEzIDQxLjU3LDU0LjEzIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDYxMCI+PC9wYXRoPjxwYXRoIGQ9Im0gMjYzLjk0NSw0MTk5LjQ5IGMgMCwxNy4xNyAxNy43OTMsMjUuNzQgMzQuNTc4LDI1Ljc0IDE4LjA0NywwIDMyLjE3NiwtOC4yIDM1Ljg0LC0yNy4yNSBIIDMxOC44NCBjIC0yLjY1MiwxMC45NyAtMTIuMjQyLDE0LjEzIC0yMS4yMDMsMTQuMTMgLTcuMDYzLDAgLTE3LjUzOSwtMy4xNiAtMTcuNTM5LC0xMi4xMSAwLC03LjA3IDUuODA4LC0xMC42IDEzLjYyOSwtMTIuMTIgbCAxMS4yMywtMi4xNCBjIDE2LjAyNywtMy4xNSAzMS4yOTMsLTguOTYgMzEuMjkzLC0yNy4zOCAwLC0xOC40MyAtMTguMjk3LC0yNy44OSAtMzYuMzQsLTI3Ljg5IC0yMS43MDcsMCAtMzYuNTk0LDExLjg2IC0zOC40ODgsMzEuOTIgaCAxNS43NzMgYyAyLjc3OCwtMTIuNDkgMTAuODUyLC0xOC44IDIzLjQ2OSwtMTguOCAxMC44NTYsMCAxOS41NjMsNC45MyAxOS41NjMsMTMuNzUgMCw5LjM1IC0xMC4wOTQsMTIuNSAtMTguODA1LDE0LjE0IGwgLTExLjEwMiwyLjE0IGMgLTE0LjM4NiwyLjkgLTI2LjM3NSwxMC4zNSAtMjYuMzc1LDI1Ljg3IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDYxMiI+PC9wYXRoPjxwYXRoIGQ9Im0gMzQ1Ljc5Nyw0MTMyLjExIHYgOTEuNDggaCAxNS4wMTYgdiAtOTEuNDggaCAtMTUuMDE2IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDYxNCI+PC9wYXRoPjxwYXRoIGQ9Im0gNDIxLjk5Niw0MTY1LjkzIGMgMCwxNS42NCAtOC40NTcsMjMuMzUgLTE3LjkxOCwyMy4zNSAtOS40NjksMCAtMTcuOTE4LC03LjcxIC0xNy45MTgsLTIzLjM1IDAsLTE1LjY1IDguNDQ5LC0yMy4yMyAxNy45MTgsLTIzLjIzIDkuNDYxLDAgMTcuOTE4LDcuNTggMTcuOTE4LDIzLjIzIHogbSAtMTcuOTE4LC0zNS40NiBjIC0xNi41MzEsMCAtMzMuNDQxLDEwLjk4IC0zMy40NDEsMzUuNDYgMCwyNC40OCAxNi45MSwzNS41OCAzMy40NDEsMzUuNTggMTYuNTI3LDAgMzMuNDM4LC0xMS4xIDMzLjQzOCwtMzUuNTggMCwtMjQuNDggLTE2LjkxMSwtMzUuNDYgLTMzLjQzOCwtMzUuNDYiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjE2Ij48L3BhdGg+PHBhdGggZD0iTSA0NjQuNDczLDQyMTcuOTIgViA0MjAwIGggMTMuNjI5IHYgLTEwLjg1IGggLTEzLjYyOSB2IC0zNi45NyBjIDAsLTYuOTUgMS42NCwtOC41OSA4LjA3OCwtOC41OSBoIDUuNDI5IHYgLTExLjQ4IGggLTExLjEwOSBjIC0xNC41MTIsMCAtMTcuNDEsMy45MSAtMTcuNDEsMTcuNzkgdiAzOS4yNSBIIDQzOS4zNjMgViA0MjAwIGggMTAuMDk4IHYgMTcuOTIgaCAxNS4wMTIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjE4Ij48L3BhdGg+PHBhdGggZD0ibSA1NDkuNzM4LDQyMDEuNTEgYyAxNi40MDcsMCAyMy4wOTQsLTEwLjYgMjMuMDk0LC0yNi43NCB2IC00Mi42NiBoIC0xNS4wMTkgdiAzOC45OSBjIDAsOS4yMSAtMS4zODcsMTguMTggLTEyLjg3MiwxOC4xOCAtMTEuNDc2LDAgLTE1Ljc2OSwtOC44NCAtMTUuNzY5LC0yMS4wOCB2IC0zNi4wOSBIIDUxNC4xNTYgViA0MjAwIGggMTUuMDE2IHYgLTkuNDYgYyAzLjkxLDcuMDYgMTEuMTAxLDEwLjk3IDIwLjU2NiwxMC45NyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2MjAiPjwvcGF0aD48cGF0aCBkPSJtIDYwNy43NDYsNDEzMC40NyBjIC0xNi4xNTIsMCAtMjIuNzExLDEwLjU5IC0yMi43MTEsMjYuNzQgViA0MjAwIGggMTUuMDE2IHYgLTM5LjEyIGMgMCwtOS4yMSAxLjI1OCwtMTguMTggMTIuNDk2LC0xOC4xOCAxMS4yMywwIDE1LjI2Niw4Ljg0IDE1LjI2NiwyMS4wOCBWIDQyMDAgaCAxNS4wMTUgdiAtNjcuODkgaCAtMTUuMDE1IHYgOS4zNCBjIC0zLjkxNSwtNy4wNyAtMTAuODUyLC0xMC45OCAtMjAuMDY3LC0xMC45OCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2MjIiPjwvcGF0aD48cGF0aCBkPSJNIDY1Ny4xNjgsNDEzMi4xMSBWIDQyMDAgaCAxNS4wMTYgdiAtOS40NiBjIDMuOTEsNy4wNiAxMC42MDEsMTAuOTcgMTkuNjg3LDEwLjk3IDEwLjQ3MywwIDE2LjY1NiwtNC40MSAxOS44MDksLTExLjk5IDUuODA4LDguNTkgMTMuNzU4LDExLjk5IDIyLjA4NiwxMS45OSAxNi4wMjcsMCAyMi4yMDcsLTEwLjYgMjIuMjA3LC0yNi43NCB2IC00Mi42NiBoIC0xNS4wMTYgdiAzOC45OSBjIDAsOS4yMSAtMC44ODMsMTguMTggLTExLjk4NCwxOC4xOCAtMTEuMTEsMCAtMTQuODk1LC04Ljg0IC0xNC44OTUsLTIxLjA4IHYgLTM2LjA5IGggLTE1LjAxNSB2IDM4Ljk5IGMgMCw5LjIxIC0wLjg4MywxOC4xOCAtMTEuOTkzLDE4LjE4IC0xMS4xMDEsMCAtMTQuODg2LC04Ljg0IC0xNC44ODYsLTIxLjA4IHYgLTM2LjA5IGggLTE1LjAxNiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2MjQiPjwvcGF0aD48cGF0aCBkPSJtIDgxOC4xMTcsNDE2Ni4wNSBjIDAsMTQuMjYgLTcuMTkxLDIzLjIzIC0xNy4xNjQsMjMuMjMgLTkuODQ0LDAgLTE3LjUzOSwtNy41OCAtMTcuNTM5LC0yMy4yMyAwLC0xNS42NCA3LjY5NSwtMjMuMzUgMTcuNTM5LC0yMy4zNSA5Ljk3MywwIDE3LjE2NCw4Ljk3IDE3LjE2NCwyMy4zNSB6IG0gLTM0LjA3NCwyNC44NiBjIDQuMDM5LDYuNjkgMTEuMTA1LDEwLjYgMjAuMTkxLDEwLjYgMTYuMDI4LDAgMjkuNTI4LC0xMy43NSAyOS41MjgsLTM1LjQ2IDAsLTIxLjgzIC0xMy41LC0zNS41OCAtMjkuNTI4LC0zNS41OCAtOS4wODYsMCAtMTYuMTUyLDMuOTEgLTIwLjE5MSwxMC41OSB2IC04Ljk1IGggLTE1LjAxMiB2IDkxLjQ4IGggMTUuMDEyIHYgLTMyLjY4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDYyNiI+PC9wYXRoPjxwYXRoIGQ9Im0gODkwLjI1NCw0MTcyLjc0IGMgLTAuMzc5LDEwLjYgLTguNDU3LDE3LjAzIC0xNy4yODksMTcuMDMgLTcuMDY3LDAgLTE2Ljc4MSwtNC4xNiAtMTguMDQ3LC0xNy4wMyB6IG0gLTE2LjkxNCwtMjkuNzggYyA3LjgyOCwwIDE0LjAxMiwzLjE1IDE2LjY2LDkuNDYgaCAxNC43NjYgYyAtMy4xNTcsLTEwLjg1IC0xMy4yNSwtMjEuOTUgLTMwLjc4OSwtMjEuOTUgLTIxLjgzMiwwIC0zNC4zMjksMTYuNjYgLTM0LjMyOSwzNi4wOSAwLDIwLjQ0IDE0LjAxMiwzNC45NSAzMy4zMTcsMzQuOTUgMjAuODIsMCAzMy44MiwtMTYuOSAzMi41NTgsLTM5Ljc0IGggLTUwLjYwNSBjIDEuMDEyLC0xMi42MyA5Ljg0NCwtMTguODEgMTguNDIyLC0xOC44MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2MjgiPjwvcGF0aD48cGF0aCBkPSJtIDk0NS4yMjcsNDE4NS4xMSBjIC05LjQ2NSwwIC0xNC44ODcsLTMuNzkgLTE0Ljg4NywtMTcuNDEgdiAtMzUuNTkgSCA5MTUuMzI0IFYgNDIwMCBoIDE0Ljc2MiB2IC0xMi4xMiBjIDMuNjYsNy41OCAxMC4yMjMsMTIuMTIgMTguNDIyLDEyLjI1IDEuMTM3LDAgMi43NzcsLTAuMTMgMy45MTQsLTAuMjYgdiAtMTUuMTQgYyAtMi41MjQsMC4yNSAtNC45MjIsMC4zOCAtNy4xOTUsMC4zOCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2MzAiPjwvcGF0aD48cGF0aCBkPSJtIDk5Ny42NzYsNDE1MS4xNiBjIDAsLTUuOTMgNC45MjQsLTkuNDYgMTIuNDk0LC05LjQ2IDExLjExLDAgMTcuNjYsNS42OCAxNy42NiwxNy4xNiB2IDUuMTcgYyAtMjEuNDUsLTIuMDIgLTMwLjE1NCwtNS4wNSAtMzAuMTU0LC0xMi44NyB6IG0gMjkuNzg0LDIzLjM1IHYgMS4yNiBjIDAsMTEuNjEgLTYuNjksMTUuMTQgLTE0LjE0LDE1LjE0IC03LjU3LDAgLTEzLjI1LC00LjA0IC0xMy42MjUsLTEyLjI0IGggLTE0Ljc2MSBjIDEuMDA0LDEzLjg5IDEyLjQ4OCwyMy4zNSAyOC44OTYsMjMuMzUgMTYuMjgsMCAyOS4wMiwtNy40NSAyOC42NCwtMjkuMTUgMCwtMy40MSAtMC4yNSwtMTEuMzYgLTAuMjUsLTE3LjU0IDAsLTguNTggMC43NiwtMTcuNTUgMi4wMiwtMjMuMjIgaCAtMTMuNzYgYyAtMC41LDIuOSAtMS4wMSw0LjU0IC0xLjI2LDkuMjEgLTQuMjksLTcuMzIgLTEyLjM2LC0xMC44NSAtMjIuMzMsLTEwLjg1IC0xNC43NjUsMCAtMjUuMTEzLDcuOTQgLTI1LjExMywyMC4zMSAwLDE2LjkyIDIwLjgyMywyMS4yIDQ1LjY4MywyMy43MyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2MzIiPjwvcGF0aD48cGF0aCBkPSJtIDEwOTkuNDcsNDE3Ni43OCBjIC0xLjI2LDcuMTkgLTcuNTcsMTIuMjQgLTE1Ljc3LDEyLjI0IC05LjM0LDAgLTE3LjgsLTYuOTQgLTE3LjgsLTIyLjk3IDAsLTE2LjE1IDguNTgsLTIzLjA5IDE3LjQyLC0yMy4wOSA3LjMyLDAgMTQuNzYsMy4yOCAxNi42NiwxMi4zNyBoIDE0LjY0IGMgLTMuMDMsLTE1LjkxIC0xNy4wNCwtMjQuODYgLTMxLjU1LC0yNC44NiAtMTkuNjksMCAtMzIuNjksMTUuMjcgLTMyLjY5LDM1LjQ2IDAsMjAuMTkgMTMuMTMsMzUuNTggMzMuMzIsMzUuNTggMTQuNzYsMCAyNy44OSwtOS41OSAzMC40MSwtMjQuNzMgaCAtMTQuNjQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjM0Ij48L3BhdGg+PHBhdGggZD0ibSAxMTcwLjcyLDQxNjUuOTMgYyAwLDE1LjY0IC04LjQ1LDIzLjM1IC0xNy45MiwyMy4zNSAtOS40NiwwIC0xNy45MiwtNy43MSAtMTcuOTIsLTIzLjM1IDAsLTE1LjY1IDguNDYsLTIzLjIzIDE3LjkyLC0yMy4yMyA5LjQ3LDAgMTcuOTIsNy41OCAxNy45MiwyMy4yMyB6IG0gLTE3LjkyLC0zNS40NiBjIC0xNi41MywwIC0zMy40NCwxMC45OCAtMzMuNDQsMzUuNDYgMCwyNC40OCAxNi45MSwzNS41OCAzMy40NCwzNS41OCAxNi41MywwIDMzLjQ0LC0xMS4xIDMzLjQ0LC0zNS41OCAwLC0yNC40OCAtMTYuOTEsLTM1LjQ2IC0zMy40NCwtMzUuNDYiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjM2Ij48L3BhdGg+PHBhdGggZD0ibSAxMjI1Ljk1LDQxODUuMTEgYyAtOS40NywwIC0xNC44OSwtMy43OSAtMTQuODksLTE3LjQxIHYgLTM1LjU5IGggLTE1LjAyIFYgNDIwMCBoIDE0Ljc2IHYgLTEyLjEyIGMgMy42Niw3LjU4IDEwLjIzLDEyLjEyIDE4LjQyLDEyLjI1IDEuMTQsMCAyLjc4LC0wLjEzIDMuOTIsLTAuMjYgdiAtMTUuMTQgYyAtMi41MiwwLjI1IC00LjkyLDAuMzggLTcuMTksMC4zOCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2MzgiPjwvcGF0aD48cGF0aCBkPSJtIDEyNDkuNTIsNDE2Ni4wNSBjIDAsLTE0LjM4IDcuMiwtMjMuMzUgMTcuMTcsLTIzLjM1IDkuODMsMCAxNy41Myw3LjcxIDE3LjUzLDIzLjM1IDAsMTUuNjUgLTcuNywyMy4yMyAtMTcuNTMsMjMuMjMgLTkuOTcsMCAtMTcuMTcsLTguOTcgLTE3LjE3LC0yMy4yMyB6IG0gNDkuMDksNTcuNTQgdiAtOTEuNDggaCAtMTUuMDIgdiA4Ljk1IGMgLTQuMDMsLTYuNjggLTExLjEsLTEwLjU5IC0yMC4xOSwtMTAuNTkgLTE2LjAyLDAgLTI5LjUzLDEzLjc1IC0yOS41MywzNS41OCAwLDIxLjcxIDEzLjUxLDM1LjQ2IDI5LjUzLDM1LjQ2IDkuMDksMCAxNi4xNiwtMy45MSAyMC4xOSwtMTAuNiB2IDMyLjY4IGggMTUuMDIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjQwIj48L3BhdGg+PHBhdGggZD0ibSAxMzI3Ljk3LDQxMzIuMTEgaCAtMTUuMDIgViA0MjAwIGggMTUuMDIgeiBtIDAsNzYuMzQgaCAtMTUuMDIgdiAxNS4xNCBoIDE1LjAyIHYgLTE1LjE0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY0MiI+PC9wYXRoPjxwYXRoIGQ9Im0gMTM3Ny45Miw0MjAxLjUxIGMgMTYuNCwwIDIzLjA5LC0xMC42IDIzLjA5LC0yNi43NCB2IC00Mi42NiBoIC0xNS4wMiB2IDM4Ljk5IGMgMCw5LjIxIC0xLjM4LDE4LjE4IC0xMi44NywxOC4xOCAtMTEuNDgsMCAtMTUuNzcsLTguODQgLTE1Ljc3LC0yMS4wOCB2IC0zNi4wOSBoIC0xNS4wMSBWIDQyMDAgaCAxNS4wMSB2IC05LjQ2IGMgMy45MSw3LjA2IDExLjEsMTAuOTcgMjAuNTcsMTAuOTciIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjQ0Ij48L3BhdGg+PHBhdGggZD0ibSAxNDI1LjA3LDQxNjcuNDQgYyAwLC0xMy44OCA3LjE5LC0yMi4zMyAxNy4xNiwtMjIuMzMgOS44NCwwIDE3LjU0LDcuMDcgMTcuNTQsMjIuMzMgMCwxNS4xNSAtNy43LDIyLjA4IC0xNy41NCwyMi4wOCAtOS45NywwIC0xNy4xNiwtOC40NSAtMTcuMTYsLTIyLjA4IHogbSA0OS4wOSwzMi41NiB2IC02MS4wNyBjIDAsLTExLjExIC0yLjc4LC0xOC45MyAtOC4yMSwtMjMuOTggLTUuNDIsLTUuMDUgLTEzLjUsLTcuMzIgLTI0LjEsLTcuMzIgLTE0Ljg5LDAgLTI2Ljc1LDUuOTIgLTI5LjAyLDIwLjgyIGggMTQuODkgYyAxLjM5LC02LjMxIDUuNTUsLTguOTYgMTQuNTEsLTguOTYgNi42OSwwIDEwLjk4LDEuOSAxMy41LDQuOTIgMi41MywyLjkgMy40MSw3LjA2IDMuNDEsMTEuNDkgdiA3Ljk1IGMgLTQuMDQsLTYuNjkgLTExLjEsLTEwLjYxIC0yMC4xOSwtMTAuNjEgLTE2LjAyLDAgLTI5LjUzLDEzIC0yOS41MywzNC4yIDAsMjEuMiAxMy41MSwzNC4wNyAyOS41MywzNC4wNyA5LjA5LDAgMTYuMTUsLTMuOTEgMjAuMTksLTEwLjYgdiA5LjA5IGggMTUuMDIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjQ2Ij48L3BhdGg+PHBhdGggZD0ibSAyODMuNzU4LDQwNjAuMjcgdiAtMTcuOTIgaCAxMy42MjUgdiAtMTAuODUgaCAtMTMuNjI1IHYgLTM2Ljk3IGMgMCwtNi45NCAxLjY0LC04LjU4IDguMDc0LC04LjU4IGggNS40MyB2IC0xMS40OSBoIC0xMS4xMSBjIC0xNC41MTEsMCAtMTcuNDEsMy45MiAtMTcuNDEsMTcuNzkgdiAzOS4yNSBoIC0xMC4wOTcgdiAxMC44NSBoIDEwLjA5NyB2IDE3LjkyIGggMTUuMDE2IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY0OCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzUzLjc3LDQwMDguMjggYyAwLDE1LjY1IC04LjQ1NywyMy4zNSAtMTcuOTE4LDIzLjM1IC05LjQ2OSwwIC0xNy45MjIsLTcuNyAtMTcuOTIyLC0yMy4zNSAwLC0xNS42NCA4LjQ1MywtMjMuMjIgMTcuOTIyLC0yMy4yMiA5LjQ2MSwwIDE3LjkxOCw3LjU4IDE3LjkxOCwyMy4yMiB6IG0gLTE3LjkxOCwtMzUuNDYgYyAtMTYuNTM2LDAgLTMzLjQ0MiwxMC45OCAtMzMuNDQyLDM1LjQ2IDAsMjQuNDggMTYuOTA2LDM1LjU4IDMzLjQ0MiwzNS41OCAxNi41MjcsMCAzMy40MzcsLTExLjEgMzMuNDM3LC0zNS41OCAwLC0yNC40OCAtMTYuOTEsLTM1LjQ2IC0zMy40MzcsLTM1LjQ2IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY1MCI+PC9wYXRoPjxwYXRoIGQ9Im0gNDIyLjczLDQwNjAuMjcgdiAtMTcuOTIgaCAxMy42MjkgViA0MDMxLjUgSCA0MjIuNzMgdiAtMzYuOTcgYyAwLC02Ljk0IDEuNjQxLC04LjU4IDguMDc5LC04LjU4IGggNS40MjkgdiAtMTEuNDkgaCAtMTEuMTA5IGMgLTE0LjUxMiwwIC0xNy40MTQsMy45MiAtMTcuNDE0LDE3Ljc5IHYgMzkuMjUgaCAtMTAuMDk4IHYgMTAuODUgaCAxMC4wOTggdiAxNy45MiBoIDE1LjAxNSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2NTIiPjwvcGF0aD48cGF0aCBkPSJtIDQ4MS41MTYsNDA0My44NiBjIDE2LjQwNiwwIDIzLjA5MywtMTAuNTkgMjMuMDkzLC0yNi43NCB2IC00Mi42NiBIIDQ4OS41OSB2IDM4Ljk5IGMgMCw5LjIxIC0xLjM4NywxOC4xOCAtMTIuODcxLDE4LjE4IC0xMS40NzcsMCAtMTUuNzcsLTguODQgLTE1Ljc3LC0yMS4wOCB2IC0zNi4wOSBoIC0xNS4wMTUgdiA5MS40OSBoIDE1LjAxNSB2IC0zMy4wNiBjIDMuOTEsNy4wNiAxMS4xMDIsMTAuOTcgMjAuNTY3LDEwLjk3IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY1NCI+PC9wYXRoPjxwYXRoIGQ9Im0gNTYzLjc1LDQwMTUuMSBjIC0wLjM3OSwxMC41OSAtOC40NTcsMTcuMDMgLTE3LjI4OSwxNy4wMyAtNy4wNjYsMCAtMTYuNzgxLC00LjE2IC0xOC4wNDcsLTE3LjAzIHogbSAtMTYuOTE0LC0yOS43OSBjIDcuODI4LDAgMTQuMDEyLDMuMTUgMTYuNjYsOS40NiBoIDE0Ljc2NiBjIC0zLjE1NywtMTAuODQgLTEzLjI1LC0yMS45NSAtMzAuNzg5LC0yMS45NSAtMjEuODMyLDAgLTM0LjMyOCwxNi42NiAtMzQuMzI4LDM2LjA5IDAsMjAuNDUgMTQuMDExLDM0Ljk1IDMzLjMxNiwzNC45NSAyMC44MiwwIDMzLjgyLC0xNi45MSAzMi41NTksLTM5Ljc0IGggLTUwLjYwNiBjIDEuMDEyLC0xMi42MyA5Ljg0NCwtMTguODEgMTguNDIyLC0xOC44MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2NTYiPjwvcGF0aD48cGF0aCBkPSJtIDY2NC4zOTEsNDAwOC40MSBjIDAsMTQuMjUgLTcuMTkyLDIzLjIyIC0xNy4xNjQsMjMuMjIgLTkuODQ0LDAgLTE3LjUzOSwtNy41OCAtMTcuNTM5LC0yMy4yMiAwLC0xNS42NSA3LjY5NSwtMjMuMzUgMTcuNTM5LC0yMy4zNSA5Ljk3MiwwIDE3LjE2NCw4Ljk2IDE3LjE2NCwyMy4zNSB6IG0gLTM0LjA3MSwyNC44NiBjIDQuMDM1LDYuNjggMTEuMTAyLDEwLjU5IDIwLjE4OCwxMC41OSAxNi4wMjcsMCAyOS41MjcsLTEzLjc1IDI5LjUyNywtMzUuNDUgMCwtMjEuODMgLTEzLjUsLTM1LjU5IC0yOS41MjcsLTM1LjU5IC05LjA4NiwwIC0xNi4xNTMsMy45MSAtMjAuMTg4LDEwLjU5IHYgLTguOTUgaCAtMTUuMDE1IHYgOTEuNDkgaCAxNS4wMTUgdiAtMzIuNjgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjU4Ij48L3BhdGg+PHBhdGggZD0ibSA2ODkuNzA3LDM5NzQuNDYgdiA5MS40OSBoIDE1LjAxNiB2IC05MS40OSBoIC0xNS4wMTYiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjYwIj48L3BhdGg+PHBhdGggZD0ibSA3NjUuOTEsNDAwOC4yOCBjIDAsMTUuNjUgLTguNDU3LDIzLjM1IC0xNy45MjIsMjMuMzUgLTkuNDY1LDAgLTE3LjkxOCwtNy43IC0xNy45MTgsLTIzLjM1IDAsLTE1LjY0IDguNDUzLC0yMy4yMiAxNy45MTgsLTIzLjIyIDkuNDY1LDAgMTcuOTIyLDcuNTggMTcuOTIyLDIzLjIyIHogbSAtMTcuOTIyLC0zNS40NiBjIC0xNi41MzEsMCAtMzMuNDQxLDEwLjk4IC0zMy40NDEsMzUuNDYgMCwyNC40OCAxNi45MSwzNS41OCAzMy40NDEsMzUuNTggMTYuNTMyLDAgMzMuNDM4LC0xMS4xIDMzLjQzOCwtMzUuNTggMCwtMjQuNDggLTE2LjkwNiwtMzUuNDYgLTMzLjQzOCwtMzUuNDYiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjYyIj48L3BhdGg+PHBhdGggZD0ibSA4MzYuNDAyLDQwMTkuMTMgYyAtMS4yNjUsNy4xOSAtNy41NzQsMTIuMjUgLTE1Ljc3NywxMi4yNSAtOS4zMzYsMCAtMTcuNzkzLC02Ljk1IC0xNy43OTMsLTIyLjk3IDAsLTE2LjE2IDguNTc4LC0yMy4xIDE3LjQxOCwtMjMuMSA3LjMxNiwwIDE0Ljc2MiwzLjI4IDE2LjY1NiwxMi4zNyBoIDE0LjYzNyBjIC0zLjAyNywtMTUuOSAtMTcuMDM1LC0yNC44NiAtMzEuNTQ3LC0yNC44NiAtMTkuNjg3LDAgLTMyLjY4MywxNS4yNyAtMzIuNjgzLDM1LjQ2IDAsMjAuMiAxMy4xMjUsMzUuNTggMzMuMzEyLDM1LjU4IDE0Ljc2NiwwIDI3Ljg5MSwtOS41OCAzMC40MSwtMjQuNzMgaCAtMTQuNjMzIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY2NCI+PC9wYXRoPjxwYXRoIGQ9Im0gODc1LjYwNSw0MDE1LjEgMjUuMTE0LDI3LjI1IGggMTguMDQzIGwgLTI1Ljk5MiwtMjcuODkgMjguODk4LC00MCBoIC0xNy41MzkgbCAtMjEuMzI4LDI5LjQgLTcuMTk2LC03LjY5IHYgLTIxLjcxIGggLTE1LjAxMSB2IDkxLjQ5IGggMTUuMDExIHYgLTUwLjg1IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY2NiI+PC9wYXRoPjxwYXRoIGQ9Im0gMTAwMC43Myw0MDA4LjQxIGMgMCwxNC4yNSAtNi4zMDgsMjMuMjIgLTE2Ljc4NSwyMy4yMiAtOS44NDMsMCAtMTcuNTM5LC03LjU4IC0xNy41MzksLTIzLjIyIDAsLTE1LjY1IDcuNjk2LC0yMy4zNSAxNy41MzksLTIzLjM1IDEwLjQ3NywwIDE2Ljc4NSw4Ljk2IDE2Ljc4NSwyMy4zNSB6IG0gLTMzLjY5NSwyNC44NiBjIDQuMDM5LDYuNjggMTEuMTA2LDEwLjU5IDIwLjE5MiwxMC41OSAxNi41MzMsMCAyOS4xNTMsLTEzLjc1IDI5LjE1MywtMzUuNDUgMCwtMjEuODMgLTEyLjYyLC0zNS41OSAtMjkuMTUzLC0zNS41OSAtOS4wODYsMCAtMTYuMTUzLDMuOTEgLTIwLjE5MiwxMC41OSB2IC0zMS4wMyBoIC0xNS4wMTIgdiA4OS45NyBoIDE1LjAxMiB2IC05LjA4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY2OCI+PC9wYXRoPjxwYXRoIGQ9Im0gMTA1NS45Niw0MDI3LjQ2IGMgLTkuNDcsMCAtMTQuODksLTMuNzggLTE0Ljg5LC0xNy40MSB2IC0zNS41OSBoIC0xNS4wMiB2IDY3Ljg5IGggMTQuNzYgdiAtMTIuMTIgYyAzLjY2LDcuNTggMTAuMjMsMTIuMTIgMTguNDIsMTIuMjUgMS4xNCwwIDIuNzgsLTAuMTMgMy45MiwtMC4yNSB2IC0xNS4xNSBjIC0yLjUyLDAuMjUgLTQuOTIsMC4zOCAtNy4xOSwwLjM4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY3MCI+PC9wYXRoPjxwYXRoIGQ9Im0gMTExNS4zNiw0MDA4LjI4IGMgMCwxNS42NSAtOC40NSwyMy4zNSAtMTcuOTIsMjMuMzUgLTkuNDcsMCAtMTcuOTIsLTcuNyAtMTcuOTIsLTIzLjM1IDAsLTE1LjY0IDguNDUsLTIzLjIyIDE3LjkyLC0yMy4yMiA5LjQ3LDAgMTcuOTIsNy41OCAxNy45MiwyMy4yMiB6IG0gLTE3LjkyLC0zNS40NiBjIC0xNi41MywwIC0zMy40NCwxMC45OCAtMzMuNDQsMzUuNDYgMCwyNC40OCAxNi45MSwzNS41OCAzMy40NCwzNS41OCAxNi41MywwIDMzLjQ0LC0xMS4xIDMzLjQ0LC0zNS41OCAwLC0yNC40OCAtMTYuOTEsLTM1LjQ2IC0zMy40NCwtMzUuNDYiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjcyIj48L3BhdGg+PHBhdGggZD0ibSAxMTUyLjQyLDQwMDguNDEgYyAwLC0xNC4zOSA3LjE5LC0yMy4zNSAxNy4xNiwtMjMuMzUgOS44NSwwIDE3LjU0LDcuNyAxNy41NCwyMy4zNSAwLDE1LjY0IC03LjY5LDIzLjIyIC0xNy41NCwyMy4yMiAtOS45NywwIC0xNy4xNiwtOC45NyAtMTcuMTYsLTIzLjIyIHogbSA0OS4wOSw1Ny41NCB2IC05MS40OSBoIC0xNS4wMiB2IDguOTUgYyAtNC4wNCwtNi42OCAtMTEuMTEsLTEwLjU5IC0yMC4xOSwtMTAuNTkgLTE2LjAzLDAgLTI5LjUzLDEzLjc2IC0yOS41MywzNS41OSAwLDIxLjcgMTMuNSwzNS40NSAyOS41MywzNS40NSA5LjA4LDAgMTYuMTUsLTMuOTEgMjAuMTksLTEwLjU5IHYgMzIuNjggaCAxNS4wMiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2NzQiPjwvcGF0aD48cGF0aCBkPSJtIDEyMzcuNjgsMzk3Mi44MiBjIC0xNi4xNiwwIC0yMi43MiwxMC41OSAtMjIuNzIsMjYuNzUgdiA0Mi43OCBoIDE1LjAyIHYgLTM5LjEyIGMgMCwtOS4yMSAxLjI2LC0xOC4xNyAxMi40OSwtMTguMTcgMTEuMjMsMCAxNS4yNyw4LjgzIDE1LjI3LDIxLjA3IHYgMzYuMjIgaCAxNS4wMiB2IC02Ny44OSBoIC0xNS4wMiB2IDkuMzQgYyAtMy45MSwtNy4wNyAtMTAuODUsLTEwLjk4IC0yMC4wNiwtMTAuOTgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjc2Ij48L3BhdGg+PHBhdGggZD0ibSAxMzMxLjUyLDQwMTkuMTMgYyAtMS4yNiw3LjE5IC03LjU3LDEyLjI1IC0xNS43OCwxMi4yNSAtOS4zMywwIC0xNy43OSwtNi45NSAtMTcuNzksLTIyLjk3IDAsLTE2LjE2IDguNTgsLTIzLjEgMTcuNDIsLTIzLjEgNy4zMSwwIDE0Ljc2LDMuMjggMTYuNjUsMTIuMzcgaCAxNC42NCBjIC0zLjAzLC0xNS45IC0xNy4wMywtMjQuODYgLTMxLjU1LC0yNC44NiAtMTkuNjgsMCAtMzIuNjgsMTUuMjcgLTMyLjY4LDM1LjQ2IDAsMjAuMiAxMy4xMiwzNS41OCAzMy4zMSwzNS41OCAxNC43NywwIDI3Ljg5LC05LjU4IDMwLjQxLC0yNC43MyBoIC0xNC42MyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2NzgiPjwvcGF0aD48cGF0aCBkPSJtIDE0MDIuMDEsNDAxNS4xIGMgLTAuMzcsMTAuNTkgLTguNDUsMTcuMDMgLTE3LjI4LDE3LjAzIC03LjA3LDAgLTE2Ljc4LC00LjE2IC0xOC4wNSwtMTcuMDMgeiBtIC0xNi45MSwtMjkuNzkgYyA3LjgzLDAgMTQuMDEsMy4xNSAxNi42Niw5LjQ2IGggMTQuNzcgYyAtMy4xNiwtMTAuODQgLTEzLjI1LC0yMS45NSAtMzAuNzksLTIxLjk1IC0yMS44MywwIC0zNC4zMywxNi42NiAtMzQuMzMsMzYuMDkgMCwyMC40NSAxNC4wMSwzNC45NSAzMy4zMiwzNC45NSAyMC44MiwwIDMzLjgyLC0xNi45MSAzMi41NiwtMzkuNzQgaCAtNTAuNjEgYyAxLjAxLC0xMi42MyA5Ljg0LC0xOC44MSAxOC40MiwtMTguODEiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjgwIj48L3BhdGg+PHBhdGggZD0ibSAxNDU2Ljk5LDQwMjcuNDYgYyAtOS40NiwwIC0xNC44OCwtMy43OCAtMTQuODgsLTE3LjQxIHYgLTM1LjU5IGggLTE1LjAyIHYgNjcuODkgaCAxNC43NiB2IC0xMi4xMiBjIDMuNjYsNy41OCAxMC4yMywxMi4xMiAxOC40MiwxMi4yNSAxLjE0LDAgMi43OCwtMC4xMyAzLjkyLC0wLjI1IHYgLTE1LjE1IGMgLTIuNTIsMC4yNSAtNC45MiwwLjM4IC03LjIsMC4zOCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2ODIiPjwvcGF0aD48cGF0aCBkPSJtIDAsNDIxMS42NCBjIDAsMjkuNjcgMjQuMDUwOCw1My43MSA1My43MTg4LDUzLjcxIDEwLjIzODIsMCA0NS41ODk4LDAgNTUuODI0MiwwIDI5LjY2OCwwIDUzLjcxOSwtMjQuMDQgNTMuNzE5LC01My43MSAwLC0xMC4yNSAwLC00NS42IDAsLTU1LjgzIDAsLTI5LjY3IC0yNC4wNTEsLTUzLjcyIC01My43MTksLTUzLjcyIC0xMC4yMzQ0LDAgLTQ1LjU4NiwwIC01NS44MjQyLDAgLTI5LjY2OCwwIC01My43MTg4LDI0LjA1IC01My43MTg4LDUzLjcyIDAsMTAuMjMgMCw0NS41OCAwLDU1LjgzIiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY4NCI+PC9wYXRoPjxwYXRoIGQ9Im0gNTYuNDY0OCw0MjEwLjA2IGggMTAuOTcyNyBsIDEyLjU1ODYsLTE3LjgzIDEyLjg0NzcsMTcuODMgaCAxMC4zOTQyIGwgLTE4LjA0NjYsLTI1LjEyIDE5LjI3MzYsLTI3LjIxIEggOTMuNDkyMiBsIC0xMy44NTU1LDE5LjU2IC0xNC4wNzQyLC0xOS41NiBIIDU1LjI0MjIgbCAxOS4yNjk1LDI2Ljc4IC0xOC4wNDY5LDI1LjU1IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY4NiI+PC9wYXRoPjxwYXRoIGQ9Im0gMzA0LjcwMywzNjU1LjE5IGMgMTEuMzYsMCAxNy4wMzUsNS4xOCAxNy4wMzUsMTQuMjYgMCw5LjM0IC01LjY3NSwxMy44OSAtMTcuOTE4LDEzLjg5IGggLTIwLjQ0MSB2IC0yOC4xNSB6IG0gLTEuMzg3LDQwLjM4IGMgOS4zNCwwIDE1LjE0MSw0LjE2IDE1LjE0MSwxMy4xMyAwLDguMDggLTYuMDU1LDEyLjI0IC0xNS4xNDEsMTIuMjQgaCAtMTkuOTM3IHYgLTI1LjM3IHogbSAtMS41MTEsMzguMjQgYyAxNi42NTIsMCAzMi45MzMsLTQuNTQgMzIuOTMzLC0yMy4zNCAwLC04LjU5IC00Ljc5NywtMTYuMjggLTEwLjIxOCwtMTkuNTYgNy41NjYsLTMuNDEgMTMuNzUzLC05LjM0IDEzLjc1MywtMjEuNDYgMCwtMTkuNjkgLTE1LjUyMywtMjcuMTMgLTM0LjE5OSwtMjcuMTMgaCAtMzYuNzE5IHYgOTEuNDkgaCAzNC40NSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2ODgiPjwvcGF0aD48cGF0aCBkPSJtIDM0OC4xOTEsMzY0Mi4zMiB2IDkxLjQ5IGggMTUuMDEyIHYgLTkxLjQ5IGggLTE1LjAxMiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg2OTAiPjwvcGF0aD48cGF0aCBkPSJtIDQyNC4zOTEsMzY3Ni4xNCBjIDAsMTUuNjUgLTguNDU3LDIzLjM1IC0xNy45MTgsMjMuMzUgLTkuNDY5LDAgLTE3LjkyMiwtNy43IC0xNy45MjIsLTIzLjM1IDAsLTE1LjY0IDguNDUzLC0yMy4yMiAxNy45MjIsLTIzLjIyIDkuNDYxLDAgMTcuOTE4LDcuNTggMTcuOTE4LDIzLjIyIHogbSAtMTcuOTE4LC0zNS40NiBjIC0xNi41MzUsMCAtMzMuNDQ2LDEwLjk4IC0zMy40NDYsMzUuNDYgMCwyNC40OCAxNi45MTEsMzUuNTkgMzMuNDQ2LDM1LjU5IDE2LjUyNywwIDMzLjQzNywtMTEuMTEgMzMuNDM3LC0zNS41OSAwLC0yNC40OCAtMTYuOTEsLTM1LjQ2IC0zMy40MzcsLTM1LjQ2IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY5MiI+PC9wYXRoPjxwYXRoIGQ9Im0gNDk0Ljg4MywzNjg2Ljk5IGMgLTEuMjY2LDcuMiAtNy41NywxMi4yNSAtMTUuNzc0LDEyLjI1IC05LjMzNiwwIC0xNy43OTMsLTYuOTUgLTE3Ljc5MywtMjIuOTcgMCwtMTYuMTUgOC41NzksLTIzLjEgMTcuNDE0LC0yMy4xIDcuMzE3LDAgMTQuNzYyLDMuMjggMTYuNjU3LDEyLjM4IGggMTQuNjQgYyAtMy4wMzEsLTE1LjkxIC0xNy4wMzksLTI0Ljg3IC0zMS41NSwtMjQuODcgLTE5LjY4OCwwIC0zMi42ODQsMTUuMjggLTMyLjY4NCwzNS40NiAwLDIwLjIgMTMuMTI1LDM1LjU5IDMzLjMxNiwzNS41OSAxNC43NjIsMCAyNy44ODcsLTkuNTkgMzAuNDExLC0yNC43NCBoIC0xNC42MzciIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjk0Ij48L3BhdGg+PHBhdGggZD0ibSA1MzQuMDksMzY4Mi45NiAyNS4xMDksMjcuMjUgaCAxOC4wNDcgbCAtMjUuOTk2LC0yNy44OSAyOC44OTgsLTQwIGggLTE3LjUzOSBsIC0yMS4zMjgsMjkuNDEgLTcuMTkxLC03LjcgdiAtMjEuNzEgaCAtMTUuMDE2IHYgOTEuNDkgaCAxNS4wMTYgdiAtNTAuODUiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNjk2Ij48L3BhdGg+PHBhdGggZD0ibSA2MDYuNjA5LDM3MDAuMjQgYyAtNi41NjIsMCAtMTIuNjE3LC0yLjkgLTEyLjYxNywtNy40NCAwLC00LjU0IDMuMjgxLC02Ljk0IDkuMDgyLC04LjA4IGwgOS41OTQsLTEuODkgYyAxMy43NSwtMi42NSAyNC4yMjcsLTYuOTQgMjQuMjI3LC0yMC4yIDAsLTE0LjEzIC0xMy4zNzksLTIxLjk1IC0yOC43NzQsLTIxLjk1IC0xNi42NTYsMCAtMjcuNzU4LDkuNDYgLTI5LjM5OCwyMi4zNCBoIDE0LjYzMiBjIDEuMzkxLC02Ljk1IDYuNDM4LC0xMC45OCAxNS4yNywtMTAuOTggNy44MjQsMCAxMy42MzMsMy4yOCAxMy42MzMsOC44NCAwLDUuNTQgLTUuMDUxLDguMDcgLTExLjczOCw5LjMzIGwgLTEwLjIxOSwyLjAxIGMgLTExLjQ4NSwyLjI4IC0yMC40NDYsNy40NiAtMjAuNDQ2LDE5LjgyIDAsMTEuOTkgMTIuODcyLDE5LjY5IDI3LjYzNywxOS42OSAxMy4yNSwwIDI1LjM2LC02LjQ0IDI4LjE0MSwtMjAuMDcgSCA2MjEuNSBjIC0xLjY0MSw2LjE5IC03LjMyLDguNTggLTE0Ljg5MSw4LjU4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDY5OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNzE5Ljg2NywzNjc2LjE0IGMgMCwxNS42NSAtOC40NTcsMjMuMzUgLTE3LjkxOCwyMy4zNSAtOS40NjksMCAtMTcuOTE4LC03LjcgLTE3LjkxOCwtMjMuMzUgMCwtMTUuNjQgOC40NDksLTIzLjIyIDE3LjkxOCwtMjMuMjIgOS40NjEsMCAxNy45MTgsNy41OCAxNy45MTgsMjMuMjIgeiBtIC0xNy45MTgsLTM1LjQ2IGMgLTE2LjUzMSwwIC0zMy40NDEsMTAuOTggLTMzLjQ0MSwzNS40NiAwLDI0LjQ4IDE2LjkxLDM1LjU5IDMzLjQ0MSwzNS41OSAxNi41MjgsMCAzMy40MzgsLTExLjExIDMzLjQzOCwtMzUuNTkgMCwtMjQuNDggLTE2LjkxLC0zNS40NiAtMzMuNDM4LC0zNS40NiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3MDAiPjwvcGF0aD48cGF0aCBkPSJtIDc3MC4yOTMsMzczMy44MSBoIDUuOTM0IHYgLTExLjQ5IGggLTQuMjkzIGMgLTcuNDQ2LDAgLTkuMDg2LC0xLjM4IC05LjA4NiwtOC40NCB2IC0zLjY3IGggMTMuMzc5IHYgLTEwLjg1IGggLTEzLjM3OSB2IC01Ny4wNCBoIC0xNS4wMTYgdiA1Ny4wNCBoIC05LjQ2MSB2IDEwLjg1IGggOS40NjEgdiA0LjE2IGMgMCwxNS45MSA2LjA2MywxOS40NCAyMi40NjEsMTkuNDQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzAyIj48L3BhdGg+PHBhdGggZD0ibSA4MjcuNjcyLDM3MjguMTMgdiAtMTcuOTIgaCAxMy42MjkgdiAtMTAuODUgaCAtMTMuNjI5IHYgLTM2Ljk3IGMgMCwtNi45NCAxLjY0MSwtOC41OCA4LjA3NCwtOC41OCBoIDUuNDM0IHYgLTExLjQ5IGggLTExLjExIGMgLTE0LjUxMSwwIC0xNy40MTQsMy45MiAtMTcuNDE0LDE3LjggdiAzOS4yNCBoIC0xMC4wOTcgdiAxMC44NSBoIDEwLjA5NyB2IDE3LjkyIGggMTUuMDE2IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDcwNCI+PC9wYXRoPjxwYXRoIGQ9Im0gODg2LjQ1NywzNzExLjczIGMgMTYuNDA2LDAgMjMuMDk0LC0xMC42IDIzLjA5NCwtMjYuNzUgdiAtNDIuNjYgaCAtMTUuMDIgdiAzOSBjIDAsOS4yMSAtMS4zODYsMTguMTcgLTEyLjg3MSwxOC4xNyAtMTEuNDc2LDAgLTE1Ljc2OSwtOC44NCAtMTUuNzY5LC0yMS4wNyB2IC0zNi4xIGggLTE1LjAxNiB2IDkxLjQ5IGggMTUuMDE2IHYgLTMzLjA2IGMgMy45MSw3LjA2IDExLjEwMSwxMC45OCAyMC41NjYsMTAuOTgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzA2Ij48L3BhdGg+PHBhdGggZD0ibSA5NjguNjkxLDM2ODIuOTYgYyAtMC4zNzgsMTAuNTkgLTguNDU3LDE3LjAzIC0xNy4yODksMTcuMDMgLTcuMDY2LDAgLTE2Ljc4MSwtNC4xNiAtMTguMDQ3LC0xNy4wMyB6IG0gLTE2LjkxNCwtMjkuNzkgYyA3LjgyOCwwIDE0LjAwOCwzLjE2IDE2LjY2MSw5LjQ2IGggMTQuNzY1IGMgLTMuMTU2LC0xMC44NCAtMTMuMjUsLTIxLjk1IC0zMC43ODksLTIxLjk1IC0yMS44MzIsMCAtMzQuMzI4LDE2LjY2IC0zNC4zMjgsMzYuMSAwLDIwLjQzIDE0LjAxMiwzNC45NSAzMy4zMTYsMzQuOTUgMjAuODIxLDAgMzMuODIxLC0xNi45MSAzMi41NTksLTM5Ljc1IGggLTUwLjYwNiBjIDEuMDEyLC0xMi42MyA5Ljg0NCwtMTguODEgMTguNDIyLC0xOC44MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3MDgiPjwvcGF0aD48cGF0aCBkPSJtIDI2Ni41OTgsMzQ4NC42OCB2IDkxLjQ4IGggMTUuMDE1IHYgLTkxLjQ4IGggLTE1LjAxNSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3MTAiPjwvcGF0aD48cGF0aCBkPSJtIDM0Mi43OTMsMzUxOC40OSBjIDAsMTUuNjUgLTguNDU3LDIzLjM1IC0xNy45MTgsMjMuMzUgLTkuNDY5LDAgLTE3LjkyMiwtNy43IC0xNy45MjIsLTIzLjM1IDAsLTE1LjY0IDguNDUzLC0yMy4yMiAxNy45MjIsLTIzLjIyIDkuNDYxLDAgMTcuOTE4LDcuNTggMTcuOTE4LDIzLjIyIHogbSAtMTcuOTE4LC0zNS40NSBjIC0xNi41MzUsMCAtMzMuNDQxLDEwLjk3IC0zMy40NDEsMzUuNDUgMCwyNC40OSAxNi45MDYsMzUuNTkgMzMuNDQxLDM1LjU5IDE2LjUyNywwIDMzLjQzOCwtMTEuMSAzMy40MzgsLTM1LjU5IDAsLTI0LjQ4IC0xNi45MTEsLTM1LjQ1IC0zMy40MzgsLTM1LjQ1IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDcxMiI+PC9wYXRoPjxwYXRoIGQ9Im0gNDAzLjY5OSwzNTU0LjA4IGMgMTYuNDA2LDAgMjMuMDk0LC0xMC42IDIzLjA5NCwtMjYuNzUgdiAtNDIuNjUgaCAtMTUuMDIgdiAzOC45OSBjIDAsOS4yMSAtMS4zODYsMTguMTcgLTEyLjg3MSwxOC4xNyAtMTEuNDgsMCAtMTUuNzY5LC04LjgzIC0xNS43NjksLTIxLjA3IHYgLTM2LjA5IGggLTE1LjAxNiB2IDY3Ljg5IGggMTUuMDE2IHYgLTkuNDcgYyAzLjkxLDcuMDYgMTEuMTAxLDEwLjk4IDIwLjU2NiwxMC45OCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3MTQiPjwvcGF0aD48cGF0aCBkPSJtIDQ1MC44NTIsMzUyMC4wMSBjIDAsLTEzLjg4IDcuMTkxLC0yMi4zNCAxNy4xNjQsLTIyLjM0IDkuODM2LDAgMTcuNTM5LDcuMDcgMTcuNTM5LDIyLjM0IDAsMTUuMTQgLTcuNzAzLDIyLjA4IC0xNy41MzksMjIuMDggLTkuOTczLDAgLTE3LjE2NCwtOC40NSAtMTcuMTY0LC0yMi4wOCB6IG0gNDkuMDg2LDMyLjU2IHYgLTYxLjA4IGMgMCwtMTEuMSAtMi43NzQsLTE4LjkzIC04LjIwNCwtMjMuOTcgLTUuNDI1LC01LjA1IC0xMy41LC03LjMzIC0yNC4xMDEsLTcuMzMgLTE0Ljg4NywwIC0yNi43NTQsNS45MyAtMjkuMDI0LDIwLjgyIGggMTQuODk1IGMgMS4zODcsLTYuMyA1LjU1MSwtOC45NSAxNC41MTIsLTguOTUgNi42ODMsMCAxMC45NzYsMS44OSAxMy41LDQuOTIgMi41MjMsMi45IDMuNDA2LDcuMDYgMy40MDYsMTEuNDggdiA3Ljk1IGMgLTQuMDM1LC02LjY5IC0xMS4xMDIsLTEwLjYgLTIwLjE4OCwtMTAuNiAtMTYuMDI3LDAgLTI5LjUzNSwxMyAtMjkuNTM1LDM0LjIgMCwyMS4yIDEzLjUwOCwzNC4wNyAyOS41MzUsMzQuMDcgOS4wODYsMCAxNi4xNTMsLTMuOTIgMjAuMTg4LC0xMC42IHYgOS4wOSBoIDE1LjAxNiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3MTYiPjwvcGF0aD48cGF0aCBkPSJtIDU2MC4yMTUsMzUyNS4zMSBjIC0wLjM3OSwxMC42IC04LjQ1NywxNy4wMyAtMTcuMjg5LDE3LjAzIC03LjA2NywwIC0xNi43ODEsLTQuMTYgLTE4LjA0NywtMTcuMDMgeiBtIC0xNi45MTQsLTI5Ljc4IGMgNy44MjgsMCAxNC4wMTIsMy4xNSAxNi42Niw5LjQ2IGggMTQuNzY2IGMgLTMuMTU3LC0xMC44NSAtMTMuMjUsLTIxLjk1IC0zMC43ODksLTIxLjk1IC0yMS44MzMsMCAtMzQuMzI5LDE2LjY2IC0zNC4zMjksMzYuMDkgMCwyMC40NCAxNC4wMDgsMzQuOTUgMzMuMzE3LDM0Ljk1IDIwLjgyLDAgMzMuODE2LC0xNi45MSAzMi41NTgsLTM5Ljc1IGggLTUwLjYwNSBjIDEuMDEyLC0xMi42MiA5Ljg0NCwtMTguOCAxOC40MjIsLTE4LjgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzE4Ij48L3BhdGg+PHBhdGggZD0ibSA2MDkuMzg3LDM1NDIuNiBjIC02LjU2MywwIC0xMi42MTcsLTIuOSAtMTIuNjE3LC03LjQ1IDAsLTQuNTQgMy4yODEsLTYuOTQgOS4wODIsLTguMDcgbCA5LjU4OSwtMS45IGMgMTMuNzU0LC0yLjY0IDI0LjIyNywtNi45NCAyNC4yMjcsLTIwLjE5IDAsLTE0LjEzIC0xMy4zNzEsLTIxLjk1IC0yOC43NywtMjEuOTUgLTE2LjY1NiwwIC0yNy43NjEsOS40NiAtMjkuMzk4LDIyLjMzIGggMTQuNjMzIGMgMS4zOTQsLTYuOTQgNi40MzcsLTEwLjk4IDE1LjI3MywtMTAuOTggNy44MjQsMCAxMy42MjksMy4yOCAxMy42MjksOC44NCAwLDUuNTUgLTUuMDQ3LDguMDggLTExLjczOCw5LjM0IGwgLTEwLjIxOSwyLjAxIGMgLTExLjQ4NCwyLjI3IC0yMC40NDUsNy40NSAtMjAuNDQ1LDE5LjgxIDAsMTEuOTkgMTIuODcxLDE5LjY5IDI3LjYzNywxOS42OSAxMy4yNDYsMCAyNS4zNjcsLTYuNDQgMjguMTQsLTIwLjA3IGggLTE0LjEzMyBjIC0xLjY0LDYuMTkgLTcuMzE2LDguNTkgLTE0Ljg5LDguNTkiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzIwIj48L3BhdGg+PHBhdGggZD0ibSA2NjcuMzkxLDM1NzAuNDkgdiAtMTcuOTIgaCAxMy42MjUgdiAtMTAuODUgaCAtMTMuNjI1IHYgLTM2Ljk4IGMgMCwtNi45NCAxLjY0LC04LjU4IDguMDc0LC04LjU4IGggNS40MyB2IC0xMS40OCBoIC0xMS4xMSBjIC0xNC41MTIsMCAtMTcuNDEsMy45MSAtMTcuNDEsMTcuNzkgdiAzOS4yNSBoIC0xMC4wOTggdiAxMC44NSBoIDEwLjA5OCB2IDE3LjkyIGggMTUuMDE2IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDcyMiI+PC9wYXRoPjxwYXRoIGQ9Im0gNzYxLjQ4NCwzNTI5LjM0IGMgLTEuMjYxLDcuMiAtNy41NzQsMTIuMjUgLTE1Ljc3MywxMi4yNSAtOS4zNCwwIC0xNy43OTMsLTYuOTQgLTE3Ljc5MywtMjIuOTcgMCwtMTYuMTUgOC41NzgsLTIzLjA5IDE3LjQxNCwtMjMuMDkgNy4zMTYsMCAxNC43NjIsMy4yOCAxNi42NTYsMTIuMzcgaCAxNC42NDEgYyAtMy4wMjcsLTE1LjkxIC0xNy4wMzksLTI0Ljg2IC0zMS41NTEsLTI0Ljg2IC0xOS42ODcsMCAtMzIuNjgzLDE1LjI3IC0zMi42ODMsMzUuNDUgMCwyMC4yIDEzLjEyNSwzNS41OSAzMy4zMTYsMzUuNTkgMTQuNzY2LDAgMjcuODkxLC05LjU5IDMwLjQwNiwtMjQuNzQgaCAtMTQuNjMzIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDcyNCI+PC9wYXRoPjxwYXRoIGQ9Im0gODIxLjI1OCwzNTU0LjA4IGMgMTYuNDAyLDAgMjMuMDk0LC0xMC42IDIzLjA5NCwtMjYuNzUgdiAtNDIuNjUgaCAtMTUuMDIgdiAzOC45OSBjIDAsOS4yMSAtMS4zODcsMTguMTcgLTEyLjg3MSwxOC4xNyAtMTEuNDgxLDAgLTE1Ljc3LC04LjgzIC0xNS43NywtMjEuMDcgdiAtMzYuMDkgaCAtMTUuMDE1IHYgOTEuNDggaCAxNS4wMTUgdiAtMzMuMDYgYyAzLjkxMSw3LjA2IDExLjEwMiwxMC45OCAyMC41NjcsMTAuOTgiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzI2Ij48L3BhdGg+PHBhdGggZD0ibSA4NjkuMjkzLDM1MDMuNzMgYyAwLC01LjkzIDQuOTIyLC05LjQ2IDEyLjQ5MiwtOS40NiAxMS4xMDYsMCAxNy42NjgsNS42OCAxNy42NjgsMTcuMTUgdiA1LjE4IGMgLTIxLjQ1MywtMi4wMiAtMzAuMTYsLTUuMDUgLTMwLjE2LC0xMi44NyB6IG0gMjkuNzgxLDIzLjM1IHYgMS4yNiBjIDAsMTEuNjEgLTYuNjkxLDE1LjE0IC0xNC4xMzYsMTUuMTQgLTcuNTcxLDAgLTEzLjI0NywtNC4wNCAtMTMuNjI5LC0xMi4yNCBoIC0xNC43NTggYyAxLjAwNCwxMy44OSAxMi40ODgsMjMuMzUgMjguODk0LDIzLjM1IDE2LjI4MiwwIDI5LjAyNCwtNy40NSAyOC42NDUsLTI5LjE1IDAsLTMuNDEgLTAuMjUsLTExLjM2IC0wLjI1LC0xNy41NCAwLC04LjU5IDAuNzU4LC0xNy41NSAyLjAxNSwtMjMuMjIgaCAtMTMuNzUzIGMgLTAuNTA0LDIuOSAtMS4wMTIsNC41NCAtMS4yNjIsOS4yIC00LjI4OSwtNy4zMSAtMTIuMzY3LC0xMC44NCAtMjIuMzM2LC0xMC44NCAtMTQuNzYyLDAgLTI1LjEwOSw3Ljk0IC0yNS4xMDksMjAuMzEgMCwxNi45MSAyMC44MiwyMS4yIDQ1LjY3OSwyMy43MyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3MjgiPjwvcGF0aD48cGF0aCBkPSJtIDk0MS42ODgsMzQ4NC42OCBoIC0xNS4wMTYgdiA2Ny44OSBoIDE1LjAxNiB6IG0gMCw3Ni4zNCBoIC0xNS4wMTYgdiAxNS4xNCBoIDE1LjAxNiB2IC0xNS4xNCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3MzAiPjwvcGF0aD48cGF0aCBkPSJtIDk5MS42MzMsMzU1NC4wOCBjIDE2LjQwNywwIDIzLjA5NywtMTAuNiAyMy4wOTcsLTI2Ljc1IHYgLTQyLjY1IGggLTE1LjAyMyB2IDM4Ljk5IGMgMCw5LjIxIC0xLjM4NywxOC4xNyAtMTIuODcxLDE4LjE3IC0xMS40NzcsMCAtMTUuNzcsLTguODMgLTE1Ljc3LC0yMS4wNyB2IC0zNi4wOSBoIC0xNS4wMTUgdiA2Ny44OSBoIDE1LjAxNSB2IC05LjQ3IGMgMy45MTEsNy4wNiAxMS4xMDIsMTAuOTggMjAuNTY3LDEwLjk4IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDczMiI+PC9wYXRoPjxwYXRoIGQ9Ik0gMzE3Ljg1OSwzMjczLjA0IEggMzEwLjUgYyAtMi42MzMsOC44MyAtMTAuMTk5LDEzLjY3IC0yMS43NjIsMTMuNjcgLTcuNjc1LDAgLTE4LjUwOCwtMy4wNSAtMTguNTA4LC0xMy4wNCAwLC03LjY4IDYuMjA0LC0xMS41NiAxNC43MTksLTEzLjQ2IGwgOS4wNDMsLTEuOTkgYyAxMS4wMzksLTIuNTMgMjUuNjUzLC02Ljk0IDI1LjY1MywtMjEuNDUgMCwtMTQuNjEgLTEzLjM1NiwtMjIuMjkgLTI4LjE4LC0yMi4yOSAtMTkuMDI3LDAgLTI5LjUzOSwxMC42MiAtMzEuMjE5LDI0LjI5IGggNy4zNTkgYyAyLjYyNSwtMTIuMDkgMTEuMTQxLC0xNy41NiAyMy41NDcsLTE3LjU2IDguMzA5LDAgMjEuMTMzLDMuMDUgMjEuMTMzLDE0LjQgMCw5LjM2IC05LjA0MywxMy42NyAtMTkuNzY1LDE1Ljk4IGwgLTkuNTcxLDIuMTEgYyAtOS45ODQsMi4zIC0xOS45NzIsNy4xNSAtMTkuOTcyLDE5LjY2IDAsMTQuMDggMTQuMTkxLDIwLjA4IDI2LjQ5MiwyMC4wOCAxNC45MzMsMCAyNS42NTIsLTcuNDcgMjguMzksLTIwLjQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzM0Ij48L3BhdGg+PHBhdGggZD0ibSAzNzQuMjg1LDMyNDguMjMgYyAwLDkuNTYgLTYuODM2LDE5LjI0IC0xOC4xOTEsMTkuMjQgLTEwLjUxMiwwIC0xOC4wODYsLTYuNzMgLTE5LjQ0NiwtMTkuMjQgeiBtIC0xOC4wODYsMjUuMTMgYyAxNS45ODEsMCAyNi4wNzQsLTEzLjQ2IDI1LjIzNSwtMzEuMTMgaCAtNDQuOTk2IGMgMC4yMSwtMTMuNjYgOC44MjgsLTIxLjc1IDIwLjM5NCwtMjEuNzUgOC44MjgsMCAxNS4wMzUsNC41MiAxNy4yNDIsMTIuMjkgaCA2LjgzMiBjIC0yLjczNCwtMTEuNjcgLTEyLjA5LC0xOC4yOSAtMjQuNSwtMTguMjkgLTE2LjYwNSwwIC0yNi42OTksMTEuODkgLTI2LjY5OSwyOS40MyAwLDE4LjMgMTEuMzU2LDI5LjQ1IDI2LjQ5MiwyOS40NSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3MzYiPjwvcGF0aD48cGF0aCBkPSJtIDM5NC44NjcsMzIxNS44NSB2IDc2LjIyIGggNi41MiB2IC03Ni4yMiBoIC02LjUyIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDczOCI+PC9wYXRoPjxwYXRoIGQ9Im0gNDU5LjQxLDMyNDguMjMgYyAwLDkuNTYgLTYuODM2LDE5LjI0IC0xOC4xODcsMTkuMjQgLTEwLjUxMiwwIC0xOC4wODYsLTYuNzMgLTE5LjQ1LC0xOS4yNCB6IG0gLTE4LjA4NiwyNS4xMyBjIDE1Ljk4MSwwIDI2LjA3NCwtMTMuNDYgMjUuMjM1LC0zMS4xMyBoIC00NC45OTYgYyAwLjIxLC0xMy42NiA4LjgyOCwtMjEuNzUgMjAuMzk4LC0yMS43NSA4LjgyNCwwIDE1LjAzMSw0LjUyIDE3LjIzOCwxMi4yOSBoIDYuODMyIGMgLTIuNzM0LC0xMS42NyAtMTIuMDksLTE4LjI5IC0yNC40OTYsLTE4LjI5IC0xNi42MDUsMCAtMjYuNjk5LDExLjg5IC0yNi42OTksMjkuNDMgMCwxOC4zIDExLjM1MiwyOS40NSAyNi40ODgsMjkuNDUiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzQwIj48L3BhdGg+PHBhdGggZD0ibSA1MTguNDc3LDMyNTQuMjIgYyAtMi4xMDYsOC41MSAtOC44MzIsMTMuMTQgLTE3LjAzMiwxMy4xNCAtOS43ODEsMCAtMTguMzk4LC03Ljc4IC0xOC4zOTgsLTIzLjM0IDAsLTE2LjA4IDguNjE3LC0yMy41NCAxOC41MDQsLTIzLjU0IDkuNjcyLDAgMTUuNzY5LDYuMiAxNy4zNDcsMTMuMjQgaCA2LjkzOCBjIC0yLjMxMywtMTEuNjcgLTExLjc3NywtMTkuMjQgLTI0LjI4NSwtMTkuMjQgLTE2LjA4NiwwIC0yNS40NDIsMTEuOTggLTI1LjQ0MiwyOS40MyAwLDE3LjU2IDkuNDU3LDI5LjQ1IDI1Ljk2NSwyOS40NSAxMi44MjgsMCAyMS41NTUsLTguOTQgMjMuMjM1LC0xOS4xNCBoIC02LjgzMiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3NDIiPjwvcGF0aD48cGF0aCBkPSJtIDU0Ny42ODQsMzI4NS4xMyB2IC0xMi43MiBoIDExLjE0IHYgLTUuNjcgaCAtMTEuMTQgdiAtMzYuMTggYyAwLC03LjM1IDAuMjA3LC04LjgyIDcuNzc3LC04LjgyIGggMy4zNjMgdiAtNS44OSBoIC01LjM1OSBjIC0xMC4wOTQsMCAtMTIuNDEsMi4zMSAtMTIuNDEsMTMuNDUgdiAzNy40NCBoIC05LjM1NiB2IDUuNjcgaCA5LjM1NiB2IDEyLjcyIGggNi42MjkiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzQ0Ij48L3BhdGg+PHBhdGggZD0ibSA2MDguNDMsMzI4NS4xMyB2IC0xMi43MiBoIDExLjE0IHYgLTUuNjcgaCAtMTEuMTQgdiAtMzYuMTggYyAwLC03LjM1IDAuMjExLC04LjgyIDcuNzc3LC04LjgyIGggMy4zNjMgdiAtNS44OSBoIC01LjM1OSBjIC0xMC4wOTQsMCAtMTIuNDA2LDIuMzEgLTEyLjQwNiwxMy40NSB2IDM3LjQ0IGggLTkuMzU2IHYgNS42NyBoIDkuMzU2IHYgMTIuNzIgaCA2LjYyNSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3NDYiPjwvcGF0aD48cGF0aCBkPSJtIDY1OC4yNTQsMzI3My4zNiBjIDEzLjM0OCwwIDE5LjAyNywtNy45OSAxOS4wMjcsLTIxLjg3IHYgLTM1LjY0IGggLTYuNTE5IHYgMzMuODYgYyAwLDEwLjYxIC0yLjczNSwxNy43NiAtMTQuMTkyLDE3Ljc2IC05Ljc3NywwIC0xNy4xMzYsLTguMiAtMTcuMTM2LC0yMC4xOSB2IC0zMS40MyBoIC02LjUxNiB2IDc2LjIyIGggNi41MTYgdiAtMjkuMjMgYyAyLjczNCw1LjM2IDguMzA4LDEwLjUyIDE4LjgyLDEwLjUyIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDc0OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNzMzLjYwOSwzMjQ4LjIzIGMgMCw5LjU2IC02LjgzNiwxOS4yNCAtMTguMTg3LDE5LjI0IC0xMC41MTIsMCAtMTguMDg2LC02LjczIC0xOS40NDksLTE5LjI0IHogbSAtMTguMDg2LDI1LjEzIGMgMTUuOTgxLDAgMjYuMDc1LC0xMy40NiAyNS4yMzUsLTMxLjEzIGggLTQ0Ljk5NiBjIDAuMjExLC0xMy42NiA4LjgyOCwtMjEuNzUgMjAuMzk4LC0yMS43NSA4LjgyOCwwIDE1LjAzMSw0LjUyIDE3LjIzOCwxMi4yOSBoIDYuODMyIGMgLTIuNzM0LC0xMS42NyAtMTIuMDg5LC0xOC4yOSAtMjQuNDk2LC0xOC4yOSAtMTYuNjA1LDAgLTI2LjY5OSwxMS44OSAtMjYuNjk5LDI5LjQzIDAsMTguMyAxMS4zNTIsMjkuNDUgMjYuNDg4LDI5LjQ1IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDc1MCI+PC9wYXRoPjxwYXRoIGQ9Im0gODIxLjM2MywzMjQ4LjIzIGMgMCw5LjU2IC02LjgzNiwxOS4yNCAtMTguMTg3LDE5LjI0IC0xMC41MTYsMCAtMTguMDg2LC02LjczIC0xOS40NDksLTE5LjI0IHogbSAtMTguMDg2LDI1LjEzIGMgMTUuOTgxLDAgMjYuMDc1LC0xMy40NiAyNS4yMzUsLTMxLjEzIGggLTQ0Ljk5NiBjIDAuMjExLC0xMy42NiA4LjgyOCwtMjEuNzUgMjAuMzk0LC0yMS43NSA4LjgzMiwwIDE1LjAzNSw0LjUyIDE3LjI0MiwxMi4yOSBoIDYuODMyIGMgLTIuNzM0LC0xMS42NyAtMTIuMDg5LC0xOC4yOSAtMjQuNDk2LC0xOC4yOSAtMTYuNjA1LDAgLTI2LjY5OSwxMS44OSAtMjYuNjk5LDI5LjQzIDAsMTguMyAxMS4zNTIsMjkuNDUgMjYuNDg4LDI5LjQ1IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDc1MiI+PC9wYXRoPjxwYXRoIGQ9Im0gODc3LjY5MSwzMjQxLjcxIHYgMi43MyBjIC0yMy4wMjMsLTIuNTIgLTMyLjkwNiwtNS41NiAtMzIuOTA2LC0xNC40IDAsLTUuOTkgNS40NjksLTkuNzggMTIuOTM4LC05Ljc4IDEwLjUxMSwwIDE5Ljk2OCw1LjM2IDE5Ljk2OCwyMS40NSB6IG0gLTIxLjQ0NSwtMjcuMjMgYyAtMTAuNTEyLDAgLTE4LjcxMSw2LjA5IC0xOC43MTEsMTUuNDYgMCwxMi44MiAxMi42MTMsMTcuNTUgMzkuODQ0LDIwLjI4IHYgMiBjIDAsMTIuODMgLTcuNTY2LDE1LjY3IC0xNS43NywxNS42NyAtOS41NjYsMCAtMTUuMzQ3LC01LjM2IC0xNS44NzUsLTEyLjczIGggLTYuODM2IGMgMS40NzMsMTEuMTYgMTAuNTE2LDE4LjUxIDIzLjEyOSwxOC41MSAxMy4xNDUsMCAyMS44NzEsLTUuNDcgMjEuODcxLC0yMi4yOSAwLC03Ljc4IC0wLjEwOSwtMTIuOTIgLTAuMTA5LC0xNy40NSAwLC02LjQxIDAuMzIsLTExLjk5IDAuNjMzLC0xOC4wOCBoIC02LjYyMSBsIC0wLjMyMSw4LjYyIGMgLTMuNjc1LC02IC0xMC43MjIsLTkuOTkgLTIxLjIzNCwtOS45OSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3NTQiPjwvcGF0aD48cGF0aCBkPSJtIDkyMS41MTIsMzI2NS44OSBjIC0xMS42NzIsMCAtMTUuNDU3LC04LjQxIC0xNS40NTcsLTIwLjM5IHYgLTI5LjY1IGggLTYuNDEgdiA1Ni41NiBoIDYuMjAzIHYgLTEwLjMgYyAyLjUyMyw2LjYyIDkuODgyLDEwLjcyIDE2LjcxOCwxMC43MiAwLjUyLDAgMS4yNTgsMCAxLjg4NywtMC4xMSB2IC02LjkzIGMgLTEuMDQ3LDAuMSAtMS45OTYsMC4xIC0yLjk0MSwwLjEiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzU2Ij48L3BhdGg+PHBhdGggZD0ibSA5MzQuNTM1LDMyMTUuODUgdiA3Ni4yMiBoIDYuNTIgdiAtNzYuMjIgaCAtNi41MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3NTgiPjwvcGF0aD48cGF0aCBkPSJtIDk2NS40MzgsMzIxNS44NSBoIC02LjUyIHYgNTYuNTYgaCA2LjUyIHogbSAwLDY1LjgxIGggLTYuNTIgdiAxMC40MSBoIDYuNTIgdiAtMTAuNDEiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzYwIj48L3BhdGg+PHBhdGggZD0ibSAxMDIzLjQ2LDMyNDguMjMgYyAwLDkuNTYgLTYuODMsMTkuMjQgLTE4LjE5LDE5LjI0IC0xMC41MDgsMCAtMTguMDgyLC02LjczIC0xOS40NDYsLTE5LjI0IHogbSAtMTguMDgsMjUuMTMgYyAxNS45OCwwIDI2LjA3LC0xMy40NiAyNS4yMywtMzEuMTMgaCAtNDQuOTkzIGMgMC4yMDcsLTEzLjY2IDguODI4LC0yMS43NSAyMC4zOTMsLTIxLjc1IDguODMsMCAxNS4wNCw0LjUyIDE3LjI0LDEyLjI5IGggNi44MyBjIC0yLjczLC0xMS42NyAtMTIuMDksLTE4LjI5IC0yNC40OSwtMTguMjkgLTE2LjYxLDAgLTI2LjcwMywxMS44OSAtMjYuNzAzLDI5LjQzIDAsMTguMyAxMS4zNTUsMjkuNDUgMjYuNDkzLDI5LjQ1IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDc2MiI+PC9wYXRoPjxwYXRoIGQ9Im0gMTA2Mi41NSwzMjY3LjY3IGMgLTYuMjEsMCAtMTQuNCwtMi40MSAtMTQuNCwtOS4yNCAwLC01LjU3IDQuNDEsLTguNTIgMTAuNjEsLTkuNjcgbCA3Ljk5LC0xLjQ4IGMgOS4yNSwtMS42OCAxOS41NiwtNC44MyAxOS41NiwtMTUuNTUgMCwtMTEuMjUgLTEwLjIsLTE3LjI1IC0yMi41LC0xNy4yNSAtMTEuNjcsMCAtMjEuNzYsNS43OCAtMjMuNDUsMTguNzEgaCA2Ljg0IGMgMS4yNiwtOC45MyA4LjQxLC0xMi45MyAxNy4xMywtMTIuOTMgNi44NCwwIDE1LjM1LDIuODQgMTUuMzUsMTAuNDEgMCw2LjYyIC02LjMsOC45NCAtMTMuOTgsMTAuNDEgbCAtOC44MywxLjY4IGMgLTguMiwxLjU3IC0xNS4zNSw2LjMxIC0xNS4zNSwxNS4xNCAwLDguOTMgOC45NCwxNS41NiAyMS42NiwxNS41NiAxMi4wOSwwIDIwLjQsLTcuNDcgMjEuNzYsLTE2LjUxIGggLTYuODMgYyAtMS4zNyw2LjczIC03LjU3LDEwLjcyIC0xNS41NiwxMC43MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3NjQiPjwvcGF0aD48cGF0aCBkPSJtIDExMTAuMzYsMzI4NS4xMyB2IC0xMi43MiBoIDExLjE1IHYgLTUuNjcgaCAtMTEuMTUgdiAtMzYuMTggYyAwLC03LjM1IDAuMjEsLTguODIgNy43OCwtOC44MiBoIDMuMzcgdiAtNS44OSBoIC01LjM3IGMgLTEwLjA5LDAgLTEyLjQsMi4zMSAtMTIuNCwxMy40NSB2IDM3LjQ0IGggLTkuMzYgdiA1LjY3IGggOS4zNiB2IDEyLjcyIGggNi42MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3NjYiPjwvcGF0aD48cGF0aCBkPSJtIDI4MC43NDIsMzE2OC4zOCBoIDQuNjI5IHYgLTYgaCAtMy4yNjIgYyAtNy4xNDgsMCAtNy45ODgsLTAuNjIgLTcuOTg4LC03LjU3IHYgLTYuMDkgaCAxMS4yNSB2IC01LjY3IGggLTExLjI1IHYgLTUwLjg5IGggLTYuNTE2IHYgNTAuODkgaCAtNy43ODEgdiA1LjY3IGggNy43ODEgdiA3LjA0IGMgMCw5LjI2IDIuNDE1LDEyLjYyIDEzLjEzNywxMi42MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3NjgiPjwvcGF0aD48cGF0aCBkPSJtIDMwMy41NDcsMzA5Mi4xNiBoIC02LjUyIHYgNTYuNTYgaCA2LjUyIHogbSAwLDY1LjgxIGggLTYuNTIgdiAxMC40MSBoIDYuNTIgdiAtMTAuNDEiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzcwIj48L3BhdGg+PHBhdGggZD0ibSAzNDYuNzUsMzE0OS42NyBjIDEzLjM0OCwwIDE5LjAyNywtNy45OSAxOS4wMjcsLTIxLjg3IHYgLTM1LjY0IGggLTYuNTE5IHYgMzMuODUgYyAwLDEwLjYyIC0yLjczNSwxNy43NyAtMTQuMTkyLDE3Ljc3IC05Ljc3NywwIC0xNy4xMzYsLTguMjEgLTE3LjEzNiwtMjAuMTkgdiAtMzEuNDMgaCAtNi41MiB2IDU2LjU2IGggNi41MiB2IC05LjU3IGMgMi43MzQsNS4zNiA4LjMwOCwxMC41MiAxOC44MiwxMC41MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3NzIiPjwvcGF0aD48cGF0aCBkPSJtIDQxNy42ODgsMzExOC4wMiB2IDIuNzMgYyAtMjMuMDI0LC0yLjUyIC0zMi45MDcsLTUuNTcgLTMyLjkwNywtMTQuNCAwLC01Ljk5IDUuNDY5LC05Ljc4IDEyLjkzNCwtOS43OCAxMC41MTUsMCAxOS45NzMsNS4zNiAxOS45NzMsMjEuNDUgeiBtIC0yMS40NDYsLTI3LjIzIGMgLTEwLjUxMiwwIC0xOC43MTEsNi4wOSAtMTguNzExLDE1LjQ2IDAsMTIuODIgMTIuNjE0LDE3LjU1IDM5Ljg0NCwyMC4yOCB2IDIgYyAwLDEyLjgzIC03LjU3LDE1LjY3IC0xNS43NzMsMTUuNjcgLTkuNTY3LDAgLTE1LjM0NCwtNS4zNiAtMTUuODcyLC0xMi43MyBoIC02LjgzNSBjIDEuNDcyLDExLjE2IDEwLjUxNSwxOC41MSAyMy4xMjgsMTguNTEgMTMuMTQ1LDAgMjEuODcyLC01LjQ3IDIxLjg3MiwtMjIuMjkgMCwtNy43OCAtMC4xMSwtMTIuOTMgLTAuMTEsLTE3LjQ1IDAsLTYuNDEgMC4zMTcsLTExLjk5IDAuNjI5LC0xOC4wOCBoIC02LjYyMSBsIC0wLjMxNiw4LjYyIGMgLTMuNjc2LC02IC0xMC43MjMsLTkuOTkgLTIxLjIzNSwtOS45OSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3NzQiPjwvcGF0aD48cGF0aCBkPSJtIDQzOS42NDUsMzA5Mi4xNiB2IDc2LjIyIGggNi41MTkgdiAtNzYuMjIgaCAtNi41MTkiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzc2Ij48L3BhdGg+PHBhdGggZD0ibSA1MzMuMjk3LDMxMjAuMjIgYyAwLDE1LjA0IC03LjQ2MSwyMy41NiAtMTcuOTczLDIzLjU2IC04LjUxNSwwIC0xOC4xODcsLTYuODQgLTE4LjE4NywtMjMuNTYgMCwtMTYuNzEgOS42NzIsLTIzLjU0IDE4LjE4NywtMjMuNTQgMTAuNTEyLDAgMTcuOTczLDguNTEgMTcuOTczLDIzLjU0IHogbSAtMzUuNzQyLC0xOC44MiB2IC05LjI0IGggLTYuNTIgdiA3Ni4yMiBoIDYuNTIgdiAtMjkuNDQgYyAzLjk5Niw2LjgzIDEwLjgyNCwxMC43MyAxOS4xMzMsMTAuNzMgMTMuMDM1LDAgMjMuNjU2LC0xMC43MyAyMy42NTYsLTI5LjQ1IDAsLTE4LjgyIC0xMC42MjEsLTI5LjQzIC0yMy42NTYsLTI5LjQzIC04LjMwOSwwIC0xNS4xMzcsMy44OSAtMTkuMTMzLDEwLjYxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDc3OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNTUzLjY3MiwzMDkyLjE2IHYgNzYuMjIgaCA2LjUxOSB2IC03Ni4yMiBoIC02LjUxOSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3ODAiPjwvcGF0aD48cGF0aCBkPSJtIDYxNy45MDIsMzEyMC4yMiBjIDAsMTYuMTkgLTcuODg2LDIzLjQ1IC0xOC43MTEsMjMuNDUgLTEwLjgzMiwwIC0xOC42MDksLTcuMjYgLTE4LjYwOSwtMjMuNDUgMCwtMTYuMTggNy43NzcsLTIzLjQzIDE4LjYwOSwtMjMuNDMgMTAuODI1LDAgMTguNzExLDcuMjUgMTguNzExLDIzLjQzIHogbSA2LjkzOCwwIGMgMCwtMjAuNiAtMTIuMDksLTI5LjQzIC0yNS42NDksLTI5LjQzIC0xMy41NjYsMCAtMjUuNTQ2LDguODMgLTI1LjU0NiwyOS40MyAwLDIwLjYxIDExLjk4LDI5LjQ1IDI1LjU0NiwyOS40NSAxMy41NTksMCAyNS42NDksLTguODQgMjUuNjQ5LC0yOS40NSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3ODIiPjwvcGF0aD48cGF0aCBkPSJtIDY3Ny4wNywzMTMwLjUzIGMgLTIuMTAxLDguNTEgLTguODMyLDEzLjE0IC0xNy4wMzEsMTMuMTQgLTkuNzc3LDAgLTE4LjM5OCwtNy43OCAtMTguMzk4LC0yMy4zNCAwLC0xNi4wOCA4LjYyMSwtMjMuNTQgMTguNTA0LC0yMy41NCA5LjY3MSwwIDE1Ljc2OSw2LjIgMTcuMzQ3LDEzLjI0IGggNi45MzggYyAtMi4zMTMsLTExLjY3IC0xMS43NzgsLTE5LjI0IC0yNC4yODUsLTE5LjI0IC0xNi4wODYsMCAtMjUuNDQyLDExLjk4IC0yNS40NDIsMjkuNDMgMCwxNy41NiA5LjQ1NywyOS40NSAyNS45NjksMjkuNDUgMTIuODI0LDAgMjEuNTUxLC04Ljk0IDIzLjIzLC0xOS4xNCBoIC02LjgzMiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3ODQiPjwvcGF0aD48cGF0aCBkPSJtIDcwMy41NDcsMzEyMC40NCAyNS44NTksMjguMjggaCA3Ljk5MiBsIC0yMC45MjEsLTIyLjcxIDIyLjgxMiwtMzMuODUgaCAtNy41NyBsIC0xOS40NDYsMjkuMjIgLTguNzI2LC05LjQ2IHYgLTE5Ljc2IGggLTYuNTIgdiA3Ni4yMiBoIDYuNTIgdiAtNDcuOTQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzg2Ij48L3BhdGg+PHBhdGggZD0ibSA3ODIuODkxLDMwOTIuMTYgaCAtNi41MiB2IDU2LjU2IGggNi41MiB6IG0gMCw2NS44MSBoIC02LjUyIHYgMTAuNDEgaCA2LjUyIHYgLTEwLjQxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDc4OCI+PC9wYXRoPjxwYXRoIGQ9Im0gODI2LjA5LDMxNDkuNjcgYyAxMy4zNTEsMCAxOS4wMjcsLTcuOTkgMTkuMDI3LC0yMS44NyB2IC0zNS42NCBoIC02LjUxNSB2IDMzLjg1IGMgMCwxMC42MiAtMi43MzUsMTcuNzcgLTE0LjE5NiwxNy43NyAtOS43NzcsMCAtMTcuMTMzLC04LjIxIC0xNy4xMzMsLTIwLjE5IHYgLTMxLjQzIGggLTYuNTE5IHYgNTYuNTYgaCA2LjUxOSB2IC05LjU3IGMgMi43MzUsNS4zNiA4LjMwNSwxMC41MiAxOC44MTcsMTAuNTIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzkwIj48L3BhdGg+PHBhdGggZD0ibSA4OTcuNTUxLDMxNjEuNDQgdiAtMTIuNzIgaCAxMS4xNCB2IC01LjY3IGggLTExLjE0IHYgLTM2LjE4IGMgMCwtNy4zNSAwLjIxMSwtOC44MiA3Ljc3NywtOC44MiBoIDMuMzYzIHYgLTUuODkgaCAtNS4zNTkgYyAtMTAuMDk0LDAgLTEyLjQwNiwyLjMxIC0xMi40MDYsMTMuNDUgdiAzNy40NCBoIC05LjM1NiB2IDUuNjcgaCA5LjM1NiB2IDEyLjcyIGggNi42MjUiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoNzkyIj48L3BhdGg+PHBhdGggZD0ibSA5NDcuMzc1LDMxNDkuNjcgYyAxMy4zNDgsMCAxOS4wMjcsLTcuOTkgMTkuMDI3LC0yMS44NyB2IC0zNS42NCBoIC02LjUxOSB2IDMzLjg1IGMgMCwxMC42MiAtMi43MzUsMTcuNzcgLTE0LjE5MiwxNy43NyAtOS43NzcsMCAtMTcuMTM2LC04LjIxIC0xNy4xMzYsLTIwLjE5IHYgLTMxLjQzIGggLTYuNTIgdiA3Ni4yMiBoIDYuNTIgdiAtMjkuMjMgYyAyLjczNCw1LjM2IDguMzA4LDEwLjUyIDE4LjgyLDEwLjUyIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDc5NCI+PC9wYXRoPjxwYXRoIGQ9Im0gMTAyMi43MywzMTI0LjU0IGMgMCw5LjU2IC02Ljg0LDE5LjI0IC0xOC4xOSwxOS4yNCAtMTAuNTA5LDAgLTE4LjA4MywtNi43MyAtMTkuNDQ2LC0xOS4yNCB6IG0gLTE4LjA5LDI1LjEzIGMgMTUuOTksMCAyNi4wOCwtMTMuNDYgMjUuMjQsLTMxLjEzIGggLTQ0Ljk5NyBjIDAuMjExLC0xMy42NiA4LjgyOCwtMjEuNzUgMjAuMzk3LC0yMS43NSA4LjgzLDAgMTUuMDMsNC41MiAxNy4yNCwxMi4yOSBoIDYuODMgYyAtMi43MywtMTEuNjcgLTEyLjA5LC0xOC4yOSAtMjQuNSwtMTguMjkgLTE2LjYwNCwwIC0yNi42OTQsMTEuODggLTI2LjY5NCwyOS40MyAwLDE4LjMgMTEuMzUyLDI5LjQ1IDI2LjQ4NCwyOS40NSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg3OTYiPjwvcGF0aD48cGF0aCBkPSJtIDI2Ni4wMjcsMjk2OC40NyB2IDc2LjIzIGggNi41MiB2IC03Ni4yMyBoIC02LjUyIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDc5OCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzMwLjI1LDI5OTYuNTQgYyAwLDE2LjE5IC03Ljg4NywyMy40NSAtMTguNzExLDIzLjQ1IC0xMC44MjgsMCAtMTguNjA5LC03LjI2IC0xOC42MDksLTIzLjQ1IDAsLTE2LjE4IDcuNzgxLC0yMy40NCAxOC42MDksLTIzLjQ0IDEwLjgyNCwwIDE4LjcxMSw3LjI2IDE4LjcxMSwyMy40NCB6IG0gNi45MzgsMCBjIDAsLTIwLjYgLTEyLjA5LC0yOS40MyAtMjUuNjQ5LC0yOS40MyAtMTMuNTYyLDAgLTI1LjU0Nyw4LjgzIC0yNS41NDcsMjkuNDMgMCwyMC42MSAxMS45ODUsMjkuNDQgMjUuNTQ3LDI5LjQ0IDEzLjU1OSwwIDI1LjY0OSwtOC44MyAyNS42NDksLTI5LjQ0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDgwMCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzc1Ljk2OSwzMDI1Ljk4IGMgMTMuMzQ3LDAgMTkuMDI3LC03Ljk4IDE5LjAyNywtMjEuODYgdiAtMzUuNjUgaCAtNi41MTkgdiAzMy44NiBjIDAsMTAuNjIgLTIuNzM1LDE3Ljc3IC0xNC4xOTIsMTcuNzcgLTkuNzc3LDAgLTE3LjEzNywtOC4yMSAtMTcuMTM3LC0yMC4xOSB2IC0zMS40NCBoIC02LjUxNSB2IDU2LjU3IGggNi41MTUgdiAtOS41NyBjIDIuNzM1LDUuMzYgOC4zMDUsMTAuNTEgMTguODIxLDEwLjUxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDgwMiI+PC9wYXRoPjxwYXRoIGQ9Im0gNDEzLjM3MSwyOTk3LjcgYyAwLC0xMy45OCA3LjM1OSwtMjIuNSAxNy44NzEsLTIyLjUgOC42MjEsMCAxOC4yOTMsNi44NCAxOC4yOTMsMjIuNSAwLDE1LjU2IC05LjY3MiwyMi40IC0xOC4yOTMsMjIuNCAtMTAuNTEyLDAgLTE3Ljg3MSwtOC41MiAtMTcuODcxLC0yMi40IHogbSAxNi41MDQsLTI4LjI4IGMgLTEyLjkzLDAgLTIzLjU1MSwxMC42MiAtMjMuNTUxLDI4LjI4IDAsMTcuNTYgMTAuNjIxLDI4LjI4IDIzLjU1MSwyOC4yOCA4LjQxLDAgMTUuMjQyLC0zLjg5IDE5LjEzNywtMTAuNzIgdiA5Ljc4IGggNi42MjUgdiAtNTQuNTYgYyAwLC0xNS4xNSAtMTAuNTIsLTIxLjc3IC0yMy45NzcsLTIxLjc3IC0xMS42NjgsMCAtMjAuODEyLDYuNDIgLTIxLjg2MywxNi42MSBoIDYuODMyIGMgMC43MzQsLTYgNS42NzYsLTEwLjk0IDE1LjI0NiwtMTAuOTQgMTAuNjE3LDAgMTcuMTM3LDQuODUgMTcuMTM3LDE1LjM1IHYgMTAuMzEgYyAtMy44OTUsLTYuODQgLTEwLjcyNywtMTAuNjIgLTE5LjEzNywtMTAuNjIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODA0Ij48L3BhdGg+PHBhdGggZD0ibSA1MTMuNjQ4LDMwMDAuODYgYyAwLDkuNTYgLTYuODM1LDE5LjI0IC0xOC4xODcsMTkuMjQgLTEwLjUxMiwwIC0xOC4wODYsLTYuNzMgLTE5LjQ0OSwtMTkuMjQgeiBtIC0xOC4wODUsMjUuMTIgYyAxNS45OCwwIDI2LjA3NCwtMTMuNDUgMjUuMjM0LC0zMS4xMiBoIC00NC45OTYgYyAwLjIxMSwtMTMuNjYgOC44MjgsLTIxLjc2IDIwLjM5OCwtMjEuNzYgOC44MjgsMCAxNS4wMzEsNC41MyAxNy4yMzksMTIuMyBoIDYuODMyIGMgLTIuNzM1LC0xMS42NyAtMTIuMDksLTE4LjI5IC0yNC40OTcsLTE4LjI5IC0xNi42MDksMCAtMjYuNjk5LDExLjg4IC0yNi42OTksMjkuNDMgMCwxOC4zIDExLjM1MiwyOS40NCAyNi40ODksMjkuNDQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODA2Ij48L3BhdGg+PHBhdGggZD0ibSA1NTIuNzMsMzAyMC4zIGMgLTYuMTk5LDAgLTE0LjM5OCwtMi40MSAtMTQuMzk4LC05LjI1IDAsLTUuNTcgNC40MTQsLTguNTEgMTAuNjEzLC05LjY3IGwgNy45OTYsLTEuNDcgYyA5LjI0NywtMS42OCAxOS41NTEsLTQuODMgMTkuNTUxLC0xNS41NiAwLC0xMS4yNSAtMTAuMTk1LC0xNy4yNCAtMjIuNDk2LC0xNy4yNCAtMTEuNjcyLDAgLTIxLjc2Miw1Ljc4IC0yMy40NDksMTguNzEgaCA2LjgzNiBjIDEuMjYyLC04Ljk0IDguNDEsLTEyLjkzIDE3LjEzNywtMTIuOTMgNi44MzUsMCAxNS4zNDcsMi44NCAxNS4zNDcsMTAuNDEgMCw2LjYyIC02LjMwNCw4LjkzIC0xMy45OCwxMC40MSBsIC04LjgyOCwxLjY4IGMgLTguMjA0LDEuNTcgLTE1LjM1Niw2LjMxIC0xNS4zNTYsMTUuMTQgMCw4LjkzIDguOTM4LDE1LjU2IDIxLjY1NiwxNS41NiAxMi4wOTQsMCAyMC40MDMsLTcuNDcgMjEuNzYyLC0xNi41MSBoIC02LjgyOCBjIC0xLjM2Nyw2LjczIC03LjU3LDEwLjcyIC0xNS41NjMsMTAuNzIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODA4Ij48L3BhdGg+PHBhdGggZD0ibSA2MDAuNTU1LDMwMzcuNzYgdiAtMTIuNzIgaCAxMS4xNCB2IC01LjY4IGggLTExLjE0IHYgLTM2LjE3IGMgMCwtNy4zNSAwLjIwNywtOC44MyA3Ljc3NywtOC44MyBoIDMuMzYzIHYgLTUuODkgaCAtNS4zNTkgYyAtMTAuMDk0LDAgLTEyLjQxLDIuMzIgLTEyLjQxLDEzLjQ2IHYgMzcuNDMgaCAtOS4zNTYgdiA1LjY4IGggOS4zNTYgdiAxMi43MiBoIDYuNjI5IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDgxMCI+PC9wYXRoPjxwYXRoIGQ9Im0gNjkwLDMwMDYuODQgYyAtMi4xMDIsOC41MiAtOC44MzIsMTMuMTUgLTE3LjAzMSwxMy4xNSAtOS43NzgsMCAtMTguMzk5LC03Ljc4IC0xOC4zOTksLTIzLjM0IDAsLTE2LjA5IDguNjIxLC0yMy41NSAxOC41MDQsLTIzLjU1IDkuNjcyLDAgMTUuNzcsNi4yIDE3LjM0OCwxMy4yNSBoIDYuOTM3IGMgLTIuMzEyLC0xMS42NyAtMTEuNzc3LC0xOS4yNCAtMjQuMjg1LC0xOS4yNCAtMTYuMDg2LDAgLTI1LjQ0MSwxMS45OCAtMjUuNDQxLDI5LjQzIDAsMTcuNTYgOS40NTcsMjkuNDQgMjUuOTY5LDI5LjQ0IDEyLjgyNCwwIDIxLjU1LC04LjkzIDIzLjIzLC0xOS4xNCBIIDY5MCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4MTIiPjwvcGF0aD48cGF0aCBkPSJtIDczNS4yODksMzAyNS45OCBjIDEzLjM1MiwwIDE5LjAyNywtNy45OCAxOS4wMjcsLTIxLjg2IHYgLTM1LjY1IGggLTYuNTE1IHYgMzMuODYgYyAwLDEwLjYyIC0yLjczNSwxNy43NyAtMTQuMTk2LDE3Ljc3IC05Ljc3NywwIC0xNy4xMzIsLTguMjEgLTE3LjEzMiwtMjAuMTkgdiAtMzEuNDQgaCAtNi41MiB2IDc2LjIzIGggNi41MiB2IC0yOS4yMyBjIDIuNzMsNS4zNiA4LjMwNCwxMC41MSAxOC44MTYsMTAuNTEiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODE0Ij48L3BhdGg+PHBhdGggZD0ibSA4MDYuMjMsMjk5NC4zMyB2IDIuNzQgYyAtMjMuMDE5LC0yLjUyIC0zMi45MDYsLTUuNTcgLTMyLjkwNiwtMTQuNDEgMCwtNS45OCA1LjQ3MywtOS43NyAxMi45MzgsLTkuNzcgMTAuNTExLDAgMTkuOTY4LDUuMzYgMTkuOTY4LDIxLjQ0IHogbSAtMjEuNDQ1LC0yNy4yMiBjIC0xMC41MTIsMCAtMTguNzExLDYuMDkgLTE4LjcxMSwxNS40NiAwLDEyLjgyIDEyLjYxNCwxNy41NSAzOS44NDQsMjAuMjggdiAyIGMgMCwxMi44MiAtNy41NjYsMTUuNjcgLTE1Ljc3LDE1LjY3IC05LjU2NiwwIC0xNS4zNDcsLTUuMzcgLTE1Ljg3NSwtMTIuNzMgaCAtNi44MzUgYyAxLjQ3MiwxMS4xNCAxMC41MTUsMTguNTEgMjMuMTI4LDE4LjUxIDEzLjE0NSwwIDIxLjg3MiwtNS40NyAyMS44NzIsLTIyLjI5IDAsLTcuNzggLTAuMTEsLTEyLjkzIC0wLjExLC0xNy40NSAwLC02LjQyIDAuMzIsLTExLjk5IDAuNjMzLC0xOC4wOSBoIC02LjYyMSBsIC0wLjMxNyw4LjYzIGMgLTMuNjc5LC02IC0xMC43MjIsLTkuOTkgLTIxLjIzOCwtOS45OSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4MTYiPjwvcGF0aD48cGF0aCBkPSJtIDgzNC43MDMsMjk2OC40NyBoIC02LjUxOSB2IDU2LjU3IGggNi41MTkgeiBtIDAsNjUuODIgaCAtNi41MTkgdiAxMC40MSBoIDYuNTE5IHYgLTEwLjQxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDgxOCI+PC9wYXRoPjxwYXRoIGQ9Im0gODc3LjkwNiwzMDI1Ljk4IGMgMTMuMzUyLDAgMTkuMDI4LC03Ljk4IDE5LjAyOCwtMjEuODYgdiAtMzUuNjUgaCAtNi41MTYgdiAzMy44NiBjIDAsMTAuNjIgLTIuNzM0LDE3Ljc3IC0xNC4xOTUsMTcuNzcgLTkuNzc4LDAgLTE3LjEzMywtOC4yMSAtMTcuMTMzLC0yMC4xOSB2IC0zMS40NCBoIC02LjUyIHYgNTYuNTcgaCA2LjUyIHYgLTkuNTcgYyAyLjczNCw1LjM2IDguMzA1LDEwLjUxIDE4LjgxNiwxMC41MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4MjAiPjwvcGF0aD48cGF0aCBkPSJtIDk3My4wMiwzMDI1LjA0IDE0LjUwNywtNDYuMzcgMTIuMDk0LDQ2LjM3IGggNy4yNDkgbCAtMTYuNDAxLC01Ni41NyBoIC02LjA5NCBsIC0xNC44MjQsNDcuNTIgLTE0LjQwMywtNDcuNTIgaCAtNS45OTIgbCAtMTYuNDAyLDU2LjU3IGggNy4yNTQgbCAxMi41MTIsLTQ2LjI2IDEzLjk4LDQ2LjI2IGggNi41MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4MjIiPjwvcGF0aD48cGF0aCBkPSJtIDEwNDIuNjksMzAyNS45OCBjIDEzLjM1LDAgMTkuMDMsLTcuOTggMTkuMDMsLTIxLjg2IHYgLTM1LjY1IGggLTYuNTIgdiAzMy44NiBjIDAsMTAuNjIgLTIuNzMsMTcuNzcgLTE0LjE5LDE3Ljc3IC05Ljc4LDAgLTE3LjE0LC04LjIxIC0xNy4xNCwtMjAuMTkgdiAtMzEuNDQgaCAtNi41MiB2IDc2LjIzIGggNi41MiB2IC0yOS4yMyBjIDIuNzQsNS4zNiA4LjMxLDEwLjUxIDE4LjgyLDEwLjUxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDgyNCI+PC9wYXRoPjxwYXRoIGQ9Im0gMTA4NC40MSwyOTY4LjQ3IGggLTYuNTIgdiA1Ni41NyBoIDYuNTIgeiBtIDAsNjUuODIgaCAtNi41MiB2IDEwLjQxIGggNi41MiB2IC0xMC40MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4MjYiPjwvcGF0aD48cGF0aCBkPSJtIDExNDAuMjMsMzAwNi44NCBjIC0yLjExLDguNTIgLTguODQsMTMuMTUgLTE3LjA0LDEzLjE1IC05Ljc4LDAgLTE4LjM5LC03Ljc4IC0xOC4zOSwtMjMuMzQgMCwtMTYuMDkgOC42MSwtMjMuNTUgMTguNSwtMjMuNTUgOS42NywwIDE1Ljc3LDYuMiAxNy4zNSwxMy4yNSBoIDYuOTMgYyAtMi4zMSwtMTEuNjcgLTExLjc3LC0xOS4yNCAtMjQuMjgsLTE5LjI0IC0xNi4wOSwwIC0yNS40NCwxMS45OCAtMjUuNDQsMjkuNDMgMCwxNy41NiA5LjQ2LDI5LjQ0IDI1Ljk2LDI5LjQ0IDEyLjgzLDAgMjEuNTYsLTguOTMgMjMuMjQsLTE5LjE0IGggLTYuODMiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODI4Ij48L3BhdGg+PHBhdGggZD0ibSAxMTg1LjUxLDMwMjUuOTggYyAxMy4zNSwwIDE5LjAzLC03Ljk4IDE5LjAzLC0yMS44NiB2IC0zNS42NSBoIC02LjUyIHYgMzMuODYgYyAwLDEwLjYyIC0yLjczLDE3Ljc3IC0xNC4xOSwxNy43NyAtOS43OCwwIC0xNy4xMywtOC4yMSAtMTcuMTMsLTIwLjE5IHYgLTMxLjQ0IGggLTYuNTIgdiA3Ni4yMyBoIDYuNTIgdiAtMjkuMjMgYyAyLjczLDUuMzYgOC4zLDEwLjUxIDE4LjgxLDEwLjUxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDgzMCI+PC9wYXRoPjxwYXRoIGQ9Im0gMTI3My4wNiwzMDI1Ljk4IGMgMTMuMzUsMCAxOS4wMywtNy45OCAxOS4wMywtMjEuODYgdiAtMzUuNjUgaCAtNi41MiB2IDMzLjg2IGMgMCwxMC42MiAtMi43NCwxNy43NyAtMTQuMiwxNy43NyAtOS43NywwIC0xNy4xMywtOC4yMSAtMTcuMTMsLTIwLjE5IHYgLTMxLjQ0IGggLTYuNTIgdiA3Ni4yMyBoIDYuNTIgdiAtMjkuMjMgYyAyLjczLDUuMzYgOC4zMSwxMC41MSAxOC44MiwxMC41MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4MzIiPjwvcGF0aD48cGF0aCBkPSJtIDEzNDQsMjk5NC4zMyB2IDIuNzQgYyAtMjMuMDIsLTIuNTIgLTMyLjkxLC01LjU3IC0zMi45MSwtMTQuNDEgMCwtNS45OCA1LjQ3LC05Ljc3IDEyLjk0LC05Ljc3IDEwLjUxLDAgMTkuOTcsNS4zNiAxOS45NywyMS40NCB6IG0gLTIxLjQ1LC0yNy4yMiBjIC0xMC41MSwwIC0xOC43MSw2LjA5IC0xOC43MSwxNS40NiAwLDEyLjgyIDEyLjYyLDE3LjU1IDM5Ljg1LDIwLjI4IHYgMiBjIDAsMTIuODIgLTcuNTcsMTUuNjcgLTE1Ljc3LDE1LjY3IC05LjU3LDAgLTE1LjM1LC01LjM3IC0xNS44OCwtMTIuNzMgaCAtNi44MyBjIDEuNDcsMTEuMTQgMTAuNTEsMTguNTEgMjMuMTMsMTguNTEgMTMuMTQsMCAyMS44NywtNS40NyAyMS44NywtMjIuMjkgMCwtNy43OCAtMC4xMSwtMTIuOTMgLTAuMTEsLTE3LjQ1IDAsLTYuNDIgMC4zMiwtMTEuOTkgMC42MywtMTguMDkgaCAtNi42MiBsIC0wLjMyLDguNjMgYyAtMy42OCwtNiAtMTAuNzIsLTkuOTkgLTIxLjI0LC05Ljk5IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDgzNCI+PC9wYXRoPjxwYXRoIGQ9Im0gMTM4NC4yNCwzMDIwLjMgYyAtNi4yLDAgLTE0LjQsLTIuNDEgLTE0LjQsLTkuMjUgMCwtNS41NyA0LjQyLC04LjUxIDEwLjYyLC05LjY3IGwgNy45OSwtMS40NyBjIDkuMjUsLTEuNjggMTkuNTUsLTQuODMgMTkuNTUsLTE1LjU2IDAsLTExLjI1IC0xMC4xOSwtMTcuMjQgLTIyLjQ5LC0xNy4yNCAtMTEuNjcsMCAtMjEuNzYsNS43OCAtMjMuNDUsMTguNzEgaCA2Ljg0IGMgMS4yNiwtOC45NCA4LjQxLC0xMi45MyAxNy4xMywtMTIuOTMgNi44NCwwIDE1LjM1LDIuODQgMTUuMzUsMTAuNDEgMCw2LjYyIC02LjMxLDguOTMgLTEzLjk4LDEwLjQxIGwgLTguODMsMS42OCBjIC04LjIsMS41NyAtMTUuMzUsNi4zMSAtMTUuMzUsMTUuMTQgMCw4LjkzIDguOTMsMTUuNTYgMjEuNjUsMTUuNTYgMTIuMSwwIDIwLjQsLTcuNDcgMjEuNzcsLTE2LjUxIGggLTYuODMgYyAtMS4zNyw2LjczIC03LjU3LDEwLjcyIC0xNS41NywxMC43MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4MzYiPjwvcGF0aD48cGF0aCBkPSJtIDI3NS4yODEsMjkxNC4wNyB2IC0xMi43MiBoIDExLjE0MSB2IC01LjY4IGggLTExLjE0MSB2IC0zNi4xNyBjIDAsLTcuMzUgMC4yMDcsLTguODMgNy43NzgsLTguODMgaCAzLjM2MyB2IC01Ljg5IGggLTUuMzU5IGMgLTEwLjA5NCwwIC0xMi40MTEsMi4zMiAtMTIuNDExLDEzLjQ2IHYgMzcuNDMgaCAtOS4zNTUgdiA1LjY4IGggOS4zNTUgdiAxMi43MiBoIDYuNjI5IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDgzOCI+PC9wYXRoPjxwYXRoIGQ9Im0gMzI1LjA5OCwyOTAyLjI5IGMgMTMuMzUxLDAgMTkuMDMxLC03Ljk5IDE5LjAzMSwtMjEuODYgdiAtMzUuNjUgaCAtNi41MiB2IDMzLjg2IGMgMCwxMC42MiAtMi43MzQsMTcuNzYgLTE0LjE5NSwxNy43NiAtOS43NzMsMCAtMTcuMTMzLC04LjIgLTE3LjEzMywtMjAuMTggdiAtMzEuNDQgaCAtNi41MTkgViAyOTIxIGggNi41MTkgdiAtMjkuMjIgYyAyLjczNSw1LjM2IDguMzA1LDEwLjUxIDE4LjgxNywxMC41MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4NDAiPjwvcGF0aD48cGF0aCBkPSJtIDQwMC40NjEsMjg3Ny4xNyBjIDAsOS41NiAtNi44MzYsMTkuMjMgLTE4LjE4OCwxOS4yMyAtMTAuNTE1LDAgLTE4LjA4MiwtNi43MiAtMTkuNDQ5LC0xOS4yMyB6IG0gLTE4LjA4NiwyNS4xMiBjIDE1Ljk4LDAgMjYuMDc0LC0xMy40NSAyNS4yMzQsLTMxLjEyIGggLTQ0Ljk5NiBjIDAuMjExLC0xMy42NiA4LjgyOCwtMjEuNzYgMjAuMzk1LC0yMS43NiA4LjgyOCwwIDE1LjAzNSw0LjUyIDE3LjI0MiwxMi4zIGggNi44MzIgYyAtMi43MzQsLTExLjY3IC0xMi4wOSwtMTguMjkgLTI0LjQ5NiwtMTguMjkgLTE2LjYwOSwwIC0yNi42OTksMTEuODggLTI2LjY5OSwyOS40MyAwLDE4LjMgMTEuMzUxLDI5LjQ0IDI2LjQ4OCwyOS40NCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4NDIiPjwvcGF0aD48cGF0aCBkPSJtIDQ2Ni4zNDQsMjg5Ni42MSBjIC02LjE5OSwwIC0xNC4zOTksLTIuNDEgLTE0LjM5OSwtOS4yNSAwLC01LjU3IDQuNDE0LC04LjUxIDEwLjYxNCwtOS42NyBsIDcuOTk2LC0xLjQ3IGMgOS4yNDYsLTEuNjggMTkuNTUsLTQuODQgMTkuNTUsLTE1LjU2IDAsLTExLjI1IC0xMC4xOTUsLTE3LjI0IC0yMi40OTYsLTE3LjI0IC0xMS42NzEsMCAtMjEuNzYxLDUuNzggLTIzLjQ0OSwxOC43MSBoIDYuODM2IGMgMS4yNjIsLTguOTQgOC40MSwtMTIuOTMgMTcuMTM3LC0xMi45MyA2LjgzNiwwIDE1LjM1MSwyLjg0IDE1LjM1MSwxMC40MSAwLDYuNjIgLTYuMzA4LDguOTMgLTEzLjk4OCwxMC40MSBsIC04LjgyNCwxLjY4IGMgLTguMjAzLDEuNTcgLTE1LjM1Miw2LjMxIC0xNS4zNTIsMTUuMTMgMCw4Ljk0IDguOTM0LDE1LjU3IDIxLjY1MywxNS41NyAxMi4wOTcsMCAyMC40MDIsLTcuNDcgMjEuNzY1LC0xNi41MSBoIC02LjgzMiBjIC0xLjM2Nyw2LjczIC03LjU3LDEwLjcyIC0xNS41NjIsMTAuNzIiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODQ0Ij48L3BhdGg+PHBhdGggZD0iTSA1MDQuOTEsMjg0NC43OCBWIDI5MjEgaCA2LjUxNiB2IC03Ni4yMiBoIC02LjUxNiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4NDYiPjwvcGF0aD48cGF0aCBkPSJtIDU2OS4xMzcsMjg3Mi44NSBjIDAsMTYuMTkgLTcuODg3LDIzLjQ1IC0xOC43MTEsMjMuNDUgLTEwLjgyOCwwIC0xOC42MSwtNy4yNiAtMTguNjEsLTIzLjQ1IDAsLTE2LjE4IDcuNzgyLC0yMy40NCAxOC42MSwtMjMuNDQgMTAuODI0LDAgMTguNzExLDcuMjYgMTguNzExLDIzLjQ0IHogbSA2LjkzNywwIGMgMCwtMjAuNjEgLTEyLjA5LC0yOS40MyAtMjUuNjQ4LC0yOS40MyAtMTMuNTYzLDAgLTI1LjU0Nyw4LjgyIC0yNS41NDcsMjkuNDMgMCwyMC42MSAxMS45ODQsMjkuNDQgMjUuNTQ3LDI5LjQ0IDEzLjU1OCwwIDI1LjY0OCwtOC44MyAyNS42NDgsLTI5LjQ0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDg0OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNTk4Ljc2NiwyOTE0LjA3IHYgLTEyLjcyIGggMTEuMTQ0IHYgLTUuNjggaCAtMTEuMTQ0IHYgLTM2LjE3IGMgMCwtNy4zNSAwLjIxMSwtOC44MyA3Ljc3NywtOC44MyBoIDMuMzY3IHYgLTUuODkgaCAtNS4zNjMgYyAtMTAuMDk0LDAgLTEyLjQwNiwyLjMyIC0xMi40MDYsMTMuNDYgdiAzNy40MyBoIC05LjM1NiB2IDUuNjggaCA5LjM1NiB2IDEyLjcyIGggNi42MjUiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODUwIj48L3BhdGg+PHBhdGggZD0ibSA2NzUuNTk4LDI5MDIuMjkgYyAxMy4zNDcsMCAxOS4wMjcsLTcuOTkgMTkuMDI3LC0yMS44NiB2IC0zNS42NSBoIC02LjUyIHYgMzMuODYgYyAwLDEwLjYyIC0yLjczNCwxNy43NiAtMTQuMTk1LDE3Ljc2IC05Ljc3MywwIC0xNy4xMzMsLTguMiAtMTcuMTMzLC0yMC4xOCB2IC0zMS40NCBoIC02LjUxNSB2IDU2LjU3IGggNi41MTUgdiAtOS41NyBjIDIuNzM1LDUuMzYgOC4zMDksMTAuNTEgMTguODIxLDEwLjUxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDg1MiI+PC9wYXRoPjxwYXRoIGQ9Im0gNzI3LjUxMiwyODQzLjQyIGMgLTEyLjkzLDAgLTE4LjM5OSw3Ljk4IC0xOC4zOTksMjEuODYgdiAzNi4wNyBoIDYuNTIgdiAtMzQuMjggYyAwLC0xMC42MiAyLjUyMywtMTcuNzcgMTMuNTYyLC0xNy43NyA5LjAzOSwwIDE2LjUwNCw4LjIxIDE2LjUwNCwyMC4xOSB2IDMxLjg2IGggNi41MiB2IC01Ni41NyBoIC02LjUyIHYgOS4xNSBjIC0yLjczNCwtNS4zNiAtOC40MDYsLTEwLjUxIC0xOC4xODcsLTEwLjUxIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDg1NCI+PC9wYXRoPjxwYXRoIGQ9Im0gNzcwLjA3LDI4NDQuNzggdiA1Ni41NyBoIDYuNTIgdiAtOS41NyBjIDIuNzM0LDUuMzYgNy43NzcsMTAuNTEgMTcuNzY1LDEwLjUxIDkuMDQsMCAxNC4yOTcsLTMuOTkgMTYuNjE0LC0xMS4yNSA0LjMwNCw3LjE1IDkuOTg0LDExLjI1IDE5LjEyOSwxMS4yNSAxMi44MjgsMCAxNy45OCwtNy45OSAxNy45OCwtMjEuODYgdiAtMzUuNjUgaCAtNi41MTkgdiAzMy44NiBjIDAsMTAuNjIgLTIuMjA3LDE3Ljc2IC0xMy4xNDEsMTcuNzYgLTkuMjUsMCAtMTYuMDksLTguMiAtMTYuMDksLTIwLjE4IHYgLTMxLjQ0IGggLTYuNTE1IHYgMzMuODYgYyAwLDEwLjYyIC0yLjIwOCwxNy43NiAtMTMuMTQxLDE3Ljc2IC05LjI1NCwwIC0xNi4wODIsLTguMiAtMTYuMDgyLC0yMC4xOCB2IC0zMS40NCBoIC02LjUyIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDg1NiI+PC9wYXRoPjxwYXRoIGQ9Im0gOTA2LjUsMjg3Mi44NSBjIDAsMTUuMDQgLTcuNDYxLDIzLjU1IC0xNy45NzMsMjMuNTUgLTguNTE1LDAgLTE4LjE4NywtNi44MyAtMTguMTg3LC0yMy41NSAwLC0xNi43MSA5LjY3MiwtMjMuNTUgMTguMTg3LC0yMy41NSAxMC41MTIsMCAxNy45NzMsOC41MiAxNy45NzMsMjMuNTUgeiBtIC0zNS43NDIsLTE4LjgyIHYgLTkuMjUgaCAtNi41MiBWIDI5MjEgaCA2LjUyIHYgLTI5LjQzIGMgMy45OTYsNi44MyAxMC44MjQsMTAuNzIgMTkuMTMzLDEwLjcyIDEzLjAzNSwwIDIzLjY1NiwtMTAuNzIgMjMuNjU2LC0yOS40NCAwLC0xOC44MiAtMTAuNjIxLC0yOS40MyAtMjMuNjU2LC0yOS40MyAtOC4zMDksMCAtMTUuMTM3LDMuODggLTE5LjEzMywxMC42MSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4NTgiPjwvcGF0aD48cGF0aCBkPSJtIDk2Ny44NzEsMjg3Ny4xNyBjIDAsOS41NiAtNi44MzYsMTkuMjMgLTE4LjE4NywxOS4yMyAtMTAuNTEyLDAgLTE4LjA4MiwtNi43MiAtMTkuNDUsLTE5LjIzIHogbSAtMTguMDg2LDI1LjEyIGMgMTUuOTg1LDAgMjYuMDc0LC0xMy40NSAyNS4yMzUsLTMxLjEyIGggLTQ0Ljk5MyBjIDAuMjA3LC0xMy42NiA4LjgyOCwtMjEuNzYgMjAuMzk1LC0yMS43NiA4LjgyOCwwIDE1LjAzMSw0LjUyIDE3LjIzOCwxMi4zIGggNi44MzIgYyAtMi43MzQsLTExLjY3IC0xMi4wOSwtMTguMjkgLTI0LjQ5NiwtMTguMjkgLTE2LjYwNSwwIC0yNi42OTksMTEuODggLTI2LjY5OSwyOS40MyAwLDE4LjMgMTEuMzUxLDI5LjQ0IDI2LjQ4OCwyOS40NCIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4NjAiPjwvcGF0aD48cGF0aCBkPSJtIDEwMTAuMzIsMjg5NC44MiBjIC0xMS42NjgsMCAtMTUuNDUzLC04LjQxIC0xNS40NTMsLTIwLjM5IHYgLTI5LjY1IGggLTYuNDEgdiA1Ni41NyBoIDYuMjAzIHYgLTEwLjMxIGMgMi41MjQsNi42MiA5Ljg4LDEwLjczIDE2LjcyLDEwLjczIDAuNTIsMCAxLjI2LDAgMS44OSwtMC4xMSB2IC02Ljk0IGMgLTEuMDUsMC4xIC0yLDAuMSAtMi45NSwwLjEiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODYyIj48L3BhdGg+PHBhdGggZD0ibSAxMDUyLjU2LDI4NzQuMDEgYyAwLC0xMy45OCA3LjM2LC0yMi41IDE3Ljg4LC0yMi41IDguNjIsMCAxOC4yOSw2Ljg0IDE4LjI5LDIyLjUgMCwxNS41NiAtOS42NywyMi4zOSAtMTguMjksMjIuMzkgLTEwLjUyLDAgLTE3Ljg4LC04LjUxIC0xNy44OCwtMjIuMzkgeiBtIDE2LjUxLC0yOC4yOCBjIC0xMi45MywwIC0yMy41NSwxMC42MiAtMjMuNTUsMjguMjggMCwxNy41NiAxMC42MiwyOC4yOCAyMy41NSwyOC4yOCA4LjQxLDAgMTUuMjQsLTMuODkgMTkuMTMsLTEwLjcyIHYgOS43OCBoIDYuNjMgdiAtNTQuNTYgYyAwLC0xNS4xNSAtMTAuNTIsLTIxLjc3IC0yMy45NywtMjEuNzcgLTExLjY3LDAgLTIwLjgyLDYuNDEgLTIxLjg3LDE2LjYxIGggNi44MyBjIDAuNzQsLTYgNS42OCwtMTAuOTQgMTUuMjUsLTEwLjk0IDEwLjYyLDAgMTcuMTMsNC44NSAxNy4xMywxNS4zNSB2IDEwLjMxIGMgLTMuODksLTYuODQgLTEwLjcyLC0xMC42MiAtMTkuMTMsLTEwLjYyIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDg2NCI+PC9wYXRoPjxwYXRoIGQ9Im0gMTEzNC41NCwyODk0LjgyIGMgLTExLjY3LDAgLTE1LjQ1LC04LjQxIC0xNS40NSwtMjAuMzkgdiAtMjkuNjUgaCAtNi40MSB2IDU2LjU3IGggNi4yIHYgLTEwLjMxIGMgMi41Miw2LjYyIDkuODgsMTAuNzMgMTYuNzIsMTAuNzMgMC41MiwwIDEuMjYsMCAxLjg5LC0wLjExIHYgLTYuOTQgYyAtMS4wNSwwLjEgLTIsMC4xIC0yLjk1LDAuMSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4NjYiPjwvcGF0aD48cGF0aCBkPSJtIDExODcuNzMsMjg3Ny4xNyBjIDAsOS41NiAtNi44NCwxOS4yMyAtMTguMTksMTkuMjMgLTEwLjUyLDAgLTE4LjA4LC02LjcyIC0xOS40NSwtMTkuMjMgeiBtIC0xOC4wOSwyNS4xMiBjIDE1Ljk4LDAgMjYuMDcsLTEzLjQ1IDI1LjIzLC0zMS4xMiBoIC00NC45OSBjIDAuMjEsLTEzLjY2IDguODMsLTIxLjc2IDIwLjM5LC0yMS43NiA4LjgzLDAgMTUuMDQsNC41MiAxNy4yNSwxMi4zIGggNi44MyBjIC0yLjc0LC0xMS42NyAtMTIuMDksLTE4LjI5IC0yNC41LC0xOC4yOSAtMTYuNjEsMCAtMjYuNywxMS44OCAtMjYuNywyOS40MyAwLDE4LjMgMTEuMzUsMjkuNDQgMjYuNDksMjkuNDQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODY4Ij48L3BhdGg+PHBhdGggZD0ibSAxMjQ0LjA1LDI4NzAuNjQgdiAyLjc0IGMgLTIzLjAyLC0yLjUyIC0zMi45LC01LjU3IC0zMi45LC0xNC40MSAwLC01Ljk4IDUuNDcsLTkuNzcgMTIuOTMsLTkuNzcgMTAuNTIsMCAxOS45Nyw1LjM2IDE5Ljk3LDIxLjQ0IHogbSAtMjEuNDQsLTI3LjIyIGMgLTEwLjUxLDAgLTE4LjcxLDYuMDkgLTE4LjcxLDE1LjQ2IDAsMTIuODIgMTIuNjEsMTcuNTQgMzkuODQsMjAuMjggdiAyIGMgMCwxMi44MiAtNy41NywxNS42NiAtMTUuNzcsMTUuNjYgLTkuNTcsMCAtMTUuMzUsLTUuMzYgLTE1Ljg3LC0xMi43MiBoIC02Ljg0IGMgMS40NywxMS4xNCAxMC41MiwxOC41MSAyMy4xMywxOC41MSAxMy4xNCwwIDIxLjg3LC01LjQ3IDIxLjg3LC0yMi4yOSAwLC03Ljc4IC0wLjExLC0xMi45MyAtMC4xMSwtMTcuNDUgMCwtNi40MiAwLjMyLC0xMS45OSAwLjYzLC0xOC4wOSBoIC02LjYyIGwgLTAuMzIsOC42MyBjIC0zLjY3LC02IC0xMC43MiwtOS45OSAtMjEuMjMsLTkuOTkiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODcwIj48L3BhdGg+PHBhdGggZD0ibSAxMjc1LjI2LDI5MTQuMDcgdiAtMTIuNzIgaCAxMS4xNCB2IC01LjY4IGggLTExLjE0IHYgLTM2LjE3IGMgMCwtNy4zNSAwLjIxLC04LjgzIDcuNzgsLTguODMgaCAzLjM2IHYgLTUuODkgaCAtNS4zNiBjIC0xMC4wOSwwIC0xMi40MSwyLjMyIC0xMi40MSwxMy40NiB2IDM3LjQzIGggLTkuMzUgdiA1LjY4IGggOS4zNSB2IDEyLjcyIGggNi42MyIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4NzIiPjwvcGF0aD48cGF0aCBkPSJtIDEzMzkuOTEsMjg3Ny4xNyBjIDAsOS41NiAtNi44NCwxOS4yMyAtMTguMTksMTkuMjMgLTEwLjUxLDAgLTE4LjA5LC02LjcyIC0xOS40NSwtMTkuMjMgeiBtIC0xOC4wOSwyNS4xMiBjIDE1Ljk4LDAgMjYuMDgsLTEzLjQ1IDI1LjI0LC0zMS4xMiBoIC00NSBjIDAuMjEsLTEzLjY2IDguODMsLTIxLjc2IDIwLjQsLTIxLjc2IDguODMsMCAxNS4wMyw0LjUyIDE3LjI0LDEyLjMgaCA2LjgzIGMgLTIuNzMsLTExLjY3IC0xMi4wOSwtMTguMjkgLTI0LjUsLTE4LjI5IC0xNi42LDAgLTI2LjcsMTEuODggLTI2LjcsMjkuNDMgMCwxOC4zIDExLjM2LDI5LjQ0IDI2LjQ5LDI5LjQ0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDg3NCI+PC9wYXRoPjxwYXRoIGQ9Im0gMTM4Mi4zNSwyODk0LjgyIGMgLTExLjY3LDAgLTE1LjQ1LC04LjQxIC0xNS40NSwtMjAuMzkgdiAtMjkuNjUgaCAtNi40MSB2IDU2LjU3IGggNi4yIHYgLTEwLjMxIGMgMi41Myw2LjYyIDkuODgsMTAuNzMgMTYuNzIsMTAuNzMgMC41MiwwIDEuMjYsMCAxLjg5LC0wLjExIHYgLTYuOTQgYyAtMS4wNSwwLjEgLTIsMC4xIC0yLjk1LDAuMSIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4NzYiPjwvcGF0aD48cGF0aCBkPSJtIDMwNS44NzEsMjc0OS4xNiBjIDAsMTYuMTkgLTcuODg3LDIzLjQ1IC0xOC43MTEsMjMuNDUgLTEwLjgzMiwwIC0xOC42MDksLTcuMjYgLTE4LjYwOSwtMjMuNDUgMCwtMTYuMTggNy43NzcsLTIzLjQ0IDE4LjYwOSwtMjMuNDQgMTAuODI0LDAgMTguNzExLDcuMjYgMTguNzExLDIzLjQ0IHogbSA2LjkzOCwwIGMgMCwtMjAuNjEgLTEyLjA5LC0yOS40NCAtMjUuNjQ5LC0yOS40NCAtMTMuNTY2LDAgLTI1LjU0Nyw4LjgzIC0yNS41NDcsMjkuNDQgMCwyMC42IDExLjk4MSwyOS40NCAyNS41NDcsMjkuNDQgMTMuNTU5LDAgMjUuNjQ5LC04Ljg0IDI1LjY0OSwtMjkuNDQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODc4Ij48L3BhdGg+PHBhdGggZD0ibSAzNDguMTEzLDI3NzEuMTMgYyAtMTEuNjcyLDAgLTE1LjQ1NywtOC40MSAtMTUuNDU3LC0yMC4zOSB2IC0yOS42NSBoIC02LjQxIHYgNTYuNTYgaCA2LjIwMyB2IC0xMC4zIGMgMi41MjQsNi42MiA5Ljg3OSwxMC43MiAxNi43MTUsMTAuNzIgMC41MjQsMCAxLjI2MiwwIDEuODkxLC0wLjEgdiAtNi45NCBjIC0xLjA0NywwLjEgLTEuOTk2LDAuMSAtMi45NDIsMC4xIiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDg4MCI+PC9wYXRoPjxwYXRoIGQ9Im0gNDI4LjMwOSwyNzUzLjQ3IGMgMCw5LjU3IC02LjgzNiwxOS4yNCAtMTguMTkyLDE5LjI0IC0xMC41MTIsMCAtMTguMDg2LC02LjczIC0xOS40NDUsLTE5LjI0IHogbSAtMTguMDg2LDI1LjEzIGMgMTUuOTgsMCAyNi4wNzQsLTEzLjQ2IDI1LjIzLC0zMS4xMiBoIC00NC45OTIgYyAwLjIxMSwtMTMuNjYgOC44MjgsLTIxLjc2IDIwLjM5NCwtMjEuNzYgOC44MjksMCAxNS4wMzYsNC41MiAxNy4yNDMsMTIuMyBoIDYuODMyIGMgLTIuNzM1LC0xMS42NyAtMTIuMDksLTE4LjMgLTI0LjUsLTE4LjMgLTE2LjYwNiwwIC0yNi43LDExLjg5IC0yNi43LDI5LjQ0IDAsMTguMyAxMS4zNTYsMjkuNDQgMjYuNDkzLDI5LjQ0IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDg4MiI+PC9wYXRoPjxwYXRoIGQ9Im0gNDUxLjk0MSwyNzQ5LjE2IGMgMCwtMTUuMDMgNy40NjEsLTIzLjU1IDE3Ljk3MywtMjMuNTUgOC41MTYsMCAxOC4xODgsNi44NCAxOC4xODgsMjMuNTUgMCwxNi43MiAtOS42NzIsMjMuNTUgLTE4LjE4OCwyMy41NSAtMTAuNTEyLDAgLTE3Ljk3MywtOC41MSAtMTcuOTczLC0yMy41NSB6IG0gMzUuNzQzLDE4LjgyIHYgOS42NyBoIDYuNTE1IHYgLTc0Ljk2IGggLTYuNTE1IHYgMjcuNzYgYyAtMy45OTYsLTYuODQgLTEwLjgyOSwtMTAuNzMgLTE5LjEzMywtMTAuNzMgLTEzLjAzNSwwIC0yMy42NTYsMTAuNzMgLTIzLjY1NiwyOS40NCAwLDE4LjgyIDEwLjYyMSwyOS40NCAyMy42NTYsMjkuNDQgOC4zMDQsMCAxNS4xMzcsLTMuODkgMTkuMTMzLC0xMC42MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4ODQiPjwvcGF0aD48cGF0aCBkPSJtIDUyOC43NjYsMjcxOS43MiBjIC0xMi45MywwIC0xOC4zOTksNy45OSAtMTguMzk5LDIxLjg3IHYgMzYuMDYgaCA2LjUyIHYgLTM0LjI3IGMgMCwtMTAuNjIgMi41MjMsLTE3Ljc3IDEzLjU2MiwtMTcuNzcgOS4wNDMsMCAxNi41MDQsOC4yMSAxNi41MDQsMjAuMTkgdiAzMS44NSBoIDYuNTIgdiAtNTYuNTYgaCAtNi41MiB2IDkuMTUgYyAtMi43MzQsLTUuMzYgLTguNDA2LC0xMC41MiAtMTguMTg3LC0xMC41MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4ODYiPjwvcGF0aD48cGF0aCBkPSJtIDYwNy4wNywyNzQ2Ljk1IHYgMi43NCBjIC0yMy4wMTksLTIuNTIgLTMyLjkwMiwtNS41NyAtMzIuOTAyLC0xNC40MSAwLC01Ljk4IDUuNDY5LC05Ljc3IDEyLjkzNCwtOS43NyAxMC41MTEsMCAxOS45NjgsNS4zNiAxOS45NjgsMjEuNDQgeiBtIC0yMS40NDUsLTI3LjIzIGMgLTEwLjUxMiwwIC0xOC43MTEsNi4xIC0xOC43MTEsMTUuNDYgMCwxMi44MyAxMi42MTMsMTcuNTUgMzkuODQ0LDIwLjI5IHYgMiBjIDAsMTIuODIgLTcuNTY3LDE1LjY2IC0xNS43NywxNS42NiAtOS41NjYsMCAtMTUuMzQ3LC01LjM2IC0xNS44NzUsLTEyLjcyIGggLTYuODM2IGMgMS40NzcsMTEuMTQgMTAuNTIsMTguNSAyMy4xMjksMTguNSAxMy4xNDUsMCAyMS44NzEsLTUuNDYgMjEuODcxLC0yMi4yOCAwLC03Ljc4IC0wLjEwNSwtMTIuOTMgLTAuMTA1LC0xNy40NSAwLC02LjQyIDAuMzE2LC0xMS45OSAwLjYyOSwtMTguMDkgaCAtNi42MjEgbCAtMC4zMTcsOC42MiBjIC0zLjY3OSwtNS45OSAtMTAuNzIyLC05Ljk5IC0yMS4yMzgsLTkuOTkiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODg4Ij48L3BhdGg+PHBhdGggZD0ibSA2MjkuMDIzLDI3MjEuMDkgdiA3Ni4yMiBoIDYuNTIgdiAtNzYuMjIgaCAtNi41MiIgc3R5bGU9ImZpbGw6IzEwMGYwZDtmaWxsLW9wYWNpdHk6MTtmaWxsLXJ1bGU6bm9uemVybztzdHJva2U6bm9uZSIgaWQ9InBhdGg4OTAiPjwvcGF0aD48cGF0aCBkPSJtIDY4OS42NjgsMjc5MC4zOCB2IC0xMi43MyBoIDExLjE0NSB2IC01LjY3IGggLTExLjE0NSB2IC0zNi4xNyBjIDAsLTcuMzUgMC4yMTEsLTguODMgNy43ODEsLTguODMgaCAzLjM2NCB2IC01Ljg5IGggLTUuMzY0IGMgLTEwLjA5LDAgLTEyLjQwNiwyLjMyIC0xMi40MDYsMTMuNDYgdiAzNy40MyBoIC05LjM1NSB2IDUuNjcgaCA5LjM1NSB2IDEyLjczIGggNi42MjUiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODkyIj48L3BhdGg+PHBhdGggZD0ibSA3NTQsMjc0OS4xNiBjIDAsMTYuMTkgLTcuODg3LDIzLjQ1IC0xOC43MTEsMjMuNDUgLTEwLjgyOCwwIC0xOC42MDksLTcuMjYgLTE4LjYwOSwtMjMuNDUgMCwtMTYuMTggNy43ODEsLTIzLjQ0IDE4LjYwOSwtMjMuNDQgMTAuODI0LDAgMTguNzExLDcuMjYgMTguNzExLDIzLjQ0IHogbSA2LjkzOCwwIGMgMCwtMjAuNjEgLTEyLjA5LC0yOS40NCAtMjUuNjQ5LC0yOS40NCAtMTMuNTYyLDAgLTI1LjU0Nyw4LjgzIC0yNS41NDcsMjkuNDQgMCwyMC42IDExLjk4NSwyOS40NCAyNS41NDcsMjkuNDQgMTMuNTU5LDAgMjUuNjQ5LC04Ljg0IDI1LjY0OSwtMjkuNDQiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoODk0Ij48L3BhdGg+PHBhdGggZD0ibSA4MDMuNTk0LDI3NzMuMTMgYyAwLC0xMi40IDcuNjc2LC0yMC42IDE5LjQ0OSwtMjAuNiAxMS43NzcsMCAxOS40NTMsOC4yIDE5LjQ1MywyMC42IDAsMTEuNjcgLTguMDk0LDE5Ljc3IC0xOS40NTMsMTkuNzcgLTExLjQ2MSwwIC0xOS40NDksLTguMSAtMTkuNDQ5LC0xOS43NyB6IG0gMTguNzE5LC0yNi4zOCBjIC0xNS4xNDUsMCAtMjUuNjU3LDEwLjkyIC0yNS42NTcsMjYuMDcgMCwxNC4zIDEwLjMwNSwyNS44NiAyNi4zODcsMjUuODYgMTguODIsMCAyNy4zMzYsLTEzLjQ2IDI3LjMzNiwtMzYuMzggMCwtMjMuODYgLTcuNjcyLC00Mi41OCAtMjkuNjQ1LC00Mi41OCAtMTMuNjY4LDAgLTIxLjM0Myw4LjIxIC0yMi44MTYsMTguOTMgaCA3LjA0MyBjIDEuMjYyLC04Ljk0IDcuODg3LC0xMy4xNCAxNi44MjQsLTEzLjE0IDEzLjM0OCwwIDIxLjk3MywxMS41NiAyMS45NzMsMzMuNDMgLTMuNDczLC03LjA1IC0xMS4zNTYsLTEyLjE5IC0yMS40NDUsLTEyLjE5IiBzdHlsZT0iZmlsbDojMTAwZjBkO2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDg5NiI+PC9wYXRoPjxwYXRoIGQ9Im0gMTA5LjU0MywzNzc1LjU2IGMgLTEwLjIzNDQsMCAtNDUuNTg2LDAgLTU1LjgyNDIsMCBDIDI0LjA1MDgsMzc3NS41NiAwLDM3NTEuNTEgMCwzNzIxLjg0IGMgMCwtMTAuMjMgMCwtNDUuNTggMCwtNTUuODIgMCwtMjkuNjYgMjQuMDUwOCwtNTMuNzIgNTMuNzE4OCwtNTMuNzIgMTAuMjM4MiwwIDQ1LjU4OTgsMCA1NS44MjQyLDAgMjkuNjY4LDAgNTMuNzE5LDI0LjA2IDUzLjcxOSw1My43MiAwLDEwLjI0IDAsNDUuNTkgMCw1NS44MiAwLDI5LjY3IC0yNC4wNTEsNTMuNzIgLTUzLjcxOSw1My43MiB6IG0gMCwtMTAgYyAyNC4xMDUsMCA0My43MTksLTE5LjYgNDMuNzE5LC00My43MiB2IC01NS44MiBjIDAsLTI0LjExIC0xOS42MTQsLTQzLjcyIC00My43MTksLTQzLjcyIEggNTMuNzE4OCBDIDI5LjYwOTQsMzYyMi4zIDEwLDM2NDEuOTEgMTAsMzY2Ni4wMiB2IDU1LjgyIGMgMCwyNC4xMiAxOS42MDk0LDQzLjcyIDQzLjcxODgsNDMuNzIgaCA1NS44MjQyIiBzdHlsZT0iZmlsbDojYjZiNmI4O2ZpbGwtb3BhY2l0eToxO2ZpbGwtcnVsZTpub256ZXJvO3N0cm9rZTpub25lIiBpZD0icGF0aDg5OCI+PC9wYXRoPjxwYXRoIGQ9Im0gNTYuNDY0OCwzNzIwLjI3IGggMTAuOTcyNyBsIDEyLjU1ODYsLTE3LjgyIDEyLjg0NzcsMTcuODIgaCAxMC4zOTQyIGwgLTE4LjA0NjYsLTI1LjEyIDE5LjI3MzYsLTI3LjIgSCA5My40OTIyIGwgLTEzLjg1NTUsMTkuNTYgLTE0LjA3NDIsLTE5LjU2IEggNTUuMjQyMiBsIDE5LjI2OTUsMjYuNzcgLTE4LjA0NjksMjUuNTUiIHN0eWxlPSJmaWxsOiMxMDBmMGQ7ZmlsbC1vcGFjaXR5OjE7ZmlsbC1ydWxlOm5vbnplcm87c3Ryb2tlOm5vbmUiIGlkPSJwYXRoOTAwIj48L3BhdGg+PHBhdGggZD0ibSA2OTE2LjUyLDE1NjkuNTIgdiAtNDQ3LjQ1IGggLTQ5NDUuNSB2IDQ2OS40OCIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6Mi41O3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDkwMiI+PC9wYXRoPjxwYXRoIGQ9Ik0gNzAzOC4yMywxNTY5LjUyIFYgMTE3MC42NyBIIDI1MDUgdiA0MzEuODEiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjIuNTtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGg5MDQiPjwvcGF0aD48cGF0aCBkPSJNIDcyNjkuODcsMTU2OS41MiBWIDEyMTkuNzQgSCAzMTQ5LjQ5IHYgMzkxLjgyIiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoyLjU7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoOTA2Ij48L3BhdGg+PHBhdGggZD0iTSA2ODc4LjIxLDE1NjUgViAxMjY4LjUgSCAzNTgxLjc4IHYgMzE0IiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoyLjU7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoOTA4Ij48L3BhdGg+PHBhdGggZD0iTSA3MDIxLjYyLDE1NjkuNTIgViAxMzE3LjIxIEggNDEzNy40NiB2IDI3NC43MiIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6Mi41O3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDkxMCI+PC9wYXRoPjxwYXRoIGQ9Ik0gNjk2Ni4xNCwxNTY5LjUyIFYgMTM2NS45MSBIIDQ0OTkuMDMgdiAyMzQuNzciIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjIuNTtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGg5MTIiPjwvcGF0aD48cGF0aCBkPSJNIDcyNDkuMzgsMTU2OS41MiBWIDE0MTQuNjEgSCA1MTkwLjg3IHYgMTk1LjUzIiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoyLjU7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoOTE0Ij48L3BhdGg+PHBhdGggZD0iTSA3NTg0LjYyLDE1NjkuNTIgViAxNDY0LjA1IEggNTkzNi42MSB2IDE1Ni4zNyIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6Mi41O3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDkxNiI+PC9wYXRoPjxwYXRoIGQ9Im0gNzE0NS4xMSwxNTY5LjUyIHYgLTU2IEggNjMyMy41IHYgNzcuNzkiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjIuNTtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGg5MTgiPjwvcGF0aD48cGF0aCBkPSJtIDY4NzguMjEsMTU2OS41MiBoIDcwNi40MyIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzEwMGYwZDtzdHJva2Utd2lkdGg6MTA7c3Ryb2tlLWxpbmVjYXA6YnV0dDtzdHJva2UtbGluZWpvaW46bWl0ZXI7c3Ryb2tlLW1pdGVybGltaXQ6MTA7c3Ryb2tlLWRhc2hhcnJheTpub25lO3N0cm9rZS1vcGFjaXR5OjEiIGlkPSJwYXRoOTIwIj48L3BhdGg+PHBhdGggZD0ibSA2ODc4LjIxLDE1ODkuMjkgdiAtMzkuNTMiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMxMDBmMGQ7c3Ryb2tlLXdpZHRoOjEwO3N0cm9rZS1saW5lY2FwOmJ1dHQ7c3Ryb2tlLWxpbmVqb2luOm1pdGVyO3N0cm9rZS1taXRlcmxpbWl0OjEwO3N0cm9rZS1kYXNoYXJyYXk6bm9uZTtzdHJva2Utb3BhY2l0eToxIiBpZD0icGF0aDkyMiI+PC9wYXRoPjxwYXRoIGQ9Im0gNzU4NC42NCwxNTg5LjI5IHYgLTM5LjUzIiBzdHlsZT0iZmlsbDpub25lO3N0cm9rZTojMTAwZjBkO3N0cm9rZS13aWR0aDoxMDtzdHJva2UtbGluZWNhcDpidXR0O3N0cm9rZS1saW5lam9pbjptaXRlcjtzdHJva2UtbWl0ZXJsaW1pdDoxMDtzdHJva2UtZGFzaGFycmF5Om5vbmU7c3Ryb2tlLW9wYWNpdHk6MSIgaWQ9InBhdGg5MjQiPjwvcGF0aD48L2c+PC9nPjwvc3ZnPg=="
id="svg2" />

</div>

<div class="title">

Figure 1. An exemplary result of Median Algorithm in first sync epoch
with \\s\_"cq" = 9\\ and \\k = 1\\.

</div>

</div>

</div>

<div class="sect2">

### <a href="#block-production" class="anchor"></a><a href="#block-production" class="link">5.4. Production Algorithm</a>

<div class="paragraph">

Throughout each epoch, each block producer should run
[Invoke-Block-Authoring](#algo-block-production) to produce blocks
during the slots it has been awarded during that epoch. The produced
block needs to carry the *Pre-Digest* ([Definition
69](#defn-babe-header)) as well as the *block signature* ([Definition
70](#defn-block-signature)) as Pre-Runtime and Seal digest items.

</div>

<div id="defn-babe-header" class="exampleblock">

<div class="title">

Definition 69. [Pre-Digest](#defn-babe-header)

</div>

<div class="content">

<div class="paragraph">

The **Pre-Digest**, or BABE header, \\P\\, is a varying datatype of the
following format:

</div>

<div class="stemblock">

<div class="content">

\\P =
{(1,-\>,(a\_"id",s,o,p)),(2,-\>,(a\_"id",s)),(3,-\>,(a\_"id",s,o,p)):}\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- *1* indicates a primary slot with VRF outputs, *2* a secondary slot
  with plain outputs and *3* a secondary slot with VRF outputs ([Section
  5.2](#sect-block-production-lottery)). Plain outputs are no longer
  actively used and only exist for backwards compatibility reasons,
  respectively to sync old blocks.

- \\a\_"id"\\ is the unsigned 32-bit integer indicating the index of the
  authority in the authority set ([Section 3.3.1](#sect-authority-set))
  who authored the block.

- \\s\\ is the slot number ([Definition 54](#defn-epoch-slot)).

- \\o\\ is VRF output
  ([Block-Production-Lottery](#algo-block-production-lottery)
  respectively [Definition 61](#defn-babe-secondary-slots)).

- \\p\\ is VRF proof
  ([Block-Production-Lottery](#algo-block-production-lottery)
  respectively [Definition 61](#defn-babe-secondary-slots)).

</div>

</div>

<div class="paragraph">

The Pre-Digest must be included as a digest item of Pre-Runtime type in
the header digest ([Definition 11](#defn-digest)) \\H_d(B)\\.

</div>

</div>

</div>

<div class="sidebarblock">

<div class="content">

\require \$sk, pk, n, BT\$ \state \$A \leftarrow\$
\call{Block-production-lottery}{\$sk, n\$} \for{\$s \leftarrow 1
~\textbf{to}~ sc_n\$} \state \call{Wait-Until}{\call{Slot-Time}{\$s\$}}
\state \$(d, \pi) \leftarrow A\[s\]\$ \if{\$d \< \tau\$} \state
\$C\_{Best} \leftarrow\$ \call{Longest-Chain}{\$BT\$} \state \$B_s
\leftarrow\$ \call{Build-Block}{\$C\_{Best}\$} \state
\call{Add-Digest-Item}{\$B_s,\text{Pre-Runtime}, E\_{id}(\text{BABE}),
H\_\text{BABE}(B_s)\$} \state \call{Add-Digest-Item}{\$B_s, \text{Seal},
S_B\$} \state \call{Broadcast-Block}{\$B_s\$} \endif \endfor

<div class="paragraph">

where \\"BT"\\ is the current block tree, \\"Block-Production-Lottery"\\
is defined in [Block-Production-Lottery](#algo-block-production-lottery)
and \\"Add-Digest-Item"\\ appends a digest item to the end of the header
digest \\H_d(B)\\ ([Definition 11](#defn-digest)).

</div>

</div>

</div>

<div id="defn-block-signature" class="exampleblock">

<div class="title">

Definition 70. [Block Signature](#defn-block-signature)

</div>

<div class="content">

<div class="paragraph">

The **Block Signature** \\S_B\\ is a signature of the block header hash
([Definition 12](#defn-block-header-hash)) and defined as

</div>

<div class="stemblock">

<div class="content">

\\"Sig"\_("SR25519","sk"\_j^s)(H_h(B))\\

</div>

</div>

<div class="paragraph">

\\m\\ should be included in \\H_d(B)\\ as the Seal digest item
([Definition 11](#defn-digest)) of value:

</div>

<div class="stemblock">

<div class="content">

\\(t, "id"("BABE"), m)\\

</div>

</div>

<div class="paragraph">

in which, \\t = 5\\ is the seal digest identifier and \\"id"("BABE")\\
is the BABE consensus engine unique identifier ([Definition
11](#defn-digest)). The Seal digest item is referred to as the **BABE
Seal**.

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-epoch-randomness" class="anchor"></a><a href="#sect-epoch-randomness" class="link">5.5. Epoch Randomness</a>

<div class="paragraph">

At the beginning of each epoch, \\cc E_n\\ the host will receive the
randomness seed \\cc R\_(cc E\_(n+1))\\ ([Definition
71](#defn-epoch-randomness)) necessary to participate in the block
production lottery in the next epoch \\cc E\_(n+1)\\ from the Runtime,
through the consensus message ([Definition
58](#defn-consensus-message-babe)) in the digest of the first block.

</div>

<div id="defn-epoch-randomness" class="exampleblock">

<div class="title">

Definition 71. [Randomness Seed](#defn-epoch-randomness)

</div>

<div class="content">

<div class="paragraph">

For epoch \\cc E\\, there is a 32-byte \\cc R\_(cc E)\\ computed based
on the previous epochs VRF outputs. For \\cc E_0\\ and \\cc E_1\\, the
randomness seed is provided in the genesis state ([Section
C.11.1](#sect-rte-babeapi-epoch)). For any further epochs, the
randomness is retrieved from the consensus message ([Definition
58](#defn-consensus-message-babe)).

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-verifying-authorship" class="anchor"></a><a href="#sect-verifying-authorship" class="link">5.6. Verifying
Authorship Right</a>

<div class="paragraph">

When a Polkadot node receives a produced block, it needs to verify if
the block producer was entitled to produce the block in the given slot
by running [Verify-Authorship-Right](#algo-verify-authorship-right).
[Verify-Slot-Winner](#algo-verify-slot-winner) runs as part of the
verification process, when a node is importing a block.

</div>

<div class="sidebarblock">

<div class="content">

\require \$\text{Head}\_{s(B)}\$ \state \$s \leftarrow\$
\call{Slot-Number-At-Given-Time}{\$T_B\$} \state \$\mathcal{E}\_c
\leftarrow\$ \call{Current-Epoch}{} \state \$(D_1, \ldots,
D\_{\|H_d(B)\|}) \leftarrow H_d(B)\$ \state \$D_s \leftarrow
D\_{\|H_d(B)\|}\$ \state \$H_d(B) \leftarrow \left(D_1, \ldots,
D\_{\|H_d(B)\| - 1}\right)\$ \comment{remove the seal from the digest}
\state \$(id, \text{Sig}\_B)\leftarrow \text{Dec}\_{SC}(D_s)\$ \if{\$id
\neq\$ \textsc{Seal-Id}} \state \textbf{error} \`\`Seal missing'' \endif
\state \$\text{AuthorID} \leftarrow
\text{AuthorityDirectory}^{\mathcal{E}\_c}\[H\_{BABE}(B).\text{SingerIndex}\]\$
\state \call{Verify-Signature}{\$\text{AuthorID},
H_h(B),\text{Sig}\_B\$} \if{\$\exists B' \in BT : H_h(B) \neq H_h (B)\$
\and \$s_B = s_B'\$ \and \$\text{SignerIndex}\_B =
\text{SignerIndex}\_{B'}\$} \state \textbf{error} \`\`Block producer is
equivocating'' \endif \state \call{Verify-Slot-Winner}{\$(d_B, \pi_B),
s_B, \text{AuthorID}\$}

<div class="dlist">

where  
<div class="ulist">

- \\"Head"\_s(B)\\ is the header of the block that’s being verified.

- \\T_B\\ is \\B\\’s arrival time ([Definition 67](#defn-block-time)).

- \\H_d(B)\\ is the digest sub-component ([Definition 11](#defn-digest))
  of \\"Head"(B)\\ ([Definition 10](#defn-block-header)).

- The Seal \\D_s\\ is the last element in the digest array \\H_d(B)\\ as
  described in [Definition 11](#defn-digest).

- \\"Seal-Id"\\ is the type index showing that a digest item
  ([Definition 11](#defn-digest)) of varying type ([Definition
  189](#defn-scale-variable-type)) is of type *Seal*.

- \\"AuthorityDirectory"^(cc E_c)\\ is the set of Authority ID for block
  producers of epoch \\cc E_c\\.

  <div class="olist arabic">

  1.  \\"AuthorId"\\ is the public session key of the block producer.

  </div>

- \\"BT"\\ is the pruned block tree ([Definition 5](#defn-pruned-tree)).

- \\"Verify-Slot-Winner"\\ is defined in
  [Verify-Slot-Winner](#algo-verify-slot-winner).

</div>

</div>

</div>

</div>

<div class="sidebarblock">

<div class="content">

\require \$B\$ \state \$\mathcal{E}\_c \leftarrow\$
\textsc{Current-Epoch} \state \$\rho \leftarrow\$
\call{Epoch-Randomness}{\$c\$} \state \call{Verify-VRF}{\$\rho,
H\_{BABE}(B).(d_B, \pi_B), H\_{BABE}(B).s, c\$} \if{\$d_B \geqslant
\tau\$} \state \textbf{error} \`\`Block producer is not a winner of the
slot'' \endif

<div class="dlist">

where  
<div class="olist arabic">

1.  \\"Epoch-Randomness"\\ is defined in [Definition
    71](#defn-epoch-randomness).

2.  \\H\_"BABE"(B)\\ is the BABE header defined in [Definition
    69](#defn-babe-header).

3.  \\(o,p)\\ is the block lottery result for block \\B\\
    ([Block-Production-Lottery](#algo-block-production-lottery)),
    respectively the VRF output ([Definition
    62](#defn-babe-vrf-transcript)).

4.  \\"Verify-VRF"\\ is described in [Section A.1.3](#sect-vrf).

5.  \\T\_(cc E_n)\\ is the winning threshold as defined in [Definition
    60](#defn-winning-threshold).

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-block-building" class="anchor"></a><a href="#sect-block-building" class="link">5.7. Block Building
Process</a>

<div class="paragraph">

The block building process is triggered by
[Invoke-Block-Authoring](#algo-block-production) of the consensus engine
which in turn runs [Build-Block](#algo-build-block).

</div>

<div class="sidebarblock">

<div class="content">

\state \$P_B \leftarrow \$\call{Head}{\$C\_{Best}\$} \state
\$\text{Head}(B) \leftarrow \left(H_p \leftarrow H_h(P_B), H_i
\leftarrow H_i(P_B) + 1, H_r \leftarrow \phi, H_e \leftarrow \phi, H_d
\leftarrow \phi \right)\$ \state
\call{Call-Runtime-Entry}{\$\texttt{Core\\initialize\\block},
\text{Head}(B)\$} \state \textsc{I-D}\$ \leftarrow
\$\call{Call-Runtime-Entry}{\$\texttt{BlockBuilder\\inherent\\extrinsics},
\$\textsc{Inherent-Data}} \for{\$E~\textbf{in} \$\textsc{I-D}} \state
\call{Call-Runtime-Entry}{\$\texttt{BlockBuilder\\apply\\extrinsics},
E\$} \endfor \while{\not \call{End-Of-Slot}{\$s\$}} \state \$E
\leftarrow\$ \call{Next-Ready-Extrinsic}{} \state \$R \leftarrow\$
\call{Call-Runtime-Entry}{\$\texttt{BlockBuilder\\apply\\extrinsics},
E\$} \if{\call{Block-Is-Full}{\$R\$}} \break \endif
\if{\call{Should-Drop}{\$R\$}} \state \call{Drop}{\$E\$} \endif \state
\$\text{Head}(B) \leftarrow\$
\call{Call-Runtime-Entry}{\$\texttt{BlockBuilder\\finalize\\block}, B\$}
\state \$B \leftarrow\$ \call{Add-Seal}{\$B\$} \endwhile

<div class="dlist">

where  
<div class="ulist">

- \\C\_"Best"\\ is the chain head at which the block should be
  constructed ("parent").

- \\s\\ is the slot number.

- \\"Head"(B)\\ is defined in [Definition 10](#defn-block-header).

- \\"Call-Runtime-Entry"\\ is defined in [Definition
  32](#defn-call-into-runtime).

- \\"Inherent-Data"\\ is defined in [Definition
  15](#defn-inherent-data).

- \\"End-Of-Slot"\\ indicates the end of the BABE slot as defined
  [Median-Algorithm](#algo-slot-time) respectively [Definition
  54](#defn-epoch-slot).

- \\"Next-Ready-Extrinsic"\\ indicates picking an extrinsic from the
  extrinsics queue ([Definition 14](#defn-transaction-queue)).

- \\"Block-Is-Full"\\ indicates that the maximum block size is being
  used.

- \\"Should-Drop"\\ determines based on the result \\R\\ whether the
  extrinsic should be dropped or remain in the extrinsics queue and
  scheduled for the next block. The *ApplyExtrinsicResult* ([Definition
  217](#defn-rte-apply-extrinsic-result)) describes this behavior in
  more detail.

- \\"Drop"\\ indicates removing the extrinsic from the extrinsic queue
  ([Definition 14](#defn-transaction-queue)).

- \\"Add-Seal"\\ adds the seal to the block (\<\<\>\>) before sending it
  to peers. The seal is removed again before submitting it to the
  Runtime.

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#sect-finality" class="anchor"></a><a href="#sect-finality" class="link">6. Finality</a>

<div class="sectionbody">

<div class="sect2">

### <a href="#id-introduction-4" class="anchor"></a><a href="#id-introduction-4" class="link">6.1. Introduction</a>

<div class="paragraph">

The Polkadot Host uses GRANDPA Finality protocol to finalize blocks.
Finality is obtained by consecutive rounds of voting by the validator
nodes. Validators execute GRANDPA finality process in parallel to Block
Production as an independent service. In this section, we describe the
different functions that GRANDPA service performs to successfully
participate in the block-finalization process.

</div>

<div id="defn-grandpa-voter" class="exampleblock">

<div class="title">

Definition 72. [GRANDPA Voter](#defn-grandpa-voter)

</div>

<div class="content">

<div class="paragraph">

A **GRANDPA Voter**, \\v\\, represented by a key pair
\\(K_v^("pr"),v\_("id"))\\ where \\k_v^("pr")\\ represents an *ed25519*
private key, is a node running a GRANDPA protocol and broadcasting votes
to finalize blocks in a Polkadot Host-based chain. The **set of all
GRANDPA voters** for a given block B is indicated by \\bbb V_B\\. In
that regard, we have \[To do: change function name, only call at
genesis, adjust V_B over the sections\]

</div>

<div class="stemblock">

<div class="content">

\\bbb V = tt "grandpa_authorities"(B)\\

</div>

</div>

<div class="paragraph">

where \\tt "grandpa_authorities"\\ is a function entrypoint of the
Runtime described in [Section C.10.1](#sect-rte-grandpa-auth). We refer
to \\bbb V_B\\ as \\bbb V\\ when there is no chance of ambiguity.

</div>

<div class="paragraph">

Analogously we say that a Polkadot node is a **non-voter node** for
block \\B\\, if it does not own any of the key pairs in \\bbb V_B\\.

</div>

</div>

</div>

<div id="defn-authority-set-id" class="exampleblock">

<div class="title">

Definition 73. [Authority Set Id](#defn-authority-set-id)

</div>

<div class="content">

<div class="paragraph">

The **authority set Id** (\\"id"\_(bbb V)\\) is an incremental counter
which tracks the amount of authority list changes that occurred
([Definition 86](#defn-consensus-message-grandpa)). Starting with the
value of zero at genesis, the Polkadot Host increments this value by one
every time a **Scheduled Change** or a **Forced Change** occurs. The
authority set Id is an unsigned 64-bit integer.

</div>

</div>

</div>

<div id="defn-grandpa-state" class="exampleblock">

<div class="title">

Definition 74. [GRANDPA State](#defn-grandpa-state)

</div>

<div class="content">

<div class="paragraph">

The **GRANDPA state**, \\"GS"\\, is defined as:

</div>

<div class="stemblock">

<div class="content">

\\"GS" := {bbb V, "id"\_(bbb V),r}\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\bbb V\\: is the set of voters.

- \\"id"\_(bbb V)\\: is the authority set ID ([Definition
  73](#defn-authority-set-id)).

- \\r\\: is the voting round number.

</div>

</div>

</div>

</div>

<div id="defn-vote" class="exampleblock">

<div class="title">

Definition 75. [GRANDPA Vote](#defn-vote)

</div>

<div class="content">

<div class="paragraph">

A **GRANDPA vote** or simply a vote for block \\B\\ is an ordered pair
defined as

</div>

<div class="stemblock">

<div class="content">

\\V(B) := (H_h(B),H_i(B))\\

</div>

</div>

<div class="paragraph">

where \\H_h(B)\\ and \\H_i (B)\\ are the block hash ([Definition
12](#defn-block-header-hash)) and the block number ([Definition
10](#defn-block-header)).

</div>

</div>

</div>

<div id="defn-voting-rounds" class="exampleblock">

<div class="title">

Definition 76. [Voting Rounds](#defn-voting-rounds)

</div>

<div class="content">

<div class="paragraph">

Voters engage in a maximum of two sub-rounds of voting for each round
\\r\\. The first sub-round is called **pre-vote** and the second
sub-round is called **pre-commit**.

</div>

<div class="paragraph">

By \\V_v^(r,"pv")\\ and \\V_v^(r,"pc")\\ we refer to the vote cast by
voter \\v\\ in round \\r\\ (for block \\B\\) during the pre-vote and the
pre-commit sub-round respectively.

</div>

<div class="paragraph">

Voting is done by means of broadcasting voting messages ([Section
4.8.6](#sect-msg-grandpa)) to the network. Validators inform their peers
about the block finalized in round \\r\\ by broadcasting a commit
message ([Play-Grandpa-Round](#algo-grandpa-round)).

</div>

</div>

</div>

<div id="defn-sign-round-vote" class="exampleblock">

<div class="title">

Definition 77. [Vote Signature](#defn-sign-round-vote)

</div>

<div class="content">

<div class="paragraph">

\\"Sign"\_(v_i)^(r,"stage")\\ refers to the signature of a voter for a
specific message in a round and is formally defined as:

</div>

<div class="stemblock">

<div class="content">

\\"Sign"\_(v_i)^(r,"stage") := "Sig"\_("ed25519")("msg",r,"id"\_(bbb
V))\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\"msg"\\: is an byte array containing the message to be signed
  ([Definition 75](#defn-vote)).

- \\r\\: is an unsigned 64-bit integer is the round number.

- \\"id"\_(bbb V)\\: is an unsigned 64-bit integer indicating the
  authority set Id ([Definition 33](#defn-authority-list)).

</div>

</div>

</div>

</div>

<div id="defn-grandpa-justification" class="exampleblock">

<div class="title">

Definition 78. [Justification](#defn-grandpa-justification)

</div>

<div class="content">

<div class="paragraph">

The **justification** for block \\B\\ in round \\r\\,
\\J^(r,"stage")(B)\\, is a vector of pairs of the type:

</div>

<div class="stemblock">

<div class="content">

\\(V(B'),"Sign"\_(v_i)^(r,"stage")(B'),v\_("id"))\\

</div>

</div>

<div class="paragraph">

in which either

</div>

<div class="stemblock">

<div class="content">

\\B' \>= B\\

</div>

</div>

<div class="paragraph">

or \\V\_(v_i)^(r,"pc")(B')\\ is an equivocatory vote.

</div>

<div class="paragraph">

In all cases, \\"Sign"\_(v_i)^(r,"stage")(B')\\ is the signature
([Definition 77](#defn-sign-round-vote)) of voter \\v\_("id") in bbb
V_B\\ broadcasted during either the pre-vote (stage = pv) or the
pre-commit (stage = pc) sub-round of round r. A **valid justification**
must only contain up-to-one valid vote from each voter and must not
contain more than two equivocatory votes from each voter.

</div>

</div>

</div>

<div id="defn-finalizing-justification" class="exampleblock">

<div class="title">

Definition 79. [Finalizing
Justification](#defn-finalizing-justification)

</div>

<div class="content">

<div class="paragraph">

We say \\J^(r,"pc")(B)\\ **justifies the finalization** of \\B' \>= B\\
**for a non-voter node** \\n\\ if the number of valid signatures in
\\J^(r,"pc")(B)\\ for \\B'\\ is greater than \\2/3\|bbb V_B\|\\.

</div>

<div class="paragraph">

Note that \\J^(r,"pc")(B)\\ can only be used by a non-voter node to
finalize a block. In contrast, a voter node can only be assured of the
finality ([Definition 90](#defn-finalized-block)) of block \\B\\ by
actively participating in the voting process. That is by invoking
[Play-Grandpa-Round](#algo-grandpa-round).

</div>

<div class="paragraph">

The GRANDPA protocol dictates how an honest voter should vote in each
sub-round, which is described by
[Play-Grandpa-Round](#algo-grandpa-round). After defining what
constitutes a vote in GRANDPA, we define how GRANDPA counts votes.

</div>

</div>

</div>

<div id="defn-equivocation" class="exampleblock">

<div class="title">

Definition 80. [Equivocation](#defn-equivocation)

</div>

<div class="content">

<div class="paragraph">

Voter \\v\\ **equivocates** if they broadcast two or more valid votes to
blocks during one voting sub-round. In such a situation, we say that
\\v\\ is an **equivocator** and any vote \\V_v^(r,"stage")(B)\\ cast by
\\v\\ in that sub-round is an **equivocatory vote**, and

</div>

<div class="stemblock">

<div class="content">

\\cc E^(r,"stage")\\

</div>

</div>

<div class="paragraph">

represents the set of all equivocators voters in sub-round *stage* of
round \\r\\. When we want to refer to the number of equivocators whose
equivocation has been observed by voter \\v\\ we refer to it by:

</div>

<div class="stemblock">

<div class="content">

\\cc E\_("obs"(v))^(r,"stage")\\

</div>

</div>

<div class="paragraph">

The Polkadot Host must detect equivocations committed by other
validators and submit those to the Runtime as described in [Section
C.10.2](#sect-grandpaapi_submit_report_equivocation_unsigned_extrinsic).

</div>

<div class="paragraph">

A vote \\V_v^(r,"stage") = V(B)\\ is **invalid** if

</div>

<div class="ulist">

- \\H (B)\\ does not correspond to a valid block.

- \\B\\ is not an (eventual) descendant of a previously finalized block.

- \\M_v^(r,"stage")\\ does not bear a valid signature.

- \\"id"\_(bbb V)\\ does no match the current \\bbb V\\.

- \\V_v^(r,"stage")\\ is an equivocatory vote.

</div>

</div>

</div>

<div id="defn-observed-direct-votes" class="exampleblock">

<div class="title">

Definition 81. [Set of Observed Direct
Votes](#defn-observed-direct-votes)

</div>

<div class="content">

<div class="paragraph">

For validator \\v\\, **the set of observed direct votes for Block \\B\\
in round \\r\\**, formally denoted by
\\"VD"\_("obs"(v))^(r,"stage")(B)\\ is equal to the union of:

</div>

<div class="ulist">

- set of *valid* votes \\V\_(v_i)^(r,"stage")\\ cast in round \\r\\ and
  received by \\v\\ such that \\V\_(v_i)^(r,"stage") = V(B)\\.

</div>

</div>

</div>

<div id="defn-observed-votes" class="exampleblock">

<div class="title">

Definition 82. [Set of Total Observed Votes](#defn-observed-votes)

</div>

<div class="content">

<div class="paragraph">

We refer to **the set of total votes observed by voter \\v\\ in
sub-round *stage* of round \\r\\** by \\V\_("obs"(v))^(r,"stage")\\.

</div>

<div class="paragraph">

The **set of all observed votes by \\v\\ in the sub-round stage of round
\\r\\ for block \\B\\**, **\\V\_("obs"(v))^(r,"stage")\\** is equal to
all of the observed direct votes cast for block \\B\\ and all of the
\\B\\’s descendants defined formally as:

</div>

<div class="stemblock">

<div class="content">

\\V\_("obs"(v))^(r,"stage")(B) := uuu\_(v_i in bbb V, B \< B')
"VD"\_("obs"(v))^(r,"stage")(B')\\

</div>

</div>

<div class="paragraph">

The **total number of observed votes for Block \\B\\ in round \\r\\** is
defined to be the size of that set plus the total number of equivocator
voters:

</div>

<div class="stemblock">

<div class="content">

\\#V\_("obs"(v))^(r,"stage")(B) := \|V\_("obs"(v))^(r,"stage")(B)\|+\|cc
E\_("obs"(v))^(r,"stage")\|\\

</div>

</div>

<div class="paragraph">

Note that for genesis state we always have \\#V\_("obs"(v))^(r,"pv")(B)
= \|bbb V\|\\.

</div>

</div>

</div>

<div id="defn-total-potential-votes" class="exampleblock">

<div class="title">

Definition 83. [Set of Total Potential
Votes](#defn-total-potential-votes)

</div>

<div class="content">

<div class="paragraph">

Let \\V\_("unobs"(v))^(r,"stage")\\ be the set of voters whose vote in
the given stage has not been received. We define the **total number of
potential votes for Block \\B\\ in round \\r\\** to be:

</div>

<div class="stemblock">

<div class="content">

\\#V\_("obs"(v),"pot")^(r,"stage")(B) :=
\|V\_("obs"(v))^(r,"stage")(B)\|+\|V\_("unobs"(v))^(r,"stage")\|+"Min"(1/3\|bbb
V\|,\|bbb
V\|-\|V\_("obs"(v))^(r,"stage")(B)\|-\|V\_("unobs"(v))^(r,"stage")\|)\\

</div>

</div>

</div>

</div>

<div id="defn-grandpa-ghost" class="exampleblock">

<div class="title">

Definition 84. [Current Pre-Voted Block](#defn-grandpa-ghost)

</div>

<div class="content">

<div class="paragraph">

The current **pre-voted** block \\B_v^(r,"pv")\\ also know as GRANDPA
GHOST is the block chosen by [GRANDPA-GHOST](#algo-grandpa-ghost):

</div>

<div class="stemblock">

<div class="content">

\\B_v^(r,"pv") := "GRANDPA-GHOST"(r)\\

</div>

</div>

<div class="paragraph">

Finally, we define when a voter \\v\\ sees a round as completable, that
is when they are confident that \\B_v^(r,"pv")\\ is an upper bound for
what is going to be finalized in this round.

</div>

</div>

</div>

<div id="defn-grandpa-completable" class="exampleblock">

<div class="title">

Definition 85. [Completable Round](#defn-grandpa-completable)

</div>

<div class="content">

<div class="paragraph">

We say that round \\r\\ is **completable** if
\\\|V\_("obs"(v))^(r,"pc")\|+ cc E\_("obs"(v))^(r,"pc") \> 2/3 bbb V\\
and for all \\B' \> B_v^(r,"pv")\\:

</div>

<div class="stemblock">

<div class="content">

\\\|V\_("obs"(v))^(r,"pc")\|- cc E\_("obs"(v))^(r,"pc") -
\|V\_("obs"(v))^(r,"pc")(B')\|\> 2/3\|bbb V\|\\

</div>

</div>

<div class="paragraph">

Note that in practice we only need to check the inequality for those
\\B' \> B_v^(r,"pv")\\ where \\\|V\_("obs"(v))^(r,"pc")(B')\| \> 0\\.

</div>

</div>

</div>

<div id="defn-consensus-message-grandpa" class="exampleblock">

<div class="title">

Definition 86. [GRANDPA Consensus Message](#defn-consensus-message-babe)

</div>

<div class="content">

<div class="paragraph">

\\"CM"\_g\\, the consensus message for GRANDPA, is of the following
format:

</div>

<div class="stemblock">

<div class="content">

\\"CM"\_g =
{(1,("Auth"\_C,N\_("delay"))),(2,(m,"Auth"\_C,N\_("delay"))),(3,"A"\_i),(4,N\_("delay")),(5,N\_("delay")):}\\

</div>

</div>

<div class="dlist">

where

</div>

<div class="hdlist">

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td class="hdlist1">\$N_"delay"\$</td>
<td class="hdlist2"><p>is an unsigned 32-bit integer indicating how deep
in the chain the announcing block must be before the change is
applied.</p></td>
</tr>
<tr class="even">
<td class="hdlist1">1</td>
<td class="hdlist2"><p>implies <strong>scheduled change</strong>:
Schedule an authority set change after the given delay of \$N_("delay")
:= |"SubChain"(B,B')|\$ where \$B'\$ is the block where the change is
applied. The earliest digest of this type in a single block will be
respected, unless a force change is present, in which case the force
change takes precedence.</p></td>
</tr>
<tr class="odd">
<td class="hdlist1">2</td>
<td class="hdlist2"><p>implies <strong>forced change</strong>: Schedule
a forced authority set change after the given delay of \$N_("delay") :=
|"SubChain"(B,m + B')|\$ where \$B'\$ is the block where the change is
applied. The earliest digest of this type in a block will be
respected.</p>
<div class="paragraph">
<p>Forced changes are explained further in <a
href="#sect-finality-forced-changes">Section 6.5</a>.</p>
</div></td>
</tr>
<tr class="even">
<td class="hdlist1">3</td>
<td class="hdlist2"><p>implies <strong>on disabled</strong>: An index to
the individual authority in the current authority list (<a
href="#defn-authority-list">Definition 33</a>) that should be
immediately disabled until the next authority set changes. When an
authority gets disabled, the node should stop performing any authority
functionality from that authority, including authoring blocks and
casting GRANDPA votes for finalization. Similarly, other nodes should
ignore all messages from the indicated authority which pertain to their
authority role.</p></td>
</tr>
<tr class="odd">
<td class="hdlist1">4</td>
<td class="hdlist2"><p>implies <strong>pause</strong>: A signal to pause
the current authority set after the given delay of \$N_("delay") :=
|"SubChain"(B,B')|\$ where \$B'\$ is a block where the change is
applied. Once applied, the authorities should stop voting.</p></td>
</tr>
<tr class="even">
<td class="hdlist1">5</td>
<td class="hdlist2"><p>implies <strong>resume</strong>: A signal to
resume the current authority set after the given delay of \$N_("delay")
:= |"SubChain"(B,B')|\$ where \$B'\$ is the block where the change is
applied. Once applied, the authorities should resume voting.</p></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

<div id="defn-consensus-message-beefy" class="exampleblock">

<div class="title">

Definition 87. [BEEFY Consensus Message](#defn-consensus-message-beefy)

</div>

<div class="content">

<div class="admonitionblock important">

|     |                                                                                                                                             |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------|
|     | The BEEFY protocol is still under construction. The following part will be updated in the future and certain information will be clarified. |

</div>

<div class="paragraph">

\\"CM"\_y\\, the consensus message for BEEFY ([Section
6.7](#sect-grandpa-beefy)), is of the following format:

</div>

<div class="stemblock">

<div class="content">

\\"CM"\_y = {(1,(V_B,V_i)),(2,A_i),(3,R):}\\

</div>

</div>

<div class="dlist">

where

</div>

<div class="hdlist">

|     |                                                                                                                                                                                  |
|-----|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1   | implies that the remote **authorities have changed**. \\V_B\\ is the array of the new BEEFY authorities’s public keys and \\V_i\\ is the identifier of the remote validator set. |
| 2   | implies **on disabled**: an index to the individual authorty in \\V_B\\ that should be immediately disabled until the next authority change.                                     |
| 3   | implies **MMR root**: a 32-byte array containing the MMR root.                                                                                                                   |

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#id-initiating-the-grandpa-state" class="anchor"></a><a href="#id-initiating-the-grandpa-state" class="link">6.2. Initiating
the GRANDPA State</a>

<div class="paragraph">

In order to participate coherently in the voting process, a validator
must initiate its state and sync it with other active validators. In
particular, considering that voting is happening in different distinct
rounds where each round of voting is assigned a unique sequential round
number \\r_v\\, it needs to determine and set its round counter \\r\\
equal to the voting round \\r_n\\ currently undergoing in the network.
The mandated initialization procedure for the GRANDPA protocol for a
joining validator is described in detail in
[Initiate-Grandpa](#algo-initiate-grandpa).

</div>

<div class="paragraph">

The process of joining a new voter set is different from the one of
rejoining the current voter set after a network disconnect. The details
of this distinction are described further in this section.

</div>

<div class="sect3">

#### <a href="#id-voter-set-changes" class="anchor"></a><a href="#id-voter-set-changes" class="link">6.2.1. Voter Set
Changes</a>

<div class="paragraph">

A GRANDPA voter node which is initiating GRANDPA protocol as part of
joining a new authority set is required to execute
[Initiate-Grandpa](#algo-initiate-grandpa). The algorithm mandates the
initialization procedure for GRANDPA protocol.

</div>

<div class="admonitionblock note">

|     |                                                                     |
|-----|---------------------------------------------------------------------|
|     | The GRANDPA round number reset to 0 for every authority set change. |

</div>

<div class="paragraph">

Voter set changes are signaled by Runtime via a consensus engine message
([Section 3.3.2](#sect-consensus-message-digest)). When Authorities
process such messages they must not vote on any block with a higher
number than the block at which the change is supposed to happen. The new
authority set should reinitiate GRANDPA protocol by executing
[Initiate-Grandpa](#algo-initiate-grandpa).

</div>

<div class="sidebarblock">

<div class="content">

\input \$r\_{last}, B\_{last}\$ \state \textsc{Last-Finalized-Block}
\$\leftarrow B\_{last}\$ \state \textsc{Best-Final-Candidate}\$(0)
\leftarrow B\_{last}\$ \state \textsc{GRANDPA-GHOST}\$(0) \leftarrow
B\_{last}\$ \state \textsc{Last-Completed-Round}\$ \leftarrow 0\$ \state
\$r_n \leftarrow 1\$ \state \call{Play-Grandpa-round}{\$r_n\$}

<div class="paragraph">

where \\B\_("last")\\ is the last block which has been finalized on the
chain ([Definition 90](#defn-finalized-block)). \\r\_("last")\\ is equal
to the latest round the voter has observed that other voters are voting
on. The voter obtains this information through various gossiped messages
including those mentioned in [Definition 90](#defn-finalized-block).
\\r\_("last")\\ is set to *0* if the GRANDPA node is initiating the
GRANDPA voting process as a part of a new authority set. This is because
the GRANDPA round number resets to *0* for every authority set change.

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#id-rejoining-the-same-voter-set" class="anchor"></a><a href="#id-rejoining-the-same-voter-set" class="link">6.3. Rejoining
the Same Voter Set</a>

<div class="paragraph">

When a voter node rejoins the network after a disconnect from the voter
set and with the condition that there has been no change to the voter
set at the time of the disconnect, the node must continue performing the
GRANDPA protocol at the same state as before getting disconnected from
the network, ignoring any possible progress in GRANDPA finalization.
Following reconnection, the node eventually gets updated to the current
GRANDPA round and synchronizes its state with the rest of the voting set
through the process called Catchup ([Section
6.6.1](#sect-grandpa-catchup)).

</div>

</div>

<div class="sect2">

### <a href="#id-voting-process-in-round-r" class="anchor"></a><a href="#id-voting-process-in-round-r" class="link">6.4. Voting Process
in Round \$r\$</a>

<div class="paragraph">

For each round \\r\\, an honest voter \\v\\ must participate in the
voting process by following [Play-Grandpa-Round](#algo-grandpa-round).

</div>

<div class="sidebarblock">

<div class="content">

\REQUIRE(\$r\$) \STATE \$t\_{r, v} \leftarrow\$ Current local time
\STATE \$\textrm{primary} \leftarrow\$ \call{Derive-Primary}{\$r\$}
\IF{\$v = \textrm{primary}\$} \STATE \call{Broadcast}{\$M\_{v}^{r - 1,
\textrm{Fin}}(\$\call{Best-Final-Candidate}{\$r - 1\$}\$)\$}
\IF{\call{Best-Final-Candidate}{\$r - 1\$} \$\geqslant\$
\textsc{Last-Finalized-Block}} \STATE \call{Broadcast}{\$M\_{v}^{r - 1,
\textrm{Prim}}(\$\call{Best-Final-Candidate}{\$r - 1\$}\$)\$} \ENDIF
\ENDIF \STATE \call{Receive-Messages}{\textbf{until} Time \$\geqslant
t\_{r\_,v} + 2 \times T\$ \or \$r\$ \textbf{is} completable} \STATE \$L
\leftarrow\$ \call{Best-Final-Candidate}{\$r - 1\$} \STATE \$N
\leftarrow\$ \call{Best-PreVote-Candidate}{\$r\$} \STATE
\call{Broadcast}{\$M_v^{r, \textrm{pv}} (N)\$} \STATE
\call{Receive-Messages}{\textbf{until} \$B^{r,\textrm{pv}}\_v \geqslant
L\$ \and \$(\$ Time \$\geqslant t\_{r\_,v} + 4 \times T\$ \or \$r\$
\textbf{is} completable \$)\$} \STATE \call{Broadcast}{\$M_v^{r,
\textrm{pc}}(B_v^{r, \textrm{pv}})\$} \REPEAT \STATE
\call{Receive-Messages}{} \STATE
\call{Attempt-To-Finalize-At-Round}{\$r\$} \UNTIL{\$r\$ \textbf{is}
completable \and \call{Finalizable}{\$r\$} \and
\textsc{Last-Finalized-Block} \$\geqslant\$
\call{Best-Final-Candidate}{\$r - 1\$}} \STATE
\call{Play-Grandpa-round}{\$r + 1\$} \REPEAT \STATE
\call{Receive-Messages}{} \STATE
\call{Attempt-To-Finalize-At-Round}{\$r\$}
\UNTIL{\textsc{Last-Finalized-Block} \$\geqslant\$
\call{Best-Final-Candidate}{\$r\$}} \IF{\textsc{Last-Completed-Round} \$
\< r \$} \STATE \textsc{Last-Completed-Round} \$\leftarrow r\$ \ENDIF

<div class="dlist">

where  
<div class="ulist">

- \\T\\ is sampled from a log-normal distribution whose mean and
  standard deviation are equal to the average network delay for a
  message to be sent and received from one validator to another.

- \\"Derive-Primary"\\ is described in
  [Derive-Primary](#algo-derive-primary).

- The condition of *completablitiy* is defined in [Definition
  85](#defn-grandpa-completable).

- \\"Best-Final-Candidate"\\ function is explained in
  [Best-Final-Candidate](#algo-grandpa-best-candidate).

- \\"Attempt-To-Finalize-At-Round"(r)\\ is described in
  [Attempt-To-Finalize-At-Round](#algo-attempt-to–finalize).

- \\"Finalizable"\\ is defined in [Finalizable](#algo-finalizable).

</div>

</div>

</div>

</div>

<div class="sidebarblock">

<div class="content">

\input \$r\$ \return \$r \bmod \|\mathbb{V}\|\$

<div class="paragraph">

where \\r\\ is the GRANDPA round whose primary is to be determined.

</div>

</div>

</div>

<div class="sidebarblock">

<div class="content">

\input \$r\$ \state \$B_v^{r, pv} \leftarrow\$
\call{GRANDPA-GHOST}{\$r\$} \if{\$r = 0\$} \return \$B_v^{r, pv}\$ \else
\state \$\mathcal{C} \leftarrow \\ B' \| B' \leqslant B_v^{r,pv} \|
\\V^{r, pc}\_{\operatorname{obv}(v), pot}(B') \> \frac{2}{3}
\|\mathbb{V}\| \\\$ \if{\$\mathcal{C} = \phi\$} \return \$B_v^{r, pv}\$
\else \return \$E \in \mathcal{C} : H_n (E) =
\operatorname{max}\left(H_n (B') \| B' \in \mathcal{C}\right)\$ \endif
\endif

<div class="paragraph">

where \\#V\_("obv"(v),pot)^(r,pc)\\ is defined in [Definition
83](#defn-total-potential-votes).

</div>

</div>

</div>

<div class="sidebarblock">

<div class="content">

\input \$r\$ \if{\$r = 0\$} \state \$G \leftarrow B\_{last}\$ \else
\state \$L \leftarrow\$ \call{Best-Final-Candidate}{\$r - 1\$} \state
\$\mathcal{G} = \\ \forall B \> L \| \\V\_{\operatorname{obs}(v)}^{r,
pv}(B) \geqslant \frac{2}{3} \|\mathbb{V}\| \\\$ \if{\$\mathcal{G} =
\phi\$} \state \$G \leftarrow L\$ \else \state \$G \in \mathcal{G} \|
H_n(G) = \operatorname{max}\left( H_n (B) \| \forall B \in \mathcal{G}
\right)\$ \endif \endif \return \$G\$

<div class="dlist">

where  
<div class="ulist">

- \\B\_("last")\\ is the last block which has been finalized on the
  chain ([Definition 90](#defn-finalized-block)).

- \\#V\_("obs"(v))^(r,pv)(B)\\ is defined in [Definition
  82](#defn-observed-votes).

</div>

</div>

</div>

</div>

<div class="sidebarblock">

<div class="content">

\input \$r\$ \state \$B^{r, pv}\_v \leftarrow\$
\call{GRANDPA-GHOST}{\$r\$} \if{\call{Received}{\$M\_{v\_{primary}}^{r,
prim}(B))\$ \and \$B^{r, pv}\_v \geqslant B \> L\$}} \state \$N
\leftarrow B\$ \else \state \$N \leftarrow B^{r, pv}\_v\$ \endif

</div>

</div>

<div class="sidebarblock">

<div class="content">

\REQUIRE(\$r\$) \STATE \$L \leftarrow\$ \textsc{Last-Finalized-Block}
\STATE \$E \leftarrow\$ \call{Best-Final-Candidate}{\$r\$} \IF{\$E
\geqslant L\$ \and \${V^{r, \textrm{pc}}\_{\textrm{obs}(v)}}(E) \> 2 / 3
\|\mathbb{V}\|\$} \STATE{\textsc{Last-Finalized-Block}\$\leftarrow E\$}
\IF{\$M_v^{r, \textrm{Fin}} (E) \notin \$\textsc{Received-Messages}}
\STATE \call{Broadcast}{\$M_v^{r, \textrm{Fin}}(E)\$} \RETURN \ENDIF
\ENDIF

</div>

</div>

<div class="sidebarblock">

<div class="content">

\REQUIRE(\$r\$) \IF{\$r\$ \textbf{is not} Completable} \RETURN
\textbf{False} \ENDIF \STATE \$G \leftarrow\$
\call{GRANDPA-GHOST}{\$J^{r, pv}(B)\$} \IF{\$G = \phi\$} \RETURN
\textbf{False} \ENDIF \STATE \$E_r \leftarrow\$
\call{Best-Final-Candidate}{\$r\$} \IF{\$E_r \neq \phi\$ \and
\call{Best-Final-Candidate}{\$r - 1\$} \$\leqslant E_r \leqslant G\$}
\RETURN \textbf{True} \ELSE \RETURN \textbf{False} \ENDIF

<div class="paragraph">

where the condition for *completability* is defined in [Definition
85](#defn-grandpa-completable).

</div>

</div>

</div>

<div class="paragraph">

Note that we might not always succeed in finalizing our best final
candidate due to the possibility of equivocation. We might even not
finalize anything in a round (although
[Play-Grandpa-Round](#algo-grandpa-round) prevents us from moving to the
round \\r+1\\ before finalizing the best final candidate of round
\\r-1\\) The example in [Definition 88](#exmp-candid-unfinalized) serves
to demonstrate a situation where the best final candidate of a round
cannot be finalized during its own round:

</div>

<div id="exmp-candid-unfinalized" class="exampleblock">

<div class="title">

Definition 88. Unfinalized Candidate

</div>

<div class="content">

<div class="paragraph">

Let us assume that we have 100 voters and there are two blocks in the
chain (\\B_1 \< B_2\\). At round 1, we get 67 pre-votes for \\B_2\\ and
at least one pre-vote for \\B_1\\ which means that \\"GRANDPA-GHOST"(1)
= B_2\\.

</div>

<div class="paragraph">

Subsequently, potentially honest voters who could claim not seeing all
the pre-votes for \\B_2\\ but receiving the pre-votes for \\B_1\\ would
pre-commit to \\B_1\\. In this way, we receive 66 pre-commits for
\\B_1\\ and 1 pre-commit for \\B_2\\. Henceforth, we finalize \\B_1\\
since we have a threshold commit (67 votes) for \\B_1\\.

</div>

<div class="paragraph">

At this point, though, we have \\tt "Best-Final-Candidate"(r) = B_2\\ as
\\#V\_("obs"(v),"pot")^(r,"stage")(B_2) = 67\\ and \\2 \> 1\\.

</div>

<div class="paragraph">

However, at this point, the round is already completable as we know that
we have \\tt "GRANDPA-GHOST"(1) = B_2\\ as an upper limit on what we can
finalize and nothing greater than \\B_2\\ can be finalized at \\r = 1\\.
Therefore, the condition of [Play-Grandpa-Round](#algo-grandpa-round) is
satisfied and we must proceed to round 2.

</div>

<div class="paragraph">

Nonetheless, we must continue to attempt to finalize round *1* in the
background as the condition of
[Attempt-To-Finalize-At-Round](#algo-attempt-to–finalize) has not been
fulfilled.

</div>

<div class="paragraph">

This prevents us from proceeding to round 3 until either:

</div>

<div class="ulist">

- We finalize \\B_2\\ in round 2, or

- We receive an extra pre-commit vote for \\B_1\\ in round 1. This will
  make it impossible to finalize \\B_2\\ in round 1, no matter to whom
  the remaining pre-commits are going to be cast for (even with
  considering the possibility of 1/3 of voter equivocating) and
  therefore we have \\tt "Best-Final-Candidate"(r) = B_1\\.

</div>

<div class="paragraph">

Both scenarios unblock [Play-Grandpa-Round](#algo-grandpa-round), \\tt
"Last-Finalized-Block" \>= tt "Best-Final-Candidate"(r - 1)\\ albeit in
different ways: the former with increasing the \\tt
"Last-Finalized-Block"\\ and the latter with decreasing \\tt
"Best-Final-Candidate"(r - 1)\\.

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-finality-forced-changes" class="anchor"></a><a href="#sect-finality-forced-changes" class="link">6.5. Forced
Authority Set Changes</a>

<div class="paragraph">

In a case of emergency where the Polkadot network is unable to finalize
blocks, such as in an event of mass validator outage, the Polkadot
governance mechanism must enact a forced change, which the Host must
handle in a specific manner. Given that in such a case finality cannot
be relied on, the Host must detect the forced change ([Definition
86](#defn-consensus-message-grandpa)) in a (valid) block and apply it to
all forks.

</div>

<div class="paragraph">

The \\m in CM_g\\, which is specified by the governance mechanism,
defines the starting block at which \\N\_("delay")\\ is applied. This
provides some degree of probabilistic consensus to the network with the
assumption that the forced change was received by most participants and
that finality can be continued.

</div>

<div class="imageblock">

<div class="content">

![](data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOiByZ2IoMjU1LCAyNTUsIDI1NSk7IiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiB3aWR0aD0iODcxcHgiIGhlaWdodD0iNDIycHgiIHZpZXdib3g9Ii0wLjUgLTAuNSA4NzEgNDIyIiBjb250ZW50PSImbHQ7bXhmaWxlIGhvc3Q9JnF1b3Q7YXBwLmRpYWdyYW1zLm5ldCZxdW90OyBtb2RpZmllZD0mcXVvdDsyMDIyLTA2LTA3VDEwOjU2OjAyLjE5OFomcXVvdDsgYWdlbnQ9JnF1b3Q7NS4wIChYMTEpJnF1b3Q7IHZlcnNpb249JnF1b3Q7MTkuMC4yJnF1b3Q7IGV0YWc9JnF1b3Q7TVpuS21lWXJreVA4OEZ3ZThBaHMmcXVvdDsgdHlwZT0mcXVvdDtkZXZpY2UmcXVvdDsmZ3Q7Jmx0O2RpYWdyYW0gaWQ9JnF1b3Q7bGlaNUFWSXk3Rk5JZVhOS2RsOEwmcXVvdDsmZ3Q7N1Z4TGs2TTJFUDQxcmlTSGNTSEV3ejc2c1pNY05xbXRUS3AyOTRoQlk3T0RMUWZqSFR1L1BoSklnRURZbVBkdU1RY1Bhb1NRMVAxSlg3Y2tKbkMxdi96dVc4ZmRuOWhCM2tSVm5Nc0VyaWVxT3A5RDhrc0ZWeVpRelVpdzlWMG5Fb0ZFOE9MK2g1aFFZZEt6NjZDVGtESEEyQXZjb3lpMDhlR0E3RUNRV2I2UDM4VnNyOWdUMzNxMHRpZ25lTEV0THkvOTdEckJqa21Cb2lRMy9rRHVkc2RlUGRQWmpZMWx2MjE5ZkQ2dzl4M3dBVVYzOWhZdmhtVTk3U3dIdjZkRThNTUVybnlNZytocWYxa2hqL1lxNzdIb3VlZUN1M0dWZlhRSXlqeWdzbW9FVjk1cTVKQk9ZRW5zQnp1OHhRZkwrNUJJbDJITEVDMUFJYWtrejBlTWowUUlpUEFiQ29JcjA2aDFEakFSN1lLOXgrNlN1dm5YTHpReFZXWWFGM3lsQlU2MWVaeGpmV0d2aUZMWGRPb1Q4dDA5Q3BEUGhLLzRFRHhiZTllanVmNGh0MDZrVlgraGQvTDdOOTViQjVhRlZRa1lKQjIxbkRaWDZMc1RQdnMyRXpFRERpeC9pMWgzcWtxK2kwR3NPQUlGaEVtOS9Ddko0aVBQQ3R6dll2RVdNOHB0bkMvUkRybGdDcElyaTFYbnUrV2RXYUZMRDl0dkUxb25HSnRsU3BlaXB0NTNib0JlamxiWXVuY0NXVkVycjY3bnJiQ0gvZkJaQ0V4VlVXay9uUUlmdnlGK0o3Umx1TFE4ZDBzNmRlMmhWOUlKeSsvSUQxeUNuQVVUQjlRU3doNVBsZmdjL3RFU1NSM2N3L1pqK093YTFsRWZmVEc2RkJwL2dXYllBeXJRbzBmWUFBVm1yQXZmVTNEbkN0K2xrRzRvOVpXcDlZczhFWFg2SGN5MUF5ODlEeS9ZSDdyMDIrZ0N2eXhHZkQyR0wyaG04S1YyaUM5anhKYzVLSHlaOS9DMUhQRlZEMStxMWlHK1pqbDFMbzVIenlYYTZoTjNLYWg5RlpBbXg1MWpuWGJoZTBGcklBVGNkVW1qMEhoVTFhUmQ1bXd1YUJzeUpaWUdLaXY4RTNiSk8rT1M5WG5CSU0yTGlDck9ua3E3RXJ3Z25oRy92cDZRa0dmaCs5WTFsZU5JbnpnVjE4VXdGYUV1cHVDOGtJdW93TVErNDQ0cVpiTHoycWI1N2J3Lzh2eVdiMWN6VnNIb2FPS1RGUkJQNWhCS1ZDV3laMmRCUGRoa3dDS1NaNWUyTExMaWl4dEU1cTdxTFBtVlE0RmNKOVpPRTRMakZEMEZUQ2hPVUlwaURzZnRra0ZHYjM3aWt0dWdwaW1WOFBDb3JjTUMzRFZsN0NEdkR0YXg5bTA0M2RZY21xR2FzVG9OVnJHNkZEcHN6enFkWEZzQVNBNWpIUTdzcy83NEZhOVBha2FlcUlaSDZZMHIySUh4NzVtR2w4STJQNTNDUmkvb3VHTWNMMkhMK1gxeXRXWC9QWjYvVmtHL3Z0aEVLV2VQY2dSbHRiTU9XL1FiTDN6ak4xSkgwa2xSTlhOaWw4c1daMkxEdmh0UUpielErWXJ5VDFMNEtyeHFzc00ydFVweGlJSFFPdXFwUm14dU5hd2VmYjdEaVBldTQ0UkRSSVptcjFlcjVkb3NvdGtaQnAxdzhxRXdhRjBjaEhVSmdlWWtPMDJndFFZSU5PZ2w5dHJGd0doSUJrYXRxL25iVUFncG1tV1lzanFkYTByeXA1ZWEwYXRNdXZrUTdTMnY2S08xUVo0Y2hqYnBKanJoRlFQUlIyUVFzVFpoZWRRWUdPRWdoZXZMaWI1dUdGTnNrWVc5YnlLUGc2dDNmQmh0cm9oNGV3S04rRENxNkJrOXpjUUM4bzVKRmRYV0Q5ZzI0ajBJTEQ1TnA4QlVpZWxWR1hlM291Y2hKV1J5ZHlUMlFLVHVTSGVEajlraktkT0h4OEoxUFdNMlB6UUxsK2hiNjNHTmp0ZW5jUmJlRFhtK3paS1hJMHN1eTVJTGlPOUQ3SG1vTEJuQ0xtbHlmdDNnR2Z0dnNkdVcwU1pwWmRBZW82SUQ2NGwxYnFIUGsxSnh5ZzNxUVcwWnNnVWthak1scXdQWmdGY2xyZVdYQnhLdDVURTRhcTFRYTdHS3V0QmFzeEh5eW13bDI2MGxxRVlKWlpWZ0U3d1RCVFpSWG9XTnN3bGVueFNNcHRQcENKOWkrQUF0QXg4bER4L1lFbnhpaStvdm9wTjRZcFhXaFhSZFdCZDZVcWFLY2MrcDdIQmhpTWQxMnQ2UVYybEJCNERNd3BHUjJYcVp6VytvdC9MWFhnQlNlNGt2TnJJU3o2MFlwR3c0c2VndXd3a3lpK3R4RHcxL2Q0OGpUSDZDNzdEbmUzVHNHOWl3Mlhna1I4dXM0czluUnBYQit0RklUcFZKcGtNalVRYzZJY0RzWHZ6c1Rod2QzTXBmZjBJWVlDenlrU2xpR0FGSG1jbTFzRG1sOUxCVWY1OXJxMHE5ZjVyalp4cDdXbGhwNkdUbzBhQitLMy85b2NjY25wWEN1VGg1S2thbExYQzVJYWNnY0hGbkh4K0kzczd0ZWFxb3Qra3VUY2lxa2wvUmF5Z3lJckgyWGlNaitRRGp6N1BPOGlXSGxpNjI4amkydlhITXlZMWRPN0xJejVFYjRVdTBXc0dxT0ppMUMzRWdsSjN3TWlUaG9DWldMb2F5MzdqcW9aUm1vcTVWamwxS29yQTlVaXc0Qm1FZkJKMmVvUk5BY2pDbHJTQXNyQitFYlFoMWZhRkg3WVNYbHRhSE9xS25IbnJpNDFwZG9LZCtnTEhoT1d1cTZNSTJOekp2cVRGemJ6aksxUklndFR3ZzJ3aFNsZGF4bGtPa2NCTFRHRTlpUGdwWkkrTnZkM29TRXpZYjEyc0Nzd0JvSW1ZMXM5Sm5QZnJEckd3UGU1K2Yvc2h2Szh4Z2R2dzZRVTNNZHZwMUFqaTBnTmdQNHh2S1ZuektINmR1SHBqNU9OUkliMi9penN3Yzh1N1VPUnpJQnJjZkRuYWFKQ1RUeHBtdTBsOVBHbU15TldIWHBWZkpGd3BHYlpYVlZ1WWpCQzN1WWlUSjVIT0QwZEplOGpWSCtPRi8mbHQ7L2RpYWdyYW0mZ3Q7Jmx0Oy9teGZpbGUmZ3Q7Ij48ZGVmcz48L2RlZnM+PGc+PHBhdGggZD0iTSAyMzUgMjEwIEwgMjE1IDIxMCBMIDIwMy44OSAyMDkuODkiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDE5OC42NCAyMDkuODMgTCAyMDUuNjcgMjA2LjQgTCAyMDMuODkgMjA5Ljg5IEwgMjA1LjYgMjEzLjQgWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHJlY3QgeD0iMjM1IiB5PSIxODAiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiMxNzIwMjYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9yZWN0PjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25vYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkZmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgZmxleC1zdGFydDsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgZmxleC1zdGFydDsgd2lkdGg6IDExNXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE4N3B4OyBtYXJnaW4tbGVmdDogMjQwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDBweDsgdGV4dC1hbGlnbjogbGVmdDsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6ICNGRkZGRkY7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMjU1LCAyNTUsIDI1NSk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IG92ZXJmbG93LXdyYXA6IG5vcm1hbDsiPkJsb2NrICMxMDA8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iMjQwIiB5PSIyMDMiIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJUaW1lcyBOZXcgUm9tYW4iIGZvbnQtc2l6ZT0iMTZweCI+QmxvY2sgIzEwMDwvdGV4dD48L3N3aXRjaD48L2c+PHBhdGggZD0iTSAzOTUgMTUwIEwgMzc1IDE1MCBMIDM3NSAyMTAgTCAzNjEuMzcgMjEwIiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PHBhdGggZD0iTSAzNTYuMTIgMjEwIEwgMzYzLjEyIDIwNi41IEwgMzYxLjM3IDIxMCBMIDM2My4xMiAyMTMuNSBaIiBmaWxsPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcGF0aD48cmVjdCB4PSIzOTUiIHk9IjEyMCIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iIzE3MjAyNiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBmbGV4LXN0YXJ0OyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBmbGV4LXN0YXJ0OyB3aWR0aDogMTE1cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTI3cHg7IG1hcmdpbi1sZWZ0OiA0MDBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMHB4OyB0ZXh0LWFsaWduOiBsZWZ0OyIgZGF0YS1kcmF3aW8tY29sb3JzPSJjb2xvcjogI0ZGRkZGRjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IFRpbWVzIE5ldyBSb21hbjsgY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgb3ZlcmZsb3ctd3JhcDogbm9ybWFsOyI+QmxvY2sgIzEwMSYjMzk7QTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbm9iamVjdD48dGV4dCB4PSI0MDAiIHk9IjE0MyIgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IlRpbWVzIE5ldyBSb21hbiIgZm9udC1zaXplPSIxNnB4Ij5CbG9jayAjMTAxJiMzOTtBPC90ZXh0Pjwvc3dpdGNoPjwvZz48cGF0aCBkPSJNIDM5NSAyNzAgTCAzNzUgMjcwIEwgMzc1IDIxMCBMIDM2MS4zNyAyMTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDM1Ni4xMiAyMTAgTCAzNjMuMTIgMjA2LjUgTCAzNjEuMzcgMjEwIEwgMzYzLjEyIDIxMy41IFoiIGZpbGw9InJnYigwLCAwLCAwKSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9wYXRoPjxyZWN0IHg9IjM5NSIgeT0iMjQwIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjMTcyMDI2IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcmVjdD48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWdub2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZGZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGZsZXgtc3RhcnQ7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGZsZXgtc3RhcnQ7IHdpZHRoOiAxMTVweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNDdweDsgbWFyZ2luLWxlZnQ6IDQwMHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGxlZnQ7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiAjRkZGRkZGOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogVGltZXMgTmV3IFJvbWFuOyBjb2xvcjogcmdiKDI1NSwgMjU1LCAyNTUpOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyBvdmVyZmxvdy13cmFwOiBub3JtYWw7Ij5CbG9jayAjMTAxJiMzOTtCPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWdub2JqZWN0Pjx0ZXh0IHg9IjQwMCIgeT0iMjYzIiBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiPkJsb2NrICMxMDEmIzM5O0I8L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gNTUwIDcwIEwgNjkwIDcwIEwgNjkwIDExMy42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PHBhdGggZD0iTSA2OTAgMTE4Ljg4IEwgNjg2LjUgMTExLjg4IEwgNjkwIDExMy42MyBMIDY5My41IDExMS44OCBaIiBmaWxsPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcGF0aD48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWdub2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZGZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDgwcHg7IG1hcmdpbi1sZWZ0OiA3MjBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMHB4OyB0ZXh0LWFsaWduOiBjZW50ZXI7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiByZ2IoMCwgMCwgMCk7IGJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IFRpbWVzIE5ldyBSb21hbjsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogcmdiKDI1NSwgMjU1LCAyNTUpOyB3aGl0ZS1zcGFjZTogbm93cmFwOyI+QXBwbGllZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbm9iamVjdD48dGV4dCB4PSI3MjAiIHk9Ijg1IiBmaWxsPSJyZ2IoMCwgMCwgMCkiIGZvbnQtZmFtaWx5PSJUaW1lcyBOZXcgUm9tYW4iIGZvbnQtc2l6ZT0iMTZweCIgdGV4dC1hbmNob3I9Im1pZGRsZSI+QXBwbGllZDwvdGV4dD48L3N3aXRjaD48L2c+PHBhdGggZD0iTSA0MTguNzUgOTAgTCA0MTguODMgMTIwLjQyIEwgNDE1LjgzIDEyMC40MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMSAxIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PHBhdGggZD0iTSA1NTAgNzAgTCA4MDYgNzAgTCA4MDUuOTYgMTM0LjQ5IiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDgwNS45NiAxMzkuNzQgTCA4MDIuNDYgMTMyLjc0IEwgODA1Ljk2IDEzNC40OSBMIDgwOS40NiAxMzIuNzQgWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHJlY3QgeD0iMzc1IiB5PSI1MCIgd2lkdGg9IjE3NSIgaGVpZ2h0PSI0MCIgZmlsbD0iI2RjY2JkNyIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGZsZXgtc3RhcnQ7IHdpZHRoOiAxNzBweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3MHB4OyBtYXJnaW4tbGVmdDogMzgwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDBweDsgdGV4dC1hbGlnbjogbGVmdDsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6ICMxNzIwMjY7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMjMsIDMyLCAzOCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IG92ZXJmbG93LXdyYXA6IG5vcm1hbDsiPjxpIHN0eWxlPSJmb250LXNpemU6IDE2cHg7Ij48Zm9udCBzdHlsZT0iZm9udC1zaXplOiAxNnB4OyI+KFNjaGVkdWxlZCBDaGFuZ2UpPGJyIHN0eWxlPSJmb250LXNpemU6IDE2cHg7IiAvPjwvZm9udD48L2k+QXV0aG9yaXR5IFNldCAjQSwgPGkgc3R5bGU9ImZvbnQtc2l6ZTogMTZweDsiPjxiIHN0eWxlPSJmb250LXNpemU6IDE2cHg7Ij5kZWxheSA1PC9iPjwvaT48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iMzgwIiB5PSI3NSIgZmlsbD0iIzE3MjAyNiIgZm9udC1mYW1pbHk9IlRpbWVzIE5ldyBSb21hbiIgZm9udC1zaXplPSIxNnB4Ij4oU2NoZWR1bGVkIENoYW5nZSkuLi48L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gNTUwIDM1MCBMIDY5MCAzNTAgTCA2OTAgMzA2LjM3IiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDY5MCAzMDEuMTIgTCA2OTMuNSAzMDguMTIgTCA2OTAgMzA2LjM3IEwgNjg2LjUgMzA4LjEyIFoiIGZpbGw9InJnYigwLCAwLCAwKSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9wYXRoPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25vYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkZmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzQxcHg7IG1hcmdpbi1sZWZ0OiA3MjBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMHB4OyB0ZXh0LWFsaWduOiBjZW50ZXI7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiByZ2IoMCwgMCwgMCk7IGJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IFRpbWVzIE5ldyBSb21hbjsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogcmdiKDI1NSwgMjU1LCAyNTUpOyB3aGl0ZS1zcGFjZTogbm93cmFwOyI+QXBwbGllZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbm9iamVjdD48dGV4dCB4PSI3MjAiIHk9IjM0NiIgZmlsbD0icmdiKDAsIDAsIDApIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPkFwcGxpZWQ8L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gNDE4Ljc1IDMzMCBMIDQxNS40MiAzMzAgTCA0MTUuNCAzMDEuMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMSAxIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PHBhdGggZD0iTSA1NTAgMzUwIEwgODA2LjY3IDM1MCBMIDgwNi42NSAyODcuMjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gODA2LjY1IDI4MS45OCBMIDgxMC4xNSAyODguOTggTCA4MDYuNjUgMjg3LjIzIEwgODAzLjE1IDI4OC45OCBaIiBmaWxsPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcGF0aD48cmVjdCB4PSIzNzUiIHk9IjMzMCIgd2lkdGg9IjE3NSIgaGVpZ2h0PSI0MCIgZmlsbD0iI2RjY2JkNyIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGZsZXgtc3RhcnQ7IHdpZHRoOiAxNzBweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNTBweDsgbWFyZ2luLWxlZnQ6IDM4MHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGxlZnQ7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiAjMTcyMDI2OyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogVGltZXMgTmV3IFJvbWFuOyBjb2xvcjogcmdiKDIzLCAzMiwgMzgpOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyBvdmVyZmxvdy13cmFwOiBub3JtYWw7Ij48aSBzdHlsZT0iZm9udC1zaXplOiAxNnB4OyI+KFNjaGVkdWxlZCBDaGFuZ2UpPGJyIHN0eWxlPSJmb250LXNpemU6IDE2cHg7IiAvPjwvaT5BdXRob3JpdHkgU2V0ICNCLCA8aSBzdHlsZT0iZm9udC1zaXplOiAxNnB4OyI+PGIgc3R5bGU9ImZvbnQtc2l6ZTogMTZweDsiPmRlbGF5IDU8L2I+PC9pPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbm9iamVjdD48dGV4dCB4PSIzODAiIHk9IjM1NSIgZmlsbD0iIzE3MjAyNiIgZm9udC1mYW1pbHk9IlRpbWVzIE5ldyBSb21hbiIgZm9udC1zaXplPSIxNnB4Ij4oU2NoZWR1bGVkIENoYW5nZSkuLi48L3RleHQ+PC9zd2l0Y2g+PC9nPjxyZWN0IHg9IjMyNSIgeT0iMTMwIiB3aWR0aD0iNzAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9yZWN0PjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25vYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkZmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTQwcHg7IG1hcmdpbi1sZWZ0OiAzNjBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMHB4OyB0ZXh0LWFsaWduOiBjZW50ZXI7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiByZ2IoMCwgMCwgMCk7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7Ij5Gb3JrICNBPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWdub2JqZWN0Pjx0ZXh0IHg9IjM2MCIgeT0iMTQ1IiBmaWxsPSJyZ2IoMCwgMCwgMCkiIGZvbnQtZmFtaWx5PSJUaW1lcyBOZXcgUm9tYW4iIGZvbnQtc2l6ZT0iMTZweCIgdGV4dC1hbmNob3I9Im1pZGRsZSI+Rm9yayAjQTwvdGV4dD48L3N3aXRjaD48L2c+PHJlY3QgeD0iMzI1IiB5PSIyNzAiIHdpZHRoPSI3MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyODBweDsgbWFyZ2luLWxlZnQ6IDM2MHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGNlbnRlcjsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6IHJnYigwLCAwLCAwKTsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IFRpbWVzIE5ldyBSb21hbjsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsiPkZvcmsgI0I8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iMzYwIiB5PSIyODUiIGZpbGw9InJnYigwLCAwLCAwKSIgZm9udC1mYW1pbHk9IlRpbWVzIE5ldyBSb21hbiIgZm9udC1zaXplPSIxNnB4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIj5Gb3JrICNCPC90ZXh0Pjwvc3dpdGNoPjwvZz48cGF0aCBkPSJNIDE2NSAyMTAgTCA5Ni4zNyAyMTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDkxLjEyIDIxMCBMIDk4LjEyIDIwNi41IEwgOTYuMzcgMjEwIEwgOTguMTIgMjEzLjUgWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHJlY3QgeD0iMTY1IiB5PSIyMDAiIHdpZHRoPSIzMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMTBweDsgbWFyZ2luLWxlZnQ6IDE4MHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGNlbnRlcjsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6IHJnYigwLCAwLCAwKTsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IFRpbWVzIE5ldyBSb21hbjsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsiPi4uLjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbm9iamVjdD48dGV4dCB4PSIxODAiIHk9IjIxNSIgZmlsbD0icmdiKDAsIDAsIDApIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPi4uLjwvdGV4dD48L3N3aXRjaD48L2c+PHBhdGggZD0iTSAxMzAgMTIwIEwgMTMwIDE2MCBMIDE4MS41OCAxNjAgTCAxODEuNTkgMTkyLjM5IiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDE4MS41OSAxOTcuNjQgTCAxNzguMDkgMTkwLjY0IEwgMTgxLjU5IDE5Mi4zOSBMIDE4NS4wOSAxOTAuNjQgWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHBhdGggZD0iTSAyMTAgMTAwIEwgMjk1IDEwMCBMIDI5NSAxNzMuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gMjk1IDE3OC44OCBMIDI5MS41IDE3MS44OCBMIDI5NSAxNzMuNjMgTCAyOTguNSAxNzEuODggWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHBhdGggZD0iTSAyMTAgMTAwIEwgNDE1Ljc4IDEwMCBNIDQyMS43OCAxMDAgTSA0MjEuNzggMTAwIEwgNTcwIDEwMCBMIDU3MCAxMzMuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gNTcwIDEzOC44OCBMIDU2Ni41IDEzMS44OCBMIDU3MCAxMzMuNjMgTCA1NzMuNSAxMzEuODggWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHBhdGggZD0iTSAxMzAgMTIwIEwgMTMwIDIwNyBNIDEzMCAyMTMgTSAxMzAgMjEzIEwgMTMwIDMyMCBMIDQxMi40MSAzMjAgTSA0MTguNDEgMzIwIE0gNDE4LjQxIDMyMCBMIDU3MS4zMyAzMjAgTCA1NzEuMyAyODYuMDkiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gNTcxLjI5IDI4MC44NCBMIDU3NC44IDI4Ny44MyBMIDU3MS4zIDI4Ni4wOSBMIDU2Ny44IDI4Ny44NCBaIiBmaWxsPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcGF0aD48cGF0aCBkPSJNIDIxMCAxMDAgTCA0MTUuNzggMTAwIE0gNDIxLjc4IDEwMCBNIDQyMS43OCAxMDAgTCA0NTUgMTAwIEwgNDU1IDExMy42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PHBhdGggZD0iTSA0NTUgMTE4Ljg4IEwgNDUxLjUgMTExLjg4IEwgNDU1IDExMy42MyBMIDQ1OC41IDExMS44OCBaIiBmaWxsPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcGF0aD48cGF0aCBkPSJNIDEzMCAxMjAgTCAxMzAgMjA3IE0gMTMwIDIxMyBNIDEzMCAyMTMgTCAxMzAgMzIwIEwgNDEyLjQxIDMyMCBNIDQxOC40MSAzMjAgTSA0MTguNDEgMzIwIEwgNDU1IDMyMCBMIDQ1NSAzMDYuMzciIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gNDU1IDMwMS4xMiBMIDQ1OC41IDMwOC4xMiBMIDQ1NSAzMDYuMzcgTCA0NTEuNSAzMDguMTIgWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHBhdGggZD0iTSA3Ni43MiAxMjEgTCA3Ni4xNyAyMDEuMzQiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjEgMSIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxyZWN0IHg9IjUwIiB5PSI4MCIgd2lkdGg9IjE2MCIgaGVpZ2h0PSI0MCIgZmlsbD0iI2RjY2JkNyIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGZsZXgtc3RhcnQ7IHdpZHRoOiAxNTVweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMDBweDsgbWFyZ2luLWxlZnQ6IDU1cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDBweDsgdGV4dC1hbGlnbjogbGVmdDsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6ICMxNzIwMjY7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMjMsIDMyLCAzOCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IG92ZXJmbG93LXdyYXA6IG5vcm1hbDsiPjxpIHN0eWxlPSJmb250LXNpemU6IDE2cHg7Ij4oU2NoZWR1bGVkIENoYW5nZSk8YnIgc3R5bGU9ImZvbnQtc2l6ZTogMTZweDsiIC8+PC9pPkF1dGhvcml0eSBTZXQgI1g8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iNTUiIHk9IjEwNSIgZmlsbD0iIzE3MjAyNiIgZm9udC1mYW1pbHk9IlRpbWVzIE5ldyBSb21hbiIgZm9udC1zaXplPSIxNnB4Ij4oU2NoZWR1bGVkIENoYW5nZSkuLi48L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gNTU1IDE1MCBMIDUyMS4zNyAxNTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDUxNi4xMiAxNTAgTCA1MjMuMTIgMTQ2LjUgTCA1MjEuMzcgMTUwIEwgNTIzLjEyIDE1My41IFoiIGZpbGw9InJnYigwLCAwLCAwKSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9wYXRoPjxyZWN0IHg9IjU1NSIgeT0iMTQwIiB3aWR0aD0iMzAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9yZWN0PjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25vYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkZmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTUwcHg7IG1hcmdpbi1sZWZ0OiA1NzBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMHB4OyB0ZXh0LWFsaWduOiBjZW50ZXI7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiByZ2IoMCwgMCwgMCk7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7Ij4uLi48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iNTcwIiB5PSIxNTUiIGZpbGw9InJnYigwLCAwLCAwKSIgZm9udC1mYW1pbHk9IlRpbWVzIE5ldyBSb21hbiIgZm9udC1zaXplPSIxNnB4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIj4uLi48L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gNTU1IDI3MCBMIDUyMS4zNyAyNzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDUxNi4xMiAyNzAgTCA1MjMuMTIgMjY2LjUgTCA1MjEuMzcgMjcwIEwgNTIzLjEyIDI3My41IFoiIGZpbGw9InJnYigwLCAwLCAwKSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9wYXRoPjxyZWN0IHg9IjU1NSIgeT0iMjYwIiB3aWR0aD0iMzAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9yZWN0PjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25vYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkZmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjcwcHg7IG1hcmdpbi1sZWZ0OiA1NzBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMHB4OyB0ZXh0LWFsaWduOiBjZW50ZXI7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiByZ2IoMCwgMCwgMCk7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7Ij4uLi48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iNTcwIiB5PSIyNzUiIGZpbGw9InJnYigwLCAwLCAwKSIgZm9udC1mYW1pbHk9IlRpbWVzIE5ldyBSb21hbiIgZm9udC1zaXplPSIxNnB4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIj4uLi48L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gNjMwIDI3MCBMIDU5My4wOCAyNzAuNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gNTg3LjgzIDI3MC41NSBMIDU5NC43MyAyNjYuODUgTCA1OTMuMDggMjcwLjQgTCA1OTQuOTIgMjczLjg1IFoiIGZpbGw9InJnYigwLCAwLCAwKSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9wYXRoPjxyZWN0IHg9IjYzMCIgeT0iMjQwIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjMTcyMDI2IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcmVjdD48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWdub2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZGZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGZsZXgtc3RhcnQ7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGZsZXgtc3RhcnQ7IHdpZHRoOiAxMTVweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNDdweDsgbWFyZ2luLWxlZnQ6IDYzNXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGxlZnQ7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiAjRkZGRkZGOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogVGltZXMgTmV3IFJvbWFuOyBjb2xvcjogcmdiKDI1NSwgMjU1LCAyNTUpOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyBvdmVyZmxvdy13cmFwOiBub3JtYWw7Ij5CbG9jayAjMTA2JiMzOTtCPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWdub2JqZWN0Pjx0ZXh0IHg9IjYzNSIgeT0iMjYzIiBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiPkJsb2NrICMxMDYmIzM5O0I8L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gNjMwIDE1MCBMIDU5NC43OSAxNDkuNjEiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDU4OS41NCAxNDkuNDUgTCA1OTYuNjQgMTQ2LjE3IEwgNTk0Ljc5IDE0OS42MSBMIDU5Ni40MyAxNTMuMTcgWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHJlY3QgeD0iNjMwIiB5PSIxMjAiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiMxNzIwMjYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9yZWN0PjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25vYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkZmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgZmxleC1zdGFydDsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgZmxleC1zdGFydDsgd2lkdGg6IDExNXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyN3B4OyBtYXJnaW4tbGVmdDogNjM1cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDBweDsgdGV4dC1hbGlnbjogbGVmdDsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6ICNGRkZGRkY7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMjU1LCAyNTUsIDI1NSk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IG92ZXJmbG93LXdyYXA6IG5vcm1hbDsiPkJsb2NrICMxMDYmIzM5O0E8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iNjM1IiB5PSIxNDMiIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJUaW1lcyBOZXcgUm9tYW4iIGZvbnQtc2l6ZT0iMTZweCI+QmxvY2sgIzEwNiYjMzk7QTwvdGV4dD48L3N3aXRjaD48L2c+PHBhdGggZD0iTSA3OTAgMTUwIEwgNzU2LjM3IDE1MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gNzUxLjEyIDE1MCBMIDc1OC4xMiAxNDYuNSBMIDc1Ni4zNyAxNTAgTCA3NTguMTIgMTUzLjUgWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHJlY3QgeD0iNzkwIiB5PSIxNDAiIHdpZHRoPSIzMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNTBweDsgbWFyZ2luLWxlZnQ6IDgwNXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGNlbnRlcjsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6IHJnYigwLCAwLCAwKTsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IFRpbWVzIE5ldyBSb21hbjsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsiPi4uLjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbm9iamVjdD48dGV4dCB4PSI4MDUiIHk9IjE1NSIgZmlsbD0icmdiKDAsIDAsIDApIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPi4uLjwvdGV4dD48L3N3aXRjaD48L2c+PHBhdGggZD0iTSA3OTAgMjcwIEwgNzU2LjM3IDI3MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gNzUxLjEyIDI3MCBMIDc1OC4xMiAyNjYuNSBMIDc1Ni4zNyAyNzAgTCA3NTguMTIgMjczLjUgWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHJlY3QgeD0iNzkwIiB5PSIyNjAiIHdpZHRoPSIzMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNzBweDsgbWFyZ2luLWxlZnQ6IDgwNXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGNlbnRlcjsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6IHJnYigwLCAwLCAwKTsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IFRpbWVzIE5ldyBSb21hbjsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsiPi4uLjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbm9iamVjdD48dGV4dCB4PSI4MDUiIHk9IjI3NSIgZmlsbD0icmdiKDAsIDAsIDApIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPi4uLjwvdGV4dD48L3N3aXRjaD48L2c+PHJlY3QgeD0iNjAiIHk9IjIwMCIgd2lkdGg9IjMwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcmVjdD48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWdub2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZGZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIxMHB4OyBtYXJnaW4tbGVmdDogNzVweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMHB4OyB0ZXh0LWFsaWduOiBjZW50ZXI7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiByZ2IoMCwgMCwgMCk7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7Ij4uLi48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iNzUiIHk9IjIxNSIgZmlsbD0icmdiKDAsIDAsIDApIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPi4uLjwvdGV4dD48L3N3aXRjaD48L2c+PC9nPjxzd2l0Y2g+PGcgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48L2c+PGEgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMCwtNSkiIHhsaW5rOmhyZWY9Imh0dHBzOi8vd3d3LmRpYWdyYW1zLm5ldC9kb2MvZmFxL3N2Zy1leHBvcnQtdGV4dC1wcm9ibGVtcyIgdGFyZ2V0PSJfYmxhbmsiPjx0ZXh0IHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTBweCIgeD0iNTAlIiB5PSIxMDAlIj5UZXh0IGlzIG5vdCBTVkcgLSBjYW5ub3QgZGlzcGxheTwvdGV4dD48L2E+PC9zd2l0Y2g+PC9zdmc+)

</div>

<div class="title">

Figure 2. Applying a scheduled change

</div>

</div>

<div class="imageblock">

<div class="content">

![](data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOiByZ2IoMjU1LCAyNTUsIDI1NSk7IiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiB3aWR0aD0iODcxcHgiIGhlaWdodD0iNDQycHgiIHZpZXdib3g9Ii0wLjUgLTAuNSA4NzEgNDQyIiBjb250ZW50PSImbHQ7bXhmaWxlIGhvc3Q9JnF1b3Q7YXBwLmRpYWdyYW1zLm5ldCZxdW90OyBtb2RpZmllZD0mcXVvdDsyMDIyLTA2LTA3VDEwOjU2OjE5LjQ5NVomcXVvdDsgYWdlbnQ9JnF1b3Q7NS4wIChYMTEpJnF1b3Q7IHZlcnNpb249JnF1b3Q7MTkuMC4yJnF1b3Q7IGV0YWc9JnF1b3Q7MXc5WUpoam82enVsQ01aUG9UTm8mcXVvdDsgdHlwZT0mcXVvdDtkZXZpY2UmcXVvdDsmZ3Q7Jmx0O2RpYWdyYW0gaWQ9JnF1b3Q7c2JzekMtam8taGtWdDl6SVhDRXYmcXVvdDsmZ3Q7N1Z4YmM2TTJGUDQxbnU0KzJNTk5ZQjV0SjJrN3MrM3NORHZUM1VkaUs1Z05SaTdnamROZlh3a2tRQ0I4QVhISjFuNUk0Q0NFMERuZnVlbWdpYjdhSFg4Tm5mMzJEN1NCL2tSVE5zZUpmamZSTk52VzhWOUNlS01FelVvSmJ1aHRVcEthRXg2OWZ5RWxLcFI2OERZdzRockdDUG14dCtlSmF4UUVjQjF6TkNjTTBTdmY3Qm41L0ZQM2pnc3JoTWUxNDFlcGYzdWJlRXVwcXFMa0YzNkRucnVsajU0RGV1SEpXYis0SVRvRTlIa0JDbUI2WmVld2JtalRhT3RzMEd1QnBOOVA5RldJVUp3ZTdZNHI2Sk5aWlRPVzN2ZFFjelViY2dpRCtKSWJORHFNK0kyOU5kemdTYUNuS0l5M3lFV0I0OS9uMUdYeVpwQjBvT0N6dk0wbmhQYVlxR0xpZHhqSGI1U2p6aUZHbUxTTmR6Njlpc2NXdm4wbEp6TmxiakRDTjlMaHpMQ3pGbmRIK29qMDdLMTQ5aG1HM2c3R01LVEVaeFRFRDg3TzgwbXJML2hTaE4vcVQvaUsvLzZGZGs1QW05QWhxU1krVDkrY3ZDNDNkeEU2aEd0S29nSWNPNkVMNlhReVduR0sxWXh4R0FvUTRYR0ZiN2hKQ0gwbjluN3czVHRVS04yc1hjNGRmRUFaSkdZV2ZmUVB4ei9RVHBjK1dyOU1DSS8xVEN3THZPUTU5YnIxWXZpNGQ1SzNlOFdRNWJueTdQbitDdmtvVE83VlZVdFROREpQVVJ5aUY4aXVKTEtzTHgzZmMvR2szdm53R1UvQzhnY01ZdzhqWjBISk1aR0VaTVlMUFQ0a1A5SWpIb01YdUorU2UrLzBOdXdqRDRiSFd1R3Y0UXk5UVZOQmVndFZVR0JPcC9DMUFIZUcxRzBCNmFiU25wbkdzTWpqVVFmT1lLNGJlSUVxdkFaRUZ6aU5MdldYeFExZjErRkx0MHI0MG5yRWwzbkRselVxZkZubjhMVzg0YXNkdmt5alIzek5XK1ByKzJHM1orMmRjTjBNY1JzbjJpWTlzcFBQVG96ZHdpQ2hhRXFLdzgyQ2hBTTU5ekhsd1NOdmxrTHg2TVZmRTVocWdKNStZeERHeHpsa3lRbm5oYVozcVpiT28xMVJyUEg0c0NvTG5RcGFBTWpYQXZUV3o4akRQV1lTYWpDSkxGc0Exa1U2S25wWExueVlYODVib2RtZU5JanFuNlBiWWt1VHkzTGFZeTdaMlR0ZUpPeTJWR0YzRTlYVlZ0akxzbkJPekhrOWlQWFozV3ExdkxPeUt5ekcxUzRUeFlhaXA5dDl5UjRBOWt3MzdQekhTWWhoS1RQVFZMS2ZlcEZjTmhBZGxzMG8yTDJKWnZyRTZqeHhJbVgrY3lCUmZ6TDMweWhoN0lKb01ITi9US2FiWGNkSEx2bi91eHVnRUVzRDdReVA0NGxkR29lMEZsUWtVT3lpaXB4aXBhbGxsR3QwNUUrQUFPTnFPNDh0Q3RBTlRueW5US3lhZ29RMVFjL1BFV3d0NDJxdGpIdXRaSnoxUXRxMzZ1akQ0eHJMemNFbmVGRldXeWR3NGNjTWhxR1VNZUpKU29kWklYdU10amhnRUlWZVRIajdTR2FkdUw2NDgxVnlKSFBDMnFtV0RSWXFNa1lnVmk3VkYydm51Wjl4eG5mZVpwUG9xSktIbjZHMzVLZlhlUDRjM2xuYWxZek85WjBvWWlyaUJjYnJMUjNYYVB4OHdIczNCaEQ0K1N3V0tQcjVoZ1EvWHgwa1JWelI4eDA0eHJiQU83SDY4azZ3NnpGak1SUmxxNlZvTTl2b3pBK3BabzhYKzczdkVZMG80TzhuNXduNllwaXU4ZFFRZzF3UDFCQmlKZU04SmYwUkFhRHVPKzRjTENmZ1RqS1E2UG9QZmQ0a1cxdmhtS2lkc2JDR3JmQWdtNnJ0REN6TE1kdkNYdVdhMy9hNVpDbXhPQmNURi8wOWRhWm9aN3c5R1hHOHlHR3NDZTZ6ZUY0WTNQZW5jRHJRTnhjcmRqQytNQUdBa3RnWStobTVFVE05bDVRMU1lN2VtaE9XQVEyTU1XQUNWbTJmRXBmT2NJN2QxNmlJRTdGZkhjdXJRVjdGUWJ6SFp0bGF5QXYvUkM1R1Z3bVFhM05td09aemM1WlpLaFU0MDk1VVQ3YzNyWlB0Vytma1ZHdDg0bHpSWDlhOGlmNGFtYVF6RzhveTRvVTFyVm9UMmxRL1hoNGN2VzkwV0hPclczVE02OTE5WlIyaUtKbytvL0JsS04rL0tOQVg2OXFtdnI5MXh2ZFhEVTNqdlhSZGl1OC9CYVZ1V1F3bTEvdTNLNXlXazB2NklDZVo5SUF3NG12UzFOMmw0azduM0phU0g5aHVoaUtzQVdNdmNJbGt4RFVUTmFiMDRPN3l0Q0NXWHRQWkVjc2FQRVg3UXJNeHZNZjdTSE5DWXFtZGlnMm5JZkRvYXhSS3VVdEx2ekIzS2FOR1FhdXV2VDBrUm8vbTNVdmN4RzhaZDJmMmlPY1kwY210NVdhQjlRVUdEOEMyVWpZTUNOaG1DU3BMeXV2N2piaFdYVTNLdVZiRjRJMXJ0VnpMUXJBK3VOWituVUJLT05ZZ1hKSVQ3SXVxeFExRGZqaHpNVU9xQ2YvWmJIYURUejE4VktNRUg2VUtINzByK0F4U0Q4NGxHdkpVZWFNeU9BQzRNcmlwTWxQTWMxbi9Qci9sRUpSaWRGRU8yeWpib0twODlnQ2N5VGFvcG5hcWZldnNnZForYlVCaVlsZzVJMFZDS2I0bVdkV2Z4QTJZL2grbUlwN2pUZFhBOXpqelEwNzlDRlBWQnFldGxaazlONXNvNjJ1WDJwb1ltUjZGcEt2SzZMWUd3U3AveDFrcGRsVlB0Vzl2RU9TVyswdGZPenhuSXNheElpd1N1UTRrN21LMU5KS3k5cVlMd2orWDd1bXE5S3hyMVdQbzRGVDcxcXFIUlZ4amtsS2RLMmNua1U2akwzNWFWYlBuMHF5bVQyZnlQRk8wMCs0dU9SRU5wVnB5SlNjeklwTDJJVE1qYkR6eVY4eDZxVEkvdmJUMXRZS1diaFlwYW1xdTYycTBoWm1mMFN4UzhCclBFTzBEWUFvU1B6THFxM1c1ZWRQMnhadFhmcm9zSjcvYXhJWUs4cTBET2xQNkxkMTZKZXBBeVhFQWdzK1h1MHEzNnFNcG1SNEtQWUxOTndZc1J0YXJ1Mi9jMEhNVmVreXpSL1NNclpJWSs3eUErK0lBMjYxbUg1Z09CMGpSYmgxRDJyT1QrM1Y4MkUyMEpmaDQyN1BqV3RpYXBlaTYxejA3OUpGczJsSEFyYW9hUEc0TnE5RUdjTVBoVmxUalArUW1jZFZ5VUFGdVI3ZVhsVTlxanBmWnhvbnZyTXF0ak9wZWQ3b3l4cFlnZXk4UnBDSElTM1h4ZWM3RmpLem1wVzVPOEVuY1dhVnZqUG9NSVEyNWladi9FZXdFaVpzdVByeS9tSkczekUxTDJQVVplN0tGZ3h1M0x1VldhUSsyRHFzYThXbStkWFc2MUpmdkRLN2Yvd2M9Jmx0Oy9kaWFncmFtJmd0OyZsdDsvbXhmaWxlJmd0OyI+PGRlZnM+PC9kZWZzPjxnPjxwYXRoIGQ9Ik0gMjM1IDIxMCBMIDIxNSAyMTAgTCAyMDMuODkgMjA5Ljg5IiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PHBhdGggZD0iTSAxOTguNjQgMjA5LjgzIEwgMjA1LjY3IDIwNi40IEwgMjAzLjg5IDIwOS44OSBMIDIwNS42IDIxMy40IFoiIGZpbGw9InJnYigwLCAwLCAwKSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9wYXRoPjxyZWN0IHg9IjIzNSIgeT0iMTgwIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjMTcyMDI2IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcmVjdD48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWdub2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZGZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGZsZXgtc3RhcnQ7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGZsZXgtc3RhcnQ7IHdpZHRoOiAxMTVweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxODdweDsgbWFyZ2luLWxlZnQ6IDI0MHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGxlZnQ7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiAjRkZGRkZGOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogVGltZXMgTmV3IFJvbWFuOyBjb2xvcjogcmdiKDI1NSwgMjU1LCAyNTUpOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyBvdmVyZmxvdy13cmFwOiBub3JtYWw7Ij5CbG9jayAjMTAwPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWdub2JqZWN0Pjx0ZXh0IHg9IjI0MCIgeT0iMjAzIiBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiPkJsb2NrICMxMDA8L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gMzk1IDE1MCBMIDM3NSAxNTAgTCAzNzUgMjEwIEwgMzYxLjM3IDIxMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gMzU2LjEyIDIxMCBMIDM2My4xMiAyMDYuNSBMIDM2MS4zNyAyMTAgTCAzNjMuMTIgMjEzLjUgWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHJlY3QgeD0iMzk1IiB5PSIxMjAiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiMxNzIwMjYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9yZWN0PjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25vYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkZmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgZmxleC1zdGFydDsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgZmxleC1zdGFydDsgd2lkdGg6IDExNXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyN3B4OyBtYXJnaW4tbGVmdDogNDAwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDBweDsgdGV4dC1hbGlnbjogbGVmdDsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6ICNGRkZGRkY7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMjU1LCAyNTUsIDI1NSk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IG92ZXJmbG93LXdyYXA6IG5vcm1hbDsiPkJsb2NrICMxMDEmIzM5O0E8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iNDAwIiB5PSIxNDMiIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJUaW1lcyBOZXcgUm9tYW4iIGZvbnQtc2l6ZT0iMTZweCI+QmxvY2sgIzEwMSYjMzk7QTwvdGV4dD48L3N3aXRjaD48L2c+PHBhdGggZD0iTSAzOTUgMjcwIEwgMzc1IDI3MCBMIDM3NSAyMTAgTCAzNjEuMzcgMjEwIiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PHBhdGggZD0iTSAzNTYuMTIgMjEwIEwgMzYzLjEyIDIwNi41IEwgMzYxLjM3IDIxMCBMIDM2My4xMiAyMTMuNSBaIiBmaWxsPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcGF0aD48cmVjdCB4PSIzOTUiIHk9IjI0MCIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iIzE3MjAyNiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBmbGV4LXN0YXJ0OyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBmbGV4LXN0YXJ0OyB3aWR0aDogMTE1cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjQ3cHg7IG1hcmdpbi1sZWZ0OiA0MDBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMHB4OyB0ZXh0LWFsaWduOiBsZWZ0OyIgZGF0YS1kcmF3aW8tY29sb3JzPSJjb2xvcjogI0ZGRkZGRjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IFRpbWVzIE5ldyBSb21hbjsgY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgb3ZlcmZsb3ctd3JhcDogbm9ybWFsOyI+QmxvY2sgIzEwMSYjMzk7QjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbm9iamVjdD48dGV4dCB4PSI0MDAiIHk9IjI2MyIgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IlRpbWVzIE5ldyBSb21hbiIgZm9udC1zaXplPSIxNnB4Ij5CbG9jayAjMTAxJiMzOTtCPC90ZXh0Pjwvc3dpdGNoPjwvZz48cGF0aCBkPSJNIDQxOC43NSA5MCBMIDQxOC44MyAxMjAuNDIgTCA0MTUuODMgMTIwLjQyIiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIxIDEiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDU1MCA3MCBMIDY5MCA3MCBMIDY5MCAxMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2RjY2JkNyIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgNiIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gNTUwIDcwIEwgODA1LjMzIDcwIEwgODA1LjI3IDEzNy40MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjZGNjYmQ3IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iNiA2IiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA4MHB4OyBtYXJnaW4tbGVmdDogNzIwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDBweDsgdGV4dC1hbGlnbjogY2VudGVyOyIgZGF0YS1kcmF3aW8tY29sb3JzPSJjb2xvcjogcmdiKDAsIDAsIDApOyBiYWNrZ3JvdW5kLWNvbG9yOiByZ2IoMjU1LCAyNTUsIDI1NSk7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsgd2hpdGUtc3BhY2U6IG5vd3JhcDsiPjxiIHN0eWxlPSJmb250LXNpemU6IDE2cHg7Ij5JZ25vcmVkPC9iPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbm9iamVjdD48dGV4dCB4PSI3MjAiIHk9Ijg1IiBmaWxsPSJyZ2IoMCwgMCwgMCkiIGZvbnQtZmFtaWx5PSJUaW1lcyBOZXcgUm9tYW4iIGZvbnQtc2l6ZT0iMTZweCIgdGV4dC1hbmNob3I9Im1pZGRsZSI+SWdub3JlZDwvdGV4dD48L3N3aXRjaD48L2c+PHJlY3QgeD0iMzc1IiB5PSI1MCIgd2lkdGg9IjE3NSIgaGVpZ2h0PSI0MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PHBhdGggZD0iTSAzNzQuOTEgNTAuMSBDIDM3NC45MSA1MC4xIDM3NC45MSA1MC4xIDM3NC45MSA1MC4xIE0gMzc0LjkxIDUwLjEgQyAzNzQuOTEgNTAuMSAzNzQuOTEgNTAuMSAzNzQuOTEgNTAuMSBNIDM3NS4zMSA1NS43NCBDIDM3Ni4zNCA1My45NyAzNzcuOTIgNTMuNDQgMzgwLjU2IDQ5LjcxIE0gMzc1LjMxIDU1Ljc0IEMgMzc2LjcxIDU0LjU0IDM3Ny4xNiA1My4xNyAzODAuNTYgNDkuNzEgTSAzNzUuMDUgNjIuMTQgQyAzNzguNjYgNTkuMDMgMzgyLjkxIDUzLjkzIDM4NS41NCA1MC4wNyBNIDM3NS4wNSA2Mi4xNCBDIDM3OC45IDU3LjgzIDM4MS4yMyA1NC44OSAzODUuNTQgNTAuMDcgTSAzNzQuNzggNjguNTQgQyAzNzguNzYgNjEuODcgMzgzLjg4IDU2LjI4IDM5MS4xOSA0OS42NyBNIDM3NC43OCA2OC41NCBDIDM3OS4xNSA2Mi4xMSAzODUuMzIgNTcuMTQgMzkxLjE5IDQ5LjY3IE0gMzc1LjE4IDc0LjE4IEMgMzgyLjA1IDY3Ljk3IDM4NC44OSA2Mi45NyAzOTYuMTcgNTAuMDMgTSAzNzUuMTggNzQuMTggQyAzODAuNjIgNjcuNTYgMzg0LjU3IDYzLjMxIDM5Ni4xNyA1MC4wMyBNIDM3NC45MiA4MC41OCBDIDM4MS40OSA3My4wNyAzOTIuNjkgNjEuOTggNDAxLjgyIDQ5LjY0IE0gMzc0LjkyIDgwLjU4IEMgMzgxLjQgNzQuMTQgMzg2Ljc0IDY2LjQ4IDQwMS44MiA0OS42NCBNIDM3NS4zMSA4Ni4yMiBDIDM4OS4xNSA3MC4yIDM5OC43MiA1OC43OCA0MDYuOCA1MCBNIDM3NS4zMSA4Ni4yMiBDIDM4My40OCA3Ni4zNyAzOTIuNCA2NS40OSA0MDYuOCA1MCBNIDM3Ni4zNiA5MS4xMSBDIDM5MC4wNyA3Ny45NCA0MDIuNTUgNjMuMDEgNDExLjc5IDUwLjM2IE0gMzc2LjM2IDkxLjExIEMgMzg3LjQgNzkuMTMgMzk5LjQ5IDY2LjYgNDExLjc5IDUwLjM2IE0gMzgxLjM1IDkxLjQ3IEMgMzk3LjQgNzQuMzEgNDEwLjM1IDYwLjQxIDQxNy40MyA0OS45NiBNIDM4MS4zNSA5MS40NyBDIDM5NC40NCA3NS43NSA0MDcuNDIgNjIuOTEgNDE3LjQzIDQ5Ljk2IE0gMzg2Ljk5IDkxLjA4IEMgNDAwLjgxIDc1LjQgNDE1LjYgNTguNDggNDIyLjQyIDUwLjMyIE0gMzg2Ljk5IDkxLjA4IEMgMzk3LjQ5IDc5LjAzIDQwNi4zNCA2Ny45OCA0MjIuNDIgNTAuMzIgTSAzOTEuOTggOTEuNDQgQyA0MDEuMTIgODQuNTMgNDA5LjI0IDc0LjU4IDQyOC4wNiA0OS45MyBNIDM5MS45OCA5MS40NCBDIDM5OC42NCA4Mi42OSA0MDcuMSA3NC45NSA0MjguMDYgNDkuOTMgTSAzOTcuNjIgOTEuMDQgQyA0MTIuMjYgNzMuMDIgNDI0LjU2IDU4LjcyIDQzMy4wNSA1MC4yOSBNIDM5Ny42MiA5MS4wNCBDIDQwNC42MSA4MS45IDQxMS41MiA3NC4wMSA0MzMuMDUgNTAuMjkgTSA0MDIuNjEgOTEuNCBDIDQxNi45NCA3My40MyA0MzEuMDkgNTYuOSA0MzguNjkgNDkuODkgTSA0MDIuNjEgOTEuNCBDIDQxMy40OSA3Ny42NyA0MjUuMSA2NC4zNiA0MzguNjkgNDkuODkgTSA0MDguMjUgOTEuMDEgQyA0MTguNjggNzcuMzYgNDMxLjc1IDYzLjU5IDQ0My42OCA1MC4yNSBNIDQwOC4yNSA5MS4wMSBDIDQxOC4zOCA4MS4xMSA0MjYuODIgNzAuMzIgNDQzLjY4IDUwLjI1IE0gNDEzLjI0IDkxLjM3IEMgNDIyLjkzIDgxLjE5IDQzNC4wOSA2OC4yMSA0NDkuMzIgNDkuODYgTSA0MTMuMjQgOTEuMzcgQyA0MjMuMTcgODEuNzUgNDMxLjQ4IDcyLjI1IDQ0OS4zMiA0OS44NiBNIDQxOC44OCA5MC45NyBDIDQyNy43NyA4MC4yNyA0MzYuODQgNjkuOTMgNDU0LjMxIDUwLjIyIE0gNDE4Ljg4IDkwLjk3IEMgNDI3LjUzIDgwLjcgNDM2LjE4IDcwLjM3IDQ1NC4zMSA1MC4yMiBNIDQyMy44NyA5MS4zMyBDIDQzNS43MyA3Ny43MyA0NDguODkgNjMuMDUgNDU5Ljk1IDQ5LjgyIE0gNDIzLjg3IDkxLjMzIEMgNDMyLjU2IDgxLjUxIDQ0MS4yNiA3MC44OCA0NTkuOTUgNDkuODIgTSA0MjkuNTEgOTAuOTQgQyA0NDAuMzEgNzkuNzkgNDQ1LjAyIDcyLjQzIDQ2NC45NCA1MC4xOCBNIDQyOS41MSA5MC45NCBDIDQ0Mi44NyA3NC4yIDQ1Ni41NiA1OS41MiA0NjQuOTQgNTAuMTggTSA0MzQuNSA5MS4zIEMgNDQ0LjQzIDc3LjcgNDU1Ljg5IDY3LjUgNDcwLjU4IDQ5Ljc5IE0gNDM0LjUgOTEuMyBDIDQ0NC4xNSA3OS42MSA0NTMuNjkgNjkuOTggNDcwLjU4IDQ5Ljc5IE0gNDQwLjE0IDkwLjkgQyA0NTQuNDYgNzUuOTYgNDY2LjcyIDU5LjQxIDQ3NS41NyA1MC4xNSBNIDQ0MC4xNCA5MC45IEMgNDUyLjg4IDc1Ljk4IDQ2NC41MyA2My4yNSA0NzUuNTcgNTAuMTUgTSA0NDUuMTMgOTEuMjYgQyA0NTEuNjkgODIuMjkgNDYyLjA3IDcxLjQgNDgxLjIxIDQ5Ljc2IE0gNDQ1LjEzIDkxLjI2IEMgNDU3Ljg0IDc3LjgxIDQ3MC4wNSA2Mi45OSA0ODEuMjEgNDkuNzYgTSA0NTAuNzcgOTAuODcgQyA0NjQuOTEgNzUuNzMgNDc5LjE4IDYyLjExIDQ4Ni4yIDUwLjEyIE0gNDUwLjc3IDkwLjg3IEMgNDYxLjIxIDc5Ljc2IDQ3MC44IDY4LjgyIDQ4Ni4yIDUwLjEyIE0gNDU1Ljc2IDkxLjIzIEMgNDY0Ljc4IDgyLjAzIDQ2OS4yMSA3NS41OSA0OTEuODQgNDkuNzIgTSA0NTUuNzYgOTEuMjMgQyA0NjkuODcgNzQuMjYgNDgzLjc2IDU4Ljc1IDQ5MS44NCA0OS43MiBNIDQ2MS40IDkwLjgzIEMgNDcxLjU5IDgyLjA3IDQ3NS44OSA3MS4yNiA0OTYuODMgNTAuMDggTSA0NjEuNCA5MC44MyBDIDQ3MS42OCA3OS4wNyA0ODMuNDkgNjYuMTUgNDk2LjgzIDUwLjA4IE0gNDY2LjM5IDkxLjIgQyA0NzYuNDUgODEuOSA0ODMuMTUgNzMuMDkgNTAyLjQ3IDQ5LjY5IE0gNDY2LjM5IDkxLjIgQyA0NzQuODMgODAuNjUgNDg0LjAxIDcwLjU4IDUwMi40NyA0OS42OSBNIDQ3Mi4wMyA5MC44IEMgNDgwLjkyIDc3LjY1IDQ5NS4zNiA2NC43IDUwNy40NiA1MC4wNSBNIDQ3Mi4wMyA5MC44IEMgNDgxLjgxIDc5LjQgNDkyLjk0IDY2LjEzIDUwNy40NiA1MC4wNSBNIDQ3Ny4wMiA5MS4xNiBDIDQ5MS4yNSA3Ny42NyA1MDMuNyA2MS4zOSA1MTMuMSA0OS42NSBNIDQ3Ny4wMiA5MS4xNiBDIDQ4NC40NCA4MS45OCA0OTIuNTcgNzUuMjIgNTEzLjEgNDkuNjUgTSA0ODIuMDEgOTEuNTIgQyA0OTEuOSA3OS42NCA1MDAuNDcgNzAuNzcgNTE4LjA5IDUwLjAxIE0gNDgyLjAxIDkxLjUyIEMgNDg5LjM5IDgxLjg4IDQ5OC4yOSA3My44MiA1MTguMDkgNTAuMDEgTSA0ODcuNjUgOTEuMTMgQyA0OTUuOTMgODMuNTcgNTAwLjkxIDc0Ljk4IDUyMy4wOCA1MC4zNyBNIDQ4Ny42NSA5MS4xMyBDIDQ5Ny4yMyA3OC43OSA1MDguMDMgNjYuNDEgNTIzLjA4IDUwLjM3IE0gNDkyLjY0IDkxLjQ5IEMgNTAzLjI4IDc2LjQ0IDUxNS4wMyA2NC44OCA1MjguNzIgNDkuOTggTSA0OTIuNjQgOTEuNDkgQyA1MDAuMzkgODIuNzEgNTA5LjE3IDcyLjU2IDUyOC43MiA0OS45OCBNIDQ5OC4yOCA5MS4wOSBDIDUxMC4xNSA3NS40OCA1MjQuMjUgNjEuNzYgNTMzLjcxIDUwLjM0IE0gNDk4LjI4IDkxLjA5IEMgNTA0LjQ2IDgzLjM2IDUxMi45NCA3NC4yMSA1MzMuNzEgNTAuMzQgTSA1MDMuMjcgOTEuNDUgQyA1MTEuNjQgODAuODggNTIzLjY3IDcwLjUyIDUzOS4zNSA0OS45NCBNIDUwMy4yNyA5MS40NSBDIDUxNy45MyA3NC4zNyA1MzIuMSA1OC4xOSA1MzkuMzUgNDkuOTQgTSA1MDguOTEgOTEuMDYgQyA1MjIuOTUgNzUuOTIgNTM1LjAzIDU5LjcyIDU0NC4zNCA1MC4zIE0gNTA4LjkxIDkxLjA2IEMgNTIxLjExIDc3LjM0IDUzMC45OSA2NC43NCA1NDQuMzQgNTAuMyBNIDUxMy45IDkxLjQyIEMgNTI2LjE3IDgwLjM3IDUzNy40NCA2NC44NSA1NDkuOTggNDkuOTEgTSA1MTMuOSA5MS40MiBDIDUyNi42NiA3Ny4xNyA1NDAuMTUgNjIuMTUgNTQ5Ljk4IDQ5LjkxIE0gNTE5LjU0IDkxLjAyIEMgNTI2LjYzIDgyLjg3IDUzMy45IDc1Ljg4IDU1MyA1Mi41MyBNIDUxOS41NCA5MS4wMiBDIDUzMC4xMiA3Ny42NiA1NDEuOTkgNjUuMzYgNTUzIDUyLjUzIE0gNTI0LjUzIDkxLjM4IEMgNTMyLjkgODMuNzQgNTQwLjM5IDczLjQ1IDU1Mi43NCA1OC45MyBNIDUyNC41MyA5MS4zOCBDIDUzMS41OCA4MS41MyA1MzkuNDcgNzQuNCA1NTIuNzQgNTguOTMgTSA1MzAuMTcgOTAuOTkgQyA1MzUuNjIgODQuOTIgNTM5LjQyIDc4LjQ5IDU1My4xMyA2NC41NyBNIDUzMC4xNyA5MC45OSBDIDUzNC4wNiA4NS4wOCA1MzguOTkgNzkuODUgNTUzLjEzIDY0LjU3IE0gNTM1LjE2IDkxLjM1IEMgNTQzLjExIDg1LjczIDU0Ni45OSA3Ni4xNSA1NTIuODcgNzAuOTcgTSA1MzUuMTYgOTEuMzUgQyA1MzguMzcgODUuNTggNTQ0LjU5IDgwLjgxIDU1Mi44NyA3MC45NyBNIDU0MC44IDkwLjk1IEMgNTQ0Ljg5IDg0LjQ3IDU0Ny42OSA4Mi4zNiA1NTMuMjcgNzYuNjEgTSA1NDAuOCA5MC45NSBDIDU0My4yOCA4OC4xOSA1NDYuNTcgODQuNDUgNTUzLjI3IDc2LjYxIE0gNTQ1Ljc5IDkxLjMxIEMgNTQ5LjU1IDg4LjgxIDU1MC4zIDg2LjEyIDU1My4wMSA4My4wMSBNIDU0NS43OSA5MS4zMSBDIDU0OC4xIDg3Ljk2IDU1MC4xOSA4NS42OCA1NTMuMDEgODMuMDEiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2RjY2JkNyIgc3Ryb2tlLXdpZHRoPSIwLjUiIHN0cm9rZS1saW5lam9pbj0icm91bmQiIHN0cm9rZS1saW5lY2FwPSJyb3VuZCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHBhdGggZD0iTSAzNzUgNTAgQyA0MjYuMDQgNTIuNDIgNDc2LjUyIDUwLjkxIDU1MCA1MCBNIDM3NSA1MCBDIDQyNC42OCA1Mi4zMiA0NzUuOTUgNTEuNTkgNTUwIDUwIE0gNTUwIDUwIEMgNTUwLjgxIDY1LjY0IDU0OC43MyA3Ni43OSA1NTAgOTAgTSA1NTAgNTAgQyA1NDkuOTUgNTguNTEgNTUxLjAzIDY2LjE2IDU1MCA5MCBNIDU1MCA5MCBDIDUxMC4xNSA4OC44MiA0NzUuMDcgOTAuMTEgMzc1IDkwIE0gNTUwIDkwIEMgNDgxLjg3IDkwLjM2IDQxNC4xOSA5MC4yNiAzNzUgOTAgTSAzNzUgOTAgQyAzNzMuODggNzkuMjIgMzczLjkgNjguOCAzNzUgNTAgTSAzNzUgOTAgQyAzNzUuMjUgNzguNTEgMzc1LjE0IDY3LjA3IDM3NSA1MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjZGNjYmQ3IiBzdHJva2UtbGluZWpvaW49InJvdW5kIiBzdHJva2UtbGluZWNhcD0icm91bmQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9wYXRoPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25vYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkZmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBmbGV4LXN0YXJ0OyB3aWR0aDogMTcwcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNzBweDsgbWFyZ2luLWxlZnQ6IDM4MHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGxlZnQ7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiAjMTcyMDI2OyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogVGltZXMgTmV3IFJvbWFuOyBjb2xvcjogcmdiKDIzLCAzMiwgMzgpOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyBvdmVyZmxvdy13cmFwOiBub3JtYWw7Ij48aSBzdHlsZT0iZm9udC1zaXplOiAxNnB4OyI+PGZvbnQgc3R5bGU9ImZvbnQtc2l6ZTogMTZweDsiPihTY2hlZHVsZWQgQ2hhbmdlKTxiciBzdHlsZT0iZm9udC1zaXplOiAxNnB4OyIgLz48L2ZvbnQ+PC9pPkF1dGhvcml0eSBTZXQgI0EsIDxpIHN0eWxlPSJmb250LXNpemU6IDE2cHg7Ij48YiBzdHlsZT0iZm9udC1zaXplOiAxNnB4OyI+ZGVsYXkgNTwvYj48L2k+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWdub2JqZWN0Pjx0ZXh0IHg9IjM4MCIgeT0iNzUiIGZpbGw9IiMxNzIwMjYiIGZvbnQtZmFtaWx5PSJUaW1lcyBOZXcgUm9tYW4iIGZvbnQtc2l6ZT0iMTZweCI+KFNjaGVkdWxlZCBDaGFuZ2UpLi4uPC90ZXh0Pjwvc3dpdGNoPjwvZz48cGF0aCBkPSJNIDU1MCAzNjAgTCA2OTAgMzYwIEwgNjkwIDMwNi4zNyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PHBhdGggZD0iTSA2OTAgMzAxLjEyIEwgNjkzLjUgMzA4LjEyIEwgNjkwIDMwNi4zNyBMIDY4Ni41IDMwOC4xMiBaIiBmaWxsPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcGF0aD48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWdub2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZGZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM1MHB4OyBtYXJnaW4tbGVmdDogNzIwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDBweDsgdGV4dC1hbGlnbjogY2VudGVyOyIgZGF0YS1kcmF3aW8tY29sb3JzPSJjb2xvcjogcmdiKDAsIDAsIDApOyBiYWNrZ3JvdW5kLWNvbG9yOiByZ2IoMjU1LCAyNTUsIDI1NSk7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsgd2hpdGUtc3BhY2U6IG5vd3JhcDsiPkFwcGxpZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iNzIwIiB5PSIzNTUiIGZpbGw9InJnYigwLCAwLCAwKSIgZm9udC1mYW1pbHk9IlRpbWVzIE5ldyBSb21hbiIgZm9udC1zaXplPSIxNnB4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIj5BcHBsaWVkPC90ZXh0Pjwvc3dpdGNoPjwvZz48cGF0aCBkPSJNIDQxOC43NSAzMzAgTCA0MTUuNDIgMzMwIEwgNDE1LjQgMzAxLjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjEgMSIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gNTUwIDM2MCBMIDgwNi42NyAzNjAgTCA4MDYuNjUgMjg3LjIzIiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDgwNi42NSAyODEuOTggTCA4MTAuMTUgMjg4Ljk4IEwgODA2LjY1IDI4Ny4yMyBMIDgwMy4xNSAyODguOTggWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHBhdGggZD0iTSA1NTAgMzYwIEwgNjEwIDM2MCBMIDYxMCAyMTAgTCA2OTAgMjEwIEwgNjkwIDE4OC4yNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjZTYwMDdhIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iNiA2IiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PHBhdGggZD0iTSA2OTAgMTgyLjI0IEwgNjk0IDE5MC4yNCBMIDY5MCAxODguMjQgTCA2ODYgMTkwLjI0IFoiIGZpbGw9IiNlNjAwN2EiIHN0cm9rZT0iI2U2MDA3YSIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcGF0aD48cGF0aCBkPSJNIDU1MCAzNjAgTCA2MTAgMzYwIEwgNjEwIDIxMCBMIDgwNi42NyAyMTAgTCA4MDYuNjUgMTY5LjgiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2U2MDA3YSIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgNiIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gODA2LjY1IDE2My44IEwgODEwLjY1IDE3MS43OSBMIDgwNi42NSAxNjkuOCBMIDgwMi42NSAxNzEuOCBaIiBmaWxsPSIjZTYwMDdhIiBzdHJva2U9IiNlNjAwN2EiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMDBweDsgbWFyZ2luLWxlZnQ6IDYwOHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGNlbnRlcjsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6IHJnYigwLCAwLCAwKTsgYmFja2dyb3VuZC1jb2xvcjogcmdiKDI1NSwgMjU1LCAyNTUpOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogVGltZXMgTmV3IFJvbWFuOyBjb2xvcjogcmdiKDAsIDAsIDApOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiByZ2IoMjU1LCAyNTUsIDI1NSk7IHdoaXRlLXNwYWNlOiBub3dyYXA7Ij5BcHBsaWVkIGNyb3NzLWZvcms8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iNjA4IiB5PSIyMDUiIGZpbGw9InJnYigwLCAwLCAwKSIgZm9udC1mYW1pbHk9IlRpbWVzIE5ldyBSb21hbiIgZm9udC1zaXplPSIxNnB4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIj5BcHBsaWVkIGNyb3NzLWZvcms8L3RleHQ+PC9zd2l0Y2g+PC9nPjxyZWN0IHg9IjM3NSIgeT0iMzMwIiB3aWR0aD0iMTc1IiBoZWlnaHQ9IjYwIiBmaWxsPSIjZTYwMDdhIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcmVjdD48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWdub2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZGZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgZmxleC1zdGFydDsgd2lkdGg6IDE3MHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM2MHB4OyBtYXJnaW4tbGVmdDogMzgwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDBweDsgdGV4dC1hbGlnbjogbGVmdDsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6ICNGRkZGRkY7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMjU1LCAyNTUsIDI1NSk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IG92ZXJmbG93LXdyYXA6IG5vcm1hbDsiPjxpIHN0eWxlPSJmb250LXNpemU6IDE2cHg7Ij4oPGIgc3R5bGU9ImZvbnQtc2l6ZTogMTZweDsiPkZvcmNlZDwvYj4gQ2hhbmdlKTxiciBzdHlsZT0iZm9udC1zaXplOiAxNnB4OyIgLz48L2k+QXV0aG9yaXR5IFNldCAjQjxiciBzdHlsZT0iZm9udC1zaXplOiAxNnB4OyIgLz48YiBzdHlsZT0iZm9udC1zaXplOiAxNnB4OyI+c3RhcnRpbmcgYXQ8L2I+IDxpIHN0eWxlPSJmb250LXNpemU6IDE2cHg7Ij48YiBzdHlsZT0iZm9udC1zaXplOiAxNnB4OyI+bTwvYj48L2k+LMKgPGkgc3R5bGU9ImZvbnQtc2l6ZTogMTZweDsiPjxiIHN0eWxlPSJmb250LXNpemU6IDE2cHg7Ij5kZWxheSA1PC9iPjwvaT48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iMzgwIiB5PSIzNjUiIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJUaW1lcyBOZXcgUm9tYW4iIGZvbnQtc2l6ZT0iMTZweCI+KEZvcmNlZCBDaGFuZ2UpLi4uPC90ZXh0Pjwvc3dpdGNoPjwvZz48cmVjdCB4PSIzMjUiIHk9IjEzMCIgd2lkdGg9IjcwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcmVjdD48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWdub2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZGZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE0MHB4OyBtYXJnaW4tbGVmdDogMzYwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDBweDsgdGV4dC1hbGlnbjogY2VudGVyOyIgZGF0YS1kcmF3aW8tY29sb3JzPSJjb2xvcjogcmdiKDAsIDAsIDApOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogVGltZXMgTmV3IFJvbWFuOyBjb2xvcjogcmdiKDAsIDAsIDApOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyI+Rm9yayAjQTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbm9iamVjdD48dGV4dCB4PSIzNjAiIHk9IjE0NSIgZmlsbD0icmdiKDAsIDAsIDApIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPkZvcmsgI0E8L3RleHQ+PC9zd2l0Y2g+PC9nPjxyZWN0IHg9IjMyNSIgeT0iMjcwIiB3aWR0aD0iNzAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9yZWN0PjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25vYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkZmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjgwcHg7IG1hcmdpbi1sZWZ0OiAzNjBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMHB4OyB0ZXh0LWFsaWduOiBjZW50ZXI7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiByZ2IoMCwgMCwgMCk7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7Ij5Gb3JrICNCPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWdub2JqZWN0Pjx0ZXh0IHg9IjM2MCIgeT0iMjg1IiBmaWxsPSJyZ2IoMCwgMCwgMCkiIGZvbnQtZmFtaWx5PSJUaW1lcyBOZXcgUm9tYW4iIGZvbnQtc2l6ZT0iMTZweCIgdGV4dC1hbmNob3I9Im1pZGRsZSI+Rm9yayAjQjwvdGV4dD48L3N3aXRjaD48L2c+PHBhdGggZD0iTSAxNjUgMjEwIEwgOTYuMzcgMjEwIiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PHBhdGggZD0iTSA5MS4xMiAyMTAgTCA5OC4xMiAyMDYuNSBMIDk2LjM3IDIxMCBMIDk4LjEyIDIxMy41IFoiIGZpbGw9InJnYigwLCAwLCAwKSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9wYXRoPjxyZWN0IHg9IjE2NSIgeT0iMjAwIiB3aWR0aD0iMzAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9yZWN0PjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25vYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkZmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjEwcHg7IG1hcmdpbi1sZWZ0OiAxODBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMHB4OyB0ZXh0LWFsaWduOiBjZW50ZXI7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiByZ2IoMCwgMCwgMCk7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7Ij4uLi48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iMTgwIiB5PSIyMTUiIGZpbGw9InJnYigwLCAwLCAwKSIgZm9udC1mYW1pbHk9IlRpbWVzIE5ldyBSb21hbiIgZm9udC1zaXplPSIxNnB4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIj4uLi48L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gMTMwIDEyMCBMIDEzMCAxNjAgTCAxODEuNTggMTYwIEwgMTgxLjU5IDE5Mi4zOSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PHBhdGggZD0iTSAxODEuNTkgMTk3LjY0IEwgMTc4LjA5IDE5MC42NCBMIDE4MS41OSAxOTIuMzkgTCAxODUuMDkgMTkwLjY0IFoiIGZpbGw9InJnYigwLCAwLCAwKSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9wYXRoPjxwYXRoIGQ9Ik0gMjEwIDEwMCBMIDI5NSAxMDAgTCAyOTUgMTczLjYzIiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDI5NSAxNzguODggTCAyOTEuNSAxNzEuODggTCAyOTUgMTczLjYzIEwgMjk4LjUgMTcxLjg4IFoiIGZpbGw9InJnYigwLCAwLCAwKSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9wYXRoPjxwYXRoIGQ9Ik0gMjEwIDEwMCBMIDQxNS43OCAxMDAgTSA0MjEuNzggMTAwIE0gNDIxLjc4IDEwMCBMIDU3MCAxMDAgTCA1NzAgMTMzLjYzIiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDU3MCAxMzguODggTCA1NjYuNSAxMzEuODggTCA1NzAgMTMzLjYzIEwgNTczLjUgMTMxLjg4IFoiIGZpbGw9InJnYigwLCAwLCAwKSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9wYXRoPjxwYXRoIGQ9Ik0gMTMwIDEyMCBMIDEzMCAyMDcgTSAxMzAgMjEzIE0gMTMwIDIxMyBMIDEzMCAzMjAgTCA0MTIuNDEgMzIwIE0gNDE4LjQxIDMyMCBNIDQxOC40MSAzMjAgTCA1NzEuMzMgMzIwIEwgNTcxLjMgMjg2LjA5IiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDU3MS4yOSAyODAuODQgTCA1NzQuOCAyODcuODMgTCA1NzEuMyAyODYuMDkgTCA1NjcuOCAyODcuODQgWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHBhdGggZD0iTSAyMTAgMTAwIEwgNDE1Ljc4IDEwMCBNIDQyMS43OCAxMDAgTSA0MjEuNzggMTAwIEwgNDU1IDEwMCBMIDQ1NSAxMTMuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gNDU1IDExOC44OCBMIDQ1MS41IDExMS44OCBMIDQ1NSAxMTMuNjMgTCA0NTguNSAxMTEuODggWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHBhdGggZD0iTSAxMzAgMTIwIEwgMTMwIDIwNyBNIDEzMCAyMTMgTSAxMzAgMjEzIEwgMTMwIDMyMCBMIDQxMi40MSAzMjAgTSA0MTguNDEgMzIwIE0gNDE4LjQxIDMyMCBMIDQ1NSAzMjAgTCA0NTUgMzA2LjM3IiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDQ1NSAzMDEuMTIgTCA0NTguNSAzMDguMTIgTCA0NTUgMzA2LjM3IEwgNDUxLjUgMzA4LjEyIFoiIGZpbGw9InJnYigwLCAwLCAwKSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9wYXRoPjxwYXRoIGQ9Ik0gNzYuNzIgMTIxIEwgNzYuMTcgMjAxLjM0IiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIxIDEiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cmVjdCB4PSI1MCIgeT0iODAiIHdpZHRoPSIxNjAiIGhlaWdodD0iNDAiIGZpbGw9IiNkY2NiZDciIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCI+PC9yZWN0PjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25vYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkZmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBmbGV4LXN0YXJ0OyB3aWR0aDogMTU1cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTAwcHg7IG1hcmdpbi1sZWZ0OiA1NXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGxlZnQ7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiAjMTcyMDI2OyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogVGltZXMgTmV3IFJvbWFuOyBjb2xvcjogcmdiKDIzLCAzMiwgMzgpOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyBvdmVyZmxvdy13cmFwOiBub3JtYWw7Ij48aSBzdHlsZT0iZm9udC1zaXplOiAxNnB4OyI+KFNjaGVkdWxlZCBDaGFuZ2UpPGJyIHN0eWxlPSJmb250LXNpemU6IDE2cHg7IiAvPjwvaT5BdXRob3JpdHkgU2V0ICNYPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWdub2JqZWN0Pjx0ZXh0IHg9IjU1IiB5PSIxMDUiIGZpbGw9IiMxNzIwMjYiIGZvbnQtZmFtaWx5PSJUaW1lcyBOZXcgUm9tYW4iIGZvbnQtc2l6ZT0iMTZweCI+KFNjaGVkdWxlZCBDaGFuZ2UpLi4uPC90ZXh0Pjwvc3dpdGNoPjwvZz48cGF0aCBkPSJNIDU1NSAxNTAgTCA1MjEuMzcgMTUwIiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PHBhdGggZD0iTSA1MTYuMTIgMTUwIEwgNTIzLjEyIDE0Ni41IEwgNTIxLjM3IDE1MCBMIDUyMy4xMiAxNTMuNSBaIiBmaWxsPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcGF0aD48cmVjdCB4PSI1NTUiIHk9IjE0MCIgd2lkdGg9IjMwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcmVjdD48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWdub2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZGZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE1MHB4OyBtYXJnaW4tbGVmdDogNTcwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDBweDsgdGV4dC1hbGlnbjogY2VudGVyOyIgZGF0YS1kcmF3aW8tY29sb3JzPSJjb2xvcjogcmdiKDAsIDAsIDApOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogVGltZXMgTmV3IFJvbWFuOyBjb2xvcjogcmdiKDAsIDAsIDApOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyI+Li4uPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWdub2JqZWN0Pjx0ZXh0IHg9IjU3MCIgeT0iMTU1IiBmaWxsPSJyZ2IoMCwgMCwgMCkiIGZvbnQtZmFtaWx5PSJUaW1lcyBOZXcgUm9tYW4iIGZvbnQtc2l6ZT0iMTZweCIgdGV4dC1hbmNob3I9Im1pZGRsZSI+Li4uPC90ZXh0Pjwvc3dpdGNoPjwvZz48cGF0aCBkPSJNIDU1NSAyNzAgTCA1MjEuMzcgMjcwIiBmaWxsPSJub25lIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIj48L3BhdGg+PHBhdGggZD0iTSA1MTYuMTIgMjcwIEwgNTIzLjEyIDI2Ni41IEwgNTIxLjM3IDI3MCBMIDUyMy4xMiAyNzMuNSBaIiBmaWxsPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcGF0aD48cmVjdCB4PSI1NTUiIHk9IjI2MCIgd2lkdGg9IjMwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcmVjdD48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWdub2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZGZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI3MHB4OyBtYXJnaW4tbGVmdDogNTcwcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDBweDsgdGV4dC1hbGlnbjogY2VudGVyOyIgZGF0YS1kcmF3aW8tY29sb3JzPSJjb2xvcjogcmdiKDAsIDAsIDApOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogVGltZXMgTmV3IFJvbWFuOyBjb2xvcjogcmdiKDAsIDAsIDApOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyI+Li4uPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWdub2JqZWN0Pjx0ZXh0IHg9IjU3MCIgeT0iMjc1IiBmaWxsPSJyZ2IoMCwgMCwgMCkiIGZvbnQtZmFtaWx5PSJUaW1lcyBOZXcgUm9tYW4iIGZvbnQtc2l6ZT0iMTZweCIgdGV4dC1hbmNob3I9Im1pZGRsZSI+Li4uPC90ZXh0Pjwvc3dpdGNoPjwvZz48cGF0aCBkPSJNIDYzMCAyNzAgTCA2MTMgMjcwLjIzIE0gNjA3IDI3MC4zMSBNIDYwNyAyNzAuMzEgTCA1OTMuMDggMjcwLjQiIGZpbGw9Im5vbmUiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiPjwvcGF0aD48cGF0aCBkPSJNIDU4Ny44MyAyNzAuNTUgTCA1OTQuNzMgMjY2Ljg1IEwgNTkzLjA4IDI3MC40IEwgNTk0LjkyIDI3My44NSBaIiBmaWxsPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcGF0aD48cmVjdCB4PSI2MzAiIHk9IjI0MCIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iIzE3MjAyNiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBmbGV4LXN0YXJ0OyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBmbGV4LXN0YXJ0OyB3aWR0aDogMTE1cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjQ3cHg7IG1hcmdpbi1sZWZ0OiA2MzVweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMHB4OyB0ZXh0LWFsaWduOiBsZWZ0OyIgZGF0YS1kcmF3aW8tY29sb3JzPSJjb2xvcjogI0ZGRkZGRjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IFRpbWVzIE5ldyBSb21hbjsgY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgb3ZlcmZsb3ctd3JhcDogbm9ybWFsOyI+QmxvY2sgIyhtKzUpJiMzOTtCPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWdub2JqZWN0Pjx0ZXh0IHg9IjYzNSIgeT0iMjYzIiBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiPkJsb2NrICMobSs1KSYjMzk7QjwvdGV4dD48L3N3aXRjaD48L2c+PHBhdGggZD0iTSA2MzAgMTUwIEwgNTk0Ljc5IDE0OS42MSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gNTg5LjU0IDE0OS40NSBMIDU5Ni42NCAxNDYuMTcgTCA1OTQuNzkgMTQ5LjYxIEwgNTk2LjQzIDE1My4xNyBaIiBmaWxsPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZT0icmdiKDAsIDAsIDApIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcGF0aD48cmVjdCB4PSI2MzAiIHk9IjEyMCIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iIzE3MjAyNiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBmbGV4LXN0YXJ0OyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBmbGV4LXN0YXJ0OyB3aWR0aDogMTE1cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTI3cHg7IG1hcmdpbi1sZWZ0OiA2MzVweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMHB4OyB0ZXh0LWFsaWduOiBsZWZ0OyIgZGF0YS1kcmF3aW8tY29sb3JzPSJjb2xvcjogI0ZGRkZGRjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IFRpbWVzIE5ldyBSb21hbjsgY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgb3ZlcmZsb3ctd3JhcDogbm9ybWFsOyI+QmxvY2sgIyhtKzUpJiMzOTtBPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWdub2JqZWN0Pjx0ZXh0IHg9IjYzNSIgeT0iMTQzIiBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiPkJsb2NrICMobSs1KSYjMzk7QTwvdGV4dD48L3N3aXRjaD48L2c+PHBhdGggZD0iTSA3OTAgMTUwIEwgNzU2LjM3IDE1MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gNzUxLjEyIDE1MCBMIDc1OC4xMiAxNDYuNSBMIDc1Ni4zNyAxNTAgTCA3NTguMTIgMTUzLjUgWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHJlY3QgeD0iNzkwIiB5PSIxNDAiIHdpZHRoPSIzMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNTBweDsgbWFyZ2luLWxlZnQ6IDgwNXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGNlbnRlcjsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6IHJnYigwLCAwLCAwKTsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IFRpbWVzIE5ldyBSb21hbjsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsiPi4uLjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbm9iamVjdD48dGV4dCB4PSI4MDUiIHk9IjE1NSIgZmlsbD0icmdiKDAsIDAsIDApIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPi4uLjwvdGV4dD48L3N3aXRjaD48L2c+PHBhdGggZD0iTSA3OTAgMjcwIEwgNzU2LjM3IDI3MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2IoMCwgMCwgMCkiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSI+PC9wYXRoPjxwYXRoIGQ9Ik0gNzUxLjEyIDI3MCBMIDc1OC4xMiAyNjYuNSBMIDc1Ni4zNyAyNzAgTCA3NTguMTIgMjczLjUgWiIgZmlsbD0icmdiKDAsIDAsIDApIiBzdHJva2U9InJnYigwLCAwLCAwKSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3BhdGg+PHJlY3QgeD0iNzkwIiB5PSIyNjAiIHdpZHRoPSIzMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIj48L3JlY3Q+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbm9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNzBweDsgbWFyZ2luLWxlZnQ6IDgwNXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGNlbnRlcjsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6IHJnYigwLCAwLCAwKTsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IFRpbWVzIE5ldyBSb21hbjsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsiPi4uLjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbm9iamVjdD48dGV4dCB4PSI4MDUiIHk9IjI3NSIgZmlsbD0icmdiKDAsIDAsIDApIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPi4uLjwvdGV4dD48L3N3aXRjaD48L2c+PHJlY3QgeD0iNjAiIHk9IjIwMCIgd2lkdGg9IjMwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiPjwvcmVjdD48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWdub2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZGZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIxMHB4OyBtYXJnaW4tbGVmdDogNzVweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMHB4OyB0ZXh0LWFsaWduOiBjZW50ZXI7IiBkYXRhLWRyYXdpby1jb2xvcnM9ImNvbG9yOiByZ2IoMCwgMCwgMCk7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBUaW1lcyBOZXcgUm9tYW47IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7Ij4uLi48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25vYmplY3Q+PHRleHQgeD0iNzUiIHk9IjIxNSIgZmlsbD0icmdiKDAsIDAsIDApIiBmb250LWZhbWlseT0iVGltZXMgTmV3IFJvbWFuIiBmb250LXNpemU9IjE2cHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPi4uLjwvdGV4dD48L3N3aXRjaD48L2c+PC9nPjxzd2l0Y2g+PGcgcmVxdWlyZWRmZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48L2c+PGEgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMCwtNSkiIHhsaW5rOmhyZWY9Imh0dHBzOi8vd3d3LmRpYWdyYW1zLm5ldC9kb2MvZmFxL3N2Zy1leHBvcnQtdGV4dC1wcm9ibGVtcyIgdGFyZ2V0PSJfYmxhbmsiPjx0ZXh0IHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTBweCIgeD0iNTAlIiB5PSIxMDAlIj5UZXh0IGlzIG5vdCBTVkcgLSBjYW5ub3QgZGlzcGxheTwvdGV4dD48L2E+PC9zd2l0Y2g+PC9zdmc+)

</div>

<div class="title">

Figure 3. Applying a forced change

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-block-finalization" class="anchor"></a><a href="#sect-block-finalization" class="link">6.6. Block
Finalization</a>

<div id="defn-justified-block-header" class="exampleblock">

<div class="title">

Definition 89. [Justified Block Header](#defn-justified-block-header)

</div>

<div class="content">

<div class="paragraph">

The Justified Block Header is provided by the consensus engine and
presented to the Polkadot Host, for the block to be appended to the
blockchain. It contains the following parts:

</div>

<div class="ulist">

- **block_header** the complete block header ([Definition
  10](#defn-block-header)) and denoted by \\"Head"(B)\\.

- **justification**: as defined by the consensus specification indicated
  by \\"Just"(B)\\ as defined in [Definition
  78](#defn-grandpa-justification).

- **authority Ids**: This is the list of the Ids of authorities, which
  have voted for the block to be stored and is formally referred to as
  \\A(B)\\. An authority Id is 256-bit.

</div>

</div>

</div>

<div id="defn-finalized-block" class="exampleblock">

<div class="title">

Definition 90. [Finalized](#defn-finalized-block)

</div>

<div class="content">

<div class="paragraph">

A Polkadot relay chain node \\n\\ should consider block \\B\\ as
**finalized** if any of the following criteria hold for \\B' \>= B\\:

</div>

<div class="ulist">

- \\V\_("obs"(n))^(r,"pc")(B') \> 2/3\|bbb V\_(B')\|\\.

- It receives a \\M_v^(r,"Fin")(B')\\ message in which \\J^r(B)\\
  justifies the finalization ([Definition
  78](#defn-grandpa-justification)).

- It receives a block data message for \\B'\\ with \\"Just"(B')\\
  ([Definition 89](#defn-justified-block-header)) which justifies the
  finalization.

</div>

<div class="paragraph">

for:

</div>

<div class="ulist">

- Any round \\r\\ if the node \\n\\ is *not* a GRANDPA voter.

- Only for round \\r\\ for which the node \\n\\ has invoked
  [Play-Grandpa-Round](#algo-grandpa-round) and round \\r+1\\ if \\n\\
  is a GRANDPA voter and has already caught up to its peers according to
  the process described in Section [Section
  6.6.1](#sect-grandpa-catchup).

</div>

<div class="paragraph">

Note that all Polkadot relay chain nodes are supposed to process GRANDPA
commit messages regardless of their GRANDPA voter status.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-grandpa-catchup" class="anchor"></a><a href="#sect-grandpa-catchup" class="link">6.6.1. Catching up</a>

<div class="paragraph">

When a Polkadot node (re)joins the network, it requests the history of
state transitions in the form of blocks, which it is missing.

</div>

<div class="paragraph">

Nonetheless, the process is different for a GRANDPA voter node. When a
voter node joins the network, it needs to gather the justification
([Definition 78](#defn-grandpa-justification)) of the rounds it has
missed. Through this process, they can safely join the voting process of
the current round, on which the voting is taking place.

</div>

<div class="sect4">

##### <a href="#sect-sending-catchup-request" class="anchor"></a><a href="#sect-sending-catchup-request" class="link">6.6.1.1. Sending
the catch-up requests</a>

<div class="paragraph">

When a Polkadot voter node has the same authority list as a peer voter
node who is reporting a higher number for the *finalized round* field,
it should send a catch-up request message ([Definition
48](#defn-grandpa-catchup-request-msg)) to the reporting peer. This will
allow the node to to catch up to the more advanced finalized round,
provided that the following criteria hold:

</div>

<div class="ulist">

- The peer node is a GRANDPA voter, and:

- The last known finalized round for the Polkadot node is at least 2
  rounds behind the finalized round for the peer.

</div>

</div>

<div class="sect4">

##### <a href="#id-processing-the-catch-up-requests" class="anchor"></a><a href="#id-processing-the-catch-up-requests" class="link">6.6.1.2.
Processing the catch-up requests</a>

<div class="paragraph">

Only GRANDPA voter nodes are required to respond to the catch-up
requests. Additionally, it is only GRANDPA voters who are supposed to
send catch-up requests. As such GRANDPA voters could safely ignore the
catch-up requests from non-voter nodes. When a GRANDPA voter node
receives a catch-up request message, it needs to execute
[Process-Catchup-Request](#algo-process-catchup-request). Note: a voter
node should not respond to catch-up requests for rounds that are
actively being voted on, those are the rounds for which
[Play-Grandpa-Round](#algo-grandpa-round) is not concluded.

</div>

<div class="sidebarblock">

<div class="content">

\input \$M\_{i, v}^\text{Cat-q}(\text{id}\_\mathbb{V}, r)\$ \if{\$M\_{i,
v}^\text{Cat-q}(\text{id}\_\mathbb{V}, r).\text{id}\_\mathbb{V} \neq
\text{id}\_\mathbb{V}\$} \state \textbf{error} \`\`Catching up on
different set'' \endif \if{\$i \notin \mathbb{P}\$} \state
\textbf{error} \`\`Requesting catching up from a non-peer'' \endif
\if{\$r \>\$ \textsc{Last-Completed-Round}} \state \textbf{error}
\`\`Catching up on a round in the future'' \endif \state
\call{Send}{\$i, M\_{v, i}^\text{Cat-s}(\text{id}\_\mathbb{V}, r)\$}

<div class="dlist">

where  
<div class="ulist">

- \\M\_(i,v)^("Cat"-q)("id"\_(bbb V),r)\\ is the catch-up message
  received from peer \\i\\ ([Definition
  48](#defn-grandpa-catchup-request-msg)).

- \\"id"\_(bbb V)\\ is the voter set id with which the serving node is
  operating

- \\r\\ is the round number for which the catch-up is requested for.

- \\bbb P\\ is the set of immediate peers of node \\v\\.

- \\tt "Last-Completed-Round"\\ is initiated in
  [Initiate-Grandpa](#algo-initiate-grandpa) and gets updated by
  [Play-Grandpa-Round](#algo-grandpa-round).

- \\M\_(v,i)^("Cat"-s)("id"\_(bbb V),r)\\ is the catch-up response
  ([Definition 49](#defn-grandpa-catchup-response-msg)).

</div>

</div>

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-processing-catch-up-responses" class="anchor"></a><a href="#id-processing-catch-up-responses" class="link">6.6.1.3.
Processing catch-up responses</a>

<div class="paragraph">

A Catch-up response message contains critical information for the
requester node to update their view on the active rounds which are being
voted on by GRANDPA voters. As such, the requester node should verify
the content of the catch-up response message and subsequently updates
its view of the state of the finality of the Relay chain according to
[Process-Catchup-Response](#algo-process-catchup-response).

</div>

<div class="sidebarblock">

<div class="content">

\input \$M\_{v,i}^\text{Cat-s}(\text{id}\_{\mathbb{V}}, r)\$ \state
\$M\_{v,i}^\text{Cat-s}(\text{id}\_{\mathbb{V}},
r).\text{id}\_{\mathbb{V}}, r, J^{r, pv}(B), J^{r, pc}(B), H_h(B'),
H_i(B') \leftarrow \text{Dec}\_{SC}(M\_{v,
i}^{Cat-s}(\text{id}\_{\mathbb{V}}, r)\$ \if{\$M\_{v,
i}^\text{Cat-s}(\text{id}\_{\mathbb{V}}, r).\text{id}\_{\mathbb{V}} \neq
\text{id}\_{\mathbb{V}}\$} \state \textbf{error} \`\`Catching up on
different set'' \endif \if{\$r \leqslant\$ \textsc{Leading-Round}}
\state \textbf{error} \`\`Catching up in to the past'' \endif
\if{\$J^{r, pv}(B)\$ \textbf{is not} valid} \state \textbf{error}
\`\`Invalid pre-vote justification'' \endif \if{\$J^{r, pc}(B)\$
\textbf{is not} valid} \state \textbf{error} \`\`Invalid pre-commit
justification'' \endif \state \$G \leftarrow\$
\call{GRANDPA-GHOST}{\$J^{r, pv}(B)\$} \if{\$G = \phi\$} \state
\textbf{error} \`\`GHOST-less Catch-up'' \endif \if{\$r\$ \textbf{is
not} completable} \state \textbf{error} \`\`Catch-up round is not
completable'' \endif \if{\$J^{r, pc}(B)\$ justifies \$B'\$ finalization}
\state \textbf{error} \`\`Unjustified Catch-up target finalization''
\endif \state \textsc{Last-Completed-Round} \$\leftarrow r\$ \if{\$i \in
\mathbb{V}\$} \state \call{Play-Grandpa-round}{\$r + 1\$} \endif

<div class="paragraph">

where \\M\_(v,i)^("Cat"-s)("id"\_(bbb V),r)\\ is the catch-up response
received from node \\v\\ ([Definition
49](#defn-grandpa-catchup-response-msg)).

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-grandpa-beefy" class="anchor"></a><a href="#sect-grandpa-beefy" class="link">6.7. Bridge design
(BEEFY)</a>

<div class="admonitionblock warning">

|     |                                                                                                                           |
|-----|---------------------------------------------------------------------------------------------------------------------------|
|     | The BEEFY protocol is currently in early development and subject to change. The specification has not been completed yet. |

</div>

<div class="paragraph">

The BEEFY (Bridge Effiency Enabling Finality Yielder) is a secondary
protocol to GRANDPA to support efficient bridging between the Polkadot
network (relay chain) and remote, segregated blockchains, such as
Ethereum, which were not built with the Polkadot interchain operability
in mind. The protocol allows participants of the remote network to
verify finality proofs created by the Polkadot relay chain validators.
In other words: clients in the Ethereum network should able to verify
that the Polkadot network is at a specific state.

</div>

<div class="paragraph">

Storing all the information necessary to verify the state of the remote
chain, such as the block headers, is too expensive. BEEFY stores the
information in a space-efficient way and clients can request additional
information over the protocol.

</div>

<div class="sect3">

#### <a href="#id-preliminaries-2" class="anchor"></a><a href="#id-preliminaries-2" class="link">6.7.1. Preliminaries</a>

<div id="defn-mmr" class="exampleblock">

<div class="title">

Definition 91. [Merkle Mountain Ranges](#defn-mmr)

</div>

<div class="content">

<div class="paragraph">

Merkle Mountain Ranges, **MMR**, are used as an efficient way to send
block headers and signatures to light clients.

</div>

<div class="admonitionblock note">

|     |                                 |
|-----|---------------------------------|
|     | MMRs have not been defined yet. |

</div>

</div>

</div>

<div id="defn-beefy-statement" class="exampleblock">

<div class="title">

Definition 92. [Statement](#defn-beefy-statement)

</div>

<div class="content">

<div class="paragraph">

The **statement** is the same piece of information which every relay
chain validator is voting on. Namely, the MMR root of all the block
header hashes leading up to the latest, finalized block.

</div>

</div>

</div>

<div id="defn-beefy-witness-data" class="exampleblock">

<div class="title">

Definition 93. [Witness Data](#defn-beefy-witness-data)

</div>

<div class="content">

<div class="paragraph">

**Witness data** contains the statement ([Definition
92](#defn-beefy-statement)), an array indicating which validator of the
Polkadot network voted for the statement (but not the signatures
themselves) and a MMR root of the signatures. The indicators of which
validator voted for the statement are just claims and provide no proofs.
The network message is defined in [Definition
53](#defn-grandpa-beefy-signed-commitment-witness) and the relayer saves
it on the chain of the remote network.

</div>

</div>

</div>

<div id="defn-beefy-light-client" class="exampleblock">

<div class="title">

Definition 94. [Light Client](#defn-beefy-light-client)

</div>

<div class="content">

<div class="paragraph">

A **light client** is an abstract entity in a remote network such as
Ethereum. It can be a node or a smart contract with the intent of
requesting finality proofs from the Polkadot network. A light client
reads the witness data ([Definition 93](#defn-beefy-witness-data) from
the chain, then requests the signatures directly from the relayer in
order to verify those.

</div>

<div class="paragraph">

The light client is expected to know who the validators are and has
access to their public keys.

</div>

</div>

</div>

<div id="defn-beefy-relayer" class="exampleblock">

<div class="title">

Definition 95. [Relayer](#defn-beefy-relayer)

</div>

<div class="content">

<div class="paragraph">

A **relayer** (or "prover") is an abstract entity which takes finality
proofs from the Polkadot network and makes those available to the light
clients. Inherently, the relayer tries to convince the light clients
that the finality proofs have been voted for by the Polkadot relay chain
validators. The relayer operates offchain and can for example be a node
or a collection of nodes.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-voting-on-statements" class="anchor"></a><a href="#id-voting-on-statements" class="link">6.7.2. Voting on
Statements</a>

<div class="paragraph">

The Polkadot Host signs a statement ([Definition
92](#defn-beefy-statement)) and gossips it as part of a vote
([Definition 51](#defn-msg-beefy-gossip)) to its peers on every new,
finalized block. The Polkadot Host uses ECDSA for signing the statement,
since Ethereum has better compatibility for it compared to SR25519 or
ED25519.

</div>

</div>

<div class="sect3">

#### <a href="#sect-beefy-committing-witnesses" class="anchor"></a><a href="#sect-beefy-committing-witnesses" class="link">6.7.3.
Committing Witnesses</a>

<div class="paragraph">

The relayer ([Definition 95](#defn-beefy-relayer)) participates in the
Polkadot network by collecting the gossiped votes ([Definition
51](#defn-msg-beefy-gossip)). Those votes are converted into the witness
data structure ([Definition 93](#defn-beefy-witness-data)). The relayer
saves the data on the chain of the remote network. The occurrence of
saving witnesses on remote networks is undefined.

</div>

</div>

<div class="sect3">

#### <a href="#id-requesting-signed-commitments" class="anchor"></a><a href="#id-requesting-signed-commitments" class="link">6.7.4.
Requesting Signed Commitments</a>

<div class="paragraph">

A light client ([Definition 94](#defn-beefy-light-client)) fetches the
witness data ([Definition 93](#defn-beefy-witness-data)) from the chain.
Once the light client knows which validators apparently voted for the
specified statement, it needs to request the signatures from the relayer
to verify whether the claims are actually true. This is achieved by
requesting signed commitments ([Definition
52](#defn-grandpa-beefy-signed-commitment)).

</div>

<div class="paragraph">

How those signed commitments are requested by the light client and
delivered by the relayer varies among networks or implementations. On
Ethereum, for example, the light client can request the signed
commitments in form of a transaction, which results in a response in
form of a transaction.

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#sect-lightclient" class="anchor"></a><a href="#sect-lightclient" class="link">7. Light Clients</a>

<div class="sectionbody">

<div class="sect2">

### <a href="#sect-requirements-lightclient" class="anchor"></a><a href="#sect-requirements-lightclient" class="link">7.1. Requirements
for Light Clients</a>

<div class="paragraph">

We list requirements of a Light Client categorized along the the three
dimensions of Functionality, Efficiency, and Security.

</div>

<div class="ulist">

- **Functional Requirements:**

  <div class="olist arabic">

  1.  Update state ([Section 2.4](#sect-state-storage)) to reflect the
      latest view of the blockchain via synchronization with full nodes.

  2.  (Optional) Verify validity of runtime transitions ([Section
      2.6](#sect-runtime-interaction)).

  3.  Make queries for data at the latest block height or across a range
      of blocks.

  4.  Append extrinsics ([Section 2.3](#sect-extrinsics)) to the
      blockchain via full nodes.

  </div>

- **Efficiency Requirements:**

  <div class="olist arabic">

  1.  Efficient bootstrapping and syncing: initializations and update
      functions of the state have tractable computation and
      communication complexity and grows at most linearly with the chain
      size. Generally, the complexity is proportional to the GRANDPA
      validator set change.

  2.  Querying operations happen by requesting athe key-value pair from
      a full node.

  3.  Further, verifying the validity of responses by the full node is
      logarithmic in the size of the state.

  </div>

- **Security Requirements:**

  <div class="olist arabic">

  1.  Secure bootstrapping and Synchronizing: Probability that an
      adversarial full node convincing a light client of a forged
      blockchain state is negligible.

  2.  Secure querying: Probability that an adversary convinces light
      client to accept a forged account state os negligible.

  3.  Assure that the submitted extrinsics are appended in a successor
      block or inform the user incase of failure.

  </div>

- **Polkadot Specific Requirements:**

  <div class="olist arabic">

  1.  The client MUST be able to connect to a relay chain using chain
      state.

  2.  The client MUST be able to retrieve checkpoint state from a
      trusted source to speed up initialization.

  3.  The client MUST be able to subscribe/unsubscribe to/from any
      polkadot-spec-conformant relay chain (Polkadot, Westend, Kusama)

  4.  The client MUST be able to subscribe/unsubscribe to/from
      parachains that do not use custom protocols or cryptography
      methods other than those that Polkadot, Westend and Kusama use.

  5.  The client MUST support the following [RPC
      methods](https://github.com/paritytech/json-rpc-interface-spec):
      `rpc_methods`, `chainHead_unstable_follow`,
      `chainHead_unstable_unfollow`, `chainHead_unstable_unpin`,
      `chainHead_unstable_storage`, `chainHead_unstable_call`
      `chainHead_unstable_stopCall`.
      `transaction_unstable_submitAndWatch`, and
      `transaction_unstable_unwatch`

  6.  The client MUST support the @substrate/connect [connection
      extension
      protocol](https://github.com/paritytech/substrate-connect/tree/main/packages/connect-extension-protocol):
      `ToApplicationError`, `ToApplicationChainReady`,
      `ToApplicationRpc`, `ToExtensionAddChain`,
      `ToExtensionAddWellKnownChain`, `ToExtensionRpc`,
      `ToExtensionRemoveChain`.

  </div>

</div>

</div>

<div class="sect2">

### <a href="#sect-sync-warp-lightclient" class="anchor"></a><a href="#sect-sync-warp-lightclient" class="link">7.2. Warp Sync for
Light Clients</a>

<div class="paragraph">

Warp sync ([Section 4.8.4](#sect-msg-warp-sync)) only downloads the
block headers where authority set changes occurred, so-called fragments
([Definition 41](#defn-warp-sync-proof)), and by verifying the GRANDPA
justifications ([Definition 78](#defn-grandpa-justification)). This
protocol allows nodes to arrive at the desired state much faster than
fast sync. Warp sync is primarily designed for Light Clients. Although,
warp sync could be used by full nodes, the sync process may lack
information to cater to complete functionality set of full nodes.

</div>

<div class="paragraph">

For light clients, it is too expensive to download the state (approx.
550MB) to respond to queries. Rather, the queries are submitted to the
Full node and only the response of the full node is validated using the
hash of the state root. Requests for warp sync are performed using the
`/dot/sync/warp` *Request-Response* substream, the corresponding network
messages are detailed in [Section 4.7](#sect-protocols-substreams).

</div>

<div class="paragraph">

Light clients base their trust in provided snapshots and the ability to
slash grandpa votes for equivocation for the period they are syncing via
warp sync. Full nodes and above in contrast verify each block
indvidually.

</div>

<div class="paragraph">

In theory, the `warp sync` process takes the Genesis Block as input and
outputs the hash of the state trie root at the latest finalized block.
This root hash acts as proof to further validate the responses to
queries by the full node. The `warp sync` works by starting from a
trusted specified block (for e.g. from a snapshot) and verifying the
block headers only at the authority set changes.

</div>

<div class="paragraph">

Eventually, the light client verifies the finality of the block returned
by a full node to ensure that the block is indeed the latest finalized
block. This entails two things:

</div>

<div class="olist arabic">

1.  Check the authenticity of GRANDPA Justifications messages from
    Genesis to the last finalized block.

2.  Check the timestamp of the last finalized block to ensure that no
    other blocks might have been finalized at a later timestamp.

</div>

<div class="admonitionblock warning">

|     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | **Long-Range Attack Vulnerabilities**: Warp syncing is particularly vulnerable to what is called long-range attacks. The authorities allowed to finalize blocks can generate multiple proofs of finality for multiple different blocks of the same height, hence, they can finalize more than one chain at a time. It is possible for two-thirds of the validators that were active at a certain past block N to collude and decide to finalize a different block N', even when N has been finalized for the first time several weeks or months in the past. When a client then warp syncs, it can be tricked to consider this alternative block N' as the finalized one. However, in practice, to mitigate Long-Range Attacks, the starting point of the warp syncing is not too far in the past. How far exactly depends on the logic of the runtime of the chain. For example, in Polkadot, the starting block for the sync should be at max 28 days old, to be within the purview of the slashing period for misbehaving nodes. Hence, even though in theory warp sync can start from Genesis Block, it is not advised to implement the same in practice. |

</div>

<div class="paragraph">

We outline the warp sync process, abstracting out details of verifying
the finality and how the full node to sync with is selected.

</div>

<div class="sidebarblock">

<div class="content">

\INPUT BlockHeader startblock, the initial block to start the sync. May
not be the Genesis Block. \OUTPUT CommitmentRootHash \$root\$, State
Tries Root hash of the latest finalized Block. \STATE \textsc{fullnode}
\$\leftarrow\$ SelectFullNode \STATE \textsc{latestBlockHeader,
grandpaJustifications} \$\leftarrow\$ SyncWithNode(\textsc{fullnode})
\STATE \textsc{isVerified} \$\leftarrow\$
verifyAuthoritySetChange(\textsc{grandpaJustifications}) \$\land\$
verifyFinality(\textsc{latestBlockHeader}) \IF{\textsc{isVerified}}
\STATE \$return\$ \$SOME\$
getCommitmentRootHash(\textsc{latestBlockHeader}) \ENDIF \STATE
{\$throw\$ \$ERROR\$}

<div class="paragraph">

Abstraction of Warp Sync and verification of latest block’s finality.

</div>

<div class="paragraph">

\\SelectFullNode\\: Determines the full node that the light client syncs
with.

</div>

<div class="paragraph">

\\SyncSithNode\\: Returns the header of latest finalized block and a
list of Grandpa Justifications by the full node.

</div>

<div class="paragraph">

\\verifyAuthoritySetChange\\: Verification algorithm which checks the
authenticity of the header only at the end of an era where the authority
set changes iteratively until reaching the latest era.

</div>

<div class="paragraph">

\\verifyFinalty\\: Verifies the finalty of the latest block using the
Grandpa Justifications messages.

</div>

</div>

</div>

<div class="paragraph">

The warp syncing process is closely coupled with the state querying
procedure used the light client. We outline the process of querying the
state by a light client and validating the response.

</div>

<div class="sidebarblock">

<div class="content">

\INPUT Query q, BlockHeight h, CommitmentRootHash \$root\$ \OUTPUT Maybe
Result \$res\$ \STATE (\$res\$, \$\pi\$) \$\leftarrow QueryFullNode (q,
h)\$ \IF{\$validityCheck\_{root}(res, \pi)\$} \STATE \$return\$ \$SOME\$
\$res\$ \ENDIF \STATE {\$throw\$ \$ERROR\$}

<div class="paragraph">

Querying State Algorithm.

</div>

<div class="paragraph">

\\QueryFullNode\\: Returns the response to the query requested from the
Full Node for the query \\q\\ at block height \\h\\.

</div>

<div class="paragraph">

\\validityCheck\_{root}\\: Predicate that checks the validity of
response \\res\\ and associated merkle proof \\\pi\\ by matching it
against the Commit Root Hash \\root\\ obtained as a result of warp sync.

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-runtime-environment-lightclient" class="anchor"></a><a href="#sect-runtime-environment-lightclient" class="link">7.3.
Runtime Environment for Light Clients</a>

<div class="paragraph">

Technically, though a runtime execution environment is not necessary to
build a light client, most clients require interacting with the Runtime
and the state of the blockchain for integrity checks at the minimum. One
can imagine an application scenarios like an on-chain light client which
only listens to the latest state without ever adding extrinsics. Current
implementations of Light Nodes (for e.g. Smoldot) uses the wasmtime as
its runtime environment to drastically simplify the code. The
performance of wasmtime is satisfying enough to not require a native
runtime. The details of runtime API that the environment needs to
suppport can be found in Appendix C ([Appendix C](#chap-runtime-api)).

</div>

</div>

<div class="sect2">

### <a href="#sect-light-msg" class="anchor"></a><a href="#sect-light-msg" class="link">7.4. Light Client Messages</a>

<div class="paragraph">

Light clients are applications that fetch the required data that they
need from a Polkadot node with an associated proof to validate the data.
This makes it possible to interact with the Polkadot network without
requiring to run a full node or having to trust the remote peers. The
light client messages make this functionality possible.

</div>

<div class="paragraph">

All light client messages are protobuf encoded and are sent over the
`/dot/light/2` substream.

</div>

<div class="sect3">

#### <a href="#id-request" class="anchor"></a><a href="#id-request" class="link">7.4.1. Request</a>

<div class="paragraph">

A message with all possible request messages. All message are sent as
part of this message.

</div>

| Type                | Id  | Description      |
|---------------------|-----|------------------|
| `oneof` (`request`) |     | The request type |

<div class="paragraph">

Where the `request` can be one of the following fields:

</div>

| Type                     | Id  | Description                                                                           |
|--------------------------|-----|---------------------------------------------------------------------------------------|
| `RemoteCallRequest`      | 1   | A remote call request ([Definition 96](#sect-light-remote-call-request))              |
| `RemoteReadRequest`      | 2   | A remote read request ([Definition 98](#sect-light-remote-read-request))              |
| `RemoteReadChildRequest` | 4   | A remote read child request ([Definition 100](#sect-light-remote-read-child-request)) |

</div>

<div class="sect3">

#### <a href="#id-response" class="anchor"></a><a href="#id-response" class="link">7.4.2. Response</a>

<div class="paragraph">

A message with all possible response messages. All message are sent as
part of this message.

</div>

| Type                 | Id  | Description       |
|----------------------|-----|-------------------|
| `oneof` (`response`) |     | The response type |

<div class="paragraph">

Where the `response` can be one of the following fields:

</div>

| Type                 | Id  | Description                                                                |
|----------------------|-----|----------------------------------------------------------------------------|
| `RemoteCallResponse` | 1   | A remote call response ([Definition 97](#sect-light-remote-call-response)) |
| `RemoteReadResponse` | 2   | A remote read response ([Definition 99](#sect-light-remote-read-response)) |

</div>

<div class="sect3">

#### <a href="#id-remote-call-messages" class="anchor"></a><a href="#id-remote-call-messages" class="link">7.4.3. Remote Call
Messages</a>

<div class="paragraph">

Execute a call to a contract at the given block.

</div>

<div id="sect-light-remote-call-request" class="exampleblock">

<div class="title">

Definition 96. [Remote Call Request](#sect-light-remote-call-request)

</div>

<div class="content">

<div class="paragraph">

Remote call request.

</div>

| Type     | Id  | Description                    |
|----------|-----|--------------------------------|
| `bytes`  | 2   | Block at which to perform call |
| `string` | 3   | Method name                    |
| `bytes`  | 4   | Call data                      |

</div>

</div>

<div id="sect-light-remote-call-response" class="exampleblock">

<div class="title">

Definition 97. [Remote Call Response](#sect-light-remote-call-response)

</div>

<div class="content">

<div class="paragraph">

Remote call response.

</div>

| Type    | Id  | Description                                                                                                            |
|---------|-----|------------------------------------------------------------------------------------------------------------------------|
| `bytes` | 2   | An *Option* type ([Definition 190](#defn-option-type)) containing the call proof or *None* if proof generation failed. |

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-remote-read-messages" class="anchor"></a><a href="#id-remote-read-messages" class="link">7.4.4. Remote Read
Messages</a>

<div class="paragraph">

Read a storage value at the given block.

</div>

<div id="sect-light-remote-read-request" class="exampleblock">

<div class="title">

Definition 98. [Remote Read Request](#sect-light-remote-read-request)

</div>

<div class="content">

<div class="paragraph">

Remote read request.

</div>

| Type             | Id  | Description                    |
|------------------|-----|--------------------------------|
| `bytes`          | 2   | Block at which to perform call |
| `repeated bytes` | 3   | Storage keys                   |

</div>

</div>

<div id="sect-light-remote-read-response" class="exampleblock">

<div class="title">

Definition 99. [Remote Read Response](#sect-light-remote-read-response)

</div>

<div class="content">

<div class="paragraph">

Remote read response.

</div>

| Type    | Id  | Description                                                                                                            |
|---------|-----|------------------------------------------------------------------------------------------------------------------------|
| `bytes` | 2   | An *Option* type ([Definition 190](#defn-option-type)) containing the read proof or *None* if proof generation failed. |

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-remote-read-child-messages" class="anchor"></a><a href="#id-remote-read-child-messages" class="link">7.4.5. Remote Read
Child Messages</a>

<div class="paragraph">

Read a child storage value at the given block.

</div>

<div id="sect-light-remote-read-child-request" class="exampleblock">

<div class="title">

Definition 100. [Remote Read Child
Request](#sect-light-remote-read-child-request)

</div>

<div class="content">

<div class="paragraph">

Remote read child request.

</div>

| Type    | Id  | Description                                                            |
|---------|-----|------------------------------------------------------------------------|
| `bytes` | 2   | Block at which to perform call                                         |
| `bytes` | 3   | Child storage key, this is relative to the child type storage location |
| `bytes` | 6   | Storage keys                                                           |

</div>

</div>

<div class="paragraph">

The response is the same as for the *Remote Read Request* message,
respectively [Definition 99](#sect-light-remote-read-response).

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-storage-lightclient" class="anchor"></a><a href="#sect-storage-lightclient" class="link">7.5. Storage for Light
Clients</a>

<div class="paragraph">

The light client requires a persistent storage for saving the state of
the blockchain. In addition it requires efficient Serialization/
De-serialization methods to transform SCALE ([Section
A.2.2](#sect-scale-codec)) encoded network traffic for storing and
reading from the persistent storage.

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#chapter-anv" class="anchor"></a><a href="#chapter-anv" class="link">8. Availability &amp; Validity</a>

<div class="sectionbody">

<div class="paragraph">

Polkadot serves as a replicated shared-state machine designed to resolve
scalability issues and interoperability among blockchains. The
validators of Polkadot execute transactions and participate in the
consensus of Polkadots primary chain, the so called relay chain.
Parachains are independent networks that maintain their own state and
are connected to the relay chain. Those parachains can take advantage of
the relay chain consensus mechanism, including sending and receiving
messages to and from other parachains. Parachain nodes that send
parachain blocks, known as candidates, to the validators in order to be
included in relay chain are referred to as collators.

</div>

<div class="paragraph">

The Polkadot relay chain validators are responsible for guaranteeing the
validity of both relay chain and parachain blocks. Additionally, the
validators are required to keep enough parachain blocks that should be
included in the relay chain available in their local storage in order to
make those retrievable by peers, who lack the information, to reliably
confirm the issued validity statements about parachain blocks. The
Availability & Validity (AnV) protocol consists of multiple steps for
successfully upholding those responsibilities.

</div>

<div class="paragraph">

Parachain blocks themselves are produced by collators ([Section
8.1](#sect-collations)), whereas the relay chain validators only verify
their validity (and later, their availability). It is possible that the
collators of a parachain produces multiple parachain block candidates
for a child of a specific block. Subsequently, they send the block
candidates to the the relay chain validators who are assigned to the
specific parachain. The assignment is determined by the Runtime
([Section 8.2](#sect-candidate-backing)). Those validators are then
required to check the validity of submitted candidates ([Section
8.3](#sect-candidate-validation)), then issue and collect statements
([Section 8.2.1](#sect-candidate-statements)) about the validity of
candidates to other validators. This process is known as candidate
backing. Once a candidate meets a specified criteria for inclusion, the
selected relay chain block author then choses any of the backed
candidate for each parachain and includes those into the relay chain
block ([Section 8.2.2](#sect-candidate-inclusion)).

</div>

<div class="paragraph">

Every relay chain validator must fetch the proposed candidates and issue
votes on whether they have the candidate saved in their local storage,
so called availability votes ([Section
8.4.1](#sect-availability-votes)), then also collect the votes sent by
other validators and include them in the relay chain state ([Section
8.2.2](#sect-candidate-inclusion)). This process ensures that only relay
chain blocks get finalized where each candidate is available on enough
nodes of validators.

</div>

<div class="paragraph">

Parachain candidates contained in non-finalized relay chain blocks must
then be retrieved by a secondary set of relay chain validators,
unrelated from the candidate backing process, who are randomly assigned
to determine the validity of specific parachains based on a VRF lottery
and are then required to vote on the validity of those candidates. This
process is known as approval voting ([Section
8.5](#sect-approval-voting)). If a validator does not have the candidate
data, it must recover the candidate data ([Section
8.4.2](#sect-candidate-recovery)).

</div>

<div class="sect2">

### <a href="#sect-collations" class="anchor"></a><a href="#sect-collations" class="link">8.1. Collations</a>

<div class="paragraph">

Collations are proposed candidates [Definition 131](#defn-candidate) to
the Polkadot relay chain validators. The Polkodat network protocol is
agnostic on what candidate productionis mechanism each parachain uses
and does not specify or mandate any of such production methods (e.g.
BABE-GRANDPA, Aura, etc). Furthermore, the relay chain validator host
implementation itself does not directly interpret or process the
internal transactions of the candidate, but rather rely on the parachain
Runtime to validate the candidate ([Section
8.3](#sect-candidate-validation)). Collators, which are parachain nodes
which produce candidate proposals and send them to the relay chain
validator, must prepare pieces of data ([Definition
101](#defn-collation)) in order to correctly comply with the
requirements of the parachain protocol.

</div>

<div id="defn-collation" class="exampleblock">

<div class="title">

Definition 101. [Collation](#defn-collation)

</div>

<div class="content">

<div class="paragraph">

A collation is a datastructure which contains the proposed parachain
candidate, including an optional validation parachain Runtime update and
upward messages. The collation datastructure, C, is a datastructure of
the following format:

</div>

<div class="stemblock">

<div class="content">

\\C = (M,H,R,h,P,p,w)\\ \\M = (u_n,…u_m)\\ \\H = (z_n,…z_m)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\M\\ is an array of upward messages ([Definition
  137](#defn-upward-message)), \\u\\, interpreted by the relay chain
  itself.

- \\H\\ is an array of outbound horizontal messages ([Definition
  139](#defn-outbound-hrmp-message)), \\z\\, interpreted by other
  parachains.

- \\R\\ is an *Option* type ([Definition 190](#defn-option-type)) which
  can contain a parachain Runtime update. The new Runtime code is an
  array of bytes.

- \\h\\ is the head data ([Definition 133](#defn-head-data)) produced as
  a result of execution of the parachain specific logic.

- \\P\\ is the PoV block ([Definition 132](#defn-para-block)).

- \\p\\ is an unsigned 32-bit integer indicating the number of processed
  downward messages ([Definition 138](#defn-downward-message)).

- \\w\\ is an unsigned 32-bit integer indicating the mark up to which
  all inbound HRMP messages have been processed by the parachain.

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-candidate-backing" class="anchor"></a><a href="#sect-candidate-backing" class="link">8.2. Candidate
Backing</a>

<div class="paragraph">

The Polkadot validator receives an arbitrary number of parachain
candidates with associated proofs from untrusted collators. The assigned
validators of each parachain ([Definition 136](#defn-validator-groups))
must verify and select a specific quantity of the proposed candidates
and issue those as backable candidates to its peers. A candidate is
considered backable when at least 2/3 of all assigned validators have
issued a *Valid* statement about that candidate, as described in
[Section 8.2.1](#sect-candidate-statements). Validators can retrieve
information about assignments via the Runtime APIs [Section
C.9.2](#sect-rt-api-validator-groups) respectively [Section
C.9.3](#sect-rt-api-availability-cores).

</div>

<div class="sect3">

#### <a href="#sect-candidate-statements" class="anchor"></a><a href="#sect-candidate-statements" class="link">8.2.1. Statements</a>

<div class="paragraph">

The assigned validator checks the validity of the proposed parachains
blocks ([Section 8.3](#sect-candidate-validation)) and issues *Valid*
statements ([Definition 102](#defn-statement)) to its peers if the
verification succeeded. Broadcasting failed verification as *Valid*
statements is a slashable offense. The validator must only issue one
*Seconded* statement, based on an arbitrary metric, which implies an
explicit vote for a candidate to be included in the relay chain.

</div>

<div class="paragraph">

This protocol attempts to produce as many backable candidates as
possible, but does not attempt to determine a final candidate for
inclusion. Once a parachain candidate has been seconded by at least one
other validator and enough Valid statements have been issued about that
candidate to meet the 2/3 quorum, the candidate is ready to be included
in the relay chain ([Section 8.2.2](#sect-candidate-inclusion)).

</div>

<div class="paragraph">

The validator issues validity statements votes in form of a validator
protocol message ([Definition
114](#net-msg-validator-protocol-message)).

</div>

<div id="defn-statement" class="exampleblock">

<div class="title">

Definition 102. [Statement](#defn-statement)

</div>

<div class="content">

<div class="paragraph">

A statement, \\S\\, is a datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\S = (d,A_i,A_s)\\ \\d = {(1,-\>,C_r),(2,-\>,C_h):}\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\d\\ is a varying datatype where *1* indicates that the validator
  “seconds” a candidate, meaning that the candidate should be included
  in the relay chain, followed by the committed candidate receipt
  ([Definition 105](#defn-committed-candidate-receipt)), \\C_r\\. *2*
  indicates that the validator has deemed the candidate valid, followed
  by the candidate hash.

- \\C_h\\ is the candidate hash.

- \\A_i\\ is the validator index in the authority set that signed this
  statement.

- \\A_s\\ is the signature of the validator.

</div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-candidate-inclusion" class="anchor"></a><a href="#sect-candidate-inclusion" class="link">8.2.2. Inclusion</a>

<div class="paragraph">

The Polkadot validator includes the backed candidates as parachain
inherent data ([Definition 103](#defn-parachain-inherent-data)) into a
block as described [Section 2.3.3](#sect-inherents). The relay chain
block author decides on whatever metric which candidate should be
selected for inclusion, as long as that candidate is valid and meets the
validity quorum of 2/3+ as described in [Section
8.2.1](#sect-candidate-statements). The candidate approval process
([Section 8.5](#sect-approval-voting)) ensures that only relay chain
blocks are finalized where each candidate for each availability core
meets the requirement of 2/3+ availability votes.

</div>

<div id="defn-parachain-inherent-data" class="exampleblock">

<div class="title">

Definition 103. [Parachain Inherent Data](#defn-parachain-inherent-data)

</div>

<div class="content">

<div class="paragraph">

The parachain inherent data contains backed candidates and is included
when authoring a relay chain block. The datastructure, \\I\\, is of the
following format:

</div>

<div class="stemblock">

<div class="content">

\\I = (A,T,D,P_h)\\ \\T = (C_0,…C_n)\\ \\D = (\*d_n,…d_m)\\ \\C =
(R,V,i)\\ \\V = (a_n,…a_m)\\ \\a = {(1,-\>,s),(2,-\>,s):}\\ \\A =
(L_n,…L_m)\\ \\L = (b,v_i,s)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\A\\ is an array of signed bitfields by validators claiming the
  candidate is available (or not). The array must be sorted by validator
  index corresponding to the authority set ([Definition
  33](#defn-authority-list)).

- \\T\\ is an array of backed candidates for inclusing in the current
  block.

- \\D\\ is an array of disputes.

- \\P_h\\ is the parachain parent head data ([Definition
  133](#defn-head-data)).

- \\d\\ is a dispute statement ([Section
  8.7.2.1](#net-msg-dispute-request)).

- \\R\\ is a committed candidate receipt ([Definition
  105](#defn-committed-candidate-receipt)).

- \\V\\ is an array of validity votes themselves, expressed as
  signatures.

- \\i\\ is a bitfield of indices of the validators within the validator
  group ([Definition 136](#defn-validator-groups)).

- \\a\\ is either an implicit or explicit attestation of the validity of
  a parachain candidate, where *1* implies an implicit vote (in
  correspondence of a *Seconded* statement) and *2* implies an explicit
  attestation (in correspondence of a *Valid* statement). Both variants
  are followed by the signature of the validator.

- \\s\\ is the signature of the validator.

- \\b\\ the availability bitfield ([Section
  8.4.1](#sect-availability-votes)).

- \\v_i\\ is the validator index of the authority set ([Definition
  33](#defn-authority-list)).

</div>

</div>

</div>

</div>

<div id="defn-candidate-receipt" class="exampleblock">

<div class="title">

Definition 104. [Candidate Receipt](#defn-candidate-receipt)

</div>

<div class="content">

<div class="paragraph">

A candidate receipt, \\R\\, contains information about the candidate and
a proof of the results of its execution. It’s a datastructure of the
following format:

</div>

<div class="stemblock">

<div class="content">

\\R = (D,C_h)\\

</div>

</div>

<div class="paragraph">

where \\D\\ is the candidate descriptor ([Definition
106](#defn-candidate-descriptor)) and \\C_h\\ is the hash of candidate
commitments ([Definition 107](#defn-candidate-commitments)).

</div>

</div>

</div>

<div id="defn-committed-candidate-receipt" class="exampleblock">

<div class="title">

Definition 105. [Committed Candidate
Receipt](#defn-committed-candidate-receipt)

</div>

<div class="content">

<div class="paragraph">

The committed candidate receipt, \\R\\, contains information about the
candidate and the the result of its execution that is included in the
relay chain. This type is similar to the candidate receipt ([Definition
104](#defn-candidate-receipt)), but actually contains the execution
results rather than just a hash of it. It’s a datastructure of the
following format:

</div>

<div class="stemblock">

<div class="content">

\\R = (D,C)\\

</div>

</div>

<div class="paragraph">

where \\D\\ is the candidate descriptor ([Definition
106](#defn-candidate-descriptor)) and \\C\\ is the candidate commitments
([Definition 107](#defn-candidate-commitments)).

</div>

</div>

</div>

<div id="defn-candidate-descriptor" class="exampleblock">

<div class="title">

Definition 106. [Candidate Descriptor](#defn-candidate-descriptor)

</div>

<div class="content">

<div class="paragraph">

The candidate descriptor, \\D\\, is a unique descriptor of a candidate
receipt. It’s a datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\D = (p,H,C_i,V,B,r,s,p_h,R_h)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\p\\ is the parachain Id ([Definition 134](#defn-para-id)).

- \\H\\ is the hash of the relay chain block the candidate is executed
  in the context of.

- \\C_i\\ is the collators public key.

- \\V\\ is the hash of the persisted validation data ([Definition
  227](#defn-persisted-validation-data)).

- \\B\\ is the hash of the PoV block.

- \\r\\ is the root of the block’s erasure encoding Merkle tree.

- \\s\\ the collator signature of the concatenated components \\p\\,
  \\H\\, \\R_h\\ and \\B\\.

- \\p_h\\ is the hash of the parachain head data ([Definition
  133](#defn-head-data)) of this candidate.

- \\R_h\\ is the hash of the parachain Runtime.

</div>

</div>

</div>

</div>

<div id="defn-candidate-commitments" class="exampleblock">

<div class="title">

Definition 107. [Candidate Commitments](#defn-candidate-commitments)

</div>

<div class="content">

<div class="paragraph">

The candidate commitments, \\C\\, is the result of the execution and
validation of a parachain (or parathread) candidate whose produced
values must be committed to the relay chain. Those values are retrieved
from the validation result ([Definition 109](#defn-validation-result)).
A candidate commitment is a datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\C =(M_u,M_h,R,h,p,w)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\M_u\\ is an array of upward messages sent by the parachain. Each
  individual message, m, is an array of bytes.

- \\M_h\\ is an array of individual outbound horizontal messages
  ([Definition 139](#defn-outbound-hrmp-message)) sent by the parachain.

- \\R\\ is an *Option* value ([Definition 190](#defn-option-type)) that
  can contain a new parachain Runtime in case of an update.

- \\h\\ is the parachain head data ([Definition 133](#defn-head-data)).

- \\p\\ is a unsigned 32-bit integer indicating the number of downward
  messages that were processed by the parachain. It is expected that the
  parachain processes the messages from first to last.

- \\w\\ is a unsigned 32-bit integer indicating the watermark which
  specifies the relay chain block number up to which all inbound
  horizontal messages have been processed.

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-candidate-validation" class="anchor"></a><a href="#sect-candidate-validation" class="link">8.3. Candidate
Validation</a>

<div class="paragraph">

Received candidates submitted by collators and must have its validity
verified by the assigned Polkadot validators. For each candidate to be
valid, the validator must successfully verify the following conditions
in the following order:

</div>

<div class="olist arabic">

1.  The candidate does not exceed any parameters in the persisted
    validation data ([Definition 227](#defn-persisted-validation-data)).

2.  The signature of the collator is valid.

3.  Validate the candidate by executing the parachain Runtime ([Section
    8.3.1](#sect-parachain-runtime)).

</div>

<div class="paragraph">

If all steps are valid, the Polkadot validator must create the necessary
candidate commitments ([Definition 107](#defn-candidate-commitments))
and submit the appropriate statement for each candidate ([Section
8.2.1](#sect-candidate-statements)).

</div>

<div class="sect3">

#### <a href="#sect-parachain-runtime" class="anchor"></a><a href="#sect-parachain-runtime" class="link">8.3.1. Parachain
Runtime</a>

<div class="paragraph">

Parachain Runtimes are stored in the relay chain state, and can either
be fetched by the parachain Id or the Runtime hash via the relay chain
Runtime API as described in [Section
C.9.7](#sect-rt-api-validation-code) and [Section
C.9.8](#sect-rt-api-validation-code-by-hash) respectively. The retrieved
parachain Runtime might need to be decompressed based on the magic
identifier as described in [Section 8.3.2](#sect-runtime-compression).

</div>

<div class="paragraph">

In order to validate a parachain block, the Polkadot validator must
prepare the validation parameters ([Definition
108](#defn-validation-parameters)), then use its local Wasm execution
environment ([Section 2.6.3](#sect-code-executor)) to execute the
validate_block parachain Runtime API by passing on the validation
parameters as an argument. The parachain Runtime function returns the
validation result ([Definition 109](#defn-validation-result)).

</div>

<div id="defn-validation-parameters" class="exampleblock">

<div class="title">

Definition 108. [Validation Parameters](#defn-validation-parameters)

</div>

<div class="content">

<div class="paragraph">

The validation parameters structure, \\P\\, is required to validate a
candidate against a parachain Runtime. It’s a datastructure of the
following format:

</div>

<div class="stemblock">

<div class="content">

\\P = (h,b,B_i,S_r)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\h\\ is the parachain head data ([Definition 133](#defn-head-data)).

- \\b\\ is the block body ([Definition 132](#defn-para-block)).

- \\B_i\\ is the latest relay chain block number.

- \\S_r\\ is the relay chain block storage root ([Section
  2.4.4](#sect-merkl-proof)).

</div>

</div>

</div>

</div>

<div id="defn-validation-result" class="exampleblock">

<div class="title">

Definition 109. [Validation Result](#defn-validation-result)

</div>

<div class="content">

<div class="paragraph">

The validation result is returned by the `validate_block` parachain
Runtime API after attempting to validate a parachain block. Those
results are then used in candidate commitments ([Definition
107](#defn-candidate-commitments)), which then will be inserted into the
relay chain via the parachain inherent data ([Definition
103](#defn-parachain-inherent-data)). The validation result, \\V\\, is a
datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\V = (h,R,M_u,M_h,p\_,w)\\ \\M_u = (m_0,…m_n)\\ \\M_h = (t_0,…t_n)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\h\\ is the parachain head data ([Definition 133](#defn-head-data)).

- \\R\\ is an *Option* value ([Definition 190](#defn-option-type)) that
  can contain a new parachain Runtime in case of an update.

- \\M_u\\ is an array of upward messages sent by the parachain. Each
  individual message, m, is an array of bytes.

- \\M_h\\ is an array of individual outbound horizontal messages
  ([Definition 139](#defn-outbound-hrmp-message)) sent by the parachain.

- \\p\\ is a unsigned 32-bit integer indicating the number of downward
  messages that were processed by the parachain. It is expected that the
  parachain processes the messages from first to last.

- \\w\\ is a unsigned 32-bit integer indicating the watermark which
  specifies the relay chain block number up to which all inbound
  horizontal messages have been processed.

</div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-runtime-compression" class="anchor"></a><a href="#sect-runtime-compression" class="link">8.3.2. Runtime
Compression</a>

<div class="admonitionblock note">

|     |                                            |
|-----|--------------------------------------------|
|     | Runtime compression is not documented yet. |

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-availability" class="anchor"></a><a href="#sect-availability" class="link">8.4. Availability</a>

<div class="sect3">

#### <a href="#sect-availability-votes" class="anchor"></a><a href="#sect-availability-votes" class="link">8.4.1. Availability
Votes</a>

<div class="paragraph">

The Polkadot validator must issue a bitfield ([Definition
141](#defn-bitfield-array)) which indicates votes for the availability
of candidates. Issued bitfields can be used by the validator and other
peers to determine which backed candidates meet the 2/3+ availability
quorum.

</div>

<div class="paragraph">

Candidates are inserted into the relay chain in form of parachain
inherent data ([Section 8.2.2](#sect-candidate-inclusion)) by a block
author. A validator can retrieve that data by calling the appropriate
Runtime API entry ([Section C.9.3](#sect-rt-api-availability-cores)),
then create a bitfield indicating for which candidate the validator has
availability data stored and broadcast it to the network ([Definition
118](#net-msg-bitfield-dist-msg)). When sending the bitfield distrubtion
message, the validator must ensure \\B_h\\ is set approriately,
therefore clarifying to which state the bitfield is referring to, given
that candidates can vary based on the chain fork.

</div>

<div class="paragraph">

Missing availability data of candidates must be recovered by the
validator as described in [Section 8.4.2](#sect-candidate-recovery). If
previously issued bitfields are no longer accurate, i.e. the
availability data has been recovered or the candidate of an availability
core has changed, the validator must create a new bitfield and broadcast
it to the network. Candidates must be kept available by validators for a
specific amount of time. If a candidate does not receive any backing,
validators should keep it available for about one hour, in case the
state of backing does change. Backed and even approved candidates
([Section 8.5](#sect-approval-voting)) must be kept by validators for
about 25 hours, since disputes ([Section 8.6](#sect-disputes)) can occur
and the candidate needs to be checked again.

</div>

<div class="paragraph">

The validator issues availability votes in form of a validator protocol
message ([Definition 115](#net-msg-collator-protocol-message)).

</div>

</div>

<div class="sect3">

#### <a href="#sect-candidate-recovery" class="anchor"></a><a href="#sect-candidate-recovery" class="link">8.4.2. Candidate
Recovery</a>

<div class="paragraph">

The availability distribution of the Polkadot validator must be able to
recover parachain candidates that the validator is assigned to, in order
to determine whether the candidate should be backed ([Section
8.2](#sect-candidate-backing)) respectively whether the candidate should
be approved ([Section 8.5](#sect-approval-voting)). Additionally, peers
can send availability requests as defined in [Definition
122](#net-msg-chunk-fetching-request) and [Definition
124](#net-msg-available-data-request) to the validator, which the
validator should be able to respond to.

</div>

<div class="paragraph">

Candidates are recovered by sending requests for specific indices of
erasure encoded chunks ([Section A.4.1](#sect-erasure-encoding)). A
validator should request chunks by picking peers randomly and must
recover at least \\f+1\\ chunks, where \\n=3f+k\\ and \\k in {1,2,3}\\.
\\n\\ is the number of validators as specified in the session info,
which can be fetched by the Runtime API as described in [Section
C.9.11](#sect-rt-api-session-info).

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-approval-voting" class="anchor"></a><a href="#sect-approval-voting" class="link">8.5. Approval Voting</a>

<div class="paragraph">

The approval voting process ensures that only valid parachain blocks are
finalized on the relay chain. After *backable* parachain candidates were
submitted to the relay chain ([Section
8.2.2](#sect-candidate-inclusion)), which can be retrieved via the
Runtime API ([Section C.9.3](#sect-rt-api-availability-cores)),
validators need to determine their assignments for each parachain and
issue approvals for valid candidates, respectively disputes for invalid
candidates. Since it cannot be expected that each validator verifies
every single parachain candidate, this mechanism ensures that enough
honest validators are selected to verify parachain candidates in order
prevent the finalization of invalid blocks. If an honest validator
detects an invalid block which was approved by one or more validators,
the honest validator must issue a disputes which wil cause escalations,
resulting in consequences for all malicious parties, i.e. slashing. This
mechanism is described more in [Section
8.5.1](#sect-availability-assignment-criteria).

</div>

<div class="sect3">

#### <a href="#sect-availability-assignment-criteria" class="anchor"></a><a href="#sect-availability-assignment-criteria" class="link">8.5.1.
Assignment Criteria</a>

<div class="paragraph">

Validators determine their assignment based on a VRF mechanism, similar
to the BABE consensus mechanism. First, validators generate an
availability core VRF assignment ([Definition
111](#defn-availability-core-vrf-assignment)), which indicates which
availability core a validator is assigned to. Then a delayed
availability core VRF assignment is generated which indicates at what
point a validator should start the approval process. The delays are
based on “tranches” ([Section 8.5.2](#sect-tranches)).

</div>

<div class="paragraph">

An assigned validator never broadcasts their assignment until relevant.
Once the assigned validator is ready to check a candidate, the validator
broadcasts their assignment by issuing an approval distribution message
([Definition 119](#net-msg-approval-distribution)), where \\M\\ is of
variant *0*. Other assigned validators that receive that network message
must keep track of if, expecting an approval vote following shortly
after. Assigned validators can retrieve the candidate by using the
availability recovery ([Section 8.4.2](#sect-candidate-recovery)) and
then validate the candidate ([Section 8.3](#sect-candidate-validation)).

</div>

<div class="paragraph">

The validator issues approval votes in form of a validator protocol
message ([Definition 114](#net-msg-validator-protocol-message))
respectively disputes ([Section 8.6](#sect-disputes)).

</div>

</div>

<div class="sect3">

#### <a href="#sect-tranches" class="anchor"></a><a href="#sect-tranches" class="link">8.5.2. Tranches</a>

<div class="paragraph">

Validators use a subjective, tick-based system to determine when the
approval process should start. A validator starts the tick-based system
when a new availability core candidates have been proposed, which can be
retrieved via the Runtime API ([Section
C.9.3](#sect-rt-api-availability-cores)) , and increments the tick every
*500 milliseconds*. Each tick/increment is referred to as a “tranche”,
represented as an integer, starting at *0*.

</div>

<div class="paragraph">

As described in [Section 8.5.1](#sect-availability-assignment-criteria),
the validator first executes the VRF mechanism to determine which
parachains (availability cores) the validator is assigned to, then an
additional VRF mechanism for each assigned parachain to determine the
*delayed assignment*. The delayed assignment indicates the tranche at
which the validator should start the approval process. A tranche of
value *0* implies that the assignment should be started immediately,
while later assignees of later tranches wait until it’s their term to
issue assignments, determined by their subjective, tick-based system.

</div>

<div class="paragraph">

Validators are required to track broadcasted assignments by other
validators assigned to the same parachain, including verifying the VRF
output. Once a valid assignment from a peer was received, the validator
must wait for the following approval vote within a certain period as
described in [Section C.9.11](#sect-rt-api-session-info) by orienting
itself on its local, tick-based system. If the waiting time after a
broadcasted assignment exceeds the specified period, the validator
interprets this behavior as a “no-show”, indicating that more validators
should commit on their tranche until enough approval votes have been
collected.

</div>

<div class="paragraph">

If enough approval votes have been collected as described in [Section
C.9.11](#sect-rt-api-session-info), then assignees of later tranches do
not have to start the approval process. Therefore, this tranche system
serves as a mechanism to ensure that enough candidate approvals from a
random set of validators are created without requiring all assigned
validators to check the candidate.

</div>

<div id="defn-relay-vrf-story" class="exampleblock">

<div class="title">

Definition 110. [Relay VRF Story](#defn-relay-vrf-story)

</div>

<div class="content">

<div class="paragraph">

The relay VRF story is an array of random bytes derived from the VRF
submitted within the block by the block author. The relay VRF story, T,
is used as input to determine approval voting criteria and generated the
following way:

</div>

<div class="stemblock">

<div class="content">

\\T = "Transcript"(b_r,b_s,e_i,A)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\"Transcript"\\ constructs a VRF transcript ([Definition
  175](#defn-vrf-transcript)).

- \\b_r\\ is the BABE randomness of the current epoch ([Definition
  71](#defn-epoch-randomness)).

- \\b_s\\ is the current BABE slot ([Definition 54](#defn-epoch-slot)).

- \\e_i\\ is the current BABE epoch index ([Definition
  54](#defn-epoch-slot)).

- \\A\\ is the public key of the authority.

</div>

</div>

</div>

</div>

<div id="defn-availability-core-vrf-assignment" class="exampleblock">

<div class="title">

Definition 111. [Availability Core VRF
Assignment](#defn-availability-core-vrf-assignment)

</div>

<div class="content">

<div class="paragraph">

An availability core VRF assignment is computed by a relay chain
validator to determine which availability core ([Definition
135](#defn-availability-core)) a validator is assigned to and should
vote for approvals. Computing this assignement relies on the VRF
mechanism, transcripts and STROBE operations described further in
[Section A.1.3](#sect-vrf).

</div>

<div class="paragraph">

The Runtime dictates how many assignments should be conducted by a
validator, as specified in the session index which can be retrieved via
the Runtime API ([Section C.9.11](#sect-rt-api-session-info)). The
amount of assignments is referred to as “samples”. For each iteration of
the number of samples, the validator calculates an individual
assignment, \\T\\, where the little-endian encoded sample number, \\s\\,
is incremented by one. At the beginning of the iteration, \\S\\ starts
at value *0*.

</div>

<div class="paragraph">

The validator executes the following steps to retrieve a (possibly
valid) core index:

</div>

<div class="stemblock">

<div class="content">

\\t_1 larr "Transcript"("'A&V MOD'")\\ \\t_2 larr "append"(t_1,
"'RC-VRF'", R_s)\\ \\t_3 larr "append"(t_2, "'sample'", s)\\ \\t_4 larr
"append"(t_3, "'vrf-nm-pk'", p_k)\\ \\t_5 larr "meta-ad"(t_4,
"'VRFHash'", "False")\\ \\t_6 larr "meta-ad"(t_5, 64\_("le"), "True")\\
\\i larr "prf"(t_6, "False")\\ \\o = s_k \* i\\

</div>

</div>

<div class="paragraph">

where \\s_k\\ is the secret key, \\p_k\\ is the public key and
\\64\_("le")\\ is the integer *64* encoded as little endian. \\R_s\\ is
the relay VRF story as defined in [Definition
110](#defn-relay-vrf-story). Following:

</div>

<div class="stemblock">

<div class="content">

\\t_1 larr "Transcript"("'VRFResult'")\\ \\t_2 larr "append"(t_1, "''",
"'A&V CORE'")\\ \\t_3 larr "append"(t_2, "'vrf-in'", i)\\ \\t_4 larr
"append"(t_3, "'vrf-out'", o)\\ \\t_5 larr "meta-ad"(t_4, "''",
"False")\\ \\t_6 larr "meta-ad"(t_5, 4\_"le", "True")\\ \\r larr
"prf"(t_6, "False")\\ \\c_i = r mod a_c\\

</div>

</div>

<div class="paragraph">

where \\4\_("le")\\ is the integer *4* encoded as little endian, \\r\\
is the 4-byte challenge interpreted as a little endian encoded interger
and \\a_c\\ is the number of availability cores used during the active
session, as defined in the session info retrieved by the Runtime API
([Section C.9.11](#sect-rt-api-session-info)). The resulting integer,
\\c_i\\, indicates the parachain Id ([Definition 134](#defn-para-id)).
If the parachain Id doesn’t exist, as can be retrieved by the Runtime
API ([Section C.9.3](#sect-rt-api-availability-cores)), the validator
discards that value and continues with the next iteration. If the Id
does exist, the validators continues with the following steps:

</div>

<div class="stemblock">

<div class="content">

\\t_1 larr "Transcript"("'A&V ASSIGNED'")\\ \\t_2 larr "append"(t_1,
"'core'", c_i)\\ \\p larr "dleq_prove"(t_2, i)\\

</div>

</div>

<div class="paragraph">

where \\"dleq_prove"\\ is described in [Definition
172](#defn-vrf-dleq-prove). The resulting values of \\o\\, \\p\\ and
\\s\\ are used to construct an assignment certificate ([Definition
113](#defn-assignment-cert)) of kind *0*.

</div>

</div>

</div>

<div id="delayed-availability-core-vrf-assignment" class="exampleblock">

<div class="title">

Definition 112. [Delayed Availability Core VRF
Assignment](#delayed-availability-core-vrf-assignment)

</div>

<div class="content">

<div class="paragraph">

The **delayed availability core VRF assignments** determined at what
point a validator should start the approval process as described in
[Section 8.5.2](#sect-tranches). Computing this assignement relies on
the VRF mechanism, transcripts and STROBE operations described further
in [Section A.1.3](#sect-vrf).

</div>

<div class="paragraph">

The validator executes the following steps:

</div>

<div class="stemblock">

<div class="content">

\\t_1 larr "Transcript"("'A&V DELAY'")\\ \\t_2 larr
"append"(t_1,"'RC-VRF'",R_s)\\ \\t_3 larr "append"(t_2, "'core'",c_i)\\
\\t_4 larr "append"(t_3, "'vrf-nm-pk'", p_k)\\ \\t_5 larr "meta-ad"(t_4,
"'VRFHash'", "False")\\ \\t_6 larr "meta-ad"(t_5, 64\_("le"), "True")\\
\\i larr "prf"(t_6, "False")\\ \\o = s_k \* i\\ \\p larr
"dleq_prove"(t_6, i)\\

</div>

</div>

<div class="paragraph">

The resulting value \\p\\ is the VRF proof ([Definition
171](#defn-vrf-proof)). \\"dleq_prove"\\ is described in [Definition
172](#defn-vrf-dleq-prove).

</div>

<div class="paragraph">

The tranche, \\d\\, is determined as:

</div>

<div class="stemblock">

<div class="content">

\\t_1 larr "Transcript"("'VRFResult'")\\ \\t_2 larr "append"(t_1, "''",
"'A&V TRANCHE'")\\ \\t_3 larr "append"(t_2, "'vrf-in'", i)\\ \\t_4 larr
"append"(t_3, "'vrf-out'", o)\\ \\t_5 larr "meta-ad"(t_4, "''",
"False")\\ \\t_6 larr "meta-ad"(t_5, 4\_("le"), "True")\\ \\c larr
"prf"(t_6, "False")\\ \\d = d mod (d_c+d_z) - d_z\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\d_c\\ is the number of delayed tranches by total as specified by the
  session info, retrieved via the Runtime API ([Section
  C.9.11](#sect-rt-api-session-info)).

- \\d_z\\ is the zeroth delay tranche width as specified by the session
  info, retrieved via the Runtime API ([Section
  C.9.11](#sect-rt-api-session-info))..

</div>

</div>

<div class="paragraph">

The resulting tranche, \\n\\, cannot be less than \\0\\. If the tranche
is less than \\0\\, then \\d=0\\. The resulting values \\o\\, \\p\\ and
\\c_i\\ are used to construct an assignment certificate (\<[Definition
113](#defn-assignment-cert)) of kind *1*.

</div>

</div>

</div>

<div id="defn-assignment-cert" class="exampleblock">

<div class="title">

Definition 113. [Assignment Certificate](#defn-assignment-cert)

</div>

<div class="content">

<div class="paragraph">

The **Assignment Certificate** proves to the network that a Polkadot
validator is assigned to an availability core and is therefore qualified
for the approval of candidates, as clarified in [Definition
111](#defn-availability-core-vrf-assignment). This certificate contains
the computed VRF output and is a datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\(k, o, p)\\ \\k = {(0,-\>,s),(1,-\>,c_i):}\\

</div>

</div>

<div class="paragraph">

where \\k\\ indicates the kind of the certificate, respectively the
value *0* proves the availability core assignment ([Definition
111](#defn-availability-core-vrf-assignment)), followed by the sample
number \\s\\, and the value *1* proves the delayed availability core
assignment ([Definition
112](#delayed-availability-core-vrf-assignment)), followed by the core
index \\c_i\\ ([Section C.9.3](#sect-rt-api-availability-cores)). \\o\\
is the VRF output and \\p\\ is the VRF proof.

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-disputes" class="anchor"></a><a href="#sect-disputes" class="link">8.6. Disputes</a>

<div class="admonitionblock note">

|     |                                  |
|-----|----------------------------------|
|     | Disputes are not documented yet. |

</div>

</div>

<div class="sect2">

### <a href="#sect-anv-network-messages" class="anchor"></a><a href="#sect-anv-network-messages" class="link">8.7. Network
Messages</a>

<div class="paragraph">

The availability and validity process requires certain network messages
to be exchanged between validators and collators.

</div>

<div class="sect3">

#### <a href="#id-notification-messges" class="anchor"></a><a href="#id-notification-messges" class="link">8.7.1. Notification
Messges</a>

<div class="paragraph">

The notification messages are exchanged between validators, including
messages sent by collators to validators. The protocol messages are
exchanged based on a streaming notification substream ([Section
4.5](#sect-connection-establishment)). The messages are SCALE encoded
([Section A.2.2](#sect-scale-codec)).

</div>

<div id="net-msg-validator-protocol-message" class="exampleblock">

<div class="title">

Definition 114. [Validator Protocol
Message](#net-msg-validator-protocol-message)

</div>

<div class="content">

<div class="paragraph">

The validator protocol message is a varying datatype used by validators
to broadcast relevant information about certain steps in the A&V
process. Specifically, this includes the backing process ([Section
8.2](#sect-candidate-backing)) and the approval process ([Section
8.5](#sect-approval-voting)). The validator protocol message, \\M\\, is
a varying datatype of the following format:

</div>

<div class="stemblock">

<div class="content">

\\M = {(1,-\>,M_f),(3,-\>,M_s),(4,-\>,M_a):}\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\M_f\\ is a bitfield distribution message ([Definition
  118](#net-msg-bitfield-dist-msg)).

- \\M_s\\ is a statement distribution message ([Definition
  117](#net-msg-statement-distribution)).

- \\M_a\\ is a approval distribution message ([Definition
  119](#net-msg-approval-distribution)).

</div>

</div>

</div>

</div>

<div id="net-msg-collator-protocol-message" class="exampleblock">

<div class="title">

Definition 115. [Collation Protocol
Message](#net-msg-collator-protocol-message)

</div>

<div class="content">

<div class="paragraph">

The collation protocol message, M, is a varying datatype of the
following format:

</div>

<div class="stemblock">

<div class="content">

\\M = {(0,-\>,M_c):}\\

</div>

</div>

<div class="paragraph">

where \\M_c\\ is the collator message ([Definition
116](#net-msg-collator-message)).

</div>

</div>

</div>

<div id="net-msg-collator-message" class="exampleblock">

<div class="title">

Definition 116. [Collator Message](#net-msg-collator-message)

</div>

<div class="content">

<div class="paragraph">

The collator message is sent as part of the collator protocol message
([Definition 115](#net-msg-collator-protocol-message)). The collator
message, \\M\\, is a varying datatype of the following format:

</div>

<div class="stemblock">

<div class="content">

\\M = {(0,-\>,(C_i,P_i,C_s)),(1,-\>,H),(4,-\>,(B_h,S)):}\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\M\\ is a varying datatype where *0* indicates the intent to
  advertise a collation and *1* indicates the advertisement of a
  collation to a validator. *4* indicates that a collation sent to a
  validator was seconded.

- \\C_i\\ is the public key of the collator.

- \\P_i\\ is the parachain Id ([Definition 134](#defn-para-id)).

- \\C_s\\ is the signature of the collator using the *PeerId* of the
  collators node.

- \\H\\ is the hash of the parachain block ([Definition
  132](#defn-para-block)).

- \\S\\ is a full statement ([Definition 102](#defn-statement)).

</div>

</div>

</div>

</div>

<div id="net-msg-statement-distribution" class="exampleblock">

<div class="title">

Definition 117. [Statement Distribution
Message](#net-msg-statement-distribution)

</div>

<div class="content">

<div class="paragraph">

The statement distribution message is sent as part of the validator
protocol message ([Definition 115](#net-msg-collator-protocol-message))
indicates the validity vote of a validator for a given candidate,
described further in [Section 8.2.1](#sect-candidate-statements). The
statement distribution message, \\M\\, is of varying type of the
following format:

</div>

<div class="stemblock">

<div class="content">

\\M = {(0,-\>,(B_h,S)),(1,-\>,S_m):}\\ \\S_m = (B_h,C_h,A_i,A_s)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\M\\ is a varying datatype where *0* indicates a signed statement and
  *1* contains metadata about a seconded statement with a larger
  payload, such as a runtime upgrade. The candidate itself can be
  fetched via the request/response message ([Definition
  128](#net-msg-statement-fetching-request)).

- \\B_h\\ is the hash of the relay chain parent, indicating the state
  this message is for.

- \\S\\ is a full statement ([Definition 102](#defn-statement)).

- \\A_i\\ is the validator index in the authority set ([Definition
  33](#defn-authority-list)) that signed this message.

- \\A_s\\ is the signature of the validator.

</div>

</div>

</div>

</div>

<div id="net-msg-bitfield-dist-msg" class="exampleblock">

<div class="title">

Definition 118. [Bitfield Distribution
Message](#net-msg-bitfield-dist-msg)

</div>

<div class="content">

<div class="paragraph">

The bitfield distribution message is sent as part of the validator
protocol message ([Definition 114](#net-msg-validator-protocol-message))
and indicates the availability vote of a validator for a given
candidate, described further in [Section
8.4.1](#sect-availability-votes). This message is sent in form of a
validator protocol message ([Definition
114](#net-msg-validator-protocol-message)). The bitfield distribution
message, \\M\\, is a datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\M = {(0,-\>,(B_h,P)):}\\ \\P = (d,A_i,A_s)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\B_h\\ is the hash of the relay chain parent, indicating the state
  this message is for.

- \\d\\ is the bitfield array ([Definition 141](#defn-bitfield-array)).

- \\A_i\\ is the validator index in the authority set ([Definition
  33](#defn-authority-list)) that signed this message.

- \\A_s\\ is the signature of the validator.

</div>

</div>

</div>

</div>

<div id="net-msg-approval-distribution" class="exampleblock">

<div class="title">

Definition 119. [Approval Distribution
Message](#net-msg-approval-distribution)

</div>

<div class="content">

<div class="paragraph">

The approval distribution message is sent as part of the validator
protocol message ([Definition 114](#net-msg-validator-protocol-message))
and indicates the approval vote of a validator for a given candidate,
described further in [Section
8.5.1](#sect-availability-assignment-criteria). The approval
distribution message, \\M\\, is a varying datatype of the following
format:

</div>

<div class="stemblock">

<div class="content">

\\M = {(0,-\>,((C\_,I\_)\_0…(C,I)\_n)),(1,-\>,(V_0,…V_n)):}\\ \\C =
(B_h,A_i,c_a)\\ \\c_a = (c_k,P_o,P_p)\\ \\c_k = {(0→s),(1→i):}\\ \\V =
(B_h,I,A_i,A_s)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\M\\ is a varying datatype where *0* indicates assignments for
  candidates in recent, unfinalized blocks and *1* indicates approvals
  for candidates in some recent, unfinalized block.

- \\C\\ is an assignment criterion which refers to the candidate under
  which the assignment is relevant by the block hash.

- \\I\\ is an unsigned 32-bit integer indicating the index of the
  candidate, corresponding the the order of the availability cores
  ([Section C.9.3](#sect-rt-api-availability-cores)).

- \\B_h\\ is the relay chain block hash where the candidate appears.

- \\A_i\\ is the authority set Id ([Definition
  33](#defn-authority-list)) of the validator that created this message.

- \\A_s\\ is the signature of the validator issuing this message.

- \\c_a\\ is the certification of the assignment.

- \\c_k\\ is a varying datatype where *0* indicates an assignment based
  on the VRF that authorized the relay chain block where the candidate
  was included, followed by a sample number, \\s\\. *1* indicates an
  assignment story based on the VRF that authorized the relay chain
  block where the candidate was included combined with the index of a
  particular core. This is described further in [Section
  8.5](#sect-approval-voting).

- \\P_o\\ is a VRF output and \\P_p\\ its corresponding proof.

</div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-request-response" class="anchor"></a><a href="#id-request-response" class="link">8.7.2. Request &amp;
Response</a>

<div class="paragraph">

The request & response network messages are sent and received between
peers in the Polkadot network, including collators and non-validator
nodes. Those messages are conducted on the request-response substreams
([Section 4.5](#sect-connection-establishment)). The network messages
are SCALE encoded as described in Section ?.

</div>

<div id="net-msg-pov-fetching-request" class="exampleblock">

<div class="title">

Definition 120. [PoV Fetching Request](#net-msg-pov-fetching-request)

</div>

<div class="content">

<div class="paragraph">

The PoV fetching request is sent by clients who want to retrieve a PoV
block from a node. The request is a datastructure of the following
format:

</div>

<div class="stemblock">

<div class="content">

\\C_h\\

</div>

</div>

<div class="paragraph">

where \\C_h\\ is the 256-bit hash of the PoV block. The response message
is defined in [Definition 121](#net-msg-pov-fetching-response).

</div>

</div>

</div>

<div id="net-msg-pov-fetching-response" class="exampleblock">

<div class="title">

Definition 121. [PoV Fetching Response](#net-msg-pov-fetching-response)

</div>

<div class="content">

<div class="paragraph">

The PoV fetching response is sent by nodes to the clients who issued a
PoV fetching request ([Definition 120](#net-msg-pov-fetching-request)).
The response, \\R\\, is a varying datatype of the following format:

</div>

<div class="stemblock">

<div class="content">

\\R = {(0,-\>,B),(1,-\>,phi):}\\

</div>

</div>

<div class="paragraph">

where *0* is followed by the PoV block and *1* indicates that the PoV
block was not found.

</div>

</div>

</div>

<div id="net-msg-chunk-fetching-request" class="exampleblock">

<div class="title">

Definition 122. [Chunk Fetching
Request](#net-msg-chunk-fetching-request)

</div>

<div class="content">

<div class="paragraph">

The chunk fetching request is sent by clients who want to retrieve
chunks of a parachain candidate. The request is a datastructure of the
following format:

</div>

<div class="stemblock">

<div class="content">

\\(C_h,i)\\

</div>

</div>

<div class="paragraph">

where \\C_h\\ is the 256-bit hash of the parachain candidate and \\i\\
is a 32-bit unsigned integer indicating the index of the chunk to fetch.
The response message is defined in [Definition
123](#net-msg-chunk-fetching-response).

</div>

</div>

</div>

<div id="net-msg-chunk-fetching-response" class="exampleblock">

<div class="title">

Definition 123. [Chunk Fetching
Response](#net-msg-chunk-fetching-response)

</div>

<div class="content">

<div class="paragraph">

The chunk fetching response is sent by nodes to the clients who issued a
chunk fetching request ([Definition
122](#net-msg-chunk-fetching-request)). The response, \\R\\, is a
varying datatype of the following format:

</div>

<div class="stemblock">

<div class="content">

\\R = {(0,-\>,C_r),(1,-\>,phi):}\\ \\C_r = (c,c_p)\\

</div>

</div>

<div class="paragraph">

where *0* is followed by the chunk response, \\C_r\\ and *1* indicates
that the requested chunk was not found. \\C_r\\ contains the
erasure-encoded chunk of data belonging to the candidate block, \\c\\,
and \\c_p\\ is that chunks proof in the Merkle tree. Both \\c\\ and
\\c_p\\ are byte arrays of type \\(b_n…b_m)\\.

</div>

</div>

</div>

<div id="net-msg-available-data-request" class="exampleblock">

<div class="title">

Definition 124. [Available Data
Request](#net-msg-available-data-request)

</div>

<div class="content">

<div class="paragraph">

The available data request is sent by clients who want to retrieve the
PoV block of a parachain candidate. The request is a datastructure of
the following format:

</div>

<div class="stemblock">

<div class="content">

\\C_h\\

</div>

</div>

<div class="paragraph">

where \\C_h\\ is the 256-bit candidate hash to get the available data
for. The response message is defined in [Definition
125](#net-msg-available-data-response).

</div>

</div>

</div>

<div id="net-msg-available-data-response" class="exampleblock">

<div class="title">

Definition 125. [Available Data
Response](#net-msg-available-data-response)

</div>

<div class="content">

<div class="paragraph">

The available data response is sent by nodes to the clients who issued a
available data request ([Definition
124](#net-msg-available-data-request)). The response, \\R\\, is a
varying datatype of the following format:

</div>

<div class="stemblock">

<div class="content">

\\R = {(0,-\>,A),(1,-\>,phi):}\\ \\A = (P\_{ov},D\_{pv})\\

</div>

</div>

<div class="paragraph">

where *0* is followed by the available data, \\A\\, and *1* indicates
the the requested candidate hash was not found. \\P\_{ov}\\ is the PoV
block ([Definition 132](#defn-para-block)) and \\D\_{pv}\\ is the
persisted validation data ([Definition
227](#defn-persisted-validation-data)).

</div>

</div>

</div>

<div id="net-msg-collation-fetching-request" class="exampleblock">

<div class="title">

Definition 126. [Collation Fetching
Request](#net-msg-collation-fetching-request)

</div>

<div class="content">

<div class="paragraph">

The collation fetching request is sent by clients who want to retrieve
the advertised collation at the specified relay chain block. The request
is a datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\(B_h,P\_{id})\\

</div>

</div>

<div class="paragraph">

where \\B_h\\ is the hash of the relay chain block and \\P\_{id}\\ is
the parachain Id ([Definition 134](#defn-para-id)). The response message
is defined in [Definition 127](#net-msg-collation-fetching-response).

</div>

</div>

</div>

<div id="net-msg-collation-fetching-response" class="exampleblock">

<div class="title">

Definition 127. [Collation Fetching
Response](#net-msg-collation-fetching-response)

</div>

<div class="content">

<div class="paragraph">

The collation fetching response is sent by nodes to the clients who
issued a collation fetching request ([Definition
126](#net-msg-collation-fetching-request)). The response, \\R\\, is a
varying datatype of the following format:

</div>

<div class="stemblock">

<div class="content">

\\R = {(0,-\>,(C_r,B)):}\\

</div>

</div>

<div class="paragraph">

where \\0\\ is followed by the candidate receipt ([Definition
104](#defn-candidate-receipt)), \\C_r\\, as and the PoV block
([Definition 132](#defn-para-block)), \\B\\. This type does not notify
the client about a statement that was not found.

</div>

</div>

</div>

<div id="net-msg-statement-fetching-request" class="exampleblock">

<div class="title">

Definition 128. [Statement Fetching
Request](#net-msg-statement-fetching-request)

</div>

<div class="content">

<div class="paragraph">

The statement fetching request is sent by clients who want to retrieve
statements about a given candidate. The request is a datastructure of
the following format:

</div>

<div class="stemblock">

<div class="content">

\\(B_h,C_h)\\

</div>

</div>

<div class="paragraph">

where \\B_h\\ is the hash of the relay chain parent and \\C_h\\ is the
candidate hash that was used to create a committed candidate receipt
([Definition 105](#defn-committed-candidate-receipt)). The response
message is defined in [Definition
129](#net-msg-statement-fetching-response).

</div>

</div>

</div>

<div id="net-msg-statement-fetching-response" class="exampleblock">

<div class="title">

Definition 129. [Statement Fetching
Response](#net-msg-statement-fetching-response)

</div>

<div class="content">

<div class="paragraph">

The statement fetching response is sent by nodes to the clients who
issued a collation fetching request ([Definition
128](#net-msg-statement-fetching-request)). The response, \\R\\, is a
varying datatype of the following format:

</div>

<div class="stemblock">

<div class="content">

\\R = {(0,-\>,C_r):}\\

</div>

</div>

<div class="paragraph">

where \\C_r\\ is the committed candidate receipt ([Definition
105](#defn-committed-candidate-receipt)). No response is returned if no
statement is found.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#net-msg-dispute-request" class="anchor"></a><a href="#net-msg-dispute-request" class="link">8.7.2.1. Dispute
Request</a>

<div class="paragraph">

The dispute request is sent by clients who want to issue a dispute about
a candidate. The request, \\D_r\\, is a datastructure of the following
format:

</div>

<div class="stemblock">

<div class="content">

\\D_r = (C_r,S_i,I_v,V_v)\\ \\I_v = (A_i,A_s,k_i)\\ \\V_v =
(A_i,A_s,k_v)\\ \\k_i = {(0,-\>,phi):}\\ \\k_v =
{(0,-\>,phi),(1,-\>,C_h),(2,-\>,C_h),(3,-\>,phi):}\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\C_r\\ is the candidate that is being disputed. The structure is a
  candidate receipt ([Definition 104](#defn-candidate-receipt)).

- \\S_i\\ is an unsigned 32-bit integer indicating the session index the
  candidate appears in.

- \\I_v\\ is the invalid vote that makes up the request.

- \\V_v\\ is the valid vote that makes this dispute request valid.

- \\A_i\\ is an unsigned 32-bit integer indicating the validator index
  in the authority set ([Definition 33](#defn-authority-list)).

- \\A_s\\ is the signature of the validator.

- \\k_i\\ is a varying datatype and implies the dispute statement. *0*
  indicates an explicit statement.

- \\k_v\\ is a varying datatype and implies the dispute statement.

  <div class="ulist">

  - \\0\\ indicates an explicit statement.

  - \\1\\ indicates a seconded statement on a candidate, \\C_h\\, from
    the backing phase. \\C_h\\ is the hash of the candidate.

  - \\2\\ indicates a valid statement on a candidate, \\C_h\\, from the
    backing phase. \\C_h\\ is the hash of the candidate.

  - \\3\\ indicates an approval vote from the approval checking phase.

  </div>

</div>

</div>

<div class="paragraph">

The response message is defined in [Section
8.7.2.2](#net-msg-dispute-response).

</div>

</div>

<div class="sect4">

##### <a href="#net-msg-dispute-response" class="anchor"></a><a href="#net-msg-dispute-response" class="link">8.7.2.2. Dispute
Response</a>

<div class="paragraph">

The dispute response is sent by nodes to the clients who who issued a
dispute request ([Section 8.7.2.1](#net-msg-dispute-request)). The
response, \\R\\, is a varying type of the following format:

</div>

<div class="stemblock">

<div class="content">

\\R = {(0,-\>,phi):}\\

</div>

</div>

<div class="paragraph">

where \\0\\ indicates that the dispute was successfully processed.

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-anv-definitions" class="anchor"></a><a href="#sect-anv-definitions" class="link">8.8. Definitions</a>

<div id="defn-collator" class="exampleblock">

<div class="title">

Definition 130. [Collator](#defn-collator)

</div>

<div class="content">

<div class="paragraph">

A collator is a parachain node that sends parachain blocks, known as
candidates ([Definition 131](#defn-candidate)), to the relay chain
validators. The relay chain validators are not concerned how the
collator works or how it creates candidates.

</div>

</div>

</div>

<div id="defn-candidate" class="exampleblock">

<div class="title">

Definition 131. [Candidate](#defn-candidate)

</div>

<div class="content">

<div class="paragraph">

A candidate is a submitted parachain block ([Definition
132](#defn-para-block)) to the relay chain validators. A parachain block
stops being referred to as a candidate as soon it has been finalized.

</div>

</div>

</div>

<div id="defn-para-block" class="exampleblock">

<div class="title">

Definition 132. [Parachain Block](#defn-para-block)

</div>

<div class="content">

<div class="paragraph">

A parachain block or a Proof-of-Validity block (PoV block) contains the
necessary data for the parachain specific state transition logic. Relay
chain validators are not concerned with the inner structure of the block
and treat it as a byte array.

</div>

</div>

</div>

<div id="defn-head-data" class="exampleblock">

<div class="title">

Definition 133. [Head Data](#defn-head-data)

</div>

<div class="content">

<div class="paragraph">

The head data is contains information about a parachain block
([Definition 132](#defn-para-block)). The head data is returned by
executing the parachain Runtime and relay chain validators are not
concerned with its inner structure and treat it as a byte arrays.

</div>

</div>

</div>

<div id="defn-para-id" class="exampleblock">

<div class="title">

Definition 134. [Parachain Id](#defn-para-id)

</div>

<div class="content">

<div class="paragraph">

The Parachain Id is a unique, unsigned 32-bit integer which serves as an
identifier of a parachain, assigned by the Runtime.

</div>

</div>

</div>

<div id="defn-availability-core" class="exampleblock">

<div class="title">

Definition 135. [Availability Core](#defn-availability-core)

</div>

<div class="content">

<div class="paragraph">

Availability cores are slots used to process parachains. The Runtime
assigns each parachain to a availability core and validators can fetch
information about the cores, such as parachain block candidates, by
calling the appropriate Runtime API ([Section
C.9.3](#sect-rt-api-availability-cores)). Validators are not concerned
with the internal workings from the Runtimes perspective.

</div>

</div>

</div>

<div id="defn-validator-groups" class="exampleblock">

<div class="title">

Definition 136. [Validator Groups](#defn-validator-groups)

</div>

<div class="content">

<div class="paragraph">

Validator groups indicate which validators are responsible for creating
backable candidates for parachains ([Section
8.2](#sect-candidate-backing)), and are assigned by the Runtime
([Section C.9.2](#sect-rt-api-validator-groups)). Validators are not
concerned with the internal workings from the Runtimes perspective.
Collators can use this information for submitting blocks.

</div>

</div>

</div>

<div id="defn-upward-message" class="exampleblock">

<div class="title">

Definition 137. [Upward Message](#defn-upward-message)

</div>

<div class="content">

<div class="paragraph">

An upward message is an opaque byte array sent from a parachain to a
relay chain.

</div>

</div>

</div>

<div id="defn-downward-message" class="exampleblock">

<div class="title">

Definition 138. [Downward Message](#defn-downward-message)

</div>

<div class="content">

<div class="paragraph">

A downward message is an opaque byte array received by the parachain
from the relay chain.

</div>

</div>

</div>

<div id="defn-outbound-hrmp-message" class="exampleblock">

<div class="title">

Definition 139. [Outbound HRMP Message](#defn-outbound-hrmp-message)

</div>

<div class="content">

<div class="paragraph">

An outbound HRMP message (Horizontal Relay-routed Message Passing) is
sent from the perspective of a sender of a parachain to an other
parachain by passing it through the relay chain. It’s a datastructure of
the following format:

</div>

<div class="stemblock">

<div class="content">

\\(I,M)\\

</div>

</div>

<div class="paragraph">

where \\I\\ is the recipient Id ([Definition 134](#defn-para-id)) and
\\M\\ is an upward message ([Definition 137](#defn-upward-message)).

</div>

</div>

</div>

<div id="defn-inbound-hrmp-message" class="exampleblock">

<div class="title">

Definition 140. [Inbound HRMP Message](#defn-inbound-hrmp-message)

</div>

<div class="content">

<div class="paragraph">

An inbound HRMP message (Horizontal Relay-routed Message Passing) is
seen from the perspective of a recipient parachain sent from an other
parachain by passing it through the relay chain. It’s a datastructure of
the following format:

</div>

<div class="stemblock">

<div class="content">

\\(N,M)\\

</div>

</div>

<div class="paragraph">

where \\N\\ is the unsigned 32-bit integer indicating the relay chain
block number at which the message was passed down to the recipient
parachain and \\M\\ is a downward message ([Definition
138](#defn-downward-message)).

</div>

</div>

</div>

<div id="defn-bitfield-array" class="exampleblock">

<div class="title">

Definition 141. [Bitfield Array](#defn-bitfield-array)

</div>

<div class="content">

<div class="paragraph">

A bitfield array contains single-bit values which indidate whether a
candidate is available. The number of items is equal of to the number of
availability cores ([Definition 135](#defn-availability-core)) and each
bit represents a vote on the corresponding core in the given order.
Respectively, if the single bit equals 1, then the Polkadot validator
claims that the availability core is occupied, there exists a committed
candidate receipt ([Definition 105](#defn-committed-candidate-receipt))
and that the validator has a stored chunk of the parachain block
([Definition 132](#defn-para-block)).

</div>

</div>

</div>

</div>

</div>

</div>

# <a href="#part-polkadot-runtime" class="anchor"></a><a href="#part-polkadot-runtime" class="link">Polkadot Runtime</a>

<div class="openblock partintro">

<div class="content">

Description of various useful Runtime internals

</div>

</div>

<div class="sect1">

## <a href="#id-extrinsics" class="anchor"></a><a href="#id-extrinsics" class="link">9. Extrinsics</a>

<div class="sectionbody">

<div class="sect2">

### <a href="#id-introduction-5" class="anchor"></a><a href="#id-introduction-5" class="link">9.1. Introduction</a>

<div class="paragraph">

An extrinsic is a SCALE encoded array consisting of a version number,
signature, and varying data types indicating the resulting Runtime
function to be called, including the parameters required for that
function to be executed.

</div>

</div>

<div class="sect2">

### <a href="#id-preliminaries-3" class="anchor"></a><a href="#id-preliminaries-3" class="link">9.2. Preliminaries</a>

<div id="defn-extrinsic" class="exampleblock">

<div class="title">

Definition 142. Extrinsic

</div>

<div class="content">

<div class="paragraph">

An extrinsic , \\tx\\, is a tuple consisting of the extrinsic version,
\\T_v\\ ([Definition 143](#defn-extrinsic-version)), and the body of the
extrinsic, \\T_b\\.

</div>

<div class="stemblock">

<div class="content">

\\tx := (T_v, T_b)\\

</div>

</div>

<div class="paragraph">

The value of \\T_b\\ varies for each version. The current version 4 is
described in [Section 9.3.1](#sect-version-four).

</div>

</div>

</div>

<div id="defn-extrinsic-version" class="exampleblock">

<div class="title">

Definition 143. Extrinsic Version

</div>

<div class="content">

<div class="paragraph">

\\T_v\\ is a 8-bit bitfield and defines the extrinsic version. The
required format of an extrinsic body, \\T_b\\, is dictated by the
Runtime. Older or unsupported version are rejected.

</div>

<div class="paragraph">

The most significant bit of \\T_v\\ indicates whether the transaction is
**signed** (\\1\\) or **unsigned** (\\0\\). The remaining 7-bits
represent the version number. As an example, for extrinsic format
version 4, an signed extrinsic represents \\T_v\\ as `132` while a
unsigned extrinsic represents it as `4`.

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#id-extrinsics-body" class="anchor"></a><a href="#id-extrinsics-body" class="link">9.3. Extrinsics Body</a>

<div class="sect3">

#### <a href="#sect-version-four" class="anchor"></a><a href="#sect-version-four" class="link">9.3.1. Version 4</a>

<div class="paragraph">

Version 4 of the Polkadot extrinsic format is defined as follows:

</div>

<div class="stemblock">

<div class="content">

\\T_b := (A_i, Sig, E, M_i, F_i(m))\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\A_i\\: the 32-byte address of the sender ([Definition
  144](#defn-extrinsic-address)).

- \\Sig\\: the signature of the sender ([Definition
  145](#defn-extrinsic-signature)).

- \\E\\: the extra data for the extrinsic ([Definition
  146](#defn-extra-data)).

- \\M_i\\: the indicator of the Polkadot module ([Definition
  147](#defn-module-indicator)).

- \\F_i(m)\\: the indicator of the function of the Polkadot module
  ([Definition 148](#defn-function-indicator)).

</div>

</div>

<div id="defn-extrinsic-address" class="exampleblock">

<div class="title">

Definition 144. Extrinsic Address

</div>

<div class="content">

<div class="paragraph">

Account Id, \\A_i\\, is the 32-byte address of the sender of the
extrinsic as described in the [external SS58 address
format](https://github.com/paritytech/substrate/wiki/External-Address-Format-(SS58)).

</div>

</div>

</div>

<div id="defn-extrinsic-signature" class="exampleblock">

<div class="title">

Definition 145. Extrinsic Signature

</div>

<div class="content">

<div class="paragraph">

The signature, \\Sig\\, is a varying data type indicating the used
signature type, followed by the signature created by the extrinsic
author. The following types are supported:

</div>

<div class="stemblock">

<div class="content">

\\Sig := \begin{cases} 0, & \text{Ed25519, followed by: } (b_0,
...,b\_{63}) \\ 1, & \text{Sr25519, followed by: } (b_0, ...,b\_{63}) \\
2, & \text{Ecdsa, followed by: } (b_0, ...,b\_{64}) \end{cases}\\

</div>

</div>

<div class="paragraph">

Signature types vary in sizes, but each individual type is always
fixed-size and therefore does not contain a length prefix. `Ed25519` and
`Sr25519` signatures are 512-bit while `Ecdsa` is 520-bit, where the
last 8 bits are the recovery ID.

</div>

<div class="paragraph">

The signature is created by signing payload \\P\\.

</div>

<div class="stemblock">

<div class="content">

\\\begin{aligned} P &:= \begin{cases} Raw, & \text{if } \|Raw\| \leq 256
\\ Blake2(Raw), & \text{if } \|Raw\| \> 256 \\ \end{cases} \\ Raw &:=
(M_i, F_i(m), E, R_v, F_v, H_h(G), H_h(B)) \\ \end{aligned}\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\M_i\\: the module indicator ([Definition
  147](#defn-module-indicator)).

- \\F_i(m)\\: the function indicator of the module ([Definition
  148](#defn-function-indicator)).

- \\E\\: the extra data ([Definition 146](#defn-extra-data)).

- \\R_v\\: a UINT32 containing the specification version
  (`spec_version`) of the Runtime ([Section
  C.4.1](#defn-rt-core-version)), which can be updated and is therefore
  subject to change.

- \\F_v\\: a UINT32 containing the transaction version
  (`transaction_version`) of the Runtime ([Section
  C.4.1](#defn-rt-core-version)), which can be updated and is therefore
  subject to change.

- \\H_h(G)\\: a 32-byte array containing the genesis hash.

- \\H_h(B)\\: a 32-byte array containing the hash of the block which
  starts the mortality period, as described in [Definition
  149](#defn-extrinsic-mortality).

</div>

</div>

</div>

</div>

<div id="defn-extra-data" class="exampleblock">

<div class="title">

Definition 146. Extra Data

</div>

<div class="content">

<div class="paragraph">

Extra data, \\E\\, is a tuple containing additional meta data about the
extrinsic and the system it is meant to be executed in.

</div>

<div class="stemblock">

<div class="content">

\\E := (T\_{mor}, N, P_t)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\T\_{mor}\\: contains the SCALE encoded mortality of the extrinsic
  ([Definition 149](#defn-extrinsic-mortality)).

- \\N\\: a compact integer containing the nonce of the sender. The nonce
  must be incremented by one for each extrinsic created, otherwise the
  Polkadot network will reject the extrinsic.

- \\P_t\\: a compact integer containing the transactor pay including
  tip.

</div>

</div>

</div>

</div>

<div id="defn-module-indicator" class="exampleblock">

<div class="title">

Definition 147. Module Indicator

</div>

<div class="content">

<div class="paragraph">

\\M_i\\ is an indicator for the Runtime to which Polkadot *module*,
\\m\\, the extrinsic should be forwarded to.

</div>

<div class="paragraph">

\\M_i\\ is a varying data type pointing to every module exposed to the
network.

</div>

<div class="stemblock">

<div class="content">

\\M_i := \begin{cases} 0, & \text{System} \\ 1, & \text{Utility} \\ ...
& \\ 7, & \text{Balances} \\ ... & \end{cases}\\

</div>

</div>

</div>

</div>

<div id="defn-function-indicator" class="exampleblock">

<div class="title">

Definition 148. Function Indicator

</div>

<div class="content">

<div class="paragraph">

\\F_i(m)\\ is a tuple which contains an indicator, \\m_i\\, for the
Runtime to which *function* within the Polkadot *module*, \\m\\, the
extrinsic should be forwarded to. This indicator is followed by the
concatenated and SCALE encoded parameters of the corresponding function,
\\params\\.

</div>

<div class="stemblock">

<div class="content">

\\F_i(m) := (m_i, params)\\

</div>

</div>

<div class="paragraph">

The value of \\m_i\\ varies for each Polkadot module, since every module
offers different functions. As an example, the `Balances` module has the
following functions:

</div>

<div class="stemblock">

<div class="content">

\\Balances_i := \begin{cases} 0, & \text{transfer} \\ 1, &
\text{set_balance} \\ 2, & \text{force_transfer} \\ 3, &
\text{transfer_keep_alive} \\ ... & \end{cases}\\

</div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-mortality" class="anchor"></a><a href="#id-mortality" class="link">9.3.2. Mortality</a>

<div id="defn-extrinsic-mortality" class="exampleblock">

<div class="title">

Definition 149. Extrinsic Mortality

</div>

<div class="content">

<div class="paragraph">

Extrinsic **mortality** is a mechanism which ensures that an extrinsic
is only valid within a certain period of the ongoing Polkadot lifetime.
Extrinsics can also be immortal, as clarified in [Section
9.3.2.2](#sect-mortality-encoding).

</div>

<div class="paragraph">

The mortality mechanism works with two related values:

</div>

<div class="ulist">

- \\M\_{per}\\: the period of validity in terms of block numbers from
  the block hash specified as \\H_h(B)\\ in the payload ([Definition
  145](#defn-extrinsic-signature)). The requirement is \\M\_{per} \geq
  4\\ and \\M\_{per}\\ must be the power of two, such as `32`, `64`,
  `128`, etc.

- \\M\_{pha}\\: the phase in the period that this extrinsic’s lifetime
  begins. This value is calculated with a formula and validators can use
  this value in order to determine which block hash is included in the
  payload. The requirement is \\M\_{pha} \< M\_{per}\\.

</div>

<div class="paragraph">

In order to tie a transaction’s lifetime to a certain block (\\H_i(B)\\)
after it was issued, without wasting precious space for block hashes,
block numbers are divided into regular periods and the lifetime is
instead expressed as a "phase" (\\M\_{pha}\\) from these regular
boundaries:

</div>

<div class="stemblock">

<div class="content">

\\M\_{pha} = H_i(B)\\ mod\\ M\_{per}\\

</div>

</div>

<div class="paragraph">

\\M\_{per}\\ and \\M\_{pha}\\ are then included in the extrinsic, as
clarified in [Definition 146](#defn-extra-data), in the SCALE encoded
form of \\T\_{mor}\\ ([Section 9.3.2.2](#sect-mortality-encoding)).
Polkadot validators can use \\M\_{pha}\\ to figure out the block hash
included in the payload, which will therefore result in a valid
signature if the extrinsic is within the specified period or an invalid
signature if the extrinsic "died".

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-example" class="anchor"></a><a href="#id-example" class="link">9.3.2.1. Example</a>

<div class="paragraph">

The extrinsic author choses \\M\_{per} = 256\\ at block `10'000`,
resulting with \\M\_{pha} = 16\\. The extrinsic is then valid for blocks
ranging from `10'000` to `10'256`.

</div>

</div>

<div class="sect4">

##### <a href="#sect-mortality-encoding" class="anchor"></a><a href="#sect-mortality-encoding" class="link">9.3.2.2. Encoding</a>

<div class="paragraph">

\\T\_{mor}\\ refers to the SCALE encoded form of type \\M\_{per}\\ and
\\M\_{pha}\\. \\T\_{mor}\\ is the size of two bytes if the extrinsic is
considered mortal, or simply one bytes with the value equal to zero if
the extrinsic is considered immortal.

</div>

<div class="stemblock">

<div class="content">

\\T\_{mor} := Enc\_{SC}(M\_{per}, M\_{pha})\\

</div>

</div>

<div class="paragraph">

The SCALE encoded representation of mortality \\T\_{mor}\\ deviates from
most other types, as it’s specialized to be the smallest possible value,
as described in [Encode Mortality](#algo-mortality-encode) and [Decode
Mortality](#algo-mortality-decode).

</div>

<div class="paragraph">

If the extrinsic is immortal, specify a single byte with the value equal
to zero.

</div>

<div class="sidebarblock">

<div class="content">

\Require{\$M\_{per}, M\_{pha}\$} \Return \$0 \enspace \textbf{if}
\enspace \textit{extrinsic is immortal}\$ \State \textbf{init} \$factor
= \$\call{Limit}{\$M\_{per} \>\> 12, 1, \phi\$} \State \textbf{init}
\$left = \$\call{Limit}{\call{TZ}{\$M\_{per}\$}\$ - 1, 1, 15\$} \State
\textbf{init} \$right = \frac{M\_{pha}}{factor} \<\< 4\$ \Return
\$left\|right\$ \Require{\$T\_{mor}\$} \Return \$\textit{Immortal}
\enspace \textbf{if} \enspace T^{b0}\_{mor} = 0\$ \State \textbf{init}
\$enc = T^{b0}\_{mor} + (T^{b1}\_{mor} \<\< 8)\$ \State \textbf{init}
\$M\_{per} = 2 \<\< (enc\\ mod\\ (1 \<\< 4))\$ \State \textbf{init}
\$factor =\$ \call{Limit}{\$M\_{per} \>\> 12, 1, \phi\$} \State
\textbf{init} \$M\_{pha} = (enc \>\> 4) \* factor\$ \Return \$(M\_{per},
M\_{pha})\$

<div class="dlist">

where  
<div class="ulist">

- \\T^{b0}\_{mor}\\: the first byte of \\T\_{mor}\\.

- \\T^{b1}\_{mor}\\: the second byte of \\T\_{mor}\\.

- Limit(\\num\\, \\min\\, \\max\\): Ensures that \\num\\ is between
  \\min\\ and \\max\\. If \\min\\ or \\max\\ is defined as \\\phi\\,
  then there is no requirement for the specified minimum/maximum.

- TZ(\\num\\): returns the number of trailing zeros in the binary
  representation of \\num\\. For example, the binary representation of
  `40` is `0010 1000`, which has three trailing zeros.

- \\\>\>\\: performs a binary right shift operation.

- \\\<\<\\: performs a binary left shift operation.

- \\\|\\ : performs a bitwise OR operation.

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#id-weights" class="anchor"></a><a href="#id-weights" class="link">10. Weights</a>

<div class="sectionbody">

<div class="sect2">

### <a href="#id-motivation" class="anchor"></a><a href="#id-motivation" class="link">10.1. Motivation</a>

<div class="paragraph">

The Polkadot network, like any other permissionless system, needs to
implement a mechanism to measure and to limit the usage in order to
establish an economic incentive structure, to prevent the network
overload, and to mitigate DoS vulnerabilities. In particular, Polkadot
enforces a limited time-window for block producers to create a block,
including limitations on block size, which can make the selection and
execution of certain extrinsics too expensive and decelerate the
network.

</div>

<div class="paragraph">

In contrast to some other systems such as Ethereum which implement fine
measurement for each executed low-level operation by smart contracts,
known as gas metering, Polkadot takes a more relaxed approach by
implementing a measuring system where the cost of the transactions
(referred to as ’extrinsics’) are determined before execution and are
known as the weight system.

</div>

<div class="paragraph">

The Polkadot weight system introduces a mechanism for block producers to
measure the cost of running the extrinsics and determine how "heavy" it
is in terms of execution time. Within this mechanism, block producers
can select a set of extrinsics and saturate the block to its fullest
potential without exceeding any limitations (as described in [Section
10.2.1](#sect-limitations)). Moreover, the weight system can be used to
calculate a fee for executing each extrinsics according to its weight
(as described in [Section 10.6.1](#sect-fee-calculation)).

</div>

<div class="paragraph">

Additionally, Polkadot introduces a specified block ratio (as defined in
[Section 10.2.1](#sect-limitations)), ensuring that only a certain
portion of the total block size gets used for regular extrinsics. The
remaining space is reserved for critical, operational extrinsics
required for the functionality by Polkadot itself.

</div>

<div class="paragraph">

To begin, we introduce in [Section 10.2](#sect-assumptions) the
assumption upon which the Polkadot transaction weight system is
designed. In [Section 10.2.1](#sect-limitations), we discuss the
limitation Polkadot needs to enforce on the block size. In [Section
10.3](#sect-runtime-primitives), we describe in detail the procedure
upon which the weight of any transaction should be calculated. In
[Section 10.5](#sect-practical-examples), we present how we apply this
procedure to compute the weight of particular runtime functions.

</div>

</div>

<div class="sect2">

### <a href="#sect-assumptions" class="anchor"></a><a href="#sect-assumptions" class="link">10.2. Assumptions</a>

<div class="paragraph">

In this section, we define the concept of weight and we discuss the
considerations that need to be accounted for when assigning weight to
transactions. These considerations are essential in order for the weight
system to deliver its fundamental mission, i.e. the fair distribution of
network resources and preventing a network overload. In this regard,
weights serve as an indicator on whether a block is considered full and
how much space is left for remaining, pending extrinsics. Extrinsics
which require too many resources are discarded. More formally, the
weight system should:

</div>

<div class="ulist">

- prevent the block from being filled with too many extrinsics

- avoid extrinsics where its execution takes too long, by assigning a
  transaction fee to each extrinsic proportional to their resource
  consumption.

</div>

<div class="paragraph">

These concepts are formalized in [Definition 150](#defn-block-length)
and [Definition 153](#defn-polkadot-block-limits):

</div>

<div id="defn-block-length" class="exampleblock">

<div class="title">

Definition 150. Block Length

</div>

<div class="content">

<div class="paragraph">

For a block \\B\\ with \\Head(B)\\ and \\Body(B)\\ the block length of
\\B\\, \\Len(B)\\, is defined as the amount of raw bytes of \\B\\.

</div>

</div>

</div>

<div id="defn-target-time-per-block" class="exampleblock">

<div class="title">

Definition 151. Target Time per Block

</div>

<div class="content">

<div class="paragraph">

Ṯargeted time per block denoted by \\T(B)\\ implies the amount of
seconds that a new block should be produced by a validator. The
transaction weights must consider \\T(B)\\ in order to set restrictions
on time intensive transactions in order to saturate the block to its
fullest potential until \\T(B)\\ is reached.

</div>

</div>

</div>

<div id="def:block-target-time" class="exampleblock">

<div class="title">

Definition 152. Block Target Time

</div>

<div class="content">

<div class="paragraph">

Available block ration reserved for normal, noted by \\R(B)\\, is
defined as the maximum weight of none-operational transactions in the
Body of \\B\\ divided by \\Len(B)\\.

</div>

</div>

</div>

<div id="defn-polkadot-block-limits" class="exampleblock">

<div class="title">

Definition 153. Block Limits

</div>

<div class="content">

<div class="paragraph">

P̱olkadot block limits as defined here should be respected by each block
producer for the produced block \\B\\ to be deemed valid:

</div>

<div class="ulist">

- \\Len(B) \le 5 \times 1'024 \times 1'024 = 5'242'880\\ Bytes

- \\T(B) = 6\\ seconds\\

- \\R(B) \le 0.75\\

</div>

</div>

</div>

<div id="defn:weight-function" class="exampleblock">

<div class="title">

Definition 154. Weight Function

</div>

<div class="content">

<div class="paragraph">

The P̱olkadot transaction weight function denoted by \\\mathcal{W}\\ as
follows:

</div>

<div class="stemblock">

<div class="content">

\\\begin{aligned} \mathcal{W} &: \mathcal{E} \rightarrow \mathbb{N} \\
\mathcal{W} &: E \mapsto w \end{aligned}\\

</div>

</div>

<div class="paragraph">

where \\w\\ is a non-negative integer representing the weight of the
extrinsic \\E\\. We define the weight of all inherent extrinsics as
defined in the [Section 2.3.3](#sect-inherents) to be equal to 0. We
extend the definition of \\\mathcal{W}\\ function to compute the weight
of the block as sum of weight of all extrinsics it includes:

</div>

<div class="stemblock">

<div class="content">

\\\begin{aligned} \mathcal{W} &: \mathcal{B}\rightarrow \mathbb{N} \\
\mathcal{W} &: B \mapsto \sum\_{E\in B}(W(E)) \end{aligned}\\

</div>

</div>

</div>

</div>

<div class="paragraph">

In the remainder of this section, we discuss the requirements to which
the weight function needs to comply to.

</div>

<div class="ulist">

- Computations of function \\\mathcal{W}(E)\\ must be determined before
  execution of that \\E\\.

- Due to the limited time window, computations of \\\mathcal{W}\\ must
  be done quickly and consume few resources themselves.

- \\\mathcal{W}\\ must be self contained and must not require I/O on the
  chain state. \\\mathcal{W}(E)\\ must depend solely on the Runtime
  function representing \\E\\ and its parameters.

</div>

<div class="paragraph">

Heuristically, "heaviness" corresponds to the execution time of an
extrinsic. In that way, the \\\mathcal{W}\\ value for various extrinsics
should be proportional to their execution time. For example, if
Extrinsic A takes three times longer to execute than Extrinsic B, then
Extrinsic A should roughly weighs 3 times of Extrinsic B. Or:

</div>

<div class="stemblock">

<div class="content">

\\\mathcal{W}(A) \approx 3 \times \mathcal{W}(B)\\

</div>

</div>

<div class="paragraph">

Nonetheless, \\\mathcal{W}(E)\\ can be manipulated depending on the
priority of \\E\\ the chain is supposed to endorse.

</div>

<div class="sect3">

#### <a href="#sect-limitations" class="anchor"></a><a href="#sect-limitations" class="link">10.2.1. Limitations</a>

<div class="paragraph">

In this section we discuss how applying the limitation defined in
[Definition 153](#defn-polkadot-block-limits) can be translated to
limitation \\\mathcal{W}\\. In order to be able to translate those into
concrete numbers, we need to identify an arbitrary maximum weight to
which we scale all other computations. For that we first define the
block weight and then assume a maximum on it block length in [Definition
155](#defn-block-weight):

</div>

<div id="defn-block-weight" class="exampleblock">

<div class="title">

Definition 155. Block Weight

</div>

<div class="content">

<div class="paragraph">

We define the block weight of block \\B\\, formally denoted as
\\\mathcal{W}(B)\\, to be:

</div>

<div class="stemblock">

<div class="content">

\\\mathcal{W}(B) = \sum^{\|\mathcal{E}\|}\_{n = 0} (W(E_n))\\

</div>

</div>

<div class="paragraph">

We require that:

</div>

<div class="stemblock">

<div class="content">

\\\mathcal{W}(B) \< 2'000'000'000'000\\

</div>

</div>

</div>

</div>

<div class="paragraph">

The weights must fulfill the requirements as noted by the fundamentals
and limitations, and can be assigned as the author sees fit. As a simple
example, consider a maximum block weight of 1’000’000’000, an available
ratio of 75% and a targeted transaction throughput of 500 transactions,
we could assign the (average) weight for each transaction at about
1’500’000. Block producers have economic incentive to include as many
extrinsics as possible (without exceeding limitations) into a block
before reaching the targeted block time. Weights give indicators to
block producers on which extrinsics to include in order to reach the
blocks fullest potential.

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-runtime-primitives" class="anchor"></a><a href="#sect-runtime-primitives" class="link">10.3. Calculation of the
weight function</a>

<div class="paragraph">

In order to calculate weight of block \\B\\, \\\mathcal{W}(B)\\, one
needs to evaluate the weight of each transaction included in the block.
Each transaction causes the execution certain Runtime functions. As
such, to calculate the weight of a transaction, those functions must be
analyzed in order to determine parts of the code which can significantly
contribute to the execution time and consume resources such as loops,
I/O operations, and data manipulation. Subsequently the performance and
execution time of each part will be evaluated based on variety of input
parameters. Based on those observations, weights are assigned Runtime
functions or parameters which contribute to long execution times. These
sub component of the code are discussed in [Section
10.4.1](#sect-primitive-types).

</div>

<div class="paragraph">

The general algorithm to calculate \\\mathcal{W}(E)\\ is described in
the [Section 10.4](#sect-benchmarking).

</div>

</div>

<div class="sect2">

### <a href="#sect-benchmarking" class="anchor"></a><a href="#sect-benchmarking" class="link">10.4. Benchmarking</a>

<div class="paragraph">

Calculating the extrinsic weight solely based on theoretical complexity
of the underlying implementation proves to be too complicated and
unreliable at the same time. Certain decisions in the source code
architecture, internal communication within the Runtime or other design
choices could add enough overhead to make the asymptotic complexity
practically meaningless.

</div>

<div class="paragraph">

On the other hand, benchmarking an extrinsics in a black-box fashion
could (using random parameters) most centainly results in missing corner
cases and worst case scenarios. Instead, we benchmark all available
Runtime functions which are invoked in the course of execution of
extrinsics with a large collection of carefully selected input
parameters and use the result of the benchmarking process to evaluate
\\\mathcal{W}(E)\\.

</div>

<div class="paragraph">

In order to select useful parameters, the Runtime functions have to be
analyzed to fully understand which behaviors or conditions can result in
expensive execution times, which is described closer in [Section
10.4.1](#sect-primitive-types). Not every possible benchmarking outcome
can be invoked by varying input parameters of the Runtime function. In
some circumstances, preliminary work is required before a specific
benchmark can be reliably measured, such as creating certain preexisting
entries in the storage or other changes to the environment.

</div>

<div class="paragraph">

The Practical Examples ([Section 10.5](#sect-practical-examples)) covers
the analysis process and the implementation of preliminary work in more
detail.

</div>

<div class="sect3">

#### <a href="#sect-primitive-types" class="anchor"></a><a href="#sect-primitive-types" class="link">10.4.1. Primitive Types</a>

<div class="paragraph">

The Runtime reuses components, known as "primitives", to interact with
the state storage. The execution cost of those primitives can be
measured and a weight should be applied for each occurrence within the
Runtime code.

</div>

<div class="paragraph">

For storage, Polkadot uses three different types of storage types across
its modules, depending on the context:

</div>

<div class="ulist">

- **Value**: Operations on a single value. The final key-value pair is
  stored under the key:

  <div class="listingblock">

  <div class="content">

          hash(module_prefix) + hash(storage_prefix)

  </div>

  </div>

- **Map**: Operations on multiple values, datasets, where each entry has
  its corresponding, unique key. The final key-value pair is stored
  under the key:

  <div class="listingblock">

  <div class="content">

          hash(module_prefix) + hash(storage_prefix) + hash(encode(key))

  </div>

  </div>

- **Double map**: Just like **Map**, but uses two keys instead of one.
  This type is also known as "child storage", where the first key is the
  "parent key" and the second key is the "child key". This is useful in
  order to scope storage entries (child keys) under a certain `context`
  (parent key), which is arbitrary. Therefore, one can have separated
  storage entries based on the context. The final key-value pair is
  stored under the key:

  <div class="listingblock">

  <div class="content">

          hash(module_prefix) + hash(storage_prefix)
            + hash(encode(key1)) + hash(encode(key2))

  </div>

  </div>

</div>

<div class="paragraph">

It depends on the functionality of the Runtime module (or its
sub-processes, rather) which storage type to use. In some cases, only a
single value is required. In others, multiple values need to be fetched
or inserted from/into the database.

</div>

<div class="paragraph">

Those lower level types get abstracted over in each individual Runtime
module using the `decl_storage!` macro. Therefore, each module specifies
its own types that are used as input and output values. The abstractions
do give indicators on what operations must be closely observed and where
potential performance penalties and attack vectors are possible.

</div>

<div class="sect4">

##### <a href="#sect-primitive-types-considerations" class="anchor"></a><a href="#sect-primitive-types-considerations" class="link">10.4.1.1.
Considerations</a>

<div class="paragraph">

The storage layout is mostly the same for every primitive type,
primarily differentiated by using special prefixes for the storage key.
Big differences arise on how the primitive types are used in the Runtime
function, on whether single values or entire datasets are being worked
on. Single value operations are generally quite cheap and its execution
time does not vary depending on the data that’s being processed.
However, excessive overhead can appear when I/O operations are executed
repeatedly, such as in loops. Especially, when the amount of loop
iterations can be influenced by the caller of the function or by certain
conditions in the state storage.

</div>

<div class="paragraph">

Maps, in contrast, have additional overhead when inserting or retrieving
datasets, which vary in sizes. Additionally, the Runtime function has to
process each item inside that list.

</div>

<div class="paragraph">

Indicators for performance penalties:

</div>

<div class="ulist">

- **Fixed iterations and datasets** - Fixed iterations and datasets can
  increase the overall cost of the Runtime functions, but the execution
  time does not vary depending on the input parameters or storage
  entries. A base Weight is appropriate in this case.

- **Adjustable iterations and datasets** - If the amount of iterations
  or datasets depend on the input parameters of the caller or specific
  entries in storage, then a certain weight should be applied for each
  (additional) iteration or item. The Runtime defines the maximum value
  for such cases. If it doesn’t, it unconditionally has to and the
  Runtime module must be adjusted. When selecting parameters for
  benchmarking, the benchmarks should range from the minimum value to
  the maximum value, as described in [Definition 156](#defn-max-value).

- **Input parameters** - Input parameters that users pass on to the
  Runtime function can result in expensive operations. Depending on the
  data type, it can be appropriate to add additional weights based on
  certain properties, such as data size, assuming the data type allows
  varying sizes. The Runtime must define limits on those properties. If
  it doesn’t, it unconditionally has to and the Runtime module must be
  adjusted. When selecting parameters for benchmarking, the benchmarks
  should range from the minimum values to the maximum value, as
  described in paragraph [Definition 156](#defn-max-value).

</div>

<div id="defn-max-value" class="exampleblock">

<div class="title">

Definition 156. Maximum Value

</div>

<div class="content">

<div class="paragraph">

What the maximum value should be really depends on the functionality
that the Runtime function is trying to provide. If the choice for that
value is not obvious, then it’s advised to run benchmarks on a big range
of values and pick a conservative value below the
`targeted time per block` limit as described in section [Section
10.2.1](#sect-limitations).

</div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-parameters" class="anchor"></a><a href="#id-parameters" class="link">10.4.2. Parameters</a>

<div class="paragraph">

The inputs parameters highly vary depending on the Runtime function and
must therefore be carefully selected. The benchmarks should use input
parameters which will most likely be used in regular cases, as intended
by the authors, but must also consider worst case scenarios and inputs
which might decelerate or heavily impact performance of the function.
The input parameters should be randomized in order to cause various
effects in behaviors on certain values, such as memory relocations and
other outcomes that can impact performance.

</div>

<div class="paragraph">

It’s not possible to benchmark every single value. However, one should
select a range of inputs to benchmark, spanning from the minimum value
to the maximum value which will most likely exceed the expected usage of
that function. This is described in more detail in [Section
10.4.1.1](#sect-primitive-types-considerations). The benchmarks should
run individual executions/iterations within that range, where the chosen
parameters should give insight on the execution time. Selecting
imprecise parameters or too extreme ranges might indicate an inaccurate
result of the function as it will be used in production. Therefore, when
a range of input parameters gets benchmarked, the result of each
individual parameter should be recorded and optionally visualized, then
the necessary adjustment can be made. Generally, the worst case scenario
should be assigned as the weight value for the corresponding runtime
function.

</div>

<div class="paragraph">

Additionally, given the distinction theoretical and practical usage, the
author reserves the right to make adjustments to the input parameters
and assigned weights according to the observed behavior of the actual,
real-world network.

</div>

<div class="sect4">

##### <a href="#id-weight-refunds" class="anchor"></a><a href="#id-weight-refunds" class="link">10.4.2.1. Weight Refunds</a>

<div class="paragraph">

When assigning the final weight, the worst case scenario of each runtime
function should be used. The runtime can then additional "refund" the
amount of weights which were overestimated once the runtime function is
actually executed.

</div>

<div class="paragraph">

The Polkadot runtime only returns weights if the difference between the
assigned weight and the actual weight calculated during execution is
greater than 20%.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-storage-io-cost" class="anchor"></a><a href="#id-storage-io-cost" class="link">10.4.3. Storage I/O cost</a>

<div class="paragraph">

It is advised to benchmark the raw I/O operations of the database and
assign "base weights" for each I/O operation type, such as insertion,
deletion, querying, etc. When a runtime function is executed, the
runtime can then add those base weights of each used operation in order
to calculate the final weight.

</div>

</div>

<div class="sect3">

#### <a href="#id-environment" class="anchor"></a><a href="#id-environment" class="link">10.4.4. Environment</a>

<div class="paragraph">

The benchmarks should be executed on clean systems without interference
of other processes or software. Additionally, the benchmarks should be
executed on multiple machines with different system resources, such as
CPU performance, CPU cores, RAM and storage speed.

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-practical-examples" class="anchor"></a><a href="#sect-practical-examples" class="link">10.5. Practical
examples</a>

<div class="paragraph">

This section walks through Runtime functions available in the Polkadot
Runtime to demonstrate the analysis process as described in [Section
10.4.1](#sect-primitive-types).

</div>

<div class="paragraph">

In order for certain benchmarks to produce conditions where resource
heavy computation or excessive I/O can be observed, the benchmarks might
require some preliminary work on the environment, since those conditions
cannot be created with simply selected parameters. The analysis process
shows indicators on how the preliminary work should be implemented.

</div>

<div class="sect3">

#### <a href="#id-practical-example-1-request_judgement" class="anchor"></a><a href="#id-practical-example-1-request_judgement" class="link">10.5.1.
Practical Example #1: <code>request_judgement</code></a>

<div class="paragraph">

In Polkadot, accounts can save information about themselves on-chain,
known as the "Identity Info". This includes information such as display
name, legal name, email address and so on. Polkadot offers a set of
trusted registrars, entities elected by a Polkadot public referendum,
which can verify the specified contact addresses of the identities, such
as Email, and vouch on whether the identity actually owns those
accounts. This can be achieved, for example, by sending a challenge to
the specified address and requesting a signature as a response. The
verification is done off-chain, while the final judgement is saved
onchain, directly in the corresponding Identity Info. It’s also note
worthy that Identity Info can contain additional fields, set manually by
the corresponding account holder.

</div>

<div class="paragraph">

Information such as legal name must be verified by ID card or passport
submission.

</div>

<div class="paragraph">

The function `request_judgement` from the `identity` pallet allows users
to request judgement from a specific registrar.

</div>

<div class="listingblock">

<div class="content">

    (func $request_judgement (param $req_index int) (param $max_fee int))

</div>

</div>

<div class="ulist">

- `req_index`: the index which is assigned to the registrar.

- `max_fee`: the maximum fee the requester is willing to pay. The
  judgement fee varies for each registrar.

</div>

<div class="paragraph">

Studying this function reveals multiple design choices that can impact
performance, as it will be revealed by this analysis.

</div>

<div class="sect4">

##### <a href="#id-analysis" class="anchor"></a><a href="#id-analysis" class="link">10.5.1.1. Analysis</a>

<div class="paragraph">

First, it fetches a list of current registrars from storage and then
searches that list for the specified registrar index.

</div>

<div class="listingblock">

<div class="content">

``` rouge
let registrars = <Registrars<T>>::get();
let registrar = registrars.get(reg_index as usize).and_then(Option::as_ref)
  .ok_or(Error::<T>::EmptyIndex)?;
```

</div>

</div>

<div class="paragraph">

Then, it searches for the Identity Info from storage, based on the
sender of the transaction.

</div>

<div class="listingblock">

<div class="content">

``` rouge
let mut id = <IdentityOf<T>>::get(&sender).ok_or(Error::<T>::NoIdentity)?;
```

</div>

</div>

<div class="paragraph">

The Identity Info contains all fields that have a data in them, set by
the corresponding owner of the identity, in an ordered form. It then
proceeds to search for the specific field type that will be inserted or
updated, such as email address. If the entry can be found, the
corresponding value is to the value passed on as the function parameters
(assuming the registrar is not "stickied", which implies it cannot be
changed). If the entry cannot be found, the value is inserted into the
index where a matching element can be inserted while maintaining sorted
order. This results in memory reallocation, which increases resource
consumption.

</div>

<div class="listingblock">

<div class="content">

``` rouge
match id.judgements.binary_search_by_key(&reg_index, |x| x.0) {
  Ok(i) => if id.judgements[i].1.is_sticky() {
    Err(Error::<T>::StickyJudgement)?
  } else {
    id.judgements[i] = item
  },
  Err(i) => id.judgements.insert(i, item),
}
```

</div>

</div>

<div class="paragraph">

In the end, the function deposits the specified `max_fee` balance, which
can later be redeemed by the registrar. Then, an event is created to
insert the Identity Info into storage. The creation of events is
lightweight, but its execution is what will actually commit the state
changes.

</div>

<div class="listingblock">

<div class="content">

``` rouge
T::Currency::reserve(&sender, registrar.fee)?;
<IdentityOf<T>>::insert(&sender, id);
Self::deposit_event(RawEvent::JudgementRequested(sender, reg_index));
```

</div>

</div>

</div>

<div class="sect4">

##### <a href="#sect-considerations" class="anchor"></a><a href="#sect-considerations" class="link">10.5.1.2. Considerations</a>

<div class="paragraph">

The following points must be considered:

</div>

<div class="ulist">

- Varying count of registrars.

- Varying count of preexisting accounts in storage.

- The specified registrar is searched for in the Identity Info. An
  identity can be judged by as many registrars as the identity owner
  issues requests for, therefore increase its footprint in the state
  storage. Additionally, if a new value gets inserted into the byte
  array, memory get reallocated. Depending on the size of the Identity
  Info, the execution time can vary.

- The Identity Info can contain only a few fields or many. It is
  legitimate to introduce additional weights for changes the
  owner/sender has influence over, such as the additional fields in the
  Identity Info.

</div>

</div>

<div class="sect4">

##### <a href="#id-benchmarking-framework" class="anchor"></a><a href="#id-benchmarking-framework" class="link">10.5.1.3. Benchmarking
Framework</a>

<div class="paragraph">

The Polkadot Runtime specifies the `MaxRegistrars` constant, which will
prevent the list of registrars of reaching an undesired length. This
value should have some influence on the benchmarking process.

</div>

<div class="paragraph">

The benchmarking implementation of for the function
\\request\\judgement\\ can be defined as follows:

</div>

<div class="sidebarblock">

<div class="content">

\Ensure \$\mathcal{W}\$ \State \textbf{init} \$collection = \\\\\$
\For{\$amount \leftarrow 1,MaxRegistrars\$} \State
\call{Generate-Registrars}{\$amount\$} \State \$caller \leftarrow\$
\call{Create-Account}{\$caller, 1\$} \State \call{Set-Balance}{\$caller,
100\$} \State \$time \leftarrow\$
\call{Timer}{\call{Request-Judgement}{\call{Random}{\$amount\$}\$,
100\$}} \State \call{Add-To}{\$collection, time\$} \EndFor \State
\$\mathcal{W} \leftarrow\$ \call{Compute-Weight}{\$collection\$} \Return
\$\mathcal{W}\$

<div class="dlist">

where  
<div class="ulist">

- Generate-Registrars(\\amount\\)

  <div class="paragraph">

  Creates number of registrars and inserts those records into storage.

  </div>

- Create-Account(\\name\\, \\index\\)

  <div class="paragraph">

  Creates a Blake2 hash of the concatenated input of name and index
  represent- ing the address of a account. This function only creates an
  address and does not conduct any I/O.

  </div>

- Set-Balance(\\account\\, \\balance\\)

  <div class="paragraph">

  Sets a initial balance for the specified account in the storage state.

  </div>

- Timer(\\function\\)

  <div class="paragraph">

  Measures the time from the start of the specified f unction to its
  completion.

  </div>

- Request-Judgement(\\registrar\\index\\, \\max\\fee\\)

  <div class="paragraph">

  Calls the corresponding request_judgement Runtime function and passes
  on the required parameters.

  </div>

- Random(\\num\\)

  <div class="paragraph">

  Picks a random number between 0 and num. This should be used when the
  benchmark should account for unpredictable values.

  </div>

- Add-To(\\collection\\, \\time\\)

  <div class="paragraph">

  Adds a returned time measurement (time) to collection.

  </div>

- Compute-Weight(\\collection\\)

  <div class="paragraph">

  Computes the resulting weight based on the time measurements in the
  collection. The worst case scenario should be chosen (the highest
  value).

  </div>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-practical-example-payout-stakers" class="anchor"></a><a href="#sect-practical-example-payout-stakers" class="link">10.5.2.
Practical Example #2: <code>payout_stakers</code></a>

<div class="sect4">

##### <a href="#id-analysis-2" class="anchor"></a><a href="#id-analysis-2" class="link">10.5.2.1. Analysis</a>

<div class="paragraph">

The function `payout_stakers` from the `staking` Pallet can be called by
a single account in order to payout the reward for all nominators who
back a particular validator. The reward also covers the validator’s
share. This function is interesting because it iterates over a range of
nominators, which varies, and does I/O operation for each of them.

</div>

<div class="paragraph">

First, this function makes few basic checks to verify if the specified
era is not higher then the current era (as it is not in the future) and
is within the allowed range also known as "history depth", as specified
by the Runtime. After that, it fetches the era payout from storage and
additionally verifies whether the specified account is indeed a
validator and receives the corresponding "Ledger". The Ledger keeps
information about the stash key, controller key and other informatin
such as actively bonded balance and a list of tracked rewards. The
function only retains the entries of the history depth, and conducts a
binary search for the specified era.

</div>

<div class="listingblock">

<div class="content">

``` rouge
let era_payout = <ErasValidatorReward<T>>::get(&era)
  .ok_or_else(|| Error::<T>::InvalidEraToReward)?;

let controller = Self::bonded(&validator_stash).ok_or(Error::<T>::NotStash)?;
let mut ledger = <Ledger<T>>::get(&controller).ok_or_else(|| Error::<T>::NotController)?;
```

</div>

</div>

<div class="listingblock">

<div class="content">

``` rouge
ledger.claimed_rewards.retain(|&x| x >= current_era.saturating_sub(history_depth));
match ledger.claimed_rewards.binary_search(&era) {
  Ok(_) => Err(Error::<T>::AlreadyClaimed)?,
  Err(pos) => ledger.claimed_rewards.insert(pos, era),
}
```

</div>

</div>

<div class="paragraph">

The retained claimed rewards are inserted back into storage.

</div>

<div class="listingblock">

<div class="content">

``` rouge
<Ledger<T>>::insert(&controller, &ledger);
```

</div>

</div>

<div class="paragraph">

As an optimization, Runtime only fetches a list of the 64 highest staked
nominators, although this might be changed in the future. Accordingly,
any lower staked nominator gets no reward.

</div>

<div class="listingblock">

<div class="content">

``` rouge
let exposure = <ErasStakersClipped<T>>::get(&era, &ledger.stash);
```

</div>

</div>

<div class="paragraph">

Next, the function gets the era reward points from storage.

</div>

<div class="listingblock">

<div class="content">

``` rouge
let era_reward_points = <ErasRewardPoints<T>>::get(&era);
```

</div>

</div>

<div class="paragraph">

After that, the payout is split among the validator and its nominators.
The validators receives the payment first, creating an insertion into
storage and sending a deposit event to the scheduler.

</div>

<div class="listingblock">

<div class="content">

``` rouge
if let Some(imbalance) = Self::make_payout(
  &ledger.stash,
  validator_staking_payout + validator_commission_payout
) {
  Self::deposit_event(RawEvent::Reward(ledger.stash, imbalance.peek()));
}
```

</div>

</div>

<div class="paragraph">

Then, the nominators receive their payout rewards. The functions loops
over the nominator list, conducting an insertion into storage and a
creation of a deposit event for each of the nominators.

</div>

<div class="listingblock">

<div class="content">

``` rouge
for nominator in exposure.others.iter() {
  let nominator_exposure_part = Perbill::from_rational_approximation(
    nominator.value,
    exposure.total,
  );

  let nominator_reward: BalanceOf<T> = nominator_exposure_part * validator_leftover_payout;
  // We can now make nominator payout:
  if let Some(imbalance) = Self::make_payout(&nominator.who, nominator_reward) {
    Self::deposit_event(RawEvent::Reward(nominator.who.clone(), imbalance.peek()));
  }
}
```

</div>

</div>

</div>

<div class="sect4">

##### <a href="#considerations-1" class="anchor"></a><a href="#considerations-1" class="link">10.5.2.2. Considerations</a>

<div class="paragraph">

The following points must be considered:

</div>

<div class="ulist">

- The Ledger contains a varying list of claimed rewards. Fetching,
  retaining and searching through it can affect execution time. The
  retained list is inserted back into storage.

- Looping through a list of nominators and creating I/O operations for
  each increases execution time. The Runtime fetches up to 64
  nominators.

</div>

</div>

<div class="sect4">

##### <a href="#id-benchmarking-framework-2" class="anchor"></a><a href="#id-benchmarking-framework-2" class="link">10.5.2.3.
Benchmarking Framework</a>

<div id="defn-history-depth" class="exampleblock">

<div class="title">

Definition 157. History Depth

</div>

<div class="content">

<div class="paragraph">

H̱istory Depth indicated as `MaxNominatorRewardedPerValidator` is a fixed
constant specified by the Polkadot Runtime which dictates the number of
Eras the Runtime will reward nominators and validators for.

</div>

</div>

</div>

<div id="defn-max_nominator_reward_per_validator" class="exampleblock">

<div class="title">

Definition 158. Maximum Nominator Reward

</div>

<div class="content">

<div class="paragraph">

M̱aximum Nominator Rewarded Per Validator indicated as
`MaxNominatorRewardedPerValidator`, specifies the maximum amount of the
highest-staked nominators which will get a reward. Those values should
have some influence in the benchmarking process.

</div>

</div>

</div>

<div class="paragraph">

The benchmarking implementation for the function \\payout\\stakers\\ can
be defined as follows:

</div>

<div class="sidebarblock">

<div class="content">

\Ensure \$\mathcal{W}\$ \State \textbf{init} \$collection = \\\\\$
\For{\$amount \leftarrow 1,MaxNominatorRewardedPerValidator\$}
\For{\$era\\depth \leftarrow 1,HistoryDepth\$} \State \$validator
\leftarrow\$ \call{Generate-Validator}{} \State
\call{Validate}{\$validator\$} \State \$nominators \leftarrow\$
\call{Generate-Nominators}{\$amount\$} \For{\$nominator \in
nominators\$} \State \call{Nominate}{\$validator, nominator\$} \EndFor
\State \$era\\index \leftarrow\$ \call{Create-Rewards}{\$validator,
nominators, era\\depth\$} \State \$time \leftarrow\$
\call{Timer}{\call{Payout-Stakers}{\$validator\$}\$, era\\index\$}
\State \call{Add-To}{\$collection, time\$} \EndFor \EndFor \State
\$\mathcal{W} \leftarrow\$ \call{Compute-Weight}{\$collection\$} \Return
\$\mathcal{W}\$

<div class="dlist">

where  
<div class="ulist">

- Generate-Validator()

  <div class="paragraph">

  Creates a validators with some unbonded balances.

  </div>

- Validate(\\validator\\)

  <div class="paragraph">

  Bonds balances of validator and bonds balances.

  </div>

- Generate-Nominators(\\amount\\)

  <div class="paragraph">

  Creates the amount of nominators with some unbonded balances.

  </div>

- Nominate(\\validator\\, \\nominator\\)

  <div class="paragraph">

  Starts nomination of nominator for validator by bonding balances.

  </div>

- Create-Rewards(\\validator\\, \\nominators\\, \\era\\depth\\)

  <div class="paragraph">

  Starts an Era and creates pending rewards for validator and
  nominators.

  </div>

- Timer(\\function\\)

  <div class="paragraph">

  Measures the time from the start of the specified f unction to its
  completion.

  </div>

- Add-To(\\collection\\, \\time\\)

  <div class="paragraph">

  Adds a returned time measurement (time) to collection.

  </div>

- Compute-Weight(\\collection\\)

  <div class="paragraph">

  Computes the resulting weight based on the time measurements in the
  collection. The worst case scenario should be chosen (the highest
  value).

  </div>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-practical-example-3-transfer" class="anchor"></a><a href="#id-practical-example-3-transfer" class="link">10.5.3.
Practical Example #3: <code>transfer</code></a>

<div class="paragraph">

The \\transfer\\ function of the `balances` module is designed to move
the specified balance by the sender to the receiver.

</div>

<div class="sect4">

##### <a href="#id-analysis-3" class="anchor"></a><a href="#id-analysis-3" class="link">10.5.3.1. Analysis</a>

<div class="paragraph">

The source code of this function is quite short:

</div>

<div class="listingblock">

<div class="content">

``` rouge
let transactor = ensure_signed(origin)?;
let dest = T::Lookup::lookup(dest)?;
<Self as Currency<_>>::transfer(
  &transactor,
  &dest,
  value,
  ExistenceRequirement::AllowDeath
)?;
```

</div>

</div>

<div class="paragraph">

However, one need to pay close attention to the property `AllowDeath`
and to how the function treat existingand non-existing accounts
differently. Two types of behaviors are to consider:

</div>

<div class="ulist">

- If the transfer completely depletes the sender account balance to zero
  (or bellow the minimum "keep-alive" requirement), it removes the
  address and all associated data from storage.

- If recipient account has no balance, the transfer also needs to create
  the recipient account.

</div>

</div>

<div class="sect4">

##### <a href="#considerations-2" class="anchor"></a><a href="#considerations-2" class="link">10.5.3.2. Considerations</a>

<div class="paragraph">

Specific parameters can could have a significant impact for this
specific function. In order to trigger the two behaviors mentioned
above, the following parameters are selected:

</div>

| **Type**      |               | **From** | **To** | **Description**                     |
|---------------|---------------|----------|--------|-------------------------------------|
| Account index | `index` in…​   | 1        | 1000   | Used as a seed for account creation |
| Balance       | `balance` in…​ | 2        | 1000   | Sender balance and transfer amount  |

<div class="paragraph">

Executing a benchmark for each balance increment within the balance
range for each index increment within the index range will generate too
many variants (\\1000 \times 999\\) and highly increase execution time.
Therefore, this benchmark is configured to first set the balance at
value 1’000 and then to iterate from 1 to 1’000 for the index value.
Once the index value reaches 1’000, the balance value will reset to 2
and iterate to 1’000 (see ["transfer" Runtime function
benchmark](#algo-benchmark-transfer) for more detail):

</div>

<div class="ulist">

- `index`: 1, `balance`: 1000

- `index`: 2, `balance`: 1000

- `index`: 3, `balance`: 1000

- …​

- `index`: 1000, `balance`: 1000

- `index`: 1000, `balance`: 2

- `index`: 1000, `balance`: 3

- `index`: 1000, `balance`: 4

- …​

</div>

<div class="paragraph">

The parameters itself do not influence or trigger the two worst
conditions and must be handled by the implemented benchmarking tool. The
\\transfer\\ benchmark is implemented as defined in ["transfer" Runtime
function benchmark](#algo-benchmark-transfer).

</div>

</div>

<div class="sect4">

##### <a href="#id-benchmarking-framework-3" class="anchor"></a><a href="#id-benchmarking-framework-3" class="link">10.5.3.3.
Benchmarking Framework</a>

<div class="paragraph">

The benchmarking implementation for the Polkadot Runtime function
\\transfer\\ is defined as follows (starting with the Main function):

</div>

<div class="sidebarblock">

<div class="content">

\Ensure{\$collection\$: a collection of time measurements of all
benchmark iterations} \Function{Main}{} \State \textbf{init}
\$collection = \\ \\\$ \State \textbf{init} \$balance = 1'000\$
\For{\$index \gets 1,1'000\$} \State \$time \leftarrow\$
\call{Run-Benchmark}{\$index, balance\$} \State
\call{Add-To}{\$collection, time\$} \EndFor \State \textbf{init} \$index
= 1'000\$ \For{\$balance \gets 2,1'000\$} \State \$time \leftarrow\$
\call{Run-Benchmark}{\$index, balance\$} \State
\call{Add-To}{\$collection, time\$} \EndFor \State \$\mathcal{W}
\leftarrow\$ \call{Compute-Weight}{\$collection\$} \Return
\$\mathcal{W}\$ \EndFunction \Function{Run-Benchmark}{\$index\$,
\$balance\$} \State \$sender \leftarrow\$
\call{Create-Account}{\$caller, index\$} \State \$recipient \leftarrow\$
\call{Create-Accouny}{\$recipient, index\$} \State
\call{Set-Balance}{\$sender, balance\$} \State \$time \leftarrow\$
\call{Timer}{\call{Transfer}{\$sender, recipient, balance\$}} \Return
\$time\$ \EndFunction

<div class="dlist">

where  
<div class="ulist">

- Create-Account(\\name\\, \\index\\)

  <div class="paragraph">

  Creates a Blake2 hash of the concatenated input of name and index
  representing the address of a account. This function only creates an
  address and does not conduct any I/O.

  </div>

- Set-Balance(\\account\\, \\balance\\)

  <div class="paragraph">

  Sets a initial balance for the specified account in the storage state.

  </div>

- Transfer(\\sender\\, \\recipient\\, \\balance\\)

  <div class="paragraph">

  Transfers the specified balance from sender to recipient by calling
  the corresponding Runtime function. This represents the target Runtime
  function to be benchmarked.

  </div>

- Add-To(\\collection\\, \\time\\)

  <div class="paragraph">

  Adds a returned time measurement (time) to collection.

  </div>

- Timer(\\function\\)

  <div class="paragraph">

  Adds a returned time measurement (time) to collection.

  </div>

- Compute-Weight(\\collection\\)

  <div class="paragraph">

  Computes the resulting weight based on the time measurements in the
  collection. The worst case scenario should be chosen (the highest
  value).

  </div>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-practical-example-4-withdraw_unbounded" class="anchor"></a><a href="#id-practical-example-4-withdraw_unbounded"
class="link">10.5.4. Practical Example #4:
<code>withdraw_unbounded</code></a>

<div class="paragraph">

The `withdraw_unbonded` function of the `staking` module is designed to
move any unlocked funds from the staking management system to be ready
for transfer. It contains some operations which have some I/O overhead.

</div>

<div class="sect4">

##### <a href="#id-analysis-4" class="anchor"></a><a href="#id-analysis-4" class="link">10.5.4.1. Analysis</a>

<div class="paragraph">

Similarly to the `payout_stakers` function ([Section
10.5.2](#sect-practical-example-payout-stakers)), this function fetches
the Ledger which contains information about the stash, such as bonded
balance and unlocking balance (balance that will eventually be freed and
can be withdrawn).

</div>

<div class="listingblock">

<div class="content">

``` rouge
if let Some(current_era) = Self::current_era() {
  ledger = ledger.consolidate_unlocked(current_era)
}
```

</div>

</div>

<div class="paragraph">

The function `consolidate_unlocked` does some cleaning up on the ledger,
where it removes outdated entries from the unlocking balance (which
implies that balance is now free and is no longer awaiting unlock).

</div>

<div class="listingblock">

<div class="content">

``` rouge
let mut total = self.total;
let unlocking = self.unlocking.into_iter()
  .filter(|chunk| if chunk.era > current_era {
    true
  } else {
    total = total.saturating_sub(chunk.value);
    false
  })
  .collect();
```

</div>

</div>

<div class="paragraph">

This function does a check on wether the updated ledger has any balance
left in regards to staking, both in terms of locked, staking balance and
unlocking balance. If not amount is left, the all information related to
the stash will be deleted. This results in multiple I/O calls.

</div>

<div class="listingblock">

<div class="content">

``` rouge
if ledger.unlocking.is_empty() && ledger.active.is_zero() {
  // This account must have called `unbond()` with some value that caused the active
  // portion to fall below existential deposit + will have no more unlocking chunks
  // left. We can now safely remove all staking-related information.
  Self::kill_stash(&stash, num_slashing_spans)?;
  // remove the lock.
  T::Currency::remove_lock(STAKING_ID, &stash);
  // This is worst case scenario, so we use the full weight and return None
  None
```

</div>

</div>

<div class="paragraph">

The resulting call to `Self::kill_stash()` triggers:

</div>

<div class="listingblock">

<div class="content">

``` rouge
slashing::clear_stash_metadata::<T>(stash, num_slashing_spans)?;
<Bonded<T>>::remove(stash);
<Ledger<T>>::remove(&controller);
<Payee<T>>::remove(stash);
<Validators<T>>::remove(stash);
<Nominators<T>>::remove(stash);
```

</div>

</div>

<div class="paragraph">

Alternatively, if there’s some balance left, the adjusted ledger simply
gets updated back into storage.

</div>

<div class="listingblock">

<div class="content">

``` rouge
// This was the consequence of a partial unbond. just update the ledger and move on.
Self::update_ledger(&controller, &ledger);
```

</div>

</div>

<div class="paragraph">

Finally, it withdraws the unlocked balance, making it ready for
transfer:

</div>

<div class="listingblock">

<div class="content">

``` rouge
let value = old_total - ledger.total;
Self::deposit_event(RawEvent::Withdrawn(stash, value));
```

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-parameters-2" class="anchor"></a><a href="#id-parameters-2" class="link">10.5.4.2. Parameters</a>

<div class="paragraph">

The following parameters are selected:

</div>

| **Type**      |             | **From** | **To** | **Description**                     |
|---------------|-------------|----------|--------|-------------------------------------|
| Account index | `index` in…​ | 0        | 1000   | Used as a seed for account creation |

<div class="paragraph">

This benchmark does not require complex parameters. The values are used
solely for account generation.

</div>

</div>

<div class="sect4">

##### <a href="#considerations-3" class="anchor"></a><a href="#considerations-3" class="link">10.5.4.3. Considerations</a>

<div class="paragraph">

Two important points in the `withdraw_unbonded` function must be
considered. The benchmarks should trigger both conditions

</div>

<div class="ulist">

- The updated ledger is inserted back into storage.

- If the stash gets killed, then multiple, repetitive deletion calls are
  performed in the storage.

</div>

</div>

<div class="sect4">

##### <a href="#id-benchmarking-framework-4" class="anchor"></a><a href="#id-benchmarking-framework-4" class="link">10.5.4.4.
Benchmarking Framework</a>

<div class="paragraph">

The benchmarking implementation for the Polkadot Runtime function
`withdraw_unbonded` is defined as follows:

</div>

<div class="sidebarblock">

<div class="content">

\Ensure \$\mathcal{W}\$ \Function{Main}{} \State \textbf{init}
\$collection = \\\\\$ \For{\$balance \gets 1,100\$} \State \$stash
\leftarrow\$ \call{Create-Account}{\$stash, 1\$} \State \$controller
\leftarrow\$ \call{Create-Account}{\$controller, 1\$} \State
\call{Set-Balance}{\$stash, 100\$} \State
\call{Set-Balance}{\$controller, 1\$} \State \call{Bond}{\$stash,
controller, balance\$} \State \call{Pass-Era}{} \State
\call{UnBond}{\$controller, balance\$} \State \call{Pass-Era}{} \State
\$time \leftarrow\$
\call{Timer}{\call{Withdraw-Unbonded}{\$controller\$}} \State
\call{Add-To}{\$collection, time\$} \EndFor \State \$\mathcal{W}
\leftarrow\$ \call{Compute-Weight}{\$collection\$} \Return
\$\mathcal{W}\$ \EndFunction

<div class="dlist">

where  
<div class="ulist">

- Create-Account(\\name\\, \\index\\)

  <div class="paragraph">

  Creates a Blake2 hash of the concatenated input of name and index
  representing the address of a account. This function only creates an
  address and does not conduct any I/O.

  </div>

- Set-Balance(\\account\\, \\balance\\)

  <div class="paragraph">

  Sets a initial balance for the specified account in the storage state.

  </div>

- Bond(\\stash\\, \\controller\\, \\amount\\)

  <div class="paragraph">

  Bonds the specified amount for the stash and controller pair.

  </div>

- UnBond(\\account\\, \\amount\\)

  <div class="paragraph">

  Unbonds the specified amount for the given account.

  </div>

- Pass-Era()

  <div class="paragraph">

  Pass one era. Forces the function `withdraw_unbonded` to update the
  ledger and eventually delete information.

  </div>

- Withdraw-Unbonded(\\controller\\)

  <div class="paragraph">

  Withdraws the the full unbonded amount of the specified controller
  account. This represents the target Runtime function to be
  benchmarked.

  </div>

- Add-To(\\collection\\, \\time\\)

  <div class="paragraph">

  Adds a returned time measurement (time) to collection.

  </div>

- Timer(\\function\\)

  <div class="paragraph">

  Measures the time from the start of the specified f unction to its
  completion.

  </div>

- Compute-Weight(\\collection\\)

  <div class="paragraph">

  Computes the resulting weight based on the time measurements in the
  collection. The worst case scenario should be chosen (the highest
  value).

  </div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#id-fees" class="anchor"></a><a href="#id-fees" class="link">10.6. Fees</a>

<div class="paragraph">

Block producers charge a fee in order to be economically sustainable.
That fee must always be covered by the sender of the transaction.
Polkadot has a flexible mechanism to determine the minimum cost to
include transactions in a block.

</div>

<div class="sect3">

#### <a href="#sect-fee-calculation" class="anchor"></a><a href="#sect-fee-calculation" class="link">10.6.1. Fee Calculation</a>

<div class="paragraph">

Polkadot fees consists of three parts:

</div>

<div class="ulist">

- Base fee: a fixed fee that is applied to every transaction and set by
  the Runtime.

- Length fee: a fee that gets multiplied by the length of the
  transaction, in bytes.

- Weight fee: a fee for each, varying Runtime function. Runtime
  implementers need to implement a conversion mechanism which determines
  the corresponding currency amount for the calculated weight.

</div>

<div class="paragraph">

The final fee can be summarized as:

</div>

<div class="stemblock">

<div class="content">

\\\begin{aligned} fee &= base\\ fee \\ &{} + length\\ of\\ transaction\\
in\\ bytes \times length\\ fee \\ &{} + weight\\ to\\ fee \\
\end{aligned}\\

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-definitions-in-polkadot" class="anchor"></a><a href="#id-definitions-in-polkadot" class="link">10.6.2. Definitions
in Polkadot</a>

<div class="paragraph">

The Polkadot Runtime defines the following values:

</div>

<div class="ulist">

- Base fee: 100 uDOTs

- Length fee: 0.1 uDOTs

- Weight to fee conversion:

  <div class="stemblock">

  <div class="content">

  \\weight\\ fee = weight \times (100\\ uDOTs \div (10 \times 10'000))\\

  </div>

  </div>

  <div class="paragraph">

  A weight of 10’000 (the smallest non-zero weight) is mapped to
  \\\frac{1}{10}\\ of 100 uDOT. This fee will never exceed the max size
  of an unsigned 128 bit integer.

  </div>

</div>

</div>

<div class="sect3">

#### <a href="#id-fee-multiplier" class="anchor"></a><a href="#id-fee-multiplier" class="link">10.6.3. Fee Multiplier</a>

<div class="paragraph">

Polkadot can add a additional fee to transactions if the network becomes
too busy and starts to decelerate the system. This fee can create an
incentive to avoid the production of low priority or insignificant
transactions. In contrast, those additional fees will decrease if the
network calms down and it can execute transactions without much
difficulties.

</div>

<div class="paragraph">

That additional fee is known as the `Fee Multiplier` and its value is
defined by the Polkadot Runtime. The multiplier works by comparing the
saturation of blocks; if the previous block is less saturated than the
current block (implying an uptrend), the fee is slightly increased.
Similarly, if the previous block is more saturated than the current
block (implying a downtrend), the fee is slightly decreased.

</div>

<div class="paragraph">

The final fee is calculated as:

</div>

<div class="stemblock">

<div class="content">

\\final\\ fee = fee \times Fee\\ Multiplier\\

</div>

</div>

<div class="sect4">

##### <a href="#id-update-multiplier" class="anchor"></a><a href="#id-update-multiplier" class="link">10.6.3.1. Update
Multiplier</a>

<div class="paragraph">

The `Update Multiplier` defines how the multiplier can change. The
Polkadot Runtime internally updates the multiplier after each block
according the following formula:

</div>

<div class="stemblock">

<div class="content">

\\\begin{aligned} diff &=& (target\\ weight - previous\\ block\\ weight)
\\ v &=& 0.00004 \\ next\\ weight &=& weight \times (1 + (v \times
diff) + (v \times diff)^2 / 2) \\ \end{aligned}\\

</div>

</div>

<div class="paragraph">

Polkadot defines the `target_weight` as 0.25 (25%). More information
about this algorithm is described in the [Web3 Foundation research
paper](https://research.web3.foundation/en/latest/polkadot/Token%20Economics.html#relay-chain-transaction-fees-and-per-block-transaction-limits).

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#id-consensus" class="anchor"></a><a href="#id-consensus" class="link">11. Consensus</a>

<div class="sectionbody">

<div class="sect2">

### <a href="#id-babe-digest-messages" class="anchor"></a><a href="#id-babe-digest-messages" class="link">11.1. BABE digest
messages</a>

<div class="paragraph">

The Runtime is required to provide the BABE authority list and
randomness to the host via a consensus message in the header of the
first block of each epoch.

</div>

<div class="paragraph">

The digest published in Epoch \\\mathcal{E}\_n\\ is enacted in
\\\mathcal{E}\_{n+1}\\. The randomness in this digest is computed based
on the all the VRF outputs up to including Epoch \\\mathcal{E}\_{n-2}\\
while the authority set is based on all transaction included up to Epoch
\\\mathcal{E}\_{n-1}\\.

</div>

<div class="sidebarblock">

<div class="content">

<div class="paragraph">

The computation of the randomeness seed is described in
[Epoch-Randomness](#algo-epoch-randomness) which uses the concept of
epoch subchain as described in host specification and the value \\d_B\\,
which is the VRF output computed for slot \\s_B\\.

</div>

\Require \$n \> 2\$ \State \textbf{init} \$\rho \leftarrow \phi\$
\For{\$B\$ in \call{SubChain}{\$\mathcal{E}\_{n-2}\$}} \State \$\rho
\leftarrow \rho \|\| d_B\$ \EndFor \Return
\call{Blake2b}{\call{Epoch-Randomness}{\$n-1\$}\$\|\|n\|\|\rho\$}

<div class="paragraph">

where \\n\\ is the epoch index.

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#sect-metadata" class="anchor"></a><a href="#sect-metadata" class="link">12. Metadata</a>

<div class="sectionbody">

<div class="paragraph">

The runtime metadata structure contains all the information necessary on
how to interact with the Polkadot runtime. Considering that Polkadot
runtimes are upgradable and therefore any interfaces are subject to
change, the metadata allows developers to structure any extrinsics or
storage entries accordingly.

</div>

<div class="paragraph">

The metadata of a runtime is provided by a call to `Metadata_metadata`
([Section C.5.1](#sect-rte-metadata-metadata)) and is returned as a
scale encoded ([Section A.2.2](#sect-scale-codec)) binary blob. How to
interpret and decode this data is described in this chapter.

</div>

<div class="sect2">

### <a href="#sect-rtm-structure" class="anchor"></a><a href="#sect-rtm-structure" class="link">12.1. Structure</a>

<div class="paragraph">

The Runtime Metadata is a datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\(M, v_m, R, P, t_e, v_e, E, t_r)\\ \\R = (r_0, ...,r_n)\\ \\P = (p_0,
...,p_n)\\ \\E = (e_0, ...,e_n)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\M\\ are the first four constant bytes, spelling "meta" in ASCII.

- \\v_m\\ is an unsigned 8-bit integer indicating the format version of
  the metadata structure (currently the value of `14`).

- \\R\\ is a sequence ([Definition 192](#defn-scale-list)) of type
  definitions \\r_i\\ ([Definition 159](#defn-rtm-registry-entry)).

- \\P\\ is a sequence ([Definition 192](#defn-scale-list)) of pallet
  metadata \\p_i\\ ([Section 12.2](#sect-rtm-pallet-metadata)).

- \\t_e\\ is the type Id ([Definition 160](#defn-rtm-type-id)) of the
  extrinsics.

- \\v_e\\ is an unsigned 8-bit integer indicating the format version of
  the extrinsics (implying a possible breaking change).

- \\E\\ is a sequence ([Definition 192](#defn-scale-list)) of extrinsics
  metadata \\e_i\\ ([Definition
  170](#defn-rtm-signed-extension-metadata)).

- \\t_r\\ is the type Id ([Definition 160](#defn-rtm-type-id)) of the
  runtime.

</div>

</div>

seq: - id: magic contents: meta - id: metadata_version type: u1 - id:
num_types type: scale::compact_int - id: types type: metadata_type
repeat: expr repeat-expr: num_types.value - id: num_pallets type:
scale::compact_int - id: pallets type: metadata_pallet repeat: expr
repeat-expr: num_pallets.value - id: extrinsic_type type:
scale::compact_int - id: extrinsic_version type: u1 - id: num_extrinsics
type: scale::compact_int - id: extrinsics type: metadata_extrinsic
repeat: expr repeat-expr: num_extrinsics.value - id: runtime_type type:
scale::compact_int

<div id="defn-rtm-registry-entry" class="exampleblock">

<div class="title">

Definition 159. [Runtime Registry Type Entry](#defn-rtm-registry-entry)

</div>

<div class="content">

<div class="paragraph">

A registry entry contains information about a type in its portable form
for serialization. The entry is a datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\r_i = ("id"\_t,p,T,D,c)\\ \\T = (t_0, ...,t_n)\\ \\t_i = (n, y)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\"id"\_t\\ is a compact integer indicating the identifier of the
  type.

- \\p\\ is the path of the type, optional and based on source file
  location. Encoded as a sequence ([Definition 192](#defn-scale-list))
  of strings.

- \\T\\ is a sequence ([Definition 192](#defn-scale-list)) of generic
  parameters (empty for non-generic types).

  <div class="ulist">

  - \\n\\ is the name string of the generic type parameter

  - \\y\\ is a *Option* type containing a type Id ([Definition
    160](#defn-rtm-type-id)).

  </div>

- \\D\\ is the type definition ([Definition
  161](#defn-rtm-type-definition)).

- \\c\\ is the documentation as sequence ([Definition
  192](#defn-scale-list)) of strings.

</div>

</div>

seq: - id: id type: scale::compact_int - id: path type:
scale::string_list - id: num_params type: scale::compact_int - id:
params repeat: expr repeat-expr: num_params.value type: param - id:
definition type: metadata_type_definition - id: docs type:
scale::string_list types: param: seq: - id: name type: scale::string -
id: type type: scale::maybe_compact_int

</div>

</div>

<div id="defn-rtm-type-id" class="exampleblock">

<div class="title">

Definition 160. [Runtime Type Id](#defn-rtm-type-id)

</div>

<div class="content">

<div class="paragraph">

The **runtime type Id** is a compact integer representing the index of
the entry ([Definition 159](#defn-rtm-registry-entry)) in \\R, P\\ or
\\E\\ of the runtime metadata structure ([Section
12.1](#sect-rtm-structure)), depending on context (starting at \\0\\).

</div>

</div>

</div>

<div id="defn-rtm-type-definition" class="exampleblock">

<div class="title">

Definition 161. [Type Variant](#defn-rtm-type-definition)

</div>

<div class="content">

<div class="paragraph">

The type definition \\D\\ is a varying datatype ([Definition
188](#defn-varrying-data-type)) and indicates all the possible types of
encodable values a type can have.

</div>

<div class="stemblock">

<div class="content">

\\D = { (0,-\>,C,"composite type (e.g. structure or tuple)"),
(1,-\>,V,"variant type"), (2,-\>,s_v,"sequence type varying length"),
(3,-\>,S,"sequence with fixed length"), (4,-\>,T,"tuple type"),
(5,-\>,P,"primitive type"), (6,-\>,e,"compact encoded type"),
(7,-\>,B,"sequence of bits") :}\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\C\\ is a sequence of the following format:

  <div class="stemblock">

  <div class="content">

  \\C = (f_0, ..., f_n)\\

  </div>

  </div>

  <div class="ulist">

  - \\f_i\\ is a field ([Definition 162](#defn-rtm-field)).

  </div>

- \\V\\ is a sequence of the following format:

  <div class="stemblock">

  <div class="content">

  \\V = (v_0, ..., v_n)\\

  </div>

  </div>

  <div class="ulist">

  - \\v_i\\ is a variant ([Definition 163](#defn-rtm-variant)).

  </div>

- \\s_v\\ is a type Id ([Definition 160](#defn-rtm-type-id)).

- \\S\\ is of the following format:

  <div class="stemblock">

  <div class="content">

  \\S = (l, y)\\

  </div>

  </div>

  <div class="ulist">

  - \\l\\ is a unsigned 32-bit integer indicating the length

  - \\y\\ is a type Id ([Definition 160](#defn-rtm-type-id)).

  </div>

- \\T\\ is a sequence ([Definition 192](#defn-scale-list)) of type Ids
  ([Definition 160](#defn-rtm-type-id)).

- \\P\\ is a varying datatype ([Definition
  188](#defn-varrying-data-type)) of the following structure:

  <div class="stemblock">

  <div class="content">

  \\P = { (0,"boolean"), (1,"char"), (2,"string"), (3,"unsigned 8-bit
  integer"), (4,"unsigned 16-bit integer"), (5,"unsigned 32-bit
  integer"), (6,"unsigned 64-bit integer"), (7,"unsigned 128-bit
  integer"), (8,"unsigned 256-bit integer"), (9,"signed 8-bit integer"),
  (10,"signed 16-bit integer"), (11,"signed 32-bit integer"),
  (12,"signed 64-bit integer"), (13,"signed 128-bit integer"),
  (14,"signed 256-bit integer") :}\\

  </div>

  </div>

- \\e\\ is a type Id ([Definition 160](#defn-rtm-type-id)).

- \\B\\ is a datastructure of the following format:

  <div class="stemblock">

  <div class="content">

  \\B = (s, o)\\

  </div>

  </div>

  <div class="ulist">

  - \\s\\ is a type Id ([Definition 160](#defn-rtm-type-id))
    representing the bit store order ([external
    reference](https://docs.rs/bitvec/latest/bitvec/store/trait.BitStore.html))

  - \\o\\ is a type Id ([Definition 160](#defn-rtm-type-id)) the bit
    order type ([external
    reference](https://docs.rs/bitvec/latest/bitvec/order/trait.BitOrder.html)).

  </div>

</div>

</div>

seq: - id: type type: u1 enum: type - id: details type: switch-on: type
cases: "type::composite": metadata_type_fields "type::variant":
metadata_type_variants "type::sequence": sequence "type::array": array
"type::tuple": tuple "type::primitive": primitive "type::compact":
compact "type::bits": bits enums: type: 0: composite 1: variant 2:
sequence 3: array 4: tuple 5: primitive 6: compact 7: bits types:
sequence: seq: - id: type type: scale::compact_int array: seq: - id:
length type: u4 - id: type type: scale::compact_int tuple: seq: - id:
num_types type: scale::compact_int - id: types type: scale::compact_int
repeat: expr repeat-expr: num_types.value primitive: seq: - id: id type:
u1 enum: pid enums: pid: 0: bool 1: char 2: str 3: uint8 4: uint16 5:
uint32 6: uint64 7: uint128 8: uint256 9: int8 10: int16 11: int32 12:
int64 13: int128 14: int256 compact: seq: - id: type type:
scale::compact_int bits: seq: - id: type type: scale::compact_int - id:
order type: scale::compact_int

</div>

</div>

<div id="defn-rtm-field" class="exampleblock">

<div class="title">

Definition 162. [Field](#defn-rtm-field)

</div>

<div class="content">

<div class="paragraph">

A field of a datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\f_i = (n, y, y_n, C)\\

</div>

</div>

<div class="paragraph">

where

</div>

<div class="ulist">

- \\n\\ is an *Option* type containing the string that indicates the
  field name.

- \\y\\ is a type Id ([Definition 160](#defn-rtm-type-id)).

- \\y_n\\ is an *Option* type containing a string that indicates the
  name of the type as it appears in the source code.

- \\C\\ is a sequence of varying length containing strings of
  documentation.

</div>

seq: - id: num_fields type: scale::compact_int - id: fields type: field
repeat: expr repeat-expr: num_fields.value types: field: seq: - id: name
type: scale::maybe_string - id: type type: scale::compact_int - id:
typename type: scale::maybe_string - id: docs type: scale::string_list

</div>

</div>

<div id="defn-rtm-variant" class="exampleblock">

<div class="title">

Definition 163. [Variant](#defn-rtm-variant)

</div>

<div class="content">

<div class="paragraph">

A struct variant of the following format:

</div>

<div class="stemblock">

<div class="content">

\\v_i = (n,F,k,C)\\

</div>

</div>

<div class="paragraph">

where

</div>

<div class="ulist">

- \\n\\ is a string representing the name of the variant.

- \\F\\ is a possible empty array of varying length containing field
  ([Definition 162](#defn-rtm-field)) elements.

- \\k\\ is an unsigned 8-bit integer indicating the index of the
  variant.

- \\C\\ is a sequence of strings containing the documentation.

</div>

seq: - id: num_variants type: scale::compact_int - id: variants type:
variant repeat: expr repeat-expr: num_variants.value types: variant:
seq: - id: name type: scale::string - id: composite type:
metadata_type_fields - id: index type: u1 - id: docs type:
scale::string_list

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-rtm-pallet-metadata" class="anchor"></a><a href="#sect-rtm-pallet-metadata" class="link">12.2. Pallet
Metadata</a>

<div class="paragraph">

All the metadata about a pallet, part of the main structure ([Section
12.1](#sect-rtm-structure)) and of the following format:

</div>

<div class="stemblock">

<div class="content">

\\p_i = (n, S, a, e, C, e, i)\\

</div>

</div>

<div class="paragraph">

where

</div>

<div class="ulist">

- \\n\\ is a string representing the pallet name.

- \\S\\ is an *Option* type containing the pallet storage metadata
  ([Definition 164](#defn-rtm-pallet-storage-metadata)).

- \\a\\ is an *Option* type ([Definition 190](#defn-option-type))
  containing the type Id ([Definition 160](#defn-rtm-type-id)) of pallet
  calls.

- \\e\\ is an *Option* type ([Definition 190](#defn-option-type))
  containing the type Id ([Definition 160](#defn-rtm-type-id)) of pallet
  events.

- \\C\\ is an *Sequence* ([Definition 192](#defn-scale-list)) of all
  pallet constant metadata ([Definition
  169](#defn-rtm-pallet-constants)).

- \\e\\ is an *Option* type ([Definition 190](#defn-option-type))
  containing the type Id ([Definition 160](#defn-rtm-type-id)) of the
  pallet error.

- \\i\\ is an unsigned 8-bit integers indicating the index of the
  pallet, which is used for encoding pallet events and calls.

</div>

seq: - id: name type: scale::string - id: has_storage type: u1 - id:
storage type: pallet_storage if: has_storage != 0 - id: has_calls type:
u1 - id: calls type: calls if: has_calls != 0 - id: has_events type:
u1 - id: events type: events if: has_events != 0 - id: num_constants
type: scale::compact_int - id: constants type: pallet_constant repeat:
expr repeat-expr: num_constants.value - id: has_errors type: u1 - id:
errors type: errors if: has_errors != 0 - id: index type: u1 types:
calls: seq: - id: type type: scale::compact_int events: seq: - id: type
type: scale::compact_int errors: seq: - id: type type:
scale::compact_int

<div id="defn-rtm-pallet-storage-metadata" class="exampleblock">

<div class="title">

Definition 164. [Pallet Storage
Metadata](#defn-rtm-pallet-storage-metadata)

</div>

<div class="content">

<div class="paragraph">

The metadata about a pallets storage.

</div>

<div class="stemblock">

<div class="content">

\\S = (p, E)\\ \\E = ( e_0, ... , e_n )\\

</div>

</div>

<div class="paragraph">

where

</div>

<div class="ulist">

- \\p\\ is the string representing the common prefix used by all storage
  entries.

- \\E\\ is an array of varying length containing elements of storage
  entries ([Definition 165](#defn-rtm-storage-entry-metadata)).

</div>

</div>

</div>

<div id="defn-rtm-storage-entry-metadata" class="exampleblock">

<div class="title">

Definition 165. [Storage Entry
Metadata](#defn-rtm-storage-entry-metadata)

</div>

<div class="content">

<div class="paragraph">

The metadata about a pallets storage entry.

</div>

<div class="stemblock">

<div class="content">

\\e_i = (n, m, y, d, C)\\ \\C = ( c_0, ... , c_n )\\

</div>

</div>

<div class="paragraph">

where

</div>

<div class="ulist">

- \\n\\ is the string representing the variable name of the storage
  entry.

- \\m\\ is an enum type determining the storage entry modifier
  ([Definition 166](#defn-rtm-storage-entry-modifier)).

- \\y\\ is the type of the value stored in the entry ([Definition
  167](#defn-rtm-storage-entry-type)).

- \\d\\ is an byte array containing the default value.

- \\C\\ is an array of varying length of strings containing the
  documentation.

</div>

seq: - id: prefix type: scale::string - id: num_items type:
scale::compact_int - id: items type: item repeat: expr repeat-expr:
num_items.value types: item: seq: - id: name type: scale::string - id:
modifier type: u1 enum: storage_modifier - id: definition type:
storage_definition - id: fallback type: scale::bytes - id: docs type:
scale::string_list enums: storage_modifier: 0: optional 1: default

</div>

</div>

<div id="defn-rtm-storage-entry-modifier" class="exampleblock">

<div class="title">

Definition 166. [Storage Entry
Modifier](#defn-rtm-storage-entry-modifier)

</div>

<div class="content">

<div class="admonitionblock note">

|     |                                                 |
|-----|-------------------------------------------------|
|     | This might be incorrect and has to be reviewed. |

</div>

<div class="paragraph">

The storage entry modifier is a varying datatype ([Definition
188](#defn-varrying-data-type)) and indicates how the storage entry is
returned and how it behaves if the entry is not present.

</div>

<div class="stemblock">

<div class="content">

\\m = { (0,"optional"), (1,"default") :}\\

</div>

</div>

<div class="paragraph">

where *0* indicates that the entry returns an *Option* type and
therefore *None* if the storage entry is not present. *1* indicates that
the entry returns the type \\y\\ with default value \\d\\ (in
[Definition 165](#defn-rtm-storage-entry-metadata)) if the entry is not
present.

</div>

</div>

</div>

<div id="defn-rtm-storage-entry-type" class="exampleblock">

<div class="title">

Definition 167. [Storage Entry Type](#defn-rtm-storage-entry-type)

</div>

<div class="content">

<div class="paragraph">

The type of the storage value is a varying datatype ([Definition
188](#defn-varrying-data-type)) that indicates how the entry is stored.

</div>

<div class="stemblock">

<div class="content">

\\y = { (0,-\>,t,"plain type"), (1,-\>,(H, k, v),"storage map") :}\\

</div>

</div>

<div class="paragraph">

where \\t\\, \\k\\ (key) and \\v\\ (value) are all of type Ids
([Definition 160](#defn-rtm-type-id)). \\H\\ is an array of varying
length containing the storage hasher ([Definition
168](#defn-rtm-storage-hasher)).

</div>

seq: - id: type type: u1 enum: storage_type - id: details type:
switch-on: type cases: 'storage_type::plain': plain 'storage_type::map':
map enums: storage_type: 0: plain 1: map types: plain: seq: - id: type
type: scale::compact_int map: seq: - id: num_hasher type:
scale::compact_int - id: hasher type: u1 enum: hasher_type repeat: expr
repeat-expr: num_hasher.value - id: key type: scale::compact_int - id:
value type: scale::compact_int enums: hasher_type: 0: blake2_128 1:
blake2_256 2: blake2_128_128 3: xxhash_128 4: xxhash_256 5: xxhahs_64_64
6: idhash

</div>

</div>

<div id="defn-rtm-storage-hasher" class="exampleblock">

<div class="title">

Definition 168. [Storage Hasher](#defn-rtm-storage-hasher)

</div>

<div class="content">

<div class="paragraph">

The hashing algorithm used by storage maps.

</div>

<div class="stemblock">

<div class="content">

\\{ (0,"128-bit Blake2 hash"), (1,"256-bit Blake2 hash"), (2,"Multiple
128-bit Blake2 hashes concatenated"), (3,"128-bit XX hash"), (4,"256-bit
XX hash"), (5,"Multiple 64-bit XX hashes concatenated"), (6,"Identity
hashing") :}\\

</div>

</div>

</div>

</div>

<div id="defn-rtm-pallet-constants" class="exampleblock">

<div class="title">

Definition 169. [Pallet Constants](#defn-rtm-pallet-constants)

</div>

<div class="content">

<div class="paragraph">

The metadata about the pallets constants.

</div>

<div class="stemblock">

<div class="content">

\\c_i = (n, y, v, C)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\n\\ is a string representing the name of the pallet constant.

- \\y\\ is the type Id ([Definition 160](#defn-rtm-type-id)) of the
  pallet constant.

- \\v\\ is a byte array containing the value of the constant.

- \\C\\ is an array of varying length containing string with the
  documentation.

</div>

</div>

seq: - id: name type: scale::string - id: type type:
scale::compact_int - id: value type: scale::bytes - id: docs type:
scale::string_list

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-rtm-extrinsic-metadata" class="anchor"></a><a href="#sect-rtm-extrinsic-metadata" class="link">12.3. Extrinsic
Metadata</a>

<div class="paragraph">

The metadata about a pallets extrinsics, part of the main structure
([Section 12.1](#sect-rtm-structure)) and of the following format:

</div>

<div id="defn-rtm-signed-extension-metadata" class="exampleblock">

<div class="title">

Definition 170. [Signed Extension
Metadata](#defn-rtm-signed-extension-metadata)

</div>

<div class="content">

<div class="paragraph">

The metadata about the additional, signed data required to execute an
extrinsic.

</div>

<div class="stemblock">

<div class="content">

\\e_i = (n, y, a)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\n\\ is a string representing the unique signed extension identifier,
  which may be different from the type name.

- \\y\\ is a type Id ([Definition 160](#defn-rtm-type-id)) of the signed
  extension, with the data to be included in the extrinsic.

- \\a\\ is the type Id ([Definition 160](#defn-rtm-type-id)) of the
  additional signed data, with the data to be included in the signed
  payload.

</div>

</div>

seq: - id: name type: scale::string - id: type type:
scale::compact_int - id: additional type: scale::compact_int

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#id-cryptography-encoding" class="anchor"></a><a href="#id-cryptography-encoding" class="link">Appendix A:
Cryptography &amp; Encoding</a>

<div class="sectionbody">

<div class="paragraph">

Appendix chapter containing various protocol details

</div>

<div class="sect2">

### <a href="#chapter-crypto-algos" class="anchor"></a><a href="#chapter-crypto-algos" class="link">A.1. Cryptographic
Algorithms</a>

<div class="sect3">

#### <a href="#sect-hash-functions" class="anchor"></a><a href="#sect-hash-functions" class="link">A.1.1. Hash Functions</a>

<div class="sect4">

##### <a href="#sect-blake2" class="anchor"></a><a href="#sect-blake2" class="link">A.1.1.1. BLAKE2</a>

<div class="paragraph">

BLAKE2 is a collection of cryptographic hash functions known for their
high speed. Their design closely resembles BLAKE which has been a
finalist in the SHA-3 competition.

</div>

<div class="paragraph">

Polkadot is using the Blake2b variant which is optimized for 64-bit
platforms. Unless otherwise specified, the Blake2b hash function with a
256-bit output is used whenever Blake2b is invoked in this document. The
detailed specification and sample implementations of all variants of
Blake2 hash functions can be found in RFC 7693
cite:\[saarinen_blake2_2015\].

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-randomness" class="anchor"></a><a href="#sect-randomness" class="link">A.1.2. Randomness</a>

<div class="admonitionblock note">

|     |     |
|-----|-----|
|     | TBH |

</div>

</div>

<div class="sect3">

#### <a href="#sect-vrf" class="anchor"></a><a href="#sect-vrf" class="link">A.1.3. VRF</a>

<div class="paragraph">

A Verifiable Random Function (VRF) is a mathematical operation that
takes some input and produces a random number using a secret key along
with a proof of authenticity that this random number was generated using
the submitter’s secret key and the given input. The proof can be
verified by any challenger to ensure the random number generation is
valid and has not been tampered with (for example to the benfit of
submitter).

</div>

<div class="paragraph">

In Polkadot, VRFs are used for the BABE block production lottery by
[Block-Production-Lottery](#algo-block-production-lottery) and the
parachain approval voting mechanism ([Section
8.5](#sect-approval-voting)). The VRF uses mechanism similar to
algorithms introduced in the following papers:

</div>

<div class="ulist">

- [Making NSEC5 Practical for
  DNSSEC](https://eprint.iacr.org/2017/099.pdf) cite:\[papadopoulos17\]

- [DLEQ
  Proofs](https://blog.cloudflare.com/privacy-pass-the-math/#dleqproofs)

- [Verifiable Random Functions
  (VRFs)](https://tools.ietf.org/id/draft-goldbe-vrf-01.html)
  cite:\[goldberg17\]

</div>

<div class="paragraph">

It essentially generates a deterministic elliptic curve based Schnorr
signature as a verifiable random value. The elliptic curve group used in
the VRF function is the Ristretto group specified in:

</div>

<div class="ulist">

- <a href="https://ristretto.group/" class="bare">ristretto.group/</a>

</div>

<div id="defn-vrf-proof" class="exampleblock">

<div class="title">

Definition 171. [VRF Proof](#defn-vrf-proof)

</div>

<div class="content">

<div class="paragraph">

The **VRF proof** proves the correctness for an associated VRF output.
The VRF proof, \\P\\, is a datastructure of the following format:

</div>

<div class="stemblock">

<div class="content">

\\P = (C,S)\\ \\S = (b_0, ... b_31)\\

</div>

</div>

<div class="paragraph">

where \\C\\ is the challenge and \\S\\ is the 32-byte Schnorr poof. Both
are expressed as Curve25519 scalars as defined in Definition [Definition
172](#defn-vrf-dleq-prove).

</div>

</div>

</div>

<div id="defn-vrf-dleq-prove" class="exampleblock">

<div class="title">

Definition 172. [`DLEQ Prove`](#defn-vrf-dleq-prove)

</div>

<div class="content">

<div class="paragraph">

The \\"dleq_prove"(t, i)\\ function creates a proof for a given input,
\\i\\, based on the provided transcript, \\T\\.

</div>

<div class="paragraph">

First:

</div>

<div class="stemblock">

<div class="content">

\\t_1 = "append"(t, "'proto-name'", "'DLEQProof'")\\ \\t_2 =
"append"(t_1, "'vrf:h'", i)\\

</div>

</div>

<div class="paragraph">

Then the witness scalar is calculated, \\s_w\\, where \\w\\ is the
32-byte secret seed used for nonce generation in the context of sr25519.

</div>

<div class="stemblock">

<div class="content">

\\t_3 = "meta-AD"(t_2, "'proving\\00'", "more=False")\\ \\t_4 =
"meta-AD"(t_3, w_l, "more=True")\\ \\t_5 = "KEY"(t_4, w, "more=False")\\
\\t_6 = "meta-AD"(t_5, "'rng'", "more=False")\\ \\t_7 = "KEY"(t_6, r,
"more=False")\\ \\t_8 = "meta-AD"(t_7, e\_(64), "more=False")\\ \\(phi,
s_w) = "PRF"(t_8, "more=False")\\

</div>

</div>

<div class="paragraph">

where \\w_l\\ is length of the witness, encoded as a 32-bit
little-endian integer. \\r\\ is a 32-byte array containing the secret
witness scalar.

</div>

<div class="stemblock">

<div class="content">

\\l_1 = "append"(t_2, "'vrf:R=g^r'", s_w)\\ \\l_2 = "append"(l_1,
"'vrf:h^r'", s_i)\\ \\l_3 = "append"(l_2, "'vrf:pk'", s_p)\\ \\l_4 =
"append"(l_3, "'vrf:h^sk'", "vrf"\_o)\\

</div>

</div>

<div class="paragraph">

where

</div>

<div class="ulist">

- \\s_i\\ is the compressed Ristretto point of the scalar input.

- \\s_p\\ is the compressed Ristretto point of the public key.

- \\s_w\\ is the compressed Ristretto point of the wittness:

</div>

<div class="paragraph">

For the 64-byte challenge:

</div>

<div class="stemblock">

<div class="content">

\\l_5 = "meta-AD"(l_4, "'prove'", "more=False")\\ \\l_6 = "meta-AD"(l_5,
e\_(64), "more=True")\\ \\C = "PRF"(l_6, "more=False")\\

</div>

</div>

<div class="paragraph">

And the Schnorr proof:

</div>

<div class="stemblock">

<div class="content">

\\S = s_w - (C \* p)\\

</div>

</div>

<div class="paragraph">

where \\p\\ is the secret key.

</div>

</div>

</div>

<div id="defn-vrf-dleq-verify" class="exampleblock">

<div class="title">

Definition 173. [`DLEQ Verify`](#defn-vrf-dleq-verify)

</div>

<div class="content">

<div class="paragraph">

The \\"dleq_verify"(i, o, P, p_k)\\ function verifiers the VRF input,
\\i\\ against the output, \\o\\, with the associated proof ([Definition
171](#defn-vrf-proof)) and public key, \\p_k\\.

</div>

<div class="stemblock">

<div class="content">

\\t_1 = "append"(t, "'proto-name'", "'DLEQProof'")\\ \\t_2 =
"append"(t_1, "'vrf:h'", s_i)\\ \\t_3 = "append"(t_2, "'vrf:R=g^r'",
R)\\ \\t_4 = "append"(t_3, "'vrf:h^r'", H)\\ \\t_5 = "append"(t_4,
"'vrf:pk'", p_k)\\ \\t_6 = "append"(t_5, "'vrf:h^sk'", o)\\

</div>

</div>

<div class="paragraph">

where

</div>

<div class="ulist">

- \\R\\ is calculated as:

  <div class="stemblock">

  <div class="content">

  \\R = C in P xx p_k + S in P + B\\

  </div>

  </div>

  <div class="paragraph">

  where \\B\\ is the Ristretto basepoint.

  </div>

- \\H\\ is calculated as:

  <div class="stemblock">

  <div class="content">

  \\H = C in P xx o + S in P xx i\\

  </div>

  </div>

</div>

<div class="paragraph">

The challenge is valid if \\C in P\\ equals \\y\\:

</div>

<div class="stemblock">

<div class="content">

\\t_7 = "meta-AD"(t_6, "'prove'", "more=False")\\ \\t_8 = "meta-AD"(t_7,
e\_(64), "more=True")\\ \\y = "PRF"(t_8, "more=False")\\

</div>

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-transcript" class="anchor"></a><a href="#id-transcript" class="link">A.1.3.1. Transcript</a>

<div class="paragraph">

A VRF transcript serves as a domain-specific separator of cryptographic
protocols and is represented as a mathematical object, as defined by
Merlin, which defines how that object is generated and encoded. The
usage of the transcript is implementation specific, such as for certain
mechanisms in the Availability & Validity chapter ([Chapter
8](#chapter-anv)), and is therefore described in more detail in those
protocols. The input value used to initiate the transcript is referred
to as a *context* ([Definition 174](#defn-vrf-context)).

</div>

<div id="defn-vrf-context" class="exampleblock">

<div class="title">

Definition 174. [VRF Contex](#defn-vrf-context)

</div>

<div class="content">

<div class="paragraph">

The **VRF context** is a constant byte array used to initiate VRF
transcript. The VRF context is constant for all users of the VRF for the
specific context for which the VRF function is used. Context prevents
VRF values generated by the same nodes for other purposes to be reused
for purposes not meant to. For example, the VRF context for BABE
Production lottery defined in [Section
5.2](#sect-block-production-lottery) is set to be "substrate-babe-vrf".

</div>

</div>

</div>

<div id="defn-vrf-transcript" class="exampleblock">

<div class="title">

Definition 175. [VRF Transcript](#defn-vrf-transcript)

</div>

<div class="content">

<div class="paragraph">

A **transcript**, or VRF transcript, is a STROBE object, \\"obj"\\, as
defined in the STROBE documentation, respectively section ["5. State of
a STROBE object"](https://strobe.sourceforge.io/specs/#object).

</div>

<div class="stemblock">

<div class="content">

\\"obj" = ("st","pos","pos"\_("begin"),I_0)\\

</div>

</div>

<div class="paragraph">

where:

</div>

<div class="ulist">

- The duplex state, \\"st"\\, is a 200-byte array created by the
  [keccak-f1600 sponge
  function](https://keccak.team/keccak_specs_summary.html) on the
  [initial STROBE
  state](https://strobe.sourceforge.io/specs/#object.initial).
  Specifically, `R` is of value `166` and `X.Y.Z` is of value `1.0.2`.

- \\"pos"\\ has the initial value of `0`.

- \\"pos"\_("begin")\\ has the initial value of `0`.

- \\I_0\\ has the initial value of `0`.

</div>

<div class="paragraph">

Then, the `meta-AD` operation ([Definition
176](#defn-strobe-operations)) (where `more=False`) is used to add the
protocol label `Merlin v1.0` to \\"obj"\\ followed by *appending*
([Section A.1.3.1.1](#sect-vrf-appending-messages)) label `dom-step` and
its corresponding context, \\ctx\\, resulting in the final transcript,
\\T\\.

</div>

<div class="stemblock">

<div class="content">

\\t = "meta-AD"(obj, "'Merlin v1.0'", "False")\\ \\T = "append"(t,
"'dom-step'", "ctx")\\

</div>

</div>

<div class="paragraph">

\\"ctx"\\ serves as an arbitrary identifier/separator and its value is
defined by the protocol specification individually. This transcript is
treated just like a STROBE object, wherein any operations ([Definition
176](#defn-strobe-operations)) on it modify the values such as \\"pos"\\
and \\"pos"\_("begin")\\.

</div>

<div class="paragraph">

Formally, when creating a transcript we refer to it as
\\"Transcript"(ctx)\\.

</div>

</div>

</div>

<div id="defn-strobe-operations" class="exampleblock">

<div class="title">

Definition 176. [STROBE Operations](#defn-strobe-operations)

</div>

<div class="content">

<div class="paragraph">

STROBE operations are described in the [STROBE
specification](https://strobe.sourceforge.io/specs/), respectively
section ["6. Strobe
operations"](https://strobe.sourceforge.io/specs/#ops). Operations are
indicated by their corresponding bitfield, as described in section
["6.2. Operations and
flags"](https://strobe.sourceforge.io/specs/#ops.flags) and implemented
as described in section ["7. Implementation of
operations"](https://strobe.sourceforge.io/specs/#ops.impl)

</div>

</div>

</div>

<div class="sect5">

###### <a href="#sect-vrf-appending-messages" class="anchor"></a><a href="#sect-vrf-appending-messages" class="link">Appending
Messages</a>

<div class="paragraph">

Appending messages, or "data", to the transcript ([Definition
175](#defn-vrf-transcript)) first requires `meta-AD` operations for a
given label of the messages, including the size of the message, followed
by an `AD` operation on the message itself. The size of the message is a
4-byte, little-endian encoded integer.

</div>

<div class="stemblock">

<div class="content">

\\T_0 = "meta-AD"(T, l, "False")\\ \\T_1 = "meta-AD"(T_0, m_l, "True")\\
\\T_2 = "AD"(T_1, m, "False")\\

</div>

</div>

<div class="paragraph">

where \\T\\ is the transcript ([Definition 175](#defn-vrf-transcript)),
\\l\\ is the given label and \\m\\ the message, respectively \\m_l\\
representing its size. \\T_2\\ is the resulting transcript with the
appended data. STROBE operations are described in [Definition
176](#defn-strobe-operations).

</div>

<div class="paragraph">

Formally, when appending a message we refer to it as \\"append"(T, l,
m)\\.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-cryptographic-keys" class="anchor"></a><a href="#sect-cryptographic-keys" class="link">A.1.4. Cryptographic
Keys</a>

<div class="paragraph">

Various types of keys are used in Polkadot to prove the identity of the
actors involved in the Polkadot Protocols. To improve the security of
the users, each key type has its own unique function and must be treated
differently, as described by this Section.

</div>

<div id="defn-account-key" class="exampleblock">

<div class="title">

Definition 177. [Account Key](#defn-account-key)

</div>

<div class="content">

<div class="paragraph">

**Account key \\(sk^a,pk^a)\\** is a key pair of type of either of the
schemes in the following table:

</div>

| Key Scheme | Description                                                                                                                                                                                                                                                                                                                                                                                                       |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| sr25519    | Schnorr signature on Ristretto compressed ed25519 points as implemented in TODO                                                                                                                                                                                                                                                                                                                                   |
| ed25519    | The ed25519 signature complies with cite:\[josefsson_edwards-curve_2017\] except for the verification process which adhere to Ed25519 Zebra variant specified in cite:\[devalence_ed25519zebra_2020\]. In short, the signature point is not assumed to be on in the prime ordered subgroup group. As such, the verifier must explicitly clear the cofactor during the course of verifying the signature equation. |
| secp256k1  | Only for outgoing transfer transactions.                                                                                                                                                                                                                                                                                                                                                                          |

Table 2. List of the public key scheme which can be used for an account
key

<div class="paragraph">

An account key can be used to sign transactions among other accounts and
balance-related functions. There are two prominent subcategories of
account keys namely "stash keys" and "controller keys", each being used
for a different function. Keys defined in [Definition
177](#defn-account-key), [Definition 178](#defn-stash-key) and
[Definition 179](#defn-controller-key) are created and managed by the
user independent of the Polkadot implementation. The user notifies the
network about the used keys by submitting a transaction, as defined in
[Section A.1.4.2](#sect-creating-controller-key) and [Section
A.1.4.5](#sect-certifying-keys) respectively.

</div>

</div>

</div>

<div id="defn-stash-key" class="exampleblock">

<div class="title">

Definition 178. [Stash Key](#defn-stash-key)

</div>

<div class="content">

<div class="paragraph">

The **Stash key** is a type of account key that holds funds bonded for
staking (described in [Section A.1.4.1](#sect-staking-funds)) to a
particular controller key (defined in [Definition
179](#defn-controller-key)). As a result, one may actively participate
with a stash key keeping the stash key offline in a secure location. It
can also be used to designate a Proxy account to vote in governance
proposals, as described in [Section
A.1.4.2](#sect-creating-controller-key). The Stash key holds the
majority of the users’ funds and should neither be shared with anyone,
saved on an online device, nor used to submit extrinsics.

</div>

</div>

</div>

<div id="defn-controller-key" class="exampleblock">

<div class="title">

Definition 179. [Controller Key](#defn-controller-key)

</div>

<div class="content">

<div class="paragraph">

The **Controller key** is a type of account key that acts on behalf of
the Stash account. It signs transactions that make decisions regarding
the nomination and the validation of the other keys. It is a key that
will be in direct control of a user and should mostly be kept offline,
used to submit manual extrinsics. It sets preferences like payout
account and commission, as described in [Section
A.1.4.4](#sect-controller-settings). If used for a validator, it
certifies the session keys, as described in [Section
A.1.4.5](#sect-certifying-keys). It only needs the required funds to pay
transaction fees \[TODO: key needing fund needs to be defined\].

</div>

</div>

</div>

<div id="defn-session-key" class="exampleblock">

<div class="title">

Definition 180. [Session Keys](#defn-session-key)

</div>

<div class="content">

<div class="paragraph">

**Session keys** are short-lived keys that are used to authenticate
validator operations. Session keys are generated by the Polkadot Host
and should be changed regularly due to security reasons. Nonetheless, no
validity period is enforced by the Polkadot protocol on session keys.
Various types of keys used by the Polkadot Host are presented in [Table
3](#tabl-session-keys):

</div>

| Protocol   | Key scheme |
|------------|------------|
| GRANDPA    | ED25519    |
| BABE       | SR25519    |
| I’m Online | SR25519    |
| Parachain  | SR25519    |

Table 3. List of key schemes which are used for session keys depending
on the protocol

<div class="paragraph">

Session keys must be accessible by certain Polkadot Host APIs defined in
Appendix [Appendix B](#chap-host-api). Session keys are *not* meant to
control the majority of the users’ funds and should only be used for
their intended purpose.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#sect-staking-funds" class="anchor"></a><a href="#sect-staking-funds" class="link">A.1.4.1. Holding and staking
funds</a>

<div class="admonitionblock note">

|     |     |
|-----|-----|
|     | TBH |

</div>

</div>

<div class="sect4">

##### <a href="#sect-creating-controller-key" class="anchor"></a><a href="#sect-creating-controller-key" class="link">A.1.4.2. Creating a
Controller key</a>

<div class="admonitionblock note">

|     |     |
|-----|-----|
|     | TBH |

</div>

</div>

<div class="sect4">

##### <a href="#sect-designating-proxy" class="anchor"></a><a href="#sect-designating-proxy" class="link">A.1.4.3. Designating a
proxy for voting</a>

<div class="admonitionblock note">

|     |     |
|-----|-----|
|     | TBH |

</div>

</div>

<div class="sect4">

##### <a href="#sect-controller-settings" class="anchor"></a><a href="#sect-controller-settings" class="link">A.1.4.4. Controller
settings</a>

<div class="admonitionblock note">

|     |     |
|-----|-----|
|     | TBH |

</div>

</div>

<div class="sect4">

##### <a href="#sect-certifying-keys" class="anchor"></a><a href="#sect-certifying-keys" class="link">A.1.4.5. Certifying
keys</a>

<div class="paragraph">

Due to security considerations and Runtime upgrades, the session keys
are supposed to  be changed regularly. As such, the new session keys
need to be certified by a controller key before putting them in use. The
controller only needs to create a certificate by signing a session
public key and broadcasting this certificate via an extrinsic. \[TODO:
spec the detail of the data structure of the certificate etc.\]

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#chapter-encoding" class="anchor"></a><a href="#chapter-encoding" class="link">A.2. Auxiliary Encodings</a>

<div id="defn-unix-time" class="exampleblock">

<div class="title">

Definition 181. [Unix Time](#defn-unix-time)

</div>

<div class="content">

<div class="paragraph">

By **Unix time**, we refer to the unsigned, little-endian encoded 64-bit
integer which stores the number of **milliseconds** that have elapsed
since the Unix epoch, that is the time 00:00:00 UTC on 1 January 1970,
minus leap seconds. Leap seconds are ignored, and every day is treated
as if it contained exactly 86’400 seconds.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-binary-enconding" class="anchor"></a><a href="#id-binary-enconding" class="link">A.2.1. Binary Enconding</a>

<div id="defn-byte-sequence" class="exampleblock">

<div class="title">

Definition 182. [Sequence of Bytes](#defn-byte-sequence)

</div>

<div class="content">

<div class="paragraph">

By a **sequences of bytes** or a **byte array**, \\b\\, of length \\n\\,
we refer to

</div>

<div class="stemblock">

<div class="content">

\\b := (b_0, b_1, ..., b\_{n - 1}) " such that " 0 \<= b_i \<= 255\\

</div>

</div>

<div class="paragraph">

We define \\bbb B_n\\ to be the **set of all byte arrays of length
\\n\\**. Furthermore, we define:

</div>

<div class="stemblock">

<div class="content">

\\bbb B := uuu\_(i=0)^infty bbb B_i\\

</div>

</div>

<div class="paragraph">

We represent the concatenation of byte arrays \\a :=(a_0, ..., a_n)\\
and \\b :=(b_0, ..., b_m)\\ by:

</div>

<div class="stemblock">

<div class="content">

\\a \|\\ b :=(a_0, ..., a_n, b_0, ..., b_m)\\

</div>

</div>

</div>

</div>

<div id="defn-bit-rep" class="exampleblock">

<div class="title">

Definition 183. [Bitwise Representation](#defn-bit-rep)

</div>

<div class="content">

<div class="paragraph">

For a given byte \\0 \<= b \<= 255\\ the **bitwise representation** in
bits \\b_i in {0, 1}\\ is defined as:

</div>

<div class="stemblock">

<div class="content">

\\b := b_7 ... b_0\\

</div>

</div>

<div class="paragraph">

where

</div>

<div class="stemblock">

<div class="content">

\\b = 2^7 b_7 + 2^6 b_6 + ... + 2^0 b_0\\

</div>

</div>

</div>

</div>

<div id="defn-little-endian" class="exampleblock">

<div class="title">

Definition 184. [Little Endian](#defn-little-endian)

</div>

<div class="content">

<div class="paragraph">

By the **little-endian** representation of a non-negative integer,
\\I\\, represented as

</div>

<div class="stemblock">

<div class="content">

\\I = (B_n ... B_0)\_256\\

</div>

</div>

<div class="paragraph">

in base 256, we refer to a byte array \\B = (b_0, b_1, ..., b_n)\\ such
that

</div>

<div class="stemblock">

<div class="content">

\\b_i :=B_i\\

</div>

</div>

<div class="paragraph">

Accordingly, we define the function \\sf "Enc"\_(sf "LE")\\:

</div>

<div class="stemblock">

<div class="content">

\\sf "Enc"\_(sf "LE"): bbb Z^+ -\> bbb B; (B_n ... B_0)\_256 \|-\>
(B\_{0,} B_1, ... , B_n)\\

</div>

</div>

</div>

</div>

<div id="defn-uint32" class="exampleblock">

<div class="title">

Definition 185. [UINT32](#defn-uint32)

</div>

<div class="content">

<div class="paragraph">

By **UINT32** we refer to a non-negative integer stored in a byte array
of length \\4\\ using little-endian encoding format.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-scale-codec" class="anchor"></a><a href="#sect-scale-codec" class="link">A.2.2. SCALE Codec</a>

<div class="paragraph">

The Polkadot Host uses *Simple Concatenated Aggregate Little-Endian”
(SCALE) codec* to encode byte arrays as well as other data structures.
SCALE provides a canonical encoding to produce consistent hash values
across their implementation, including the Merkle hash proof for the
State Storage.

</div>

<div id="defn-scale-decoding" class="exampleblock">

<div class="title">

Definition 186. [Decoding](#defn-scale-decoding)

</div>

<div class="content">

<div class="paragraph">

\\"Dec"\_("SC")(d)\\ refers to the decoding of a blob of data. Since the
SCALE codec is not self-describing, it’s up to the decoder to validate
whether the blob of data can be deserialized into the given type or data
structure.

</div>

<div class="paragraph">

It’s accepted behavior for the decoder to partially decode the blob of
data. Meaning, any additional data that does not fit into a
datastructure can be ignored.

</div>

<div class="admonitionblock warning">

|     |                                                                                                                                                                                                                                                                                                                                                                |
|-----|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | Considering that the decoded data is never larger than the encoded message, this information can serve as a way to validate values that can vary in sizes, such as sequences ([Definition 192](#defn-scale-list)). The decoder should strictly use the size of the encoded data as an upper bound when decoding in order to prevent denial of service attacks. |

</div>

</div>

</div>

<div id="defn-scale-tuple" class="exampleblock">

<div class="title">

Definition 187. [Tuple](#defn-scale-tuple)

</div>

<div class="content">

<div class="paragraph">

The **SCALE codec** for **Tuple**, \\T\\, such that:

</div>

<div class="stemblock">

<div class="content">

\\T := (A_1,... A_n)\\

</div>

</div>

<div class="paragraph">

Where \\A_i\\’s are values of **different types**, is defined as:

</div>

<div class="stemblock">

<div class="content">

\\"Enc"\_("SC")(T) := "Enc"\_("SC")(A_1) "\|\|" "Enc"\_("SC")(A_2)
"\|\|" ... "\|\|" "Enc"\_("SC")(A_n)\\

</div>

</div>

</div>

</div>

<div class="paragraph">

In case of a tuple (or a structure), the knowledge of the shape of data
is not encoded even though it is necessary for decoding. The decoder
needs to derive that information from the context where the
encoding/decoding is happening.

</div>

<div id="defn-varrying-data-type" class="exampleblock">

<div class="title">

Definition 188. [Varying Data Type](#defn-varrying-data-type)

</div>

<div class="content">

<div class="paragraph">

We define a **varying data** type to be an ordered set of data types.

</div>

<div class="stemblock">

<div class="content">

\\cc T = {T_1, ..., T_n}\\

</div>

</div>

<div class="paragraph">

A value \\A\\ of varying date type is a pair
\\(A\_("Type"),A\_("Value"))\\ where \\A\_("Type") = T_i\\ for some
\\T_i in cc T\\ and \\A\_("Value")\\ is its value of type \\T_i\\, which
can be empty. We define \\"idx"(T_i) = i - 1\\, unless it is explicitly
defined as another value in the definition of a particular varying data
type.

</div>

<div class="paragraph">

In particular, we define two specific varying data which are frequently
used in various part of Polkadot protocol: *Option* ([Definition
190](#defn-option-type)) and *Result* ([Definition
191](#defn-result-type)).

</div>

</div>

</div>

<div id="defn-scale-variable-type" class="exampleblock">

<div class="title">

Definition 189. [Encoding of Varying Data
Type](#defn-scale-variable-type)

</div>

<div class="content">

<div class="paragraph">

The SCALE codec for value \\A = (A\_("Type"), A\_("Value"))\\ of varying
data type \\cc T = {T_i, ... T_n}\\, formally referred to as
\\"Enc"\_("SC")(A)\\ is defined as follows:

</div>

<div class="stemblock">

<div class="content">

\\"Enc"\_("SC")(A) := "Enc"\_("SC")("idx"(A\_("Type")) "\|\|"
"Enc"\_("SC")(A\_("Value")))\\

</div>

</div>

<div class="paragraph">

Where \\"idx"\\ is a 8-bit integer determining the type of \\A\\. In
particular, for the optional type defined in [Definition
188](#defn-varrying-data-type), we have:

</div>

<div class="stemblock">

<div class="content">

\\"Enc"\_("SC")("None", phi) := 0\_(bbb B_1)\\

</div>

</div>

<div class="paragraph">

The SCALE codec does not encode the correspondence between the value and
the data type it represents; the decoder needs prior knowledge of such
correspondence to decode the data.

</div>

</div>

</div>

<div id="defn-option-type" class="exampleblock">

<div class="title">

Definition 190. [Option Type](#defn-option-type)

</div>

<div class="content">

<div class="paragraph">

The **Option** type is a varying data type of \\{"None",T_2}\\ which
indicates if data of \\T_2\\ type is available (referred to as *some*
state) or not (referred to as *empty*, *none* or *null* state). The
presence of type *none*, indicated by \\"idx"(T\_("None")) = 0\\,
implies that the data corresponding to \\T_2\\ type is not available and
contains no additional data. Where as the presence of type \\T_2\\
indicated by \\"idx"(T_2) = 1\\ implies that the data is available.

</div>

</div>

</div>

<div id="defn-result-type" class="exampleblock">

<div class="title">

Definition 191. [Result Type](#defn-result-type)

</div>

<div class="content">

<div class="paragraph">

The **Result** type is a varying data type of \\{T_1, T_2}\\ which is
used to indicate if a certain operation or function was executed
successfully (referred to as "ok" state) or not (referred to as "error"
state). \\T_1\\ implies success, \\T_2\\ implies failure. Both types can
either contain additional data or are defined as empty type otherwise.

</div>

</div>

</div>

<div id="defn-scale-list" class="exampleblock">

<div class="title">

Definition 192. [Sequence](#defn-scale-list)

</div>

<div class="content">

<div class="paragraph">

The **SCALE codec** for **sequence** \\S\\ such that:

</div>

<div class="stemblock">

<div class="content">

\\S := A_1, ... A_n\\

</div>

</div>

<div class="paragraph">

where \\A_i\\’s are values of **the same type** (and the decoder is
unable to infer value of \\n\\ from the context) is defined as:

</div>

<div class="stemblock">

<div class="content">

\\"Enc"\_("SC")(S) := "Enc"\_("SC")^("Len")(abs(S)) "\|\|"
"Enc"\_("SC")(A_2) "\|\|" ... "\|\|" "Enc"\_("SC")(A_n)\\

</div>

</div>

<div class="paragraph">

where \\"Enc"\_("SC")^("Len")\\ is defined in [Definition
198](#defn-sc-len-encoding).

</div>

<div class="paragraph">

In some cases, the length indicator \\"Enc"\_("SC")^("Len")(abs(S))\\ is
omitted if the length of the sequence is fixed and known by the decoder
upfront. Such cases are explicitly stated by the definition of the
corresponding type.

</div>

</div>

</div>

<div id="defn-scale-dictionary" class="exampleblock">

<div class="title">

Definition 193. [Dictionary](#defn-scale-dictionary)

</div>

<div class="content">

<div class="paragraph">

SCALE codec for **dictionary** or **hashtable** D with key-value pairs
\\(k_i, v_i)\\s such that:

</div>

<div class="stemblock">

<div class="content">

\\D := {(k_1, v_1), ... (k_n, v_n)}\\

</div>

</div>

<div class="paragraph">

is defined the SCALE codec of \\D\\ as a sequence of key value pairs (as
tuples):

</div>

<div class="stemblock">

<div class="content">

\\"Enc"\_("SC")(D) := "Enc"\_("SC")^("Size")(abs(D)) "\|\|"
"Enc"\_("SC")(k_1, v_1) "\|\|"..."\|\|" "Enc"\_("SC")(k_n, v_n)\\

</div>

</div>

<div class="paragraph">

where \\"Enc"\_("SC")^("Size")\\ is encoded the same way as
\\"Enc"\_("SC")^("Len")\\ but argument \\"Size"\\ refers to the number
of key-value pairs rather than the length.

</div>

</div>

</div>

<div id="defn-scale-boolean" class="exampleblock">

<div class="title">

Definition 194. [Boolean](#defn-scale-boolean)

</div>

<div class="content">

<div class="paragraph">

The SCALE codec for a **boolean value** \\b\\ defined as a byte as
follows:

</div>

<div class="stemblock">

<div class="content">

\\"Enc"\_("SC"): {"False", "True"} -\> bbb B_1\\ \\b -\> {(0,
b="False"),(1, b="True"):}\\

</div>

</div>

</div>

</div>

<div id="defn-scale-string" class="exampleblock">

<div class="title">

Definition 195. [String](#defn-scale-string)

</div>

<div class="content">

<div class="paragraph">

The SCALE codec for a **string value** is an encoded sequence
([Definition 192](#defn-scale-list)) consisting of UTF-8 encoded bytes.

</div>

</div>

</div>

<div id="defn-scale-fixed-length" class="exampleblock">

<div class="title">

Definition 196. [Fixed Length](#defn-scale-fixed-length)

</div>

<div class="content">

<div class="paragraph">

The SCALE codec, \\"Enc"\_("SC")\\, for other types such as fixed length
integers not defined here otherwise, is equal to little endian encoding
of those values defined in [Definition 184](#defn-little-endian).

</div>

</div>

</div>

<div id="defn-scale-empty" class="exampleblock">

<div class="title">

Definition 197. [Empty](#defn-scale-empty)

</div>

<div class="content">

<div class="paragraph">

The SCALE codec, \\"Enc"\_("SC")\\, for an empty type is defined to a
byte array of zero length and depicted as \\phi\\.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#sect-sc-length-and-compact-encoding" class="anchor"></a><a href="#sect-sc-length-and-compact-encoding" class="link">A.2.2.1.
Length and Compact Encoding</a>

<div class="paragraph">

SCALE Length encoding is used to encode integer numbers of variying
sizes prominently in an encoding length of arrays:

</div>

<div id="defn-sc-len-encoding" class="exampleblock">

<div class="title">

Definition 198. [Length Encoding](#defn-sc-len-encoding)

</div>

<div class="content">

<div class="paragraph">

**SCALE Length encoding**, \\"Enc"\_("SC")^("Len")\\, also known as a
*compact encoding*, of a non-negative number \\n\\ is defined as
follows:

</div>

<div class="stemblock">

<div class="content">

\\"Enc"\_("SC")^("Len"): bbb N -\> bbb B\\ \\n -\> b := {(l_1, 0 \<= n
\< 2^6),(i_1 i_2, 2^6 \<= n \< 2^14),(j_1 j_2 j_3, 2^14 \<= n \<
2^30),(k_1 k_2 ... k_m, 2^30\<=n):}\\

</div>

</div>

<div class="paragraph">

in where the least significant bits of the first byte of byte array b
are defined as follows:

</div>

<div class="stemblock">

<div class="content">

\\l_1^1 l_1^0 = 00\\ \\i_1^1 i_1^0 = 01\\ \\j_1^1 j_1^0 = 10\\ \\k_1^1
k_1^0 = 11\\

</div>

</div>

<div class="paragraph">

and the rest of the bits of \\b\\ store the value of \\n\\ in
little-endian format in base-2 as follows:

</div>

<div class="stemblock">

<div class="content">

\\n := { (l_1^7 ... l_1^3 l_1^2, n \< 2^6), (i_2^7 ... i_2^0 i_1^7 ..
i_1^2, 2^6 \<= n \< 2^14), (j_4^7 ... j_4^0 j_3^7 ... j_1^7 ... j_1^2,
2^14 \<= n \< 2^30), (k_2 + k_3 2^8 + k_4 2^(2 xx
8)+...+k_m2^((m-2)8),2^30 \<= n) :}\\

</div>

</div>

<div class="paragraph">

such that:

</div>

<div class="stemblock">

<div class="content">

\\k_1^7 ... k_1^3 k_1^2 := m-4\\

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-hex-encoding" class="anchor"></a><a href="#id-hex-encoding" class="link">A.2.3. Hex Encoding</a>

<div class="paragraph">

Practically, it is more convenient and efficient to store and process
data which is stored in a byte array. On the other hand, the trie keys
are broken into 4-bits nibbles. Accordingly, we need a method to encode
sequences of 4-bits nibbles into byte arrays canonically. To this aim,
we define hex encoding function \\"Enc" ("HE")("PK")\\ as follows:

</div>

<div id="defn-hex-encoding" class="exampleblock">

<div class="title">

Definition 199. [Hex Encoding](#defn-hex-encoding)

</div>

<div class="content">

<div class="paragraph">

Suppose that \\"PK" = (k_1, ... k_n)\\ is a sequence of nibbles, then:

</div>

<div class="stemblock">

<div class="content">

\\"Enc"\_("HE")("PK") := {("Nibbles"\_4,-\>, bbb B),("PK" = (k_1, ...
k_n),-\>,{((16k_1+k_2,...,16k\_(2i-1)+k\_(2i)),n=2i),((k_1,16k_2+k_3,...,16k\_(2i)+k\_(2i+1)),n
= 2i+1):}):}\\

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#chapter-genesis" class="anchor"></a><a href="#chapter-genesis" class="link">A.3. Genesis State</a>

<div class="paragraph">

The genesis state is a set of key-value pairs representing the initial
state of the Polkadot state storage. It can be retrieved from [the
Polkadot
repository](https://github.com/paritytech/polkadot/tree/master/node/service/chain-specs).
While each of those key-value pairs offers important identifiable
information to the Runtime, to the Polkadot Host they are a transparent
set of arbitrary chain- and network-dependent keys and values. The only
exception to this are the `:code` ([Section
2.6.2](#sect-loading-runtime-code)) and `:heappages` ([Section
2.6.3.1](#sect-memory-management)) keys, which are used by the Polkadot
Host to initialize the WASM environment and its Runtime. The other keys
and values are unspecified and solely depend on the chain and
respectively its corresponding Runtime. On initialization the data
should be inserted into the state storage with the Host API ([Section
B.2.1](#sect-storage-set)).

</div>

<div class="paragraph">

As such, Polkadot does not define a formal genesis block. Nonetheless
for the compatibility reasons in several algorithms, the Polkadot Host
defines the *genesis header* ([Definition 200](#defn-genesis-header)).
By the abuse of terminology, "genesis block" refers to the hypothetical
parent of block number *1* which holds genesis header as its header.

</div>

<div id="defn-genesis-header" class="exampleblock">

<div class="title">

Definition 200. [Genesis Header](#defn-genesis-header)

</div>

<div class="content">

<div class="paragraph">

The Polkadot genesis header is a data structure conforming to block
header format ([Definition 10](#defn-block-header)). It contains the
following values:

</div>

| Block header field | Genesis Header Value                                                                                                 |
|--------------------|----------------------------------------------------------------------------------------------------------------------|
| `parent_hash`      | *0*                                                                                                                  |
| `number`           | *0*                                                                                                                  |
| `state_root`       | Merkle hash of the state storage trie ([Definition 29](#defn-merkle-value)) after inserting the genesis state in it. |
| `extrinsics_root`  | *0*                                                                                                                  |
| `digest`           | *0*                                                                                                                  |

</div>

</div>

</div>

<div class="sect2">

### <a href="#chapter-erasure-encoding" class="anchor"></a><a href="#chapter-erasure-encoding" class="link">A.4. Erasure
Encoding</a>

<div class="sect3">

#### <a href="#sect-erasure-encoding" class="anchor"></a><a href="#sect-erasure-encoding" class="link">A.4.1. Erasure
Encoding</a>

<div class="admonitionblock note">

|     |                                               |
|-----|-----------------------------------------------|
|     | Erasure Encoding has not been documented yet. |

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#chap-host-api" class="anchor"></a><a href="#chap-host-api" class="link">Appendix B: Host API</a>

<div class="sectionbody">

<div class="paragraph">

Description of the expected environment available for import by the
Polkadot Runtime

</div>

<div class="sect2">

### <a href="#id-preliminaries-4" class="anchor"></a><a href="#id-preliminaries-4" class="link">B.1. Preliminaries</a>

<div class="paragraph">

The Polkadot Host API is a set of functions that the Polkadot Host
exposes to Runtime to access external functions needed for various
reasons, such as the Storage of the content, access and manipulation,
memory allocation, and also efficiency. The encoding of each data type
is specified or referenced in this section. If the encoding is not
mentioned, then the default Wasm encoding is used, such as little-endian
byte ordering for integers.

</div>

<div id="defn-host-api-at-state" class="exampleblock">

<div class="title">

Definition 201. [Exposed Host API](#defn-host-api-at-state)

</div>

<div class="content">

<div class="paragraph">

By \\"RE"\_B\\ we refer to the API exposed by the Polkadot Host which
interact, manipulate and response based on the state storage whose state
is set at the end of the execution of block \\B\\.

</div>

</div>

</div>

<div id="defn-runtime-pointer" class="exampleblock">

<div class="title">

Definition 202. [Runtime Pointer](#defn-runtime-pointer)

</div>

<div class="content">

<div class="paragraph">

The **Runtime pointer** type is an unsigned 32-bit integer representing
a pointer to data in memory. This pointer is the primary way to exchange
data of fixed/known size between the Runtime and Polkadot Host.

</div>

</div>

</div>

<div id="defn-runtime-pointer-size" class="exampleblock">

<div class="title">

Definition 203. [Runtime Pointer Size](#defn-runtime-pointer-size)

</div>

<div class="content">

<div class="paragraph">

The **Runtime pointer-size** type is an unsigned 64-bit integer,
representing two consecutive integers. The least significant is
**Runtime pointer** ([Definition 202](#defn-runtime-pointer)). The most
significant provides the size of the data in bytes. This representation
is the primary way to exchange data of arbitrary/dynamic sizes between
the Runtime and the Polkadot Host.

</div>

</div>

</div>

<div id="defn-lexicographic-ordering" class="exampleblock">

<div class="title">

Definition 204. [Lexicographic ordering](#defn-lexicographic-ordering)

</div>

<div class="content">

<div class="paragraph">

**Lexicographic ordering** refers to the ascending ordering of bytes or
byte arrays, such as:

</div>

<div class="stemblock">

<div class="content">

\\\[0,0,2\]\<\[0,1,1\]\<\[1\]\<\[1,1,0\]\<\[2\]\<\[...\]\\

</div>

</div>

<div class="paragraph">

The functions are specified in each subsequent subsection for each
category of those functions.

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-storage-api" class="anchor"></a><a href="#sect-storage-api" class="link">B.2. Storage</a>

<div class="paragraph">

Interface for accessing the storage from within the runtime.

</div>

<div class="admonitionblock important">

|     |                                                                                                                                                                                                                                                                                                                                                          |
|-----|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | As of now, the storage API should silently ignore any keys that start with the `:child_storage:default:` prefix. This applies to reading and writing. If the function expects a return value, then *None* ([Definition 190](#defn-option-type)) should be returned. See [substrate issue \#12461](https://github.com/paritytech/substrate/issues/12461). |

</div>

<div id="defn-state-version" class="exampleblock">

<div class="title">

Definition 205. [State Version](#defn-state-version)

</div>

<div class="content">

<div class="paragraph">

The state version, \\v\\, dictates how a merkle root should be
constructed. The datastructure is a varying type of the following
format:

</div>

<div class="stemblock">

<div class="content">

\\v = {(0, "full values"),(1, "node hashes"):}\\

</div>

</div>

<div class="paragraph">

where \\0\\ indicates that the values of the keys should be inserted
into the trie directly and \\1\\ makes use of "node hashes" when
calculating the merkle proof ([Definition 28](#defn-hashed-subvalue)).

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-storage-set" class="anchor"></a><a href="#sect-storage-set" class="link">B.2.1.
<code>ext_storage_set</code></a>

<div class="paragraph">

Sets the value under a given key into storage.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype" class="anchor"></a><a href="#id-version-1-prototype" class="link">B.2.1.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_set_version_1
        (param $key i64) (param $value i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  containing the key.

- `value`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  containing the value.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_storage_get" class="anchor"></a><a href="#id-ext_storage_get" class="link">B.2.2.
<code>ext_storage_get</code></a>

<div class="paragraph">

Retrieves the value associated with the given key from storage.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-2" class="anchor"></a><a href="#id-version-1-prototype-2" class="link">B.2.2.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_get_version_1
        (param $key i64) (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  containing the key.

- `result`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) returning the SCALE encoded *Option*
  value ([Definition 190](#defn-option-type)) containing the value.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_storage_read" class="anchor"></a><a href="#id-ext_storage_read" class="link">B.2.3.
<code>ext_storage_read</code></a>

<div class="paragraph">

Gets the given key from storage, placing the value into a buffer and
returning the number of bytes that the entry in storage has beyond the
offset.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-3" class="anchor"></a><a href="#id-version-1-prototype-3" class="link">B.2.3.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_read_version_1
        (param $key i64) (param $value_out i64) (param $offset i32) (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  containing the key.

- `value_out`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) containing the buffer to which the
  value will be written to. This function will never write more then the
  length of the buffer, even if the value’s length is bigger.

- `offset`: an u32 integer (typed as i32 due to wasm types) containing
  the offset beyond the value should be read from.

- `result`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) pointing to a SCALE encoded *Option*
  value ([Definition 190](#defn-option-type)) containing an unsigned
  32-bit integer representing the number of bytes left at supplied
  `offset`. Returns *None* if the entry does not exists.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_storage_clear" class="anchor"></a><a href="#id-ext_storage_clear" class="link">B.2.4.
<code>ext_storage_clear</code></a>

<div class="paragraph">

Clears the storage of the given key and its value. Non-existent entries
are silently ignored.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-4" class="anchor"></a><a href="#id-version-1-prototype-4" class="link">B.2.4.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_clear_version_1
        (param $key_data i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  containing the key.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_storage_exists" class="anchor"></a><a href="#id-ext_storage_exists" class="link">B.2.5.
<code>ext_storage_exists</code></a>

<div class="paragraph">

Checks whether the given key exists in storage.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-5" class="anchor"></a><a href="#id-version-1-prototype-5" class="link">B.2.5.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_exists_version_1
        (param $key_data i64) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  containing the key.

- `return`: an i32 integer value equal to *1* if the key exists or a
  value equal to *0* if otherwise.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_storage_clear_prefix" class="anchor"></a><a href="#id-ext_storage_clear_prefix" class="link">B.2.6.
<code>ext_storage_clear_prefix</code></a>

<div class="paragraph">

Clear the storage of each key/value pair where the key starts with the
given prefix.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-6" class="anchor"></a><a href="#id-version-1-prototype-6" class="link">B.2.6.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_clear_prefix_version_1
        (param $prefix i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `prefix`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) containing the prefix.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype" class="anchor"></a><a href="#id-version-2-prototype" class="link">B.2.6.2. Version 2 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_clear_prefix_version_2
        (param $prefix i64) (param $limit i64)
        (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `prefix`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) containing the prefix.

- `limit`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to an *Option* type ([Definition 190](#defn-option-type)) containing
  an unsigned 32-bit integer indicating the limit on how many keys
  should be deleted. No limit is applied if this is *None*. Any keys
  created during the current block execution do not count towards the
  limit.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the following variant, \\k\\:

  <div class="stemblock">

  <div class="content">

  \\k = {(0,-\> c),(1,-\> c):}\\

  </div>

  </div>

  <div class="paragraph">

  where *0* indicates that all keys of the child storage have been
  removed, followed by the number of removed keys, \\c\\. The variant
  *1* indicates that there are remaining keys, followed by the number of
  removed keys.

  </div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_storage_append" class="anchor"></a><a href="#id-ext_storage_append" class="link">B.2.7.
<code>ext_storage_append</code></a>

<div class="paragraph">

Append the SCALE encoded value to a SCALE encoded sequence ([Definition
192](#defn-scale-list)) at the given key. This function assumes that the
existing storage item is either empty or a SCALE encoded sequence and
that the value to append is also SCALE encoded and of the same type as
the items in the existing sequence.

</div>

<div class="paragraph">

To improve performance, this function is allowed to skip decoding the
entire SCALE encoded sequence and instead can just append the new item
to the end of the existing data and increment the length prefix
\\"Enc"\_("SC")^("Len")\\.

</div>

<div class="admonitionblock warning">

|     |                                                                                                                                                             |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | If the storage item does not exist or is not SCALE encoded, the storage item will be set to the specified value, represented as a SCALE encoded byte array. |

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-7" class="anchor"></a><a href="#id-version-1-prototype-7" class="link">B.2.7.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_append_version_1
        (param $key i64) (param $value i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  containing the key.

- `value`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  containing the value to be appended.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_storage_root" class="anchor"></a><a href="#id-ext_storage_root" class="link">B.2.8.
<code>ext_storage_root</code></a>

<div class="paragraph">

Compute the storage root.

</div>

<div class="sect4">

##### <a href="#sect-ext-storage-root-version-1" class="anchor"></a><a href="#sect-ext-storage-root-version-1" class="link">B.2.8.1. Version
1 - Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_root_version_1
        (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to a buffer containing the 256-bit
  Blake2 storage root.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#sect-ext-storage-root-version-2" class="anchor"></a><a href="#sect-ext-storage-root-version-2" class="link">B.2.8.2. Version
2 - Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_root_version_2
        (param $version i32) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `version`: the state version ([Definition 205](#defn-state-version)).

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the buffer containing the 256-bit
  Blake2 storage root.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-ext-storage-changes-root" class="anchor"></a><a href="#sect-ext-storage-changes-root" class="link">B.2.9.
<code>ext_storage_changes_root</code></a>

<div class="admonitionblock note">

|     |                                                                             |
|-----|-----------------------------------------------------------------------------|
|     | This function is not longer used and only exists for compatibility reasons. |

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-8" class="anchor"></a><a href="#id-version-1-prototype-8" class="link">B.2.9.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_changes_root_version_1
        (param $parent_hash i64) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `parent_hash`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded block hash.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to an *Option* type ([Definition
  190](#defn-option-type)) that’s always *None*.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_storage_next_key" class="anchor"></a><a href="#id-ext_storage_next_key" class="link">B.2.10.
<code>ext_storage_next_key</code></a>

<div class="paragraph">

Get the next key in storage after the given one in lexicographic order
([Definition 204](#defn-lexicographic-ordering)). The key provided to
this function may or may not exist in storage.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-9" class="anchor"></a><a href="#id-version-1-prototype-9" class="link">B.2.10.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_next_key_version_1
        (param $key i64) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Option* value
  ([Definition 190](#defn-option-type)) containing the next key in
  lexicographic order.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-ext-storage-start-transaction" class="anchor"></a><a href="#sect-ext-storage-start-transaction" class="link">B.2.11.
<code>ext_storage_start_transaction</code></a>

<div class="paragraph">

Start a new nested transaction. This allows to either commit or roll
back all changes that are made after this call. For every transaction
there must be a matching call to either
`ext_storage_rollback_transaction` ([Section
B.2.12](#sect-ext-storage-rollback-transaction)) or
`ext_storage_commit_transaction` ([Section
B.2.13](#sect-ext-storage-commit-transaction)). This is also effective
for all values manipulated using the child storage API ([Section
B.3](#sect-child-storage-api)). It’s legal to call this function
multiple times in a row.

</div>

<div class="admonitionblock warning">

|     |                                                                                                                                                                |
|-----|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This is a low level API that is potentially dangerous as it can easily result in unbalanced transactions. Runtimes should use high level storage abstractions. |

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-10" class="anchor"></a><a href="#id-version-1-prototype-10" class="link">B.2.11.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_start_transaction_version_1)

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-ext-storage-rollback-transaction" class="anchor"></a><a href="#sect-ext-storage-rollback-transaction" class="link">B.2.12.
<code>ext_storage_rollback_transaction</code></a>

<div class="paragraph">

Rollback the last transaction started by `ext_storage_start_transaction`
([Section B.2.11](#sect-ext-storage-start-transaction)). Any changes
made during that transaction are discarded. It’s legal to call this
function multiple times in a row.

</div>

<div class="admonitionblock warning">

|     |                                                                                                                   |
|-----|-------------------------------------------------------------------------------------------------------------------|
|     | Panics if `ext_storage_start_transaction` ([Section B.2.11](#sect-ext-storage-start-transaction)) was not called. |

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-11" class="anchor"></a><a href="#id-version-1-prototype-11" class="link">B.2.12.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_rollback_transaction_version_1)

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-ext-storage-commit-transaction" class="anchor"></a><a href="#sect-ext-storage-commit-transaction" class="link">B.2.13.
<code>ext_storage_commit_transaction</code></a>

<div class="paragraph">

Commit the last transaction started by `ext_storage_start_transaction`
([Section B.2.11](#sect-ext-storage-start-transaction)). Any changes
made during that transaction are committed to the main state. It’s legal
to call this function multiple times in a row.

</div>

<div class="admonitionblock warning">

|     |                                                                                                                   |
|-----|-------------------------------------------------------------------------------------------------------------------|
|     | Panics if `ext_storage_start_transaction` ([Section B.2.11](#sect-ext-storage-start-transaction)) was not called. |

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-12" class="anchor"></a><a href="#id-version-1-prototype-12" class="link">B.2.13.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_storage_commit_transaction_version_1)

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None.

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-child-storage-api" class="anchor"></a><a href="#sect-child-storage-api" class="link">B.3. Child Storage</a>

<div class="paragraph">

Interface for accessing the child storage from within the runtime.

</div>

<div id="defn-child-storage-type" class="exampleblock">

<div class="title">

Definition 206. [Child Storage](#defn-child-storage-type)

</div>

<div class="content">

<div class="paragraph">

**Child storage** key is a unprefixed location of the child trie in the
main trie.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_default_child_storage_set" class="anchor"></a><a href="#id-ext_default_child_storage_set" class="link">B.3.1.
<code>ext_default_child_storage_set</code></a>

<div class="paragraph">

Sets the value under a given key into the child storage.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-13" class="anchor"></a><a href="#id-version-1-prototype-13" class="link">B.3.1.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_default_child_storage_set_version_1
        (param $child_storage_key i64) (param $key i64) (param $value i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `child_storage_key` : a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the child storage key
  ([Definition 206](#defn-child-storage-type)).

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

- `value`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the value.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_default_child_storage_get" class="anchor"></a><a href="#id-ext_default_child_storage_get" class="link">B.3.2.
<code>ext_default_child_storage_get</code></a>

<div class="paragraph">

Retrieves the value associated with the given key from the child
storage.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-14" class="anchor"></a><a href="#id-version-1-prototype-14" class="link">B.3.2.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_default_child_storage_get_version_1
        (param $child_storage_key i64) (param $key i64) (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `child_storage_key`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the child storage key
  ([Definition 206](#defn-child-storage-type)).

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

- `result`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Option* value
  ([Definition 190](#defn-option-type)) containing the value.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_default_child_storage_read" class="anchor"></a><a href="#id-ext_default_child_storage_read" class="link">B.3.3.
<code>ext_default_child_storage_read</code></a>

<div class="paragraph">

Gets the given key from storage, placing the value into a buffer and
returning the number of bytes that the entry in storage has beyond the
offset.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-15" class="anchor"></a><a href="#id-version-1-prototype-15" class="link">B.3.3.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_default_child_storage_read_version_1
        (param $child_storage_key i64) (param $key i64) (param $value_out i64)
        (param $offset i32) (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `child_storage_key`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the child storage key
  ([Definition 206](#defn-child-storage-type)).

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

- `value_out`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the buffer to which the value
  will be written to. This function will never write more then the
  length of the buffer, even if the value’s length is bigger.

- `offset`: an u32 integer (typed as i32 due to wasm types) containing
  the offset beyond the value should be read from.

- `result`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Option* value
  ([Definition 190](#defn-option-type)) containing the number of bytes
  written into the **value_out** buffer. Returns if the entry does not
  exists.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_default_child_storage_clear" class="anchor"></a><a href="#id-ext_default_child_storage_clear" class="link">B.3.4.
<code>ext_default_child_storage_clear</code></a>

<div class="paragraph">

Clears the storage of the given key and its value from the child
storage. Non-existent entries are silently ignored.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-16" class="anchor"></a><a href="#id-version-1-prototype-16" class="link">B.3.4.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_default_child_storage_clear_version_1
        (param $child_storage_key i64) (param $key i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `child_storage_key`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the child storage key
  ([Definition 206](#defn-child-storage-type)).

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_default_child_storage_storage_kill" class="anchor"></a><a href="#id-ext_default_child_storage_storage_kill" class="link">B.3.5.
<code>ext_default_child_storage_storage_kill</code></a>

<div class="paragraph">

Clears an entire child storage.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-17" class="anchor"></a><a href="#id-version-1-prototype-17" class="link">B.3.5.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_default_child_storage_storage_kill_version_1
        (param $child_storage_key i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `child_storage_key`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the child storage key
  ([Definition 206](#defn-child-storage-type)).

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype-2" class="anchor"></a><a href="#id-version-2-prototype-2" class="link">B.3.5.2. Version 2 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_default_child_storage_storage_kill_version_2
        (param $child_storage_key i64) (param $limit i64)
        (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `child_storage_key`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the child storage key
  ([Definition 206](#defn-child-storage-type)).

- `limit`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to an *Option* type ([Definition 190](#defn-option-type)) containing
  an unsigned 32-bit integer indicating the limit on how many keys
  should be deleted. No limit is applied if this is *None*. Any keys
  created during the current block execution do not count towards the
  limit.

- `return`: a value equal to *1* if all the keys of the child storage
  have been deleted or a value equal to *0* if there are remaining keys.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-3-prototype" class="anchor"></a><a href="#id-version-3-prototype" class="link">B.3.5.3. Version 3 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_default_child_storage_storage_kill_version_3
        (param $child_storage_key i64) (param $limit i64)
        (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `child_storage_key`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the child storage key
  ([Definition 206](#defn-child-storage-type)).

- `limit`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to an *Option* type ([Definition 190](#defn-option-type)) containing
  an unsigned 32-bit integer indicating the limit on how many keys
  should be deleted. No limit is applied if this is *None*. Any keys
  created during the current block execution do not count towards the
  limit.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the following variant, \\k\\:

  <div class="stemblock">

  <div class="content">

  \\k = {(0,-\> c),(1,-\> c):}\\

  </div>

  </div>

  <div class="paragraph">

  where *0* indicates that all keys of the child storage have been
  removed, followed by the number of removed keys, \\c\\. The variant
  *1* indicates that there are remaining keys, followed by the number of
  removed keys.

  </div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_default_child_storage_exists" class="anchor"></a><a href="#id-ext_default_child_storage_exists" class="link">B.3.6.
<code>ext_default_child_storage_exists</code></a>

<div class="paragraph">

Checks whether the given key exists in the child storage.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-18" class="anchor"></a><a href="#id-version-1-prototype-18" class="link">B.3.6.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_default_child_storage_exists_version_1
        (param $child_storage_key i64) (param $key i64) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `child_storage_key`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the child storage key
  ([Definition 206](#defn-child-storage-type)).

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

- `return`: an i32 integer value equal to *1* if the key exists or a
  value equal to *0* if otherwise.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_default_child_storage_clear_prefix" class="anchor"></a><a href="#id-ext_default_child_storage_clear_prefix" class="link">B.3.7.
<code>ext_default_child_storage_clear_prefix</code></a>

<div class="paragraph">

Clears the child storage of each key/value pair where the key starts
with the given prefix.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-19" class="anchor"></a><a href="#id-version-1-prototype-19" class="link">B.3.7.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_default_child_storage_clear_prefix_version_1
        (param $child_storage_key i64) (param $prefix i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `child_storage_key`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the child storage key
  ([Definition 206](#defn-child-storage-type)).

- `prefix`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the prefix.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype-3" class="anchor"></a><a href="#id-version-2-prototype-3" class="link">B.3.7.2. Version 2 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_default_child_storage_clear_prefix_version_2
        (param $child_storage_key i64) (param $prefix i64)
        (param $limit i64) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `child_storage_key`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the child storage key
  ([Definition 206](#defn-child-storage-type)).

- `prefix`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the prefix.

- `limit`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to an *Option* type ([Definition 190](#defn-option-type)) containing
  an unsigned 32-bit integer indicating the limit on how many keys
  should be deleted. No limit is applied if this is *None*. Any keys
  created during the current block execution do not count towards the
  limit.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the following variant, \\k\\:

  <div class="stemblock">

  <div class="content">

  \\k = {(0,-\> c),(1,-\> c):}\\

  </div>

  </div>

  <div class="paragraph">

  where *0* indicates that all keys of the child storage have been
  removed, followed by the number of removed keys, \\c\\. The variant
  *1* indicates that there are remaining keys, followed by the number of
  removed keys.

  </div>

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_default_child_storage_root" class="anchor"></a><a href="#id-ext_default_child_storage_root" class="link">B.3.8.
<code>ext_default_child_storage_root</code></a>

<div class="paragraph">

Commits all existing operations and computes the resulting child storage
root.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-20" class="anchor"></a><a href="#id-version-1-prototype-20" class="link">B.3.8.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_default_child_storage_root_version_1
        (param $child_storage_key i64) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `child_storage_key`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the child storage key
  ([Definition 206](#defn-child-storage-type)).

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded storage root.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype-4" class="anchor"></a><a href="#id-version-2-prototype-4" class="link">B.3.8.2. Version 2 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_default_child_storage_root_version_2
        (param $child_storage_key i64) (param $version i32)
        (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `child_storage_key`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the child storage key
  ([Definition 206](#defn-child-storage-type)).

- `version`: the state version ([Definition 205](#defn-state-version)).

- `return`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit Blake2 storage root.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_default_child_storage_next_key" class="anchor"></a><a href="#id-ext_default_child_storage_next_key" class="link">B.3.9.
<code>ext_default_child_storage_next_key</code></a>

<div class="paragraph">

Gets the next key in storage after the given one in lexicographic order
([Definition 204](#defn-lexicographic-ordering)). The key provided to
this function may or may not exist in storage.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-21" class="anchor"></a><a href="#id-version-1-prototype-21" class="link">B.3.9.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_default_child_storage_next_key_version_1
        (param $child_storage_key i64) (param $key i64) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `child_storage_key`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the child storage key
  ([Definition 206](#defn-child-storage-type)).

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded as defined in
  [Definition 190](#defn-option-type) containing the next key in
  lexicographic order. Returns if the entry cannot be found.

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-crypto-api" class="anchor"></a><a href="#sect-crypto-api" class="link">B.4. Crypto</a>

<div class="paragraph">

Interfaces for working with crypto related types from within the
runtime.

</div>

<div id="defn-key-type-id" class="exampleblock">

<div class="title">

Definition 207. [Key Type Identifier](#defn-key-type-id)

</div>

<div class="content">

<div class="paragraph">

Cryptographic keys are stored in separate key stores based on their
intended use case. The separate key stores are identified by a 4-byte
ASCII **key type identifier**. The following known types are available:

</div>

| Id   | Description                                |
|------|--------------------------------------------|
| acco | Key type for the controlling accounts      |
| babe | Key type for the Babe module               |
| gran | Key type for the Grandpa module            |
| imon | Key type for the ImOnline module           |
| audi | Key type for the AuthorityDiscovery module |
| para | Key type for the Parachain Validator Key   |
| asgn | Key type for the Parachain Assignment Key  |

Table 4. Table of known key type identifiers

</div>

</div>

<div id="defn-ecdsa-verify-error" class="exampleblock">

<div class="title">

Definition 208. [ECDSA Verify Error](#defn-ecdsa-verify-error)

</div>

<div class="content">

<div class="paragraph">

**EcdsaVerifyError** is a varying data type ([Definition
188](#defn-varrying-data-type)) that specifies the error type when using
ECDSA recovery functionality. Following values are possible:

</div>

| Id  | Description               |
|-----|---------------------------|
| 0   | Incorrect value of R or S |
| 1   | Incorrect value of V      |
| 2   | Invalid signature         |

Table 5. Table of error types in ECDSA recovery

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_crypto_ed25519_public_keys" class="anchor"></a><a href="#id-ext_crypto_ed25519_public_keys" class="link">B.4.1.
<code>ext_crypto_ed25519_public_keys</code></a>

<div class="paragraph">

Returns all *ed25519* public keys for the given key identifier from the
keystore.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-22" class="anchor"></a><a href="#id-version-1-prototype-22" class="link">B.4.1.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_ed25519_public_keys_version_1
        (param $key_type_id i32) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key_type_id`: a pointer ([Definition 202](#defn-runtime-pointer)) to
  the key type identifier ([Definition 207](#defn-key-type-id)).

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to an SCALE encoded 256-bit public
  keys.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_crypto_ed25519_generate" class="anchor"></a><a href="#id-ext_crypto_ed25519_generate" class="link">B.4.2.
<code>ext_crypto_ed25519_generate</code></a>

<div class="paragraph">

Generates an *ed25519* key for the given key type using an optional
BIP-39 seed and stores it in the keystore.

</div>

<div class="admonitionblock warning">

|     |                                                                                                       |
|-----|-------------------------------------------------------------------------------------------------------|
|     | Panics if the key cannot be generated, such as when an invalid key type or invalid seed was provided. |

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-23" class="anchor"></a><a href="#id-version-1-prototype-23" class="link">B.4.2.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_ed25519_generate_version_1
        (param $key_type_id i32) (param $seed i64) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key_type_id`: a pointer ([Definition 202](#defn-runtime-pointer)) to
  the key type identifier ([Definition 207](#defn-key-type-id)).

- `seed`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the SCALE encoded *Option* value ([Definition
  190](#defn-option-type)) containing the BIP-39 seed which must be
  valid UTF8.

- `return`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit public key.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_crypto_ed25519_sign" class="anchor"></a><a href="#id-ext_crypto_ed25519_sign" class="link">B.4.3.
<code>ext_crypto_ed25519_sign</code></a>

<div class="paragraph">

Signs the given message with the `ed25519` key that corresponds to the
given public key and key type in the keystore.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-24" class="anchor"></a><a href="#id-version-1-prototype-24" class="link">B.4.3.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_ed25519_sign_version_1
        (param $key_type_id i32) (param $key i32) (param $msg i64) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key_type_id`: a pointer ([Definition 202](#defn-runtime-pointer)) to
  the key type identifier ([Definition 207](#defn-key-type-id)).

- `key`: a pointer to the buffer containing the 256-bit public key.

- `msg`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the message that is to be signed.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Option* value
  ([Definition 190](#defn-option-type)) containing the 64-byte
  signature. This function returns if the public key cannot be found in
  the key store.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-ext-crypto-ed25519-verify" class="anchor"></a><a href="#sect-ext-crypto-ed25519-verify" class="link">B.4.4.
<code>ext_crypto_ed25519_verify</code></a>

<div class="paragraph">

Verifies an *ed25519* signature.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-25" class="anchor"></a><a href="#id-version-1-prototype-25" class="link">B.4.4.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_ed25519_verify_version_1
        (param $sig i32) (param $msg i64) (param $key i32) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `sig`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 64-byte signature.

- `msg`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the message that is to be verified.

- `key`: a pointer to the buffer containing the 256-bit public key.

- `return`: a i32 integer value equal to *1* if the signature is valid
  or a value equal to *0* if otherwise.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-ext-crypto-ed25519-batch-verify" class="anchor"></a><a href="#sect-ext-crypto-ed25519-batch-verify" class="link">B.4.5.
<code>ext_crypto_ed25519_batch_verify</code></a>

<div class="paragraph">

Registers a ed25519 signature for batch verification. Batch verification
is enabled by calling `ext_crypto_start_batch_verify` ([Section
B.4.20](#sect-ext-crypto-start-batch-verify)). The result of the
verification is returned by `ext_crypto_finish_batch_verify` ([Section
B.4.21](#sect-ext-crypto-finish-batch-verify)). If batch verification is
not enabled, the signature is verified immediately.

</div>

<div class="sect4">

##### <a href="#id-version-1" class="anchor"></a><a href="#id-version-1" class="link">B.4.5.1. Version 1</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_ed25519_batch_verify_version_1
        (param $sig i32) (param $msg i64) (param $key i32) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `sig`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 64-byte signature.

- `msg`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the message that is to be verified.

- `key`: a pointer to the buffer containing the 256-bit public key.

- `return`: a i32 integer value equal to *1* if the signature is valid
  or batched or a value equal *0* to if otherwise.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_crypto_sr25519_public_keys" class="anchor"></a><a href="#id-ext_crypto_sr25519_public_keys" class="link">B.4.6.
<code>ext_crypto_sr25519_public_keys</code></a>

<div class="paragraph">

Returns all *sr25519* public keys for the given key id from the
keystore.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-26" class="anchor"></a><a href="#id-version-1-prototype-26" class="link">B.4.6.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_sr25519_public_keys_version_1
        (param $key_type_id i32) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key_type_id`: a pointer ([Definition 202](#defn-runtime-pointer)) to
  the key type identifier ([Definition 207](#defn-key-type-id)).

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded 256-bit public
  keys.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_crypto_sr25519_generate" class="anchor"></a><a href="#id-ext_crypto_sr25519_generate" class="link">B.4.7.
<code>ext_crypto_sr25519_generate</code></a>

<div class="paragraph">

Generates an *sr25519* key for the given key type using an optional
BIP-39 seed and stores it in the keystore.

</div>

<div class="admonitionblock warning">

|     |                                                                                                       |
|-----|-------------------------------------------------------------------------------------------------------|
|     | Panics if the key cannot be generated, such as when an invalid key type or invalid seed was provided. |

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-27" class="anchor"></a><a href="#id-version-1-prototype-27" class="link">B.4.7.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_sr25519_generate_version_1
        (param $key_type_id i32) (param $seed i64) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key_type_id`: a pointer ([Definition 202](#defn-runtime-pointer)) to
  the key identifier ([Definition 207](#defn-key-type-id)).

- `seed`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the SCALE encoded *Option* value ([Definition
  190](#defn-option-type)) containing the BIP-39 seed which must be
  valid UTF8.

- `return`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit public key.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_crypto_sr25519_sign" class="anchor"></a><a href="#id-ext_crypto_sr25519_sign" class="link">B.4.8.
<code>ext_crypto_sr25519_sign</code></a>

<div class="paragraph">

Signs the given message with the *sr25519* key that corresponds to the
given public key and key type in the keystore.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-28" class="anchor"></a><a href="#id-version-1-prototype-28" class="link">B.4.8.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_sr25519_sign_version_1
        (param $key_type_id i32) (param $key i32) (param $msg i64) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key_type_id`: a pointer ([Definition 202](#defn-runtime-pointer)) to
  the key identifier ([Definition 207](#defn-key-type-id)).

- `key`: a pointer to the buffer containing the 256-bit public key.

- `msg`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the message that is to be signed.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Option* value
  ([Definition 190](#defn-option-type)) containing the 64-byte
  signature. This function returns *None* if the public key cannot be
  found in the key store.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-ext-crypto-sr25519-verify" class="anchor"></a><a href="#sect-ext-crypto-sr25519-verify" class="link">B.4.9.
<code>ext_crypto_sr25519_verify</code></a>

<div class="paragraph">

Verifies an sr25519 signature.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-29" class="anchor"></a><a href="#id-version-1-prototype-29" class="link">B.4.9.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_sr25519_verify_version_1
        (param $sig i32) (param $msg i64) (param $key i32) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `sig`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 64-byte signature.

- `msg`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the message that is to be verified.

- `key`: a pointer to the buffer containing the 256-bit public key.

- `return`: a i32 integer value equal to *1* if the signature is valid
  or a value equal to *0* if otherwise.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype-5" class="anchor"></a><a href="#id-version-2-prototype-5" class="link">B.4.9.2. Version 2 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_sr25519_verify_version_2
        (param $sig i32) (param $msg i64) (param $key i32) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `sig`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 64-byte signature.

- `msg`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the message that is to be verified.

- `key`: a pointer to the buffer containing the 256-bit public key.

- `return`: a i32 integer value equal to *1* if the signature is valid
  or a value equal to *0* if otherwise.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-ext-crypto-sr25519-batch-verify" class="anchor"></a><a href="#sect-ext-crypto-sr25519-batch-verify" class="link">B.4.10.
<code>ext_crypto_sr25519_batch_verify</code></a>

<div class="paragraph">

Registers a sr25519 signature for batch verification. Batch verification
is enabled by calling `ext_crypto_start_batch_verify` ([Section
B.4.20](#sect-ext-crypto-start-batch-verify)). The result of the
verification is returned by `ext_crypto_finish_batch_verify` ([Section
B.4.21](#sect-ext-crypto-finish-batch-verify)). If batch verification is
not enabled, the signature is verified immediately.

</div>

<div class="sect4">

##### <a href="#id-version-1-2" class="anchor"></a><a href="#id-version-1-2" class="link">B.4.10.1. Version 1</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_sr25519_batch_verify_version_1
        (param $sig i32) (param $msg i64) (param $key i32) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `sig`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 64-byte signature.

- `msg`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the message that is to be verified.

- `key`: a pointer to the buffer containing the 256-bit public key.

- `return`: a i32 integer value equal to *1* if the signature is valid
  or batched or a value equal *0* to if otherwise.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_crypto_ecdsa_public_keys" class="anchor"></a><a href="#id-ext_crypto_ecdsa_public_keys" class="link">B.4.11.
<code>ext_crypto_ecdsa_public_keys</code></a>

<div class="paragraph">

Returns all *ecdsa* public keys for the given key id from the keystore.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-30" class="anchor"></a><a href="#id-version-1-prototype-30" class="link">B.4.11.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_ecdsa_public_key_version_1
        (param $key_type_id i64) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key_type_id`: a pointer ([Definition 202](#defn-runtime-pointer)) to
  the key type identifier ([Definition 207](#defn-key-type-id)).

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded 33-byte
  compressed public keys.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_crypto_ecdsa_generate" class="anchor"></a><a href="#id-ext_crypto_ecdsa_generate" class="link">B.4.12.
<code>ext_crypto_ecdsa_generate</code></a>

<div class="paragraph">

Generates an *ecdsa* key for the given key type using an optional BIP-39
seed and stores it in the keystore.

</div>

<div class="admonitionblock warning">

|     |                                                                                                       |
|-----|-------------------------------------------------------------------------------------------------------|
|     | Panics if the key cannot be generated, such as when an invalid key type or invalid seed was provided. |

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-31" class="anchor"></a><a href="#id-version-1-prototype-31" class="link">B.4.12.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_ecdsa_generate_version_1
        (param $key_type_id i32) (param $seed i64) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key_type_id`: a pointer ([Definition 202](#defn-runtime-pointer)) to
  the key identifier ([Definition 207](#defn-key-type-id)).

- `seed`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the SCALE encoded *Option* value ([Definition
  190](#defn-option-type)) containing the BIP-39 seed which must be
  valid UTF8.

- `return`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 33-byte compressed public key.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_crypto_ecdsa_sign" class="anchor"></a><a href="#id-ext_crypto_ecdsa_sign" class="link">B.4.13.
<code>ext_crypto_ecdsa_sign</code></a>

<div class="paragraph">

Signs the hash of the given message with the *ecdsa* key that
corresponds to the given public key and key type in the keystore.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-32" class="anchor"></a><a href="#id-version-1-prototype-32" class="link">B.4.13.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_ecdsa_sign_version_1
        (param $key_type_id i32) (param $key i32) (param $msg i64) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key_type_id`: a pointer ([Definition 202](#defn-runtime-pointer)) to
  the key identifier ([Definition 207](#defn-key-type-id)).

- `key`: a pointer to the buffer containing the 33-byte compressed
  public key.

- `msg`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the message that is to be signed.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Option* value
  ([Definition 190](#defn-option-type)) containing the signature. The
  signature is 65-bytes in size, where the first 512-bits represent the
  signature and the other 8 bits represent the recovery ID. This
  function returns if the public key cannot be found in the key store.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_crypto_ecdsa_sign_prehashed" class="anchor"></a><a href="#id-ext_crypto_ecdsa_sign_prehashed" class="link">B.4.14.
<code>ext_crypto_ecdsa_sign_prehashed</code></a>

<div class="paragraph">

Signs the prehashed message with the *ecdsa* key that corresponds to the
given public key and key type in the keystore.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-33" class="anchor"></a><a href="#id-version-1-prototype-33" class="link">B.4.14.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_ecdsa_sign_prehashed_version_1
        (param $key_type_id i32) (param $key i32) (param $msg i64) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `key_type_id`: a pointer-size ([Definition
  202](#defn-runtime-pointer)) to the key identifier ([Definition
  207](#defn-key-type-id)).

- `key`: a pointer to the buffer containing the 33-byte compressed
  public key.

- `msg`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the message that is to be signed.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Option* value
  ([Definition 190](#defn-option-type)) containing the signature. The
  signature is 65-bytes in size, where the first 512-bits represent the
  signature and the other 8 bits represent the recovery ID. This
  function returns if the public key cannot be found in the key store.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-ext-crypto-ecdsa-verify" class="anchor"></a><a href="#sect-ext-crypto-ecdsa-verify" class="link">B.4.15.
<code>ext_crypto_ecdsa_verify</code></a>

<div class="paragraph">

Verifies the hash of the given message against a ECDSA signature.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-34" class="anchor"></a><a href="#id-version-1-prototype-34" class="link">B.4.15.1. Version 1 -
Prototype</a>

<div class="paragraph">

This function allows the verification of non-standard, overflowing ECDSA
signatures, an implemenation specific mechanism of the Rust
[`libsecp256k1` library](https://github.com/paritytech/libsecp256k1),
specifically the
[`parse_overflowing`](https://docs.rs/libsecp256k1/0.7.0/libsecp256k1/struct.Signature.html#method.parse_overflowing)
function.

</div>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_ecdsa_verify_version_1
        (param $sig i32) (param $msg i64) (param $key i32) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `sig`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 65-byte signature. The signature is 65-bytes in
  size, where the first 512-bits represent the signature and the other 8
  bits represent the recovery ID.

- `msg`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the message that is to be verified.

- `key`: a pointer to the buffer containing the 33-byte compressed
  public key.

- `return`: a i32 integer value equal *1* to if the signature is valid
  or a value equal to *0* if otherwise.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype-6" class="anchor"></a><a href="#id-version-2-prototype-6" class="link">B.4.15.2. Version 2 -
Prototype</a>

<div class="paragraph">

Does not allow the verification of non-standard, overflowing ECDSA
signatures.

</div>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_ecdsa_verify_version_2
        (param $sig i32) (param $msg i64) (param $key i32) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `sig`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 65-byte signature. The signature is 65-bytes in
  size, where the first 512-bits represent the signature and the other 8
  bits represent the recovery ID.

- `msg`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the message that is to be verified.

- `key`: a pointer to the buffer containing the 33-byte compressed
  public key.

- `return`: a i32 integer value equal *1* to if the signature is valid
  or a value equal to *0* if otherwise.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_crypto_ecdsa_verify_prehashed" class="anchor"></a><a href="#id-ext_crypto_ecdsa_verify_prehashed" class="link">B.4.16.
<code>ext_crypto_ecdsa_verify_prehashed</code></a>

<div class="paragraph">

Verifies the prehashed message against a ECDSA signature.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-35" class="anchor"></a><a href="#id-version-1-prototype-35" class="link">B.4.16.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_ecdsa_verify_prehashed_version_1
        (param $sig i32) (param $msg i32) (param $key i32) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `sig`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 65-byte signature. The signature is 65-bytes in
  size, where the first 512-bits represent the signature and the other 8
  bits represent the recovery ID.

- `msg`: a pointer to the 32-bit prehashed message to be verified.

- `key`: a pointer to the 33-byte compressed public key.

- `return`: a i32 integer value equal *1* to if the signature is valid
  or a value equal to *0* if otherwise.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-ext-crypto-ecdsa-batch-verify" class="anchor"></a><a href="#sect-ext-crypto-ecdsa-batch-verify" class="link">B.4.17.
<code>ext_crypto_ecdsa_batch_verify</code></a>

<div class="paragraph">

Registers a ECDSA signature for batch verification. Batch verification
is enabled by calling `ext_crypto_start_batch_verify` ([Section
B.4.20](#sect-ext-crypto-start-batch-verify)). The result of the
verification is returned by `ext_crypto_finish_batch_verify` ([Section
B.4.21](#sect-ext-crypto-finish-batch-verify)). If batch verification is
not enabled, the signature is verified immediately.

</div>

<div class="sect4">

##### <a href="#id-version-1-3" class="anchor"></a><a href="#id-version-1-3" class="link">B.4.17.1. Version 1</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_ecdsa_batch_verify_version_1
        (param $sig i32) (param $msg i64) (param $key i32) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `sig`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 64-byte signature.

- `msg`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the message that is to be verified.

- `key`: a pointer to the buffer containing the 256-bit public key.

- `return`: a i32 integer value equal to *1* if the signature is valid
  or batched or a value equal *0* to if otherwise.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_crypto_secp256k1_ecdsa_recover" class="anchor"></a><a href="#id-ext_crypto_secp256k1_ecdsa_recover" class="link">B.4.18.
<code>ext_crypto_secp256k1_ecdsa_recover</code></a>

<div class="paragraph">

Verify and recover a *secp256k1* ECDSA signature.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-36" class="anchor"></a><a href="#id-version-1-prototype-36" class="link">B.4.18.1. Version 1 -
Prototype</a>

<div class="paragraph">

This function can handle non-standard, overflowing ECDSA signatures, an
implemenation specific mechanism of the Rust [`libsecp256k1`
library](https://github.com/paritytech/libsecp256k1), specifically the
[`parse_overflowing`](https://docs.rs/libsecp256k1/0.7.0/libsecp256k1/struct.Signature.html#method.parse_overflowing)
function.

</div>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_secp256k1_ecdsa_recover_version_1
        (param $sig i32) (param $msg i32) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `sig`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 65-byte signature in RSV format. V should be
  either `0/1` or `27/28`.

- `msg`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit Blake2 hash of the message.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Result*
  ([Definition 191](#defn-result-type)). On success it contains the
  64-byte recovered public key or an error type ([Definition
  208](#defn-ecdsa-verify-error)) on failure.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype-7" class="anchor"></a><a href="#id-version-2-prototype-7" class="link">B.4.18.2. Version 2 -
Prototype</a>

<div class="paragraph">

Does not handle non-standard, overflowing ECDSA signatures.

</div>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_secp256k1_ecdsa_recover_version_2
        (param $sig i32) (param $msg i32) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `sig`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 65-byte signature in RSV format. V should be
  either or .

- `msg`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit Blake2 hash of the message.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Result*
  ([Definition 191](#defn-result-type)). On success it contains the
  64-byte recovered public key or an error type ([Definition
  208](#defn-ecdsa-verify-error)) on failure.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_crypto_secp256k1_ecdsa_recover_compressed"
class="anchor"></a><a href="#id-ext_crypto_secp256k1_ecdsa_recover_compressed"
class="link">B.4.19.
<code>ext_crypto_secp256k1_ecdsa_recover_compressed</code></a>

<div class="paragraph">

Verify and recover a *secp256k1* ECDSA signature.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-37" class="anchor"></a><a href="#id-version-1-prototype-37" class="link">B.4.19.1. Version 1 -
Prototype</a>

<div class="paragraph">

This function can handle non-standard, overflowing ECDSA signatures, an
implemenation specific mechanism of the Rust [`libsecp256k1`
library](https://github.com/paritytech/libsecp256k1), specifically the
[`parse_overflowing`](https://docs.rs/libsecp256k1/0.7.0/libsecp256k1/struct.Signature.html#method.parse_overflowing)
function.

</div>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_secp256k1_ecdsa_recover_compressed_version_1
        (param $sig i32) (param $msg i32) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `sig`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 65-byte signature in RSV format. V should be
  either `0/1` or `27/28`.

- `msg`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit Blake2 hash of the message.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded `Result` value
  ([Definition 191](#defn-result-type)). On success it contains the
  33-byte recovered public key in compressed form on success or an error
  type ([Definition 208](#defn-ecdsa-verify-error)) on failure.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype-8" class="anchor"></a><a href="#id-version-2-prototype-8" class="link">B.4.19.2. Version 2 -
Prototype</a>

<div class="paragraph">

Does not handle non-standard, overflowing ECDSA signatures.

</div>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_secp256k1_ecdsa_recover_compressed_version_2
        (param $sig i32) (param $msg i32) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `sig`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 65-byte signature in RSV format. V should be
  either `0/1` or `27/28`.

- `msg`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit Blake2 hash of the message.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded `Result` value
  ([Definition 191](#defn-result-type)). On success it contains the
  33-byte recovered public key in compressed form on success or an error
  type ([Definition 208](#defn-ecdsa-verify-error)) on failure.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-ext-crypto-start-batch-verify" class="anchor"></a><a href="#sect-ext-crypto-start-batch-verify" class="link">B.4.20.
<code>ext_crypto_start_batch_verify</code></a>

<div class="paragraph">

Starts the verification extension. The extension is a separate
background process and is used to parallel-verify signatures which are
pushed to the batch with `ext_crypto_ed25519_batch_verify`([Section
B.4.5](#sect-ext-crypto-ed25519-batch-verify)),
`ext_crypto_sr25519_batch_verify` ([Section
B.4.10](#sect-ext-crypto-sr25519-batch-verify)) or
`ext_crypto_ecdsa_batch_verify` ([Section
B.4.17](#sect-ext-crypto-ecdsa-batch-verify)). Verification will start
immediately and the Runtime can retrieve the result when calling
`ext_crypto_finish_batch_verify` ([Section
B.4.21](#sect-ext-crypto-finish-batch-verify)).

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-38" class="anchor"></a><a href="#id-version-1-prototype-38" class="link">B.4.20.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_start_batch_verify_version_1)

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-ext-crypto-finish-batch-verify" class="anchor"></a><a href="#sect-ext-crypto-finish-batch-verify" class="link">B.4.21.
<code>ext_crypto_finish_batch_verify</code></a>

<div class="paragraph">

Finish verifying the batch of signatures since the last call to this
function. Blocks until all the signatures are verified.

</div>

<div class="admonitionblock warning">

|     |                                                                                                                   |
|-----|-------------------------------------------------------------------------------------------------------------------|
|     | Panics if `ext_crypto_start_batch_verify` ([Section B.4.20](#sect-ext-crypto-start-batch-verify)) was not called. |

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-39" class="anchor"></a><a href="#id-version-1-prototype-39" class="link">B.4.21.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_crypto_finish_batch_verify_version_1
        (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `return`: an i32 integer value equal to *1* if all the signatures are
  valid or a value equal to *0* if one or more of the signatures are
  invalid.

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-hashing-api" class="anchor"></a><a href="#sect-hashing-api" class="link">B.5. Hashing</a>

<div class="paragraph">

Interface that provides functions for hashing with different algorithms.

</div>

<div class="sect3">

#### <a href="#id-ext_hashing_keccak_256" class="anchor"></a><a href="#id-ext_hashing_keccak_256" class="link">B.5.1.
<code>ext_hashing_keccak_256</code></a>

<div class="paragraph">

Conducts a 256-bit Keccak hash.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-40" class="anchor"></a><a href="#id-version-1-prototype-40" class="link">B.5.1.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_hashing_keccak_256_version_1
        (param $data i64) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the data to be hashed.

- `return`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit hash result.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_hashing_keccak_512" class="anchor"></a><a href="#id-ext_hashing_keccak_512" class="link">B.5.2.
<code>ext_hashing_keccak_512</code></a>

<div class="paragraph">

Conducts a 512-bit Keccak hash.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-41" class="anchor"></a><a href="#id-version-1-prototype-41" class="link">B.5.2.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_hashing_keccak_512_version_1
        (param $data i64) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the data to be hashed.

- `return`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 512-bit hash result.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_hashing_sha2_256" class="anchor"></a><a href="#id-ext_hashing_sha2_256" class="link">B.5.3.
<code>ext_hashing_sha2_256</code></a>

<div class="paragraph">

Conducts a 256-bit Sha2 hash.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-42" class="anchor"></a><a href="#id-version-1-prototype-42" class="link">B.5.3.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_hashing_sha2_256_version_1
        (param $data i64) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the data to be hashed.

- `return`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit hash result.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_hashing_blake2_128" class="anchor"></a><a href="#id-ext_hashing_blake2_128" class="link">B.5.4.
<code>ext_hashing_blake2_128</code></a>

<div class="paragraph">

Conducts a 128-bit Blake2 hash.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-43" class="anchor"></a><a href="#id-version-1-prototype-43" class="link">B.5.4.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_hashing_blake2_128_version_1
        (param $data i64) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the data to be hashed.

- `return`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 128-bit hash result.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_hashing_blake2_256" class="anchor"></a><a href="#id-ext_hashing_blake2_256" class="link">B.5.5.
<code>ext_hashing_blake2_256</code></a>

<div class="paragraph">

Conducts a 256-bit Blake2 hash.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-44" class="anchor"></a><a href="#id-version-1-prototype-44" class="link">B.5.5.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_hashing_blake2_256_version_1
        (param $data i64) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the data to be hashed.

- `return`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit hash result.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_hashing_twox_64" class="anchor"></a><a href="#id-ext_hashing_twox_64" class="link">B.5.6.
<code>ext_hashing_twox_64</code></a>

<div class="paragraph">

Conducts a 64-bit xxHash hash.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-45" class="anchor"></a><a href="#id-version-1-prototype-45" class="link">B.5.6.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_hashing_twox_64_version_1
        (param $data i64) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the data to be hashed.

- `return`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 64-bit hash result.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_hashing_twox_128" class="anchor"></a><a href="#id-ext_hashing_twox_128" class="link">B.5.7.
<code>ext_hashing_twox_128</code></a>

<div class="paragraph">

Conducts a 128-bit xxHash hash.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-46" class="anchor"></a><a href="#id-version-1-prototype-46" class="link">B.5.7.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_hashing_twox_128
        (param $data i64) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the data to be hashed.

- `return`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 128-bit hash result.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_hashing_twox_256" class="anchor"></a><a href="#id-ext_hashing_twox_256" class="link">B.5.8.
<code>ext_hashing_twox_256</code></a>

<div class="paragraph">

Conducts a 256-bit xxHash hash.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-47" class="anchor"></a><a href="#id-version-1-prototype-47" class="link">B.5.8.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_hashing_twox_256
        (param $data i64) (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the data to be hashed.

- `return`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit hash result.

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-offchain-api" class="anchor"></a><a href="#sect-offchain-api" class="link">B.6. Offchain</a>

<div class="paragraph">

The Offchain Workers allow the execution of long-running and possibly
non-deterministic tasks (e.g. web requests, encryption/decryption and
signing of data, random number generation, CPU-intensive computations,
enumeration/aggregation of on-chain data, etc.) which could otherwise
require longer than the block execution time. Offchain Workers have
their own execution environment. This separation of concerns is to make
sure that the block production is not impacted by the long-running
tasks.

</div>

<div class="paragraph">

All data and results generated by Offchain workers are unique per node
and nondeterministic. Information can be propagated to other nodes by
submitting a transaction that should be included in the next block. As
Offchain workers runs on their own execution environment they have
access to their own separate storage. There are two different types of
storage available which are defined in [Definition
209](#defn-offchain-persistent-storage) and [Definition
210](#defn-offchain-local-storage).

</div>

<div id="defn-offchain-persistent-storage" class="exampleblock">

<div class="title">

Definition 209. [Persisted Storage](#defn-offchain-persistent-storage)

</div>

<div class="content">

<div class="paragraph">

**Persistent storage** is non-revertible and not fork-aware. It means
that any value set by the offchain worker is persisted even if that
block (at which the worker is called) is reverted as non-canonical
(meaning that the block was surpassed by a longer chain). The value is
available for the worker that is re-run at the new (different block with
the same block number) and future blocks. This storage can be used by
offchain workers to handle forks and coordinate offchain workers running
on different forks.

</div>

</div>

</div>

<div id="defn-offchain-local-storage" class="exampleblock">

<div class="title">

Definition 210. [Local Storage](#defn-offchain-local-storage)

</div>

<div class="content">

<div class="paragraph">

**Local storage** is revertible and fork-aware. It means that any value
set by the offchain worker triggered at a certain block is reverted if
that block is reverted as non-canonical. The value is NOT available for
the worker that is re-run at the next or any future blocks.

</div>

</div>

</div>

<div id="defn-http-status-code" class="exampleblock">

<div class="title">

Definition 211. [HTTP Status Code](#defn-http-status-code)

</div>

<div class="content">

<div class="paragraph">

**HTTP status codes** that can get returned by certain Offchain HTTP
functions.

</div>

<div class="ulist">

- `0`: the specified request identifier is invalid.

- `10`: the deadline for the started request was reached.

- `20`: an error has occurred during the request, e.g. a timeout or the
  remote server has closed the connection. On returning this error code,
  the request is considered destroyed and must be reconstructed again.

- `100`-`999`: the request has finished with the given HTTP status code.

</div>

</div>

</div>

<div id="defn-http-error" class="exampleblock">

<div class="title">

Definition 212. [HTTP Error](#defn-http-error)

</div>

<div class="content">

<div class="paragraph">

HTTP error, \\E\\, is a varying data type ([Definition
188](#defn-varrying-data-type)) and specifies the error types of certain
HTTP functions. Following values are possible:

</div>

<div class="stemblock">

<div class="content">

\\E = {(0,"The deadile was reached"),(1,"There was an IO error while
processing the request"),(2,"The Id of the request is invalid"):}\\

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_is_validator" class="anchor"></a><a href="#id-ext_offchain_is_validator" class="link">B.6.1.
<code>ext_offchain_is_validator</code></a>

<div class="paragraph">

Check whether the local node is a potential validator. Even if this
function returns *1*, it does not mean that any keys are configured or
that the validator is registered in the chain.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-48" class="anchor"></a><a href="#id-version-1-prototype-48" class="link">B.6.1.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_is_validator_version_1 (return i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `return`: a i32 integer which is equal to *1* if the local node is a
  potential validator or a integer equal to *0* if it is not.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-ext-offchain-submit-transaction" class="anchor"></a><a href="#sect-ext-offchain-submit-transaction" class="link">B.6.2.
<code>ext_offchain_submit_transaction</code></a>

<div class="paragraph">

Given a SCALE encoded extrinsic, this function submits the extrinsic to
the Host’s transaction pool, ready to be propagated to remote peers.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-49" class="anchor"></a><a href="#id-version-1-prototype-49" class="link">B.6.2.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_submit_transaction_version_1
        (param $data i64) (return i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the byte array storing the encoded extrinsic.

- `return`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Result* value
  ([Definition 191](#defn-result-type)). Neither on success or failure
  is there any additional data provided. The cause of a failure is
  implementation specific.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_network_state" class="anchor"></a><a href="#id-ext_offchain_network_state" class="link">B.6.3.
<code>ext_offchain_network_state</code></a>

<div class="paragraph">

Returns the SCALE encoded, opaque information about the local node’s
network state.

</div>

<div id="defn-opaque-network-state" class="exampleblock">

<div class="title">

Definition 213. [Opaque Network State](#defn-opaque-network-state)

</div>

<div class="content">

<div class="paragraph">

The **Opaque network state structure**, \\S\\, is a SCALE encoded blob
holding information about the the *libp2p PeerId*, \\P\_("id")\\, of the
local node and a list of *libp2p Multiaddresses*, \\(M_0, ... M_n)\\,
the node knows it can be reached at:

</div>

<div class="stemblock">

<div class="content">

\\S = (P\_("id"),(M_0, ... M_n))\\

</div>

</div>

<div class="paragraph">

where

</div>

<div class="stemblock">

<div class="content">

\\P\_("id") = (b_0,... b_n) M = (b_0, ... b_n)\\

</div>

</div>

<div class="paragraph">

The information contained in this structure is naturally opaque to the
caller of this function.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-50" class="anchor"></a><a href="#id-version-1-prototype-50" class="link">B.6.3.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_network_state_version_1 (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `result`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded `Result` value
  ([Definition 191](#defn-result-type)). On success it contains the
  *Opaque network state* structure ([Definition
  213](#defn-opaque-network-state)). On failure, an empty value is
  yielded where its cause is implementation specific.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_timestamp" class="anchor"></a><a href="#id-ext_offchain_timestamp" class="link">B.6.4.
<code>ext_offchain_timestamp</code></a>

<div class="paragraph">

Returns the current timestamp.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-51" class="anchor"></a><a href="#id-version-1-prototype-51" class="link">B.6.4.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_timestamp_version_1 (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `result`: an u64 integer (typed as i64 due to wasm types) indicating
  the current UNIX timestamp ([Definition 181](#defn-unix-time)).

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_sleep_until" class="anchor"></a><a href="#id-ext_offchain_sleep_until" class="link">B.6.5.
<code>ext_offchain_sleep_until</code></a>

<div class="paragraph">

Pause the execution until the `deadline` is reached.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-52" class="anchor"></a><a href="#id-version-1-prototype-52" class="link">B.6.5.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_sleep_until_version_1 (param $deadline i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `deadline`: an u64 integer (typed as i64 due to wasm types) specifying
  the UNIX timestamp ([Definition 181](#defn-unix-time)).

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_random_seed" class="anchor"></a><a href="#id-ext_offchain_random_seed" class="link">B.6.6.
<code>ext_offchain_random_seed</code></a>

<div class="paragraph">

Generates a random seed. This is a truly random non deterministic seed
generated by the host environment.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-53" class="anchor"></a><a href="#id-version-1-prototype-53" class="link">B.6.6.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_random_seed_version_1 (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `result`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit seed.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_local_storage_set" class="anchor"></a><a href="#id-ext_offchain_local_storage_set" class="link">B.6.7.
<code>ext_offchain_local_storage_set</code></a>

<div class="paragraph">

Sets a value in the local storage. This storage is not part of the
consensus, it’s only accessible by the offchain worker tasks running on
the same machine and is persisted between runs.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-54" class="anchor"></a><a href="#id-version-1-prototype-54" class="link">B.6.7.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_local_storage_set_version_1
        (param $kind i32) (param $key i64) (param $value i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `kind`: an i32 integer indicating the storage kind. A value equal to
  *1* is used for a persistent storage ([Definition
  209](#defn-offchain-persistent-storage)) and a value equal to *2* for
  local storage ([Definition 210](#defn-offchain-local-storage)).

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

- `value`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the value.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_local_storage_clear" class="anchor"></a><a href="#id-ext_offchain_local_storage_clear" class="link">B.6.8.
<code>ext_offchain_local_storage_clear</code></a>

<div class="paragraph">

Remove a value from the local storage.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-55" class="anchor"></a><a href="#id-version-1-prototype-55" class="link">B.6.8.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_local_storage_clear_version_1
        (param $kind i32) (param $key i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `kind`: an i32 integer indicating the storage kind. A value equal to
  *1* is used for a persistent storage ([Definition
  209](#defn-offchain-persistent-storage)) and a value equal to *2* for
  local storage ([Definition 210](#defn-offchain-local-storage)).

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_local_storage_compare_and_set"
class="anchor"></a><a href="#id-ext_offchain_local_storage_compare_and_set"
class="link">B.6.9.
<code>ext_offchain_local_storage_compare_and_set</code></a>

<div class="paragraph">

Sets a new value in the local storage if the condition matches the
current value.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-56" class="anchor"></a><a href="#id-version-1-prototype-56" class="link">B.6.9.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (fund $ext_offchain_local_storage_compare_and_set_version_1
        (param $kind i32) (param $key i64) (param $old_value i64)
        (param $new_value i64) (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `kind`: an i32 integer indicating the storage kind. A value equal to
  *1* is used for a persistent storage ([Definition
  209](#defn-offchain-persistent-storage)) and a value equal to *2* for
  local storage ([Definition 210](#defn-offchain-local-storage)).

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

- `old_value`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Option* value
  ([Definition 190](#defn-option-type)) containing the old key.

- `new_value`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the new value.

- `result`: an i32 integer equal to *1* if the new value has been set or
  a value equal to *0* if otherwise.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_local_storage_get" class="anchor"></a><a href="#id-ext_offchain_local_storage_get" class="link">B.6.10.
<code>ext_offchain_local_storage_get</code></a>

<div class="paragraph">

Gets a value from the local storage.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-57" class="anchor"></a><a href="#id-version-1-prototype-57" class="link">B.6.10.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_local_storage_get_version_1
        (param $kind i32) (param $key i64) (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `kind`: an i32 integer indicating the storage kind. A value equal to
  *1* is used for a persistent storage ([Definition
  209](#defn-offchain-persistent-storage)) and a value equal to *2* for
  local storage ([Definition 210](#defn-offchain-local-storage)).

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

- `result`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Option* value
  ([Definition 190](#defn-option-type)) containing the value or the
  corresponding key.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_http_request_start" class="anchor"></a><a href="#id-ext_offchain_http_request_start" class="link">B.6.11.
<code>ext_offchain_http_request_start</code></a>

<div class="paragraph">

Initiates a HTTP request given by the HTTP method and the URL. Returns
the Id of a newly started request.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-58" class="anchor"></a><a href="#id-version-1-prototype-58" class="link">B.6.11.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_http_request_start_version_1
      (param $method i64) (param $uri i64) (param $meta i64) (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `method`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the HTTP method. Possible values
  are “GET” and “POST”.

- `uri`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the URI.

- `meta`: a future-reserved field containing additional, SCALE encoded
  parameters. Currently, an empty array should be passed.

- `result`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Result* value
  ([Definition 191](#defn-result-type)) containing the i16 ID of the
  newly started request. On failure no additionally data is provided.
  The cause of failure is implementation specific.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_http_request_add_header" class="anchor"></a><a href="#id-ext_offchain_http_request_add_header" class="link">B.6.12.
<code>ext_offchain_http_request_add_header</code></a>

<div class="paragraph">

Append header to the request. Returns an error if the request identifier
is invalid, `http_response_wait` has already been called on the
specified request identifier, the deadline is reached or an I/O error
has happened (e.g. the remote has closed the connection).

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-59" class="anchor"></a><a href="#id-version-1-prototype-59" class="link">B.6.12.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_http_request_add_header_version_1
        (param $request_id i32) (param $name i64) (param $value i64) (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `request_id`: an i32 integer indicating the ID of the started request.

- `name`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the HTTP header name.

- `value`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the HTTP header value.

- `result`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Result* value
  ([Definition 191](#defn-result-type)). Neither on success or failure
  is there any additional data provided. The cause of failure is
  implementation specific.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_http_request_write_body" class="anchor"></a><a href="#id-ext_offchain_http_request_write_body" class="link">B.6.13.
<code>ext_offchain_http_request_write_body</code></a>

<div class="paragraph">

Writes a chunk of the request body. Returns a non-zero value in case the
deadline is reached or the chunk could not be written.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-60" class="anchor"></a><a href="#id-version-1-prototype-60" class="link">B.6.13.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_http_request_write_body_version_1
        (param $request_id i32) (param $chunk i64) (param $deadline i64) (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `request_id`: an i32 integer indicating the ID of the started request.

- `chunk`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the chunk of bytes. Writing an empty chunk finalizes the request.

- `deadline`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Option* value
  ([Definition 190](#defn-option-type)) containing the UNIX timestamp
  ([Definition 181](#defn-unix-time)). Passing *None* blocks
  indefinitely.

- `result`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Result* value
  ([Definition 191](#defn-result-type)). On success, no additional data
  is provided. On error it contains the HTTP error type ([Definition
  212](#defn-http-error)).

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_http_response_wait" class="anchor"></a><a href="#id-ext_offchain_http_response_wait" class="link">B.6.14.
<code>ext_offchain_http_response_wait</code></a>

<div class="paragraph">

Returns an array of request statuses (the length is the same as IDs).
Note that if deadline is not provided the method will block
indefinitely, otherwise unready responses will produce DeadlineReached
status.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-61" class="anchor"></a><a href="#id-version-1-prototype-61" class="link">B.6.14.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_http_response_wait_version_1
        (param $ids i64) (param $deadline i64) (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `ids`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the SCALE encoded array of started request IDs.

- `deadline`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Option* value
  ([Definition 190](#defn-option-type)) containing the UNIX timestamp
  ([Definition 181](#defn-unix-time)). Passing None blocks indefinitely.

- `result`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded array of
  request statuses ([Definition 211](#defn-http-status-code)).

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_http_response_headers" class="anchor"></a><a href="#id-ext_offchain_http_response_headers" class="link">B.6.15.
<code>ext_offchain_http_response_headers</code></a>

<div class="paragraph">

Read all HTTP response headers. Returns an array of key/value pairs.
Response headers must be read before the response body.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-62" class="anchor"></a><a href="#id-version-1-prototype-62" class="link">B.6.15.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_http_response_headers_version_1
        (param $request_id i32) (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `request_id`: an i32 integer indicating the ID of the started request.

- `result`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to a SCALE encoded array of
  key/value pairs.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_offchain_http_response_read_body" class="anchor"></a><a href="#id-ext_offchain_http_response_read_body" class="link">B.6.16.
<code>ext_offchain_http_response_read_body</code></a>

<div class="paragraph">

Reads a chunk of body response to the given buffer. Returns the number
of bytes written or an error in case a deadline is reached or the server
closed the connection. If 0 is returned it means that the response has
been fully consumed and the request_id is now invalid. This implies that
response headers must be read before draining the body.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-63" class="anchor"></a><a href="#id-version-1-prototype-63" class="link">B.6.16.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_offchain_http_response_read_body_version_1
        (param $request_id i32) (param $buffer i64) (param $deadline i64) (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `request_id`: an i32 integer indicating the ID of the started request.

- `buffer`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the buffer where the body gets
  written to.

- `deadline`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Option* value
  ([Definition 190](#defn-option-type)) containing the UNIX timestamp
  ([Definition 181](#defn-unix-time)). Passing *None* will block
  indefinitely.

- `result`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Result* value
  ([Definition 191](#defn-result-type)). On success it contains an i32
  integer specifying the number of bytes written or a HTTP error type
  ([Definition 212](#defn-http-error)) on failure.

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-trie-api" class="anchor"></a><a href="#sect-trie-api" class="link">B.7. Trie</a>

<div class="paragraph">

Interface that provides trie related functionality.

</div>

<div class="sect3">

#### <a href="#id-ext_trie_blake2_256_root" class="anchor"></a><a href="#id-ext_trie_blake2_256_root" class="link">B.7.1.
<code>ext_trie_blake2_256_root</code></a>

<div class="paragraph">

Compute a 256-bit Blake2 trie root formed from the iterated items.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-64" class="anchor"></a><a href="#id-version-1-prototype-64" class="link">B.7.1.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_trie_blake2_256_root_version_1
        (param $data i64) (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the iterated items from which the trie root gets formed. The items
  consist of a SCALE encoded array containing arbitrary key/value pairs
  (tuples).

- `result`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit trie root.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype-9" class="anchor"></a><a href="#id-version-2-prototype-9" class="link">B.7.1.2. Version 2 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_trie_blake2_256_root_version_2
        (param $data i64) (param $version i32)
        (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the iterated items from which the trie root gets formed. The items
  consist of a SCALE encoded array containing arbitrary key/value pairs
  (tuples).

- `version`: the state version ([Definition 205](#defn-state-version)).

- `result`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit trie root.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_trie_blake2_256_ordered_root" class="anchor"></a><a href="#id-ext_trie_blake2_256_ordered_root" class="link">B.7.2.
<code>ext_trie_blake2_256_ordered_root</code></a>

<div class="paragraph">

Compute a 256-bit Blake2 trie root formed from the enumerated items.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-65" class="anchor"></a><a href="#id-version-1-prototype-65" class="link">B.7.2.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_trie_blake2_256_ordered_root_version_1
        (param $data i64) (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the enumerated items from which the trie root gets formed. The
  items consist of a SCALE encoded array containing only values, where
  the corresponding key of each value is the index of the item in the
  array, starting at 0. The keys are compact encoded integers
  ([Definition 198](#defn-sc-len-encoding)).

- `result`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit trie root result.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype-10" class="anchor"></a><a href="#id-version-2-prototype-10" class="link">B.7.2.2. Version 2 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_trie_blake2_256_ordered_root_version_2
        (param $data i64) (param $version i32)
        (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the enumerated items from which the trie root gets formed. The
  items consist of a SCALE encoded array containing only values, where
  the corresponding key of each value is the index of the item in the
  array, starting at 0. The keys are compact encoded integers
  ([Definition 198](#defn-sc-len-encoding)).

- `version`: the state version ([Definition 205](#defn-state-version)).

- `result`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit trie root result.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_trie_keccak_256_root" class="anchor"></a><a href="#id-ext_trie_keccak_256_root" class="link">B.7.3.
<code>ext_trie_keccak_256_root</code></a>

<div class="paragraph">

Compute a 256-bit Keccak trie root formed from the iterated items.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-66" class="anchor"></a><a href="#id-version-1-prototype-66" class="link">B.7.3.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_trie_keccak_256_root_version_1
        (param $data i64) (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the iterated items from which the trie root gets formed. The items
  consist of a SCALE encoded array containing arbitrary key/value pairs.

- `result`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit trie root.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype-11" class="anchor"></a><a href="#id-version-2-prototype-11" class="link">B.7.3.2. Version 2 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_trie_keccak_256_root_version_2
        (param $data i64) (param $version i32)
        (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the iterated items from which the trie root gets formed. The items
  consist of a SCALE encoded array containing arbitrary key/value pairs.

- `version`: the state version ([Definition 205](#defn-state-version)).

- `result`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit trie root.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_trie_keccak_256_ordered_root" class="anchor"></a><a href="#id-ext_trie_keccak_256_ordered_root" class="link">B.7.4.
<code>ext_trie_keccak_256_ordered_root</code></a>

<div class="paragraph">

Compute a 256-bit Keccak trie root formed from the enumerated items.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-67" class="anchor"></a><a href="#id-version-1-prototype-67" class="link">B.7.4.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_trie_keccak_256_ordered_root_version_1
        (param $data i64) (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the enumerated items from which the trie root gets formed. The
  items consist of a SCALE encoded array containing only values, where
  the corresponding key of each value is the index of the item in the
  array, starting at 0. The keys are compact encoded integers
  ([Definition 198](#defn-sc-len-encoding)).

- `result`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit trie root result.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype-12" class="anchor"></a><a href="#id-version-2-prototype-12" class="link">B.7.4.2. Version 2 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_trie_keccak_256_ordered_root_version_2
        (param $data i64) (param $version i32)
        (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the enumerated items from which the trie root gets formed. The
  items consist of a SCALE encoded array containing only values, where
  the corresponding key of each value is the index of the item in the
  array, starting at 0. The keys are compact encoded integers
  ([Definition 198](#defn-sc-len-encoding)).

- `version`: the state version ([Definition 205](#defn-state-version)).

- `result`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  buffer containing the 256-bit trie root result.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_trie_blake2_256_verify_proof" class="anchor"></a><a href="#id-ext_trie_blake2_256_verify_proof" class="link">B.7.5.
<code>ext_trie_blake2_256_verify_proof</code></a>

<div class="paragraph">

Verifies a key/value pair against a Blake2 256-bit merkle root.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-68" class="anchor"></a><a href="#id-version-1-prototype-68" class="link">B.7.5.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_trie_blake2_256_verify_proof_version_1
        (param $root i32) (param $proof i64)
        (param $key i64) (param $value i64)
        (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `root`: a pointer to the 256-bit merkle root.

- `proof`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to an array containing the node proofs.

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

- `value`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the value.

- `return`: a value equal to *1* if the proof could be successfully
  verified or a value equal to *0* if otherwise.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype-13" class="anchor"></a><a href="#id-version-2-prototype-13" class="link">B.7.5.2. Version 2 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_trie_blake2_256_verify_proof_version_2
        (param $root i32) (param $proof i64)
        (param $key i64) (param $value i64)
        (param $version i32) (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `root`: a pointer to the 256-bit merkle root.

- `proof`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to an array containing the node proofs.

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

- `value`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the value.

- `version`: the state version ([Definition 205](#defn-state-version)).

- `return`: a value equal to *1* if the proof could be successfully
  verified or a value equal to *0* if otherwise.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_trie_keccak_256_verify_proof" class="anchor"></a><a href="#id-ext_trie_keccak_256_verify_proof" class="link">B.7.6.
<code>ext_trie_keccak_256_verify_proof</code></a>

<div class="paragraph">

Verifies a key/value pair against a Keccak 256-bit merkle root.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-69" class="anchor"></a><a href="#id-version-1-prototype-69" class="link">B.7.6.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_trie_keccak_256_verify_proof_version_1
        (param $root i32) (param $proof i64)
        (param $key i64) (param $value i64)
        (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `root`: a pointer to the 256-bit merkle root.

- `proof`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to an array containing the node proofs.

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

- `value`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the value.

- `return`: a value equal to *1* if the proof could be successfully
  verified or a value equal to *0* if otherwise.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-version-2-prototype-14" class="anchor"></a><a href="#id-version-2-prototype-14" class="link">B.7.6.2. Version 2 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_trie_keccak_256_verify_proof_version_2
        (param $root i32) (param $proof i64)
        (param $key i64) (param $value i64)
        (param $version i32) (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `root`: a pointer to the 256-bit merkle root.

- `proof`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to an array containing the node proofs.

- `key`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the key.

- `value`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the value.

- `version`: the state version ([Definition 205](#defn-state-version)).

- `return`: a value equal to *1* if the proof could be successfully
  verified or a value equal to *0* if otherwise.

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-misc-api" class="anchor"></a><a href="#sect-misc-api" class="link">B.8. Miscellaneous</a>

<div class="paragraph">

Interface that provides miscellaneous functions for communicating
between the runtime and the node.

</div>

<div class="sect3">

#### <a href="#id-ext_misc_print_num" class="anchor"></a><a href="#id-ext_misc_print_num" class="link">B.8.1.
<code>ext_misc_print_num</code></a>

<div class="paragraph">

Print a number.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-70" class="anchor"></a><a href="#id-version-1-prototype-70" class="link">B.8.1.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_misc_print_num_version_1 (param $value i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `value`: the number to be printed.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_misc_print_utf8" class="anchor"></a><a href="#id-ext_misc_print_utf8" class="link">B.8.2.
<code>ext_misc_print_utf8</code></a>

<div class="paragraph">

Print a valid UTF8 encoded buffer.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-71" class="anchor"></a><a href="#id-version-1-prototype-71" class="link">B.8.2.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_misc_print_utf8_version_1 (param $data i64))

</div>

</div>

<div class="paragraph">

**Arguments**:

</div>

<div class="ulist">

- : a pointer-size ([Definition 203](#defn-runtime-pointer-size)) to the
  valid buffer to be printed.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_misc_print_hex" class="anchor"></a><a href="#id-ext_misc_print_hex" class="link">B.8.3.
<code>ext_misc_print_hex</code></a>

<div class="paragraph">

Print any buffer in hexadecimal representation.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-72" class="anchor"></a><a href="#id-version-1-prototype-72" class="link">B.8.3.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_misc_print_hex_version_1 (param $data i64))

</div>

</div>

<div class="paragraph">

**Arguments**:

</div>

<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the buffer to be printed.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_misc_runtime_version" class="anchor"></a><a href="#id-ext_misc_runtime_version" class="link">B.8.4.
<code>ext_misc_runtime_version</code></a>

<div class="paragraph">

Extract the Runtime version of the given Wasm blob by calling
`Core_version` ([Section C.4.1](#defn-rt-core-version)). Returns the
SCALE encoded runtime version or *None* ([Definition
190](#defn-option-type)) if the call fails. This function gets primarily
used when upgrading Runtimes.

</div>

<div class="admonitionblock warning">

|     |                                                                                                                                                                                                                                                                                                          |
|-----|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | Calling this function is very expensive and should only be done very occasionally. For getting the runtime version, it requires instantiating the Wasm blob ([Section 2.6.2](#sect-loading-runtime-code)) and calling the `Core_version` function ([Section C.4.1](#defn-rt-core-version)) in this blob. |

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-73" class="anchor"></a><a href="#id-version-1-prototype-73" class="link">B.8.4.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_misc_runtime_version_version_1 (param $data i64) (result i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `data`: a pointer-size ([Definition 203](#defn-runtime-pointer-size))
  to the Wasm blob.

- `result`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the SCALE encoded *Option* value
  ([Definition 190](#defn-option-type)) containing the Runtime version
  of the given Wasm blob which is encoded as a byte array.

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-allocator-api" class="anchor"></a><a href="#sect-allocator-api" class="link">B.9. Allocator</a>

<div class="paragraph">

The Polkadot Runtime does not include a memory allocator and relies on
the Host API for all heap allocations. The beginning of this heap is
marked by the `__heap_base` symbol exported by the Polkadot Runtime. No
memory should be allocated below that address, to avoid clashes with the
stack and data section. The same allocator made accessible by this Host
API should be used for any other WASM memory allocations and
deallocations outside the runtime e.g. when passing the SCALE-encoded
parameters to Runtime API calls.

</div>

<div class="sect3">

#### <a href="#id-ext_allocator_malloc" class="anchor"></a><a href="#id-ext_allocator_malloc" class="link">B.9.1.
<code>ext_allocator_malloc</code></a>

<div class="paragraph">

Allocates the given number of bytes and returns the pointer to that
memory location.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-74" class="anchor"></a><a href="#id-version-1-prototype-74" class="link">B.9.1.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_allocator_malloc_version_1 (param $size i32) (result i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `size`: the size of the buffer to be allocated.

- `result`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  allocated buffer.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_allocator_free" class="anchor"></a><a href="#id-ext_allocator_free" class="link">B.9.2.
<code>ext_allocator_free</code></a>

<div class="paragraph">

Free the given pointer.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-75" class="anchor"></a><a href="#id-version-1-prototype-75" class="link">B.9.2.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_allocator_free_version_1 (param $ptr i32))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `ptr`: a pointer ([Definition 202](#defn-runtime-pointer)) to the
  memory buffer to be freed.

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-logging-api" class="anchor"></a><a href="#sect-logging-api" class="link">B.10. Logging</a>

<div class="paragraph">

Interface that provides functions for logging from within the runtime.

</div>

<div id="defn-logging-log-level" class="exampleblock">

<div class="title">

Definition 214. [Log Level](#defn-logging-log-level)

</div>

<div class="content">

<div class="paragraph">

The **Log Level**, \\L\\, is a varying data type ([Definition
188](#defn-varrying-data-type)) and implies the emergency of the log.
Possible log levels and the corresponding identifier is as follows:

</div>

<div class="stemblock">

<div class="content">

\\L = {(0,"Error = 1"),(1,"Warn = 2"),(2,"Info = 3"),(3, "Debug =
4"),(4,"Trace = 5"):}\\

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-ext_logging_log" class="anchor"></a><a href="#id-ext_logging_log" class="link">B.10.1.
<code>ext_logging_log</code></a>

<div class="paragraph">

Request to print a log message on the host. Note that this will be only
displayed if the host is enabled to display log messages with given
level and target.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-76" class="anchor"></a><a href="#id-version-1-prototype-76" class="link">B.10.1.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_logging_log_version_1
        (param $level i32) (param $target i64) (param $message i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `level`: the log level ([Definition 214](#defn-logging-log-level)).

- `target`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the string which contains the
  path, module or location from where the log was executed.

- `message`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the UTF-8 encoded log message.

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#id-abort-handler" class="anchor"></a><a href="#id-abort-handler" class="link">B.11. Abort Handler</a>

<div class="paragraph">

Interface for aborting the execution of the runtime.

</div>

<div class="sect3">

#### <a href="#id-ext_panic_handler_abort_on_panic" class="anchor"></a><a href="#id-ext_panic_handler_abort_on_panic" class="link">B.11.1.
<code>ext_panic_handler_abort_on_panic</code></a>

<div class="paragraph">

Aborts the execution of the runtime with a given message. Note that the
message will be only displayed if the host is enabled to display those
types of messages, which is implementation specific.

</div>

<div class="sect4">

##### <a href="#id-version-1-prototype-77" class="anchor"></a><a href="#id-version-1-prototype-77" class="link">B.11.1.1. Version 1 -
Prototype</a>

<div class="listingblock">

<div class="content">

    (func $ext_panic_handler_abort_on_panic_version_1
        (param $message i64))

</div>

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- `message`: a pointer-size ([Definition
  203](#defn-runtime-pointer-size)) to the UTF-8 encoded message.

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#chap-runtime-api" class="anchor"></a><a href="#chap-runtime-api" class="link">Appendix C: Runtime API</a>

<div class="sectionbody">

<div class="paragraph">

Description of how to interact with the Runtime through its exported
functions

</div>

<div class="sect2">

### <a href="#id-general-information" class="anchor"></a><a href="#id-general-information" class="link">C.1. General
Information</a>

<div class="paragraph">

The Polkadot Host assumes that at least the constants and functions
described in this Chapter are implemented in the Runtime Wasm blob.

</div>

<div class="paragraph">

It should be noted that the API can change through the Runtime updates.
Therefore, a host should check the API versions of each module returned
in the `api` field by `Core_version` ([Section
C.4.1](#defn-rt-core-version)) after every Runtime upgrade and warn if
an updated API is encountered and that this might require an update of
the host.

</div>

<div class="paragraph">

In this section, we describe all Runtime API functions alongside their
arguments and the return values. The functions are organized into
modules with each being versioned independently.

</div>

<div class="sect3">

#### <a href="#sect-json-rpc-api" class="anchor"></a><a href="#sect-json-rpc-api" class="link">C.1.1. JSON-RPC API for
external services</a>

<div class="paragraph">

Polkadot Host implementers are encouraged to implement an API in order
for external, third-party services to interact with the node. The
[JSON-RPC Interface for Polkadot
Nodes](https://github.com/w3f/PSPs/blob/master/PSPs/drafts/psp-6.md)
(PSP6) is a Polkadot Standard Proposal for such an API and makes it
easier to integrate the node with existing tools available in the
Polkadot ecosystem, such as [polkadot.js.org](https://polkadot.js.org/).
The Runtime API has a few modules designed specifically for use in the
official RPC API.

</div>

</div>

</div>

<div class="sect2">

### <a href="#id-runtime-constants" class="anchor"></a><a href="#id-runtime-constants" class="link">C.2. Runtime Constants</a>

<div class="sect3">

#### <a href="#id-__heap_base" class="anchor"></a><a href="#id-__heap_base" class="link">C.2.1.
<code>__heap_base</code></a>

<div class="paragraph">

This constant indicates the beginning of the heap in memory. The space
below is reserved for the stack and the data section. For more details
please refer to [Section 2.6.3.1](#sect-memory-management).

</div>

</div>

</div>

<div class="sect2">

### <a href="#id-runtime-call-convention" class="anchor"></a><a href="#id-runtime-call-convention" class="link">C.3. Runtime Call
Convention</a>

<div id="defn-runtime-api-convention" class="exampleblock">

<div class="title">

Definition 215. Runtime API Call Convention

</div>

<div class="content">

<div class="paragraph">

The **Runtime API Call Convention** describes that all functions receive
and return SCALE-encoded data and as a result have the following
prototype signature:

</div>

<div class="listingblock">

<div class="content">

``` rouge
(func $generic_runtime_entry
  (param $ptr i32) (parm $len i32) (result i64))
```

</div>

</div>

<div class="paragraph">

where `ptr` points to the SCALE encoded tuple of the parameters passed
to the function and `len` is the length of this data, while `result` is
a pointer-size (Definition [Definition 203](#defn-runtime-pointer-size))
to the SCALE-encoded return data.

</div>

</div>

</div>

<div class="paragraph">

See [Section 2.6.3](#sect-code-executor) for more information about the
behavior of the Wasm Runtime. Also note that any storage changes must be
fork-aware ([Section 2.4.5](#sect-managing-multiple-states)).

</div>

</div>

<div class="sect2">

### <a href="#sect-runtime-core-module" class="anchor"></a><a href="#sect-runtime-core-module" class="link">C.4. Module Core</a>

<div class="admonitionblock important">

|     |                                                                                                                                                 |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This section describes **Version 3** of this API. Please check `Core_version` ([Section C.4.1](#defn-rt-core-version)) to ensure compatibility. |

</div>

<div class="sect3">

#### <a href="#defn-rt-core-version" class="anchor"></a><a href="#defn-rt-core-version" class="link">C.4.1.
<code>Core_version</code></a>

<div class="admonitionblock important">

|     |                                                                                                                                                                                                                                                                                  |
|-----|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | For newer Runtimes, the version identifiers can be read directly from the Wasm blob in form of custom sections ([Section 2.6.3.4](#sect-runtime-version-custom-section)). That method of retrieving this data should be preferred since it involves significantly less overhead. |

</div>

<div class="paragraph">

Returns the version identifiers of the Runtime. This function can be
used by the Polkadot Host implementation when it seems appropriate, such
as for the JSON-RPC API as described in [Section
C.1.1](#sect-json-rpc-api).

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None

</div>

Return  
<div class="ulist">

- A datastructure of the following format:

  | Name                  | Type                                             | Description                                     |
  |-----------------------|--------------------------------------------------|-------------------------------------------------|
  | `spec_name`           | String                                           | Runtime identifier                              |
  | `impl_name`           | String                                           | Name of the implementation (e.g. C++)           |
  | `authoring_version`   | Unsigned 32-bit integer                          | Version of the authorship interface             |
  | `spec_version`        | Unsigned 32-bit integer                          | Version of the Runtime specification            |
  | `impl_version`        | Unsigned 32-bit integer                          | Version of the Runtime implementation           |
  | `apis`                | ApiVersions ([Definition 216](#defn-rt-apisvec)) | List of supported APIs along with their version |
  | `transaction_version` | Unsigned 32-bit integer                          | Version of the transaction format               |
  | `state_version`       | Unsigned 8-bit integer                           | Version of the trie format                      |

  Table 6. Details of the version that the data type returns from the
  Runtime function.

</div>

</div>

<div id="defn-rt-apisvec" class="exampleblock">

<div class="title">

Definition 216. ApiVersions

</div>

<div class="content">

<div class="paragraph">

**ApiVersions** is a specialized type for the ([Section
C.4.1](#defn-rt-core-version)) function entry. It represents an array of
tuples, where the first value of the tuple is an array of 8-bytes
containing the Blake2b hash of the API name. The second value of the
tuple is the version number of the corresponding API.

</div>

<div class="stemblock">

<div class="content">

\\\begin{aligned} \mathrm{ApiVersions} :=& (T_0, \ldots, T_n)\\ T :=&
((b_0, \ldots, b_7), \mathrm{UINT32}) \end{aligned}\\

</div>

</div>

</div>

</div>

<div class="paragraph">

Requires `Core_initialize_block` to be called beforehand.

</div>

</div>

<div class="sect3">

#### <a href="#sect-rte-core-execute-block" class="anchor"></a><a href="#sect-rte-core-execute-block" class="link">C.4.2.
<code>Core_execute_block</code></a>

<div class="paragraph">

This function executes a full block and all its extrinsics and updates
the state accordingly. Additionally, some integrity checks are executed
such as validating if the parent hash is correct and that the
transaction root represents the transactions. Internally, this function
performs an operation similar to the process described in
[Build-Block](#algo-build-block), by calling
`Core_initialize_block`,`BlockBuilder_apply_extrinsics` and
`BlockBuilder_finalize_block`.

</div>

<div class="paragraph">

This function should be called when a fully complete block is available
that is not actively being built on, such as blocks received from other
peers. State changes resulted from calling this function are usually
meant to persist when the block is imported successfully.

</div>

<div class="paragraph">

Additionally, the seal digest in the block header, as described in
[Definition 11](#defn-digest), must be removed by the Polkadot host
before submitting the block.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- A block represented as a tuple consisting of a block header, as
  described in [Definition 10](#defn-block-header), and the block body,
  as described in [Definition 13](#defn-block-body).

</div>

Return  
<div class="ulist">

- None.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-rte-core-initialize-block" class="anchor"></a><a href="#sect-rte-core-initialize-block" class="link">C.4.3.
<code>Core_initialize_block</code></a>

<div class="paragraph">

Sets up the environment required for building a new block as described
in [Build-Block](#algo-build-block).

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The header of the new block as defined in [Definition
  10](#defn-block-header). The values \\H_r\\, \\H_e\\ and \\H_d\\ are
  left empty.

</div>

Return  
<div class="ulist">

- None.

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-runtime-metadata-module" class="anchor"></a><a href="#sect-runtime-metadata-module" class="link">C.5. Module
Metadata</a>

<div class="admonitionblock important">

|     |                                                                                                                                                 |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This section describes **Version 1** of this API. Please check `Core_version` ([Section C.4.1](#defn-rt-core-version)) to ensure compatibility. |

</div>

<div class="sect3">

#### <a href="#sect-rte-metadata-metadata" class="anchor"></a><a href="#sect-rte-metadata-metadata" class="link">C.5.1.
<code>Metadata_metadata</code></a>

<div class="paragraph">

Returns native Runtime metadata in an opaque form. This function can be
used by the Polkadot Host implementation when it seems appropriate, such
as for the JSON-RPC API as described in [Section
C.1.1](#sect-json-rpc-api). and returns all the information necessary to
build valid transactions.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None.

</div>

Return  
<div class="ulist">

- The scale-encoded ([Section A.2.2](#sect-scale-codec)) runtime
  metadata as described in [Chapter 12](#sect-metadata).

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-runtime-blockbuilder-module" class="anchor"></a><a href="#sect-runtime-blockbuilder-module" class="link">C.6. Module
BlockBuilder</a>

<div class="admonitionblock important">

|     |                                                                                                                                                 |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This section describes **Version 4** of this API. Please check `Core_version` ([Section C.4.1](#defn-rt-core-version)) to ensure compatibility. |

</div>

<div class="paragraph">

All calls in this module require `Core_initialize_block` ([Section
C.4.3](#sect-rte-core-initialize-block)) to be called beforehand.

</div>

<div class="sect3">

#### <a href="#sect-rte-apply-extrinsic" class="anchor"></a><a href="#sect-rte-apply-extrinsic" class="link">C.6.1.
<code>BlockBuilder_apply_extrinsic</code></a>

<div class="paragraph">

Apply the extrinsic outside of the block execution function. This does
not attempt to validate anything regarding the block, but it builds a
list of transaction hashes.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- A byte array of varying size containing the opaque extrinsic.

</div>

Return  
<div class="ulist">

- Returns the varying datatype *ApplyExtrinsicResult* as defined in
  [Definition 217](#defn-rte-apply-extrinsic-result). This structure
  lets the block builder know whether an extrinsic should be included
  into the block or rejected.

</div>

</div>

<div id="defn-rte-apply-extrinsic-result" class="exampleblock">

<div class="title">

Definition 217. ApplyExtrinsicResult

</div>

<div class="content">

<div class="paragraph">

**ApplyExtrinsicResult** is a varying data type as defined in
[Definition 191](#defn-result-type). This structure can contain multiple
nested structures, indicating either module dispatch outcomes or
transaction invalidity errors.

</div>

| **Id** | **Description**                                               | **Type**                                                                            |
|--------|---------------------------------------------------------------|-------------------------------------------------------------------------------------|
| 0      | Outcome of dispatching the extrinsic.                         | *DispatchOutcome* ([Definition 218](#defn-rte-dispatch-outcome))                    |
| 1      | Possible errors while checking the validity of a transaction. | *TransactionValidityError* ([Definition 221](#defn-rte-transaction-validity-error)) |

Table 7. Possible values of varying data type *ApplyExtrinsicResult*.

</div>

</div>

<div class="admonitionblock note">

|     |                                                                                                                                                                                                                                                                     |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | As long as a *DispatchOutcome* ([Definition 218](#defn-rte-dispatch-outcome)) is returned, the extrinsic is always included in the block, even if the outcome is a dispatch error. Dispatch errors do not invalidate the block and all state changes are persisted. |

</div>

<div id="defn-rte-dispatch-outcome" class="exampleblock">

<div class="title">

Definition 218. DispatchOutcome

</div>

<div class="content">

<div class="paragraph">

**DispatchOutcome** is the varying data type as defined in [Definition
191](#defn-result-type).

</div>

| **Id** | **Description**                                    | **Type**                                                     |
|--------|----------------------------------------------------|--------------------------------------------------------------|
| 0      | Extrinsic is valid and was submitted successfully. | None                                                         |
| 1      | Possible errors while dispatching the extrinsic.   | *DispatchError* ([Definition 219](#defn-rte-dispatch-error)) |

Table 8. Possible values of varying data type *DispatchOutcome*.

</div>

</div>

<div id="defn-rte-dispatch-error" class="exampleblock">

<div class="title">

Definition 219. DispatchError

</div>

<div class="content">

<div class="paragraph">

**DispatchError** is a varying data type as defined in [Definition
188](#defn-varrying-data-type). Indicates various reasons why a dispatch
call failed.

</div>

| **Id** | **Description**              | **Type**                                                              |
|--------|------------------------------|-----------------------------------------------------------------------|
| 0      | Some unknown error occurred. | SCALE encoded byte array containing a valid UTF-8 sequence.           |
| 1      | Failed to lookup some data.  | None                                                                  |
| 2      | A bad origin.                | None                                                                  |
| 3      | A custom error in a module.  | *CustomModuleError* ([Definition 220](#defn-rte-custom-module-error)) |

Table 9. Possible values of varying data type *DispatchError*.

</div>

</div>

<div id="defn-rte-custom-module-error" class="exampleblock">

<div class="title">

Definition 220. CustomModuleError

</div>

<div class="content">

<div class="paragraph">

**CustomModuleError** is a tuple appended after a possible error in as
defined in [Definition 219](#defn-rte-dispatch-error).

</div>

| **Name** | **Description**                                  | **Type**                                                                                                                                              |
|----------|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| Index    | Module index matching the metadata module index. | Unsigned 8-bit integer.                                                                                                                               |
| Error    | Module specific error value.                     | Unsigned 8-bit integer                                                                                                                                |
| Message  | Optional error message.                          | Varying data type *Option* ([Definition 190](#defn-option-type)). The optional value is a SCALE encoded byte array containing a valid UTF-8 sequence. |

Table 10. Possible values of varying data type *CustomModuleError*.

</div>

</div>

<div class="admonitionblock note">

|     |                                                                                                                                                                                                                                                                                                                                                                                           |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | Whenever *TransactionValidityError* ([Definition 221](#defn-rte-transaction-validity-error)) is returned, the contained error type will indicate whether an extrinsic should be outright rejected or requested for a later block. This behavior is clarified further in [Definition 222](#defn-rte-invalid-transaction) and respectively [Definition 223](#defn-rte-unknown-transaction). |

</div>

<div id="defn-rte-transaction-validity-error" class="exampleblock">

<div class="title">

Definition 221. TransactionValidityError

</div>

<div class="content">

<div class="paragraph">

**TransactionValidityError** is a varying data type as defined in
[Definition 188](#defn-varrying-data-type). It indicates possible errors
that can occur while checking the validity of a transaction.

</div>

| **Id** | **Description**                           | **Type**                                                               |
|--------|-------------------------------------------|------------------------------------------------------------------------|
| 0      | Transaction is invalid.                   | *InvalidTransaction* ([Definition 222](#defn-rte-invalid-transaction)) |
| 1      | Transaction validity can’t be determined. | *UnknownTransaction* ([Definition 223](#defn-rte-unknown-transaction)) |

Table 11. Possible values of varying data type
*TransactionValidityError*.

</div>

</div>

<div id="defn-rte-invalid-transaction" class="exampleblock">

<div class="title">

Definition 222. InvalidTransaction

</div>

<div class="content">

<div class="paragraph">

**InvalidTransaction** is a varying data type as defined in [Definition
188](#defn-varrying-data-type) and specifies the invalidity of the
transaction in more detail.

</div>

| **Id** | **Description**                                                                                  | **Type**               | **Reject** |
|--------|--------------------------------------------------------------------------------------------------|------------------------|------------|
| 0      | Call of the transaction is not expected.                                                         | None                   | Yes        |
| 1      | General error to do with the inability to pay some fees (e.g. account balance too low).          | None                   | Yes        |
| 2      | General error to do with the transaction not yet being valid (e.g. nonce too high).              | None                   | No         |
| 3      | General error to do with the transaction being outdated (e.g. nonce too low).                    | None                   | Yes        |
| 4      | General error to do with the transactions’ proof (e.g. signature)                                | None                   | Yes        |
| 5      | The transaction birth block is ancient.                                                          | None                   | Yes        |
| 6      | The transaction would exhaust the resources of the current block.                                | None                   | No         |
| 7      | Some unknown error occurred.                                                                     | Unsigned 8-bit integer | Yes        |
| 8      | An extrinsic with mandatory dispatch resulted in an error.                                       | None                   | Yes        |
| 9      | A transaction with a mandatory dispatch (only inherents are allowed to have mandatory dispatch). | None                   | Yes        |

Table 12. Possible values of varying data type *InvalidTransaction*.

</div>

</div>

<div id="defn-rte-unknown-transaction" class="exampleblock">

<div class="title">

Definition 223. UnknownTransaction

</div>

<div class="content">

<div class="paragraph">

**UnknownTransaction** is a varying data type as defined in [Definition
188](#defn-varrying-data-type) and specifies the unknown invalidity of
the transaction in more detail.

</div>

| **Id** | **Description**                                                                 | **Type**               | **Reject** |
|--------|---------------------------------------------------------------------------------|------------------------|------------|
| 0      | Could not lookup some information that is required to validate the transaction. | None                   | Yes        |
| 1      | No validator found for the given unsigned transaction.                          | None                   | Yes        |
| 2      | Any other custom unknown validity that is not covered by this type.             | Unsigned 8-bit integer | Yes        |

Table 13. Possible values of varying data type *UnknownTransaction*.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#defn-rt-blockbuilder-finalize-block" class="anchor"></a><a href="#defn-rt-blockbuilder-finalize-block" class="link">C.6.2.
<code>BlockBuilder_finalize_block</code></a>

<div class="paragraph">

Finalize the block - it is up to the caller to ensure that all header
fields are valid except for the state root. State changes resulting from
calling this function are usually meant to persist upon successful
execution of the function and appending of the block to the chain.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None.

</div>

Return  
<div class="ulist">

- The header of the new block as defined in [Definition
  10](#defn-block-header).

</div>

</div>

</div>

<div class="sect3">

#### <a href="#defn-rt-builder-inherent-extrinsics" class="anchor"></a><a href="#defn-rt-builder-inherent-extrinsics" class="link">C.6.3.
<code>BlockBuilder_inherent_extrinisics</code>:</a>

<div class="paragraph">

Generates the inherent extrinsics, which are explained in more detail in
[Section 2.3.3](#sect-inherents). This function takes a SCALE-encoded
hash table as defined in [Definition 192](#defn-scale-list) and returns
an array of extrinsics. The Polkadot Host must submit each of those to
the `BlockBuilder_apply_extrinsic`, described in [Section
C.6.1](#sect-rte-apply-extrinsic). This procedure is outlined in
[Build-Block](#algo-build-block).

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- A Inherents-Data structure as defined in [Definition
  15](#defn-inherent-data).

</div>

Return  
<div class="ulist">

- A byte array of varying size containing extrinisics. Each extrinsic is
  a byte array of varying size.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-blockbuilder_check_inherents" class="anchor"></a><a href="#id-blockbuilder_check_inherents" class="link">C.6.4.
<code>BlockBuilder_check_inherents</code></a>

<div class="paragraph">

Checks whether the provided inherent is valid. This function can be used
by the Polkadot Host when deemed appropriate, e.g. during the
block-building process.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- A block represented as a tuple consisting of a block header as
  described in [Definition 10](#defn-block-header) and the block body as
  described in [Definition 13](#defn-block-body).

- A Inherents-Data structure as defined in [Definition
  15](#defn-inherent-data).

</div>

Return  
<div class="ulist">

- A data structure of the following format:

  <div class="stemblock">

  <div class="content">

  \\(o, f_e, e)\\

  </div>

  </div>

  <div class="dlist">

  where  
  <div class="ulist">

  - \\o\\ is a boolean indicating whether the check was successful.

  - \\f_e\\ is a boolean indicating whether a fatal error was
    encountered.

  - \\e\\ is a Inherents-Data structure as defined in [Definition
    15](#defn-inherent-data) containing any errors created by this
    Runtime function.

  </div>

  </div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-blockbuilder_random_seed" class="anchor"></a><a href="#id-blockbuilder_random_seed" class="link">C.6.5.
<code>BlockBuilder_random_seed</code></a>

<div class="paragraph">

Generates a random seed.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None

</div>

Return  
<div class="ulist">

- A 32-byte array containing the random seed.

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-runtime-txqueue-module" class="anchor"></a><a href="#sect-runtime-txqueue-module" class="link">C.7. Module
TaggedTransactionQueue</a>

<div class="admonitionblock important">

|     |                                                                                                                                                 |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This section describes **Version 2** of this API. Please check `Core_version` ([Section C.4.1](#defn-rt-core-version)) to ensure compatibility. |

</div>

<div class="paragraph">

All calls in this module require `Core_initialize_block` ([Section
C.4.3](#sect-rte-core-initialize-block)) to be called beforehand.

</div>

<div class="sect3">

#### <a href="#sect-rte-validate-transaction" class="anchor"></a><a href="#sect-rte-validate-transaction" class="link">C.7.1.
<code>TaggedTransactionQueue_validate_transaction</code></a>

<div class="paragraph">

This entry is invoked against extrinsics submitted through a transaction
network message ([Section 4.8.5](#sect-msg-transactions)) or by an
offchain worker through the Host API ([Section
B.6.2](#sect-ext-offchain-submit-transaction)).

</div>

<div class="paragraph">

It indicates if the submitted blob represents a valid extrinsics, the
order in which it should be applied and if it should be gossiped to
other peers. Furthermore this function gets called internally when
executing blocks with the runtime function as described in [Section
C.4.2](#sect-rte-core-execute-block).

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The source of the transaction as defined in [Definition
  224](#defn-transaction-source).

- A byte array that contains the transaction.

- The hash of the parent of the block that the transaction is included
  in.

  <div id="defn-transaction-source" class="exampleblock">

  <div class="title">

  Definition 224. TransactionSource

  </div>

  <div class="content">

  <div class="paragraph">

  **TransactionSource** is an enum describing the source of a
  transaction and can have one of the following values:

  </div>

  | Id  | Name       | Description                                                       |
  |-----|------------|-------------------------------------------------------------------|
  | 0   | *InBlock*  | Transaction is already included in a block.                       |
  | 1   | *Local*    | Transaction is coming from a local source, e.g. off-chain worker. |
  | 2   | *External* | Transaction has been received externally, e.g. over the network.  |

  Table 14. The *TransactionSource* enum

  </div>

  </div>

</div>

Return  
<div class="ulist">

- This function returns a *Result* as defined in [Definition
  191](#defn-result-type) which contains the type *ValidTransaction* as
  defined in [Definition 225](#defn-valid-transaction) on success and
  the type *TransactionValidityError* as defined in [Definition
  221](#defn-rte-transaction-validity-error) on failure.

  <div id="defn-valid-transaction" class="exampleblock">

  <div class="title">

  Definition 225. ValidTransaction

  </div>

  <div class="content">

  <div class="paragraph">

  **ValidTransaction** is a tuple that contains information concerning a
  valid transaction.

  </div>

  | **Name**    | **Description**                                                                                                                                                                                           | **Type**                      |
  |-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------|
  | *Priority*  | Determines the ordering of two transactions that have all their dependencies (required tags) are satisfied.                                                                                               | Unsigned 64bit integer        |
  | *Requires*  | List of tags specifying extrinsics which should be applied before the current exrinsics can be applied.                                                                                                   | Array containing inner arrays |
  | *Provides*  | Informs Runtime of the extrinsics depending on the tags in the list that can be applied after current extrinsics are being applied. Describes the minimum number of blocks for the validity to be correct | Array containing inner arrays |
  | *Longevity* | After this period, the transaction should be removed from the pool or revalidated.                                                                                                                        | Unsigned 64-bit integer       |
  | *Propagate* | A flag indicating if the transaction should be gossiped to other peers.                                                                                                                                   | Boolean                       |

  Table 15. The tuple provided by in the case the transaction is judged
  to be valid.

  </div>

  </div>

</div>

</div>

<div class="admonitionblock note">

|     |                                                                                                                                                                                     |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | If *Propagate* is set to `false` the transaction will still be considered for inclusion in blocks that are authored on the current node, but should not be gossiped to other peers. |

</div>

<div class="admonitionblock note">

|     |                                                                                                                                                                                            |
|-----|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | If this function gets called by the Polkadot Host in order to validate a transaction received from peers, the Polkadot Host disregards and rewinds state changes resulting in such a call. |

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-runtime-offchainapi-module" class="anchor"></a><a href="#sect-runtime-offchainapi-module" class="link">C.8. Module
OffchainWorkerApi</a>

<div class="admonitionblock important">

|     |                                                                                                                                                 |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This section describes **Version 2** of this API. Please check `Core_version` ([Section C.4.1](#defn-rt-core-version)) to ensure compatibility. |

</div>

<div class="paragraph">

Does not require `Core_initialize_block` ([Section
C.4.3](#sect-rte-core-initialize-block)) to be called beforehand.

</div>

<div class="sect3">

#### <a href="#id-offchainworkerapi_offchain_worker" class="anchor"></a><a href="#id-offchainworkerapi_offchain_worker" class="link">C.8.1.
<code>OffchainWorkerApi_offchain_worker</code></a>

<div class="paragraph">

Starts an off-chain worker and generates extrinsics. \[To do: when is
this called?\]

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The block header as defined in [Definition 10](#defn-block-header).

</div>

Return  
<div class="ulist">

- None.

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#sect-anv-runtime-api" class="anchor"></a><a href="#sect-anv-runtime-api" class="link">C.9. Module
ParachainHost</a>

<div class="admonitionblock important">

|     |                                                                                                                                                 |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This section describes **Version 1** of this API. Please check `Core_version` ([Section C.4.1](#defn-rt-core-version)) to ensure compatibility. |

</div>

<div class="sect3">

#### <a href="#sect-rt-api-validators" class="anchor"></a><a href="#sect-rt-api-validators" class="link">C.9.1.
<code>ParachainHost_validators</code></a>

<div class="paragraph">

Returns the validator set at the current state. The specified validators
are responsible for backing parachains for the current state.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None.

</div>

Return  
<div class="ulist">

- An array of public keys representing the validators.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-rt-api-validator-groups" class="anchor"></a><a href="#sect-rt-api-validator-groups" class="link">C.9.2.
<code>ParachainHost_validator_groups</code></a>

<div class="paragraph">

Returns the validator groups ([Definition 136](#defn-validator-groups))
used during the current session. The validators in the groups are
referred to by the validator set Id ([Definition
33](#defn-authority-list)).

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None

</div>

Return  
<div class="ulist">

- An array of tuples, \\T\\, of the following format:

  <div class="stemblock">

  <div class="content">

  \\T = (I,G)\\ \\I = (v_n,…v_m)\\ \\G = (B_s,f,B_c)\\

  </div>

  </div>

  <div class="dlist">

  where  
  <div class="ulist">

  - \\I\\ is an array the validator set Ids ([Definition
    33](#defn-authority-list)).

  - \\B_s\\ indicates the block number where the session started.

  - \\f\\ indicates how often groups rotate. 0 means never.

  - \\B_c\\ indicates the current block number.

  </div>

  </div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-rt-api-availability-cores" class="anchor"></a><a href="#sect-rt-api-availability-cores" class="link">C.9.3.
<code>ParachainHost_availability_cores</code></a>

<div class="paragraph">

Returns information on all availability cores ([Definition
135](#defn-availability-core)).

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None

</div>

Return  
<div class="ulist">

- An array of core states, S, of the following format:

  <div class="stemblock">

  <div class="content">

  \\S = {(0,-\>,C_o),(1,-\>,C_s),(2,-\>,phi):}\\ \\C_o =
  (n_u,B_o,B_t,n_t,b,G_i,C_h,C_d)\\ \\C_s = (P_id,C_i)\\

  </div>

  </div>

  <div class="dlist">

  where  
  <div class="ulist">

  - \\S\\ specifies the core state. *0* indicates that the core is
    occupied, *1* implies it’s currently free but scheduled and given
    the opportunity to occupy and *2* implies it’s free and there’s
    nothing scheduled.

  - \\n_u\\ is an *Option* value ([Definition 190](#defn-option-type))
    which can contain a \\C_s\\ value if the core was freed by the
    Runtime and indicates the assignment that is next scheduled on this
    core. An empty value indicates there is nothing scheduled.

  - \\B_o\\ indicates the relay chain block number at which the core got
    occupied.

  - \\B_t\\ indicates the relay chain block number the core will
    time-out at, if any.

  - \\n_t\\ is an *Option* value ([Definition 190](#defn-option-type))
    which can contain a \\C_s\\ value if the core is freed by a time-out
    and indicates the assignment that is next scheduled on this core. An
    empty value indicates there is nothing scheduled.

  - \\b\\ is a bitfield array ([Definition 141](#defn-bitfield-array)).
    A \\\>2/3\\ majority of assigned validators voting with \\1\\ values
    means that the core is available.

  - \\G_i\\ indicates the assigned validator group index ([Definition
    136](#defn-validator-groups)) is to distribute availability pieces
    of this candidate.

  - \\C_h\\ indicates the hash of the candidate occupying the core.

  - \\C_d\\ is the candidate descriptor ([Definition
    106](#defn-candidate-descriptor)).

  - \\C_i\\ is an *Option* value ([Definition 190](#defn-option-type))
    which can contain the collators public key indicating who should
    author the block.

  </div>

  </div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-rt-api-persisted-validation-data" class="anchor"></a><a href="#sect-rt-api-persisted-validation-data" class="link">C.9.4.
<code>ParachainHost_persisted_validation_data</code></a>

<div class="paragraph">

Returns the persisted validation data for the given parachain Id and a
given occupied core assumption.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The parachain Id ([Definition 134](#defn-para-id)).

- An occupied core assumption ([Definition
  226](#defn-occupied-core-assumption)).

</div>

Return  
<div class="ulist">

- An *Option* value ([Definition 190](#defn-option-type)) which can
  contain the persisted validation data ([Definition
  227](#defn-persisted-validation-data)). The value is empty if the
  parachain Id is not registered or the core assumption is of index
  \\2\\, meaning that the core was freed.

</div>

</div>

<div id="defn-occupied-core-assumption" class="exampleblock">

<div class="title">

Definition 226. [Occupied Core
Assumption](#defn-occupied-core-assumption)

</div>

<div class="content">

<div class="paragraph">

A occupied core assumption is used for fetching certain pieces of
information about a parachain by using the relay chain API. The
assumption indicates how the Runtime API should compute the result. The
assumptions, A, is a varying datatype of the following format:

</div>

<div class="stemblock">

<div class="content">

\\A = {(0,-\>,phi),(1,-\>,phi),(2,-\>,phi):}\\

</div>

</div>

<div class="paragraph">

where *0* indicates that the candidate occupying the core was made
available and included to free the core, *1* indicates that it timed-out
and freed the core without advancing the parachain and *2* indicates
that the core was not occupied to begin with.

</div>

</div>

</div>

<div id="defn-persisted-validation-data" class="exampleblock">

<div class="title">

Definition 227. [Persisted Validation
Data](#defn-persisted-validation-data)

</div>

<div class="content">

<div class="paragraph">

The persisted validation data provides information about how to create
the inputs for the validation of a candidate by calling the Runtime.
This information is derived from the parachain state and will vary from
parachain to parachain, although some of the fields may be the same for
every parachain. This validation data acts as a way to authorize the
additional data (such as messages) the collator needs to pass to the
validation function.

</div>

<div class="paragraph">

The persisted validation data, \\D\_{pv}\\, is a datastructure of the
following format:

</div>

<div class="stemblock">

<div class="content">

\\D\_{pv} = (P_h,H_i,H_r,m_b)\\

</div>

</div>

<div class="dlist">

where  
<div class="ulist">

- \\P_h\\ is the parent head data ([Definition 133](#defn-head-data)).

- \\H_i\\ is the relay chain block number this is in the context of.

- \\H_r\\ is the relay chain storage root this is in the context of.

- \\m_b\\ is the maximum legal size of the PoV block, in bytes.

</div>

</div>

<div class="paragraph">

The persisted validation data is fetched via the Runtime API ([Section
C.9.4](#sect-rt-api-persisted-validation-data)).

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-parachainhost_check_validation_outputs" class="anchor"></a><a href="#id-parachainhost_check_validation_outputs" class="link">C.9.5.
<code>ParachainHost_check_validation_outputs</code></a>

<div class="paragraph">

Checks if the given validation outputs pass the acceptance criteria.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The parachain Id ([Definition 134](#defn-para-id)).

- The candidate commitments ([Definition
  107](#defn-candidate-commitments)).

</div>

Return  
<div class="ulist">

- A boolean indicating whether the candidate commitments pass the
  acceptance criteria.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-parachainhost_session_index_for_child" class="anchor"></a><a href="#id-parachainhost_session_index_for_child" class="link">C.9.6.
<code>ParachainHost_session_index_for_child</code></a>

<div class="paragraph">

Returns the session index that is expected at the child of a block.

</div>

<div class="admonitionblock warning">

|     |                            |
|-----|----------------------------|
|     | TODO clarify session index |

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None

</div>

Return  
<div class="ulist">

- A unsigned 32-bit integer representing the session index.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-rt-api-validation-code" class="anchor"></a><a href="#sect-rt-api-validation-code" class="link">C.9.7.
<code>ParachainHost_validation_code</code></a>

<div class="paragraph">

Fetches the validation code (Runtime) of a parachain by parachain Id.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The parachain Id ([Definition 134](#defn-para-id)).

- The occupied core assumption ([Definition
  226](#defn-occupied-core-assumption)).

</div>

Return  
<div class="ulist">

- An *Option* value ([Definition 190](#defn-option-type)) containing the
  full validation code in an byte array. This value is empty if the
  parachain Id cannot be found or the assumption is wrong.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-rt-api-validation-code-by-hash" class="anchor"></a><a href="#sect-rt-api-validation-code-by-hash" class="link">C.9.8.
<code>ParachainHost_validation_code_by_hash</code></a>

<div class="paragraph">

Returns the validation code (Runtime) of a parachain by its hash.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The hash value of the validation code.

</div>

Return  
<div class="ulist">

- An *Option* value ([Definition 190](#defn-option-type)) containing the
  full validation code in an byte array. This value is empty if the
  parachain Id cannot be found or the assumption is wrong.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-parachainhost_candidate_pending_availability"
class="anchor"></a><a href="#id-parachainhost_candidate_pending_availability"
class="link">C.9.9.
<code>ParachainHost_candidate_pending_availability</code></a>

<div class="paragraph">

Returns the receipt of a candidate pending availability for any
parachain assigned to an occupied availability core.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The parachain Id ([Definition 134](#defn-para-id)).

</div>

Return  
<div class="ulist">

- An *Option* value ([Definition 190](#defn-option-type)) containing the
  committed candidate receipt ([Definition
  104](#defn-candidate-receipt)). This value is empty if the given
  parachain Id is not assigned to an occupied availability cores.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-parachainhost_candidate_events" class="anchor"></a><a href="#id-parachainhost_candidate_events" class="link">C.9.10.
<code>ParachainHost_candidate_events</code></a>

<div class="paragraph">

Returns an array of candidate events that occurred within the latest
state.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None

</div>

Return  
<div class="ulist">

- An array of single candidate events, E, of the following format:

  <div class="stemblock">

  <div class="content">

  \\E = {(0,-\>,d),(1,-\>,d),(2,-\>,(C_r,h,I_c)):}\\ \\d =
  (C_r,h,I_c,G_i)\\

  </div>

  </div>

  <div class="dlist">

  where  
  <div class="ulist">

  - \\E\\ specifies the the event type of the candidate. *0* indicates
    that the candidate receipt was backed in the latest relay chain
    block, *1* indicates that it was included and became a parachain
    block at the latest relay chain block and *2* indicates that the
    candidate receipt was not made available and timed-out.

  - \\C_r\\ is the candidate receipt ([Definition
    104](#defn-candidate-receipt)).

  - \\h\\ is the parachain head data ([Definition
    133](#defn-head-data)).

  - \\I_c\\ is the index of the availability core as can be retrieved in
    [Section C.9.3](#sect-rt-api-availability-cores) that the candidate
    is occupying. If \\E\\ is of variant \\2\\, then this indicates the
    core index the candidate *was* occupying.

  - \\G_i\\ is the group index ([Definition
    136](#defn-validator-groups)) that is responsible of backing the
    candidate.

  </div>

  </div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-rt-api-session-info" class="anchor"></a><a href="#sect-rt-api-session-info" class="link">C.9.11.
<code>ParachainHost_session_info</code></a>

<div class="paragraph">

Get the session info of the given session, if available.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The unsigned 32-bit integer indicating the session index.

</div>

Return  
<div class="ulist">

- An *Option* type ([Definition 190](#defn-option-type)) which can
  contain the session info structure, \\S\\, of the following format:

  <div class="stemblock">

  <div class="content">

  \\S = (A,D,K,G,c,z,s,d,x,a)\\ \\A = (v_n,…v_m)\\ \\D =
  (v\_(\_n),…v_m)\\ \\K = (v_n,…v_m)\\ \\G = (g_n,…g_m)\\ \\g =
  (A_n,…A_m)\\

  </div>

  </div>

  <div class="dlist">

  where  
  <div class="ulist">

  - \\A\\ indicates the validators of the current session, in canonical
    order. There might be more validators in the current session than
    validators participating in parachain consensus, as returned by the
    Runtime API ([Section C.9.1](#sect-rt-api-validators)).

  - \\D\\ indicates the validator authority discovery keys for the given
    session in canonical order. The first couple of validators are equal
    to the corresponding validators participating in the parachain
    consensus, as returned by the Runtime API ([Section
    C.9.1](#sect-rt-api-validators)). The remaining authorities are not
    participating in the parachain consensus.

  - \\K\\ indicates the assignment keys for validators. There might be
    more authorities in the session that validators participating in
    parachain consensus, as returned by the Runtime API ([Section
    C.9.1](#sect-rt-api-validators)).

  - \\G\\ indicates the validator groups in shuffled order.

  - \\v_n\\ is public key of the authority.

  - \\A_n\\ is the authority set Id ([Definition
    33](#defn-authority-list)).

  - \\c\\ is an unsigned 32-bit integer indicating the number of
    availability cores used by the protocol during the given session.

  - \\z\\ is an unsigned 32-bit integer indicating the zeroth delay
    tranche width.

  - \\s\\ is an unsigned 32-bit integer indicating the number of samples
    an assigned validator should do for approval voting.

  - \\d\\ is an unsigned 32-bit integer indicating the number of delay
    tranches in total.

  - \\x\\ is an unsigned 32-bit integer indicating how many BABE slots
    must pass before an assignment is considered a “no-show”.

  - \\a\\ is an unsigned 32-bit integer indicating the number of
    validators needed to approve a block.

  </div>

  </div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-parachainhost_dmq_contents" class="anchor"></a><a href="#id-parachainhost_dmq_contents" class="link">C.9.12.
<code>ParachainHost_dmq_contents</code></a>

<div class="paragraph">

Returns all the pending inbound messages in the downward message queue
for a given parachain.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The parachain Id ([Definition 134](#defn-para-id)).

</div>

Return  
<div class="ulist">

- An array of inbound downward messages ([Definition
  138](#defn-downward-message)).

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-parachainhost_inbound_hrmp_channels_contents"
class="anchor"></a><a href="#id-parachainhost_inbound_hrmp_channels_contents"
class="link">C.9.13.
<code>ParachainHost_inbound_hrmp_channels_contents</code></a>

<div class="paragraph">

Returns the contents of all channels addressed to the given recipient.
Channels that have no messages in them are also included.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The parachain Id ([Definition 134](#defn-para-id)).

</div>

Return  
<div class="ulist">

- An array of inbound HRMP messages ([Definition
  140](#defn-inbound-hrmp-message)).

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#id-module-grandpaapi" class="anchor"></a><a href="#id-module-grandpaapi" class="link">C.10. Module GrandpaApi</a>

<div class="admonitionblock important">

|     |                                                                                                                                                 |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This section describes **Version 2** of this API. Please check `Core_version` ([Section C.4.1](#defn-rt-core-version)) to ensure compatibility. |

</div>

<div class="paragraph">

All calls in this module require `Core_initialize_block` ([Section
C.4.3](#sect-rte-core-initialize-block)) to be called beforehand.

</div>

<div class="sect3">

#### <a href="#sect-rte-grandpa-auth" class="anchor"></a><a href="#sect-rte-grandpa-auth" class="link">C.10.1.
<code>GrandpaApi_grandpa_authorities</code></a>

<div class="paragraph">

This entry fetches the list of GRANDPA authorities according to the
genesis block and is used to initialize an authority list at genesis,
defined in [Definition 33](#defn-authority-list). Any future authority
changes get tracked via Runtime-to-consensus engine messages, as
described in [Section 3.3.2](#sect-consensus-message-digest).

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None.

</div>

Return  
<div class="ulist">

- An authority list as defined in [Definition 33](#defn-authority-list).

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-grandpaapi_submit_report_equivocation_unsigned_extrinsic"
class="anchor"></a><a href="#sect-grandpaapi_submit_report_equivocation_unsigned_extrinsic"
class="link">C.10.2.
<code>GrandpaApi_submit_report_equivocation_unsigned_extrinsic</code></a>

<div class="paragraph">

A GRANDPA equivocation occurs when a validator votes for multiple blocks
during one voting subround, as described further in [Definition
80](#defn-equivocation). The Polkadot Host is expected to identify
equivocators and report those to the Runtime by calling this function.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The equivocation proof of the following format:

  <div class="stemblock">

  <div class="content">

  \\\begin{aligned} G\_{\mathrm{Ep}} =& (\mathrm{id}\_{\mathbb{V}}, e,
  r, A\_{\mathrm{id}}, B^1_h, B^1_n A^1\_{\mathrm{sig}}, B^2_h, B^2_n,
  A^2\_{\mathrm{sig}}) \\ e =& \begin{cases} 0 &\quad
  \textrm{Equivocation at prevote stage} \\ 1 &\quad
  \textrm{Equivocation at precommit stage} \end{cases} \end{aligned}\\

  </div>

  </div>

  <div class="dlist">

  where  
  <div class="ulist">

  - \\\mathrm{id}\_{\mathbb{V}}\\ is the authority set id as defined in
    [Definition 73](#defn-authority-set-id).

  - \\e\\ indicates the stage at which the equivocation occurred.

  - \\r\\ is the round number the equivocation occurred.

  - \\A\_{\mathrm{id}}\\ is the public key of the equivocator.

  - \\B^1_h\\ is the block hash of the first block the equivocator voted
    for.

  - \\B^1_n\\ is the block number of the first block the equivocator
    voted for.

  - \\A^1\_{\mathrm{sig}}\\ is the equivocators signature of the first
    vote.

  - \\B^2_h\\ is the block hash of the second block the equivocator
    voted for.

  - \\B^2_n\\ is the block number of the second block the equivocator
    voted for.

  - \\A^2\_{\mathrm{sig}}\\ is the equivocators signature of the second
    vote.

  - A proof of the key owner in an opaque form as described in [Section
    C.10.3](#sect-grandpaapi_generate_key_ownership_proof).

  </div>

  </div>

</div>

Return  
<div class="ulist">

- A SCALE encoded *Option* as defined in [Definition
  190](#defn-option-type) containing an empty value on success.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-grandpaapi_generate_key_ownership_proof"
class="anchor"></a><a href="#sect-grandpaapi_generate_key_ownership_proof"
class="link">C.10.3.
<code>GrandpaApi_generate_key_ownership_proof</code></a>

<div class="paragraph">

Generates proof of the membership of a key owner in the specified block
state. The returned value is used to report equivocations as described
in [Section
C.10.2](#sect-grandpaapi_submit_report_equivocation_unsigned_extrinsic).

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The authority set id as defined in [Definition
  73](#defn-authority-set-id).

- The 256-bit public key of the authority.

</div>

Return  
<div class="ulist">

- A SCALE encoded *Option* as defined in [Definition
  190](#defn-option-type) containing the proof in an opaque form.

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#id-module-babeapi" class="anchor"></a><a href="#id-module-babeapi" class="link">C.11. Module BabeApi</a>

<div class="admonitionblock important">

|     |                                                                                                                                                 |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This section describes **Version 2** of this API. Please check `Core_version` ([Section C.4.1](#defn-rt-core-version)) to ensure compatibility. |

</div>

<div class="paragraph">

All calls in this module require `Core_initialized_block` ([Section
C.4.3](#sect-rte-core-initialize-block)) to be called beforehand.

</div>

<div class="sect3">

#### <a href="#sect-rte-babeapi-epoch" class="anchor"></a><a href="#sect-rte-babeapi-epoch" class="link">C.11.1.
<code>BabeApi_configuration</code></a>

<div class="paragraph">

This entry is called to obtain the current configuration of the BABE
consensus protocol.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None.

</div>

Return  
<div class="ulist">

- A tuple containing configuration data used by the Babe consensus
  engine.

  | **Name**             | **Description**                                                                                                                                                                                   | **Type**                                                                                      |
  |----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
  | *SlotDuration*       | The slot duration in milliseconds. Currently, only the value provided by this type at genesis will be used. Dynamic slot duration may be supported in the future.                                 | Unsigned 64bit integer                                                                        |
  | *EpochLength*        | The duration of epochs in slots.                                                                                                                                                                  | Unsigned 64bit integer                                                                        |
  | *Constant*           | A constant value that is used in the threshold calculation formula as defined in [Definition 59](#defn-babe-constant).                                                                            | Tuple containing two unsigned 64bit integers                                                  |
  | *GenesisAuthorities* | The authority list for the genesis epoch as defined in [Definition 33](#defn-authority-list).                                                                                                     | Array of tuples containing a 256-bit byte array and a unsigned 64bit integer                  |
  | *Randomness*         | The randomness for the genesis epoch                                                                                                                                                              | 32-byte array                                                                                 |
  | *SecondarySlot*      | Whether this chain should run with round-robin-style secondary slot and if this secondary slot requires the inclusion of an auxiliary VRF output ([Section 5.2](#sect-block-production-lottery)). | A one-byte enum as defined in [Definition 58](#defn-consensus-message-babe) as \\2\_("nd")\\. |

  Table 16. The tuple provided by **BabeApi_configuration**.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-babeapi_current_epoch_start" class="anchor"></a><a href="#id-babeapi_current_epoch_start" class="link">C.11.2.
<code>BabeApi_current_epoch_start</code></a>

<div class="paragraph">

Finds the start slot of the current epoch.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None.

</div>

Return  
<div class="ulist">

- A unsigned 64-bit integer indicating the slot number.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-babeapi_current_epoch" class="anchor"></a><a href="#sect-babeapi_current_epoch" class="link">C.11.3.
<code>BabeApi_current_epoch</code></a>

<div class="paragraph">

Produces information about the current epoch.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None.

</div>

Return  
<div class="ulist">

- A data structure of the following format:

  <div class="stemblock">

  <div class="content">

  \\(e_i, s_s, d, A, r)\\

  </div>

  </div>

  <div class="dlist">

  where  
  <div class="ulist">

  - \\e_i\\ is a unsigned 64-bit integer representing the epoch index.

  - \\s_s\\ is a unsigned 64-bit integer representing the starting slot
    of the epoch.

  - \\d\\ is a unsigned 64-bit integer representing the duration of the
    epoch.

  - \\A\\ is an authority list as defined in [Definition
    33](#defn-authority-list).

  - \\r\\ is an 256-bit array containing the randomness for the epoch as
    defined in [Definition 71](#defn-epoch-randomness).

  </div>

  </div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-babeapi_next_epoch" class="anchor"></a><a href="#id-babeapi_next_epoch" class="link">C.11.4.
<code>BabeApi_next_epoch</code></a>

<div class="paragraph">

Produces information about the next epoch.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None.

</div>

Return  
<div class="ulist">

- Returns the same datastructure as described in [Section
  C.11.3](#sect-babeapi_current_epoch).

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-babeapi_generate_key_ownership_proof" class="anchor"></a><a href="#sect-babeapi_generate_key_ownership_proof"
class="link">C.11.5.
<code>BabeApi_generate_key_ownership_proof</code></a>

<div class="paragraph">

Generates a proof of the membership of a key owner in the specified
block state. The returned value is used to report equivocations as
described in [Section
C.11.6](#sect-babeapi_submit_report_equivocation_unsigned_extrinsic).

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The unsigned 64-bit integer indicating the slot number.

- The 256-bit public key of the authority.

</div>

Return  
<div class="ulist">

- A SCALE encoded *Option* as defined in Definition [Definition
  190](#defn-option-type) containing the proof in an opaque form.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-babeapi_submit_report_equivocation_unsigned_extrinsic"
class="anchor"></a><a href="#sect-babeapi_submit_report_equivocation_unsigned_extrinsic"
class="link">C.11.6.
<code>BabeApi_submit_report_equivocation_unsigned_extrinsic</code></a>

<div class="paragraph">

A BABE equivocation occurs when a validator produces more than one block
at the same slot. The proof of equivocation are the given distinct
headers that were signed by the validator and which include the slot
number. The Polkadot Host is expected to identify equivocators and
report those to the Runtime using this function.

</div>

<div class="admonitionblock note">

|     |                                                                                                                                                                                     |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     | If there are more than two blocks which cause an equivocation, the equivocation only needs to be reported once i.e. no additional equivocations must be reported for the same slot. |

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The equivocation proof of the following format:

  <div class="stemblock">

  <div class="content">

  \\B\_{\mathrm{Ep}} = (A\_{\mathrm{id}}, s, h_1, h_2)\\

  </div>

  </div>

  <div class="dlist">

  where  
  <div class="ulist">

  - \\A\_{\mathrm{id}}\\ is the public key of the equivocator.

  - \\s\\ is the slot as described in [Definition 54](#defn-epoch-slot)
    at which the equivocation occurred.

  - \\h_1\\ is the block header of the first block produced by the
    equivocator.

  - \\h_2\\ is the block header of the second block produced by the
    equivocator.

    <div class="paragraph">

    Unlike during block execution, the Seal in both block headers is not
    removed before submission. The block headers are submitted in its
    full form.

    </div>

  </div>

  </div>

- An proof of the key owner in an opaque form as described in [Section
  C.11.5](#sect-babeapi_generate_key_ownership_proof).

</div>

Return  
<div class="ulist">

- A SCALE encoded *Option* as defined in [Definition
  190](#defn-option-type) containing an empty value on success.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-module-authoritydiscoveryapi" class="anchor"></a><a href="#id-module-authoritydiscoveryapi" class="link">C.11.7. Module
AuthorityDiscoveryApi</a>

<div class="admonitionblock important">

|     |                                                                                                                                                 |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This section describes **Version 1** of this API. Please check `Core_version` ([Section C.4.1](#defn-rt-core-version)) to ensure compatibility. |

</div>

<div class="paragraph">

All calls in this module require (Section [Section
C.4.3](#sect-rte-core-initialize-block)) to be called beforehand.

</div>

<div class="sect4">

##### <a href="#id-authoritydiscoveryapi_authorities" class="anchor"></a><a href="#id-authoritydiscoveryapi_authorities" class="link">C.11.7.1.
<code>AuthorityDiscoveryApi_authorities</code></a>

<div class="paragraph">

A function which helps to discover authorities.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- None.

</div>

Return  
<div class="ulist">

- A byte array of varying size containing 256-bit pulic keys of the
  authorities.

</div>

</div>

</div>

</div>

<div class="sect3">

#### <a href="#sect-runtime-sessionkeys-module" class="anchor"></a><a href="#sect-runtime-sessionkeys-module" class="link">C.11.8. Module
SessionKeys</a>

<div class="admonitionblock important">

|     |                                                                                                                                                 |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This section describes **Version 1** of this API. Please check `Core_version` ([Section C.4.1](#defn-rt-core-version)) to ensure compatibility. |

</div>

<div class="paragraph">

All calls in this module require `Core_initialize_block` ([Section
C.4.3](#sect-rte-core-initialize-block)) to be called beforehand.

</div>

<div class="sect4">

##### <a href="#id-sessionkeys_generate_session_keys" class="anchor"></a><a href="#id-sessionkeys_generate_session_keys" class="link">C.11.8.1.
<code>SessionKeys_generate_session_keys</code></a>

<div class="paragraph">

Generates a set of session keys with an optional seed. The keys should
be stored within the keystore exposed by the Host Api. The seed needs to
be valid and UTF-8 encoded.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- A SCALE-encoded *Option* as defined in [Definition
  190](#defn-option-type) containing an array of varying sizes
  indicating the seed.

</div>

Return  
<div class="ulist">

- A byte array of varying size containing the encoded session keys.

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-sessionkeys_decode_session_keys" class="anchor"></a><a href="#id-sessionkeys_decode_session_keys" class="link">C.11.8.2.
<code>SessionKeys_decode_session_keys</code></a>

<div class="paragraph">

Decodes the given public session keys. Returns a list of raw public keys
including their key type.

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- An array of varying size containing the encoded public session keys.

</div>

Return  
<div class="ulist">

- An array of varying size containing tuple pairs of the following
  format:

  <div class="stemblock">

  <div class="content">

  \\(k, k\_{\mathrm{id}})\\

  </div>

  </div>

  <div class="paragraph">

  where \\k\\ is an array of varying sizes containing the raw public key
  and \\k\_{\mathrm{id}}\\ is a 4-byte array indicating the key type.

  </div>

</div>

</div>

</div>

</div>

</div>

<div class="sect2">

### <a href="#id-module-accountnonceapi" class="anchor"></a><a href="#id-module-accountnonceapi" class="link">C.12. Module
AccountNonceApi</a>

<div class="admonitionblock important">

|     |                                                                                                                                                 |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This section describes **Version 1** of this API. Please check `Core_version` ([Section C.4.1](#defn-rt-core-version)) to ensure compatibility. |

</div>

<div class="paragraph">

All calls in this module require `Core_initialize_block` ([Section
C.4.3](#sect-rte-core-initialize-block)) to be called beforehand.

</div>

<div class="sect3">

#### <a href="#sect-accountnonceapi-account-nonce" class="anchor"></a><a href="#sect-accountnonceapi-account-nonce" class="link">C.12.1.
<code>AccountNonceApi_account_nonce</code></a>

<div class="paragraph">

Get the current nonce of an account. This function can be used by the
Polkadot Host implementation when it seems appropriate, such as for the
JSON-RPC API as described in [Section C.1.1](#sect-json-rpc-api).

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- The 256-bit public key of the account.

</div>

Return  
<div class="ulist">

- A 32-bit unsigned integer indicating the nonce of the account.

</div>

</div>

</div>

<div class="sect3">

#### <a href="#id-module-transactionpaymentapi" class="anchor"></a><a href="#id-module-transactionpaymentapi" class="link">C.12.2. Module
TransactionPaymentApi</a>

<div class="admonitionblock important">

|     |                                                                                                                                                 |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------|
|     | This section describes **Version 1** of this API. Please check `Core_version` ([Section C.4.1](#defn-rt-core-version)) to ensure compatibility. |

</div>

<div class="paragraph">

All calls in this module require `Core_initialize_block` ([Section
C.4.3](#sect-rte-core-initialize-block)) to be called beforehand.

</div>

<div class="sect4">

##### <a href="#id-transactionpaymentapi_query_info" class="anchor"></a><a href="#id-transactionpaymentapi_query_info" class="link">C.12.2.1.
<code>TransactionPaymentApi_query_info</code></a>

<div class="paragraph">

Returns information of a given extrinsic. This function is not aware of
the internals of an extrinsic, but only interprets the extrinsic as some
encoded value and accounts for its weight and length, the Runtime’s
extrinsic base weight and the current fee multiplier.

</div>

<div class="paragraph">

This function can be used by the Polkadot Host implementation when it
seems appropriate, such as for the JSON-RPC API as described in [Section
C.1.1](#sect-json-rpc-api).

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- A byte array of varying sizes containing the extrinsic.

- The length of the extrinsic. \[To do: why is this needed?\]

</div>

Return  
<div class="ulist">

- A data structure of the following format:

  <div class="stemblock">

  <div class="content">

  \\(w, c, f)\\

  </div>

  </div>

  <div class="dlist">

  where  
  <div class="ulist">

  - \\w\\ is the weight of the extrinsic.

  - \\c\\ is the "class" of the extrinsic, where class is a varying data
    ([Definition 188](#defn-varrying-data-type)) type defined as:

    <div class="stemblock">

    <div class="content">

    \\c = \left\\\begin{array}{l} 0 \quad \textrm{Normal extrinsic}\\ 1
    \quad \textrm{Operational extrinsic}\\ 2 \quad \textrm{Mandatory
    extrinsic, which is always included} \end{array}\right.\\

    </div>

    </div>

  - \\f\\ is the inclusion fee of the extrinsic. This does not include a
    tip or anything else that depends on the signature.

  </div>

  </div>

</div>

</div>

</div>

<div class="sect4">

##### <a href="#id-transactionpaymentapi_query_fee_details"
class="anchor"></a><a href="#id-transactionpaymentapi_query_fee_details"
class="link">C.12.2.2.
<code>TransactionPaymentApi_query_fee_details</code></a>

<div class="paragraph">

Query the detailed fee of a given extrinsic. This function can be used
by the Polkadot Host implementation when it seems appropriate, such as
for the JSON-RPC API as described in [Section
C.1.1](#sect-json-rpc-api).

</div>

<div class="dlist">

Arguments  
<div class="ulist">

- A byte array of varying sizes containing the extrinsic.

- The length of the extrinsic.

</div>

Return  
<div class="ulist">

- A data structure of the following format:

  <div class="stemblock">

  <div class="content">

  \\(f, t)\\

  </div>

  </div>

  <div class="dlist">

  where  
  <div class="ulist">

  - \\f\\ is a SCALE encoded as defined in [Definition
    190](#defn-option-type) containing the following data structure:

    <div class="stemblock">

    <div class="content">

    \\ f = (f_b, f_l, f_a)\\

    </div>

    </div>

    <div class="dlist">

    where  
    <div class="ulist">

    - \\f_b\\ is the minimum required fee for an extrinsic.

    - \\f_l\\ is the length fee, the amount paid for the encoded length
      (in bytes) of the extrinsic.

    - \\f_a\\ is the “adjusted weight fee”, which is a multiplication of
      the fee multiplier and the weight fee. The fee multiplier varies
      depending on the usage of the network.

    </div>

    </div>

  - \\t\\ is the tip for the block author.

  </div>

  </div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

## <a href="#id-bibliography" class="anchor"></a><a href="#id-bibliography" class="link">Bibliography</a>

<div class="sectionbody">

<div class="paragraph">

bibliography::\[\]

</div>

</div>

</div>

<div class="sect1">

## <a href="#id-glossary" class="anchor"></a><a href="#id-glossary" class="link">Glossary</a>

<div class="sectionbody">

<div class="dlist glossary">

\\P_n\\  
A path graph or a path of \\n\\ nodes.

\\(b_0,b_1,...,b\_{n-1})\\  
A sequence of bytes or byte array of length \\n\\

\\𝔹_n\\  
A set of all byte arrays of length \\n\\

\\I=\left(B_n…B_0\right)\_{256}\\  
A non-negative interger in base 256

\\B=(b_0,b_1,…,b_n)\\  
The little-endian representation of a non-negative interger
\\I=(B_n…B_0)\_{256}\\ such that \\b_i≔B_i\\

\\\textrm{Enc}\_{LE}\\  
The little-endian encoding function.

\\C\\  
A blockchain defined as a directed path graph.

Block  
A node of the directed path graph (blockchain) C

Genesis Block  
The unique sink of blockchain C

Head  
The source of blockchain C

\\P(B)\\  
The parent of block \\B\\

UNIX time  
The number of milliseconds that have elapsed since the Unix epoch as a
64-bit integer

\\BT\\  
The block tree of a blockchain

\\G\\  
The genesis block, the root of the block tree BT

\\\textrm{CHAIN}(B)\\  
The path graph from \\G\\ to \\B\\ in \\BT\\.

\\Head(C)\\  
The head of chain C.

\\\|C\|\\  
The length of chain \\C\\ as a path graph

\\\textrm{SubChain}(B',B)\\  
The subgraph of \\Chain(B)\\ path graph containing both \\B\\ and
\\B'\\.

\\ℂ_B(BT)\\  
The set of all subchains of \\BT\\ rooted at block \\B\\.

\\ℂ, ℂ(BT)\\  
\\ℂ_G(BT)\\ i.e. the set of all chains of \\BT\\ rooted at genesis block

\\\textrm{Longest-Chain}(BT)\\  
The longest sub path graph of \\BT\\ i.e. \\C : \|C\| = \max\_{C_i ∈ ℂ}
\|C_i\|\\

\\\textrm{Longest-Path}(BT)\\  
The longest sub path graph of \\(P)BT\\ with earliest block arrival time

\\\textrm{Deepest-Leaf}(BT)\\  
\\\textrm{Head}(\textrm{Longest-Path}(BT))\\ i.e. the head of
\\\textrm{Longest-Path}(BT)\\

\\B \> B'\\  
\\B\\ is a descendant of \\B'\\ in the block tree

\\\textrm{StoredValue}(k)\\  
The function to retrieve the value stored under a specific key in the
state storage.

State trie, trie  
The Merkle radix-16 Tree which stores hashes of storage enteries.

\\\textrm{KeyEncode}(k)\\  
The function to encode keys for labeling branaches of the trie.

\\𝒩\\  
The set of all nodes in the Polkadot state trie.

\\N\\  
An individual node in the trie.

\\𝒩_b\\  
A branch node of the trie which has at least one and at most 16 children

\\𝒩_l\\  
A childless leaf node of the trie

\\pk_N^{Agr}\\  
The aggregated prefix key of node N

\\pk_N\\  
The (suffix) partial key of node N

\\\textrm{Index}\_N\\  
A function returning an integer in range of {0, . . . ,15} represeting
the index of a child node of node \\N\\ among the children of \\N\\

\\v_N\\  
Node value containing the header of node \\N\\, its partial key and the
digest of its childern values

\\\textrm{Head}\_N\\  
The node header of trie node \\N\\ storing information about the node’s
type and kay

\\H(N)\\  
The Merkle value of node \\N\\.

\\\textrm{ChildrenBitmap}\\  
The binary function indicating which child of a given node is present in
the trie.

\\sv_N\\  
The subvalue of a trie node \\N\\.

Child storage  
A sub storage of the state storage which has the same structure although
being stored separately

Child trie  
State trie of a child storage

Transaction Queue  
See [Definition 14](#defn-transaction-queue).

\\H_p\\  
The 32-byte Blake2b hash of the header of the parent of the block.

\\H_i,H_i(B)\\  
Block number, the incremental interger index of the current block in the
chain.

\\H_r\\  
The hash of the root of the Merkle trie of the state storage at a given
block

\\H_e\\  
An auxileray field in block header used by Runtime to validate the
integrity of the extrinsics composing the block body.

\\H_d\\, \\H_d(B)\\  
A block header used to store any chain-specific auxiliary data.

\\H_h(B)\\  
The hash of the header of block \\B\\

\\\textrm{Body}(B)\\  
The body of block \\B\\ consisting of a set of extrinsics

\\M^{r,stage}\_v\\  
Vote message broadcasted by the voter v as part of the finality protocol

\\M_v^{r,Fin}(B)\\  
The commit message broadcasted by voter \\v\\ indicating that they have
finalized bock \\B\\ in round \\r\\

\\v\\  
GRANDPA voter node which casts vote in the finality protocol

\\k_v^{pr}\\  
The private key of voter \\v\\

\\v\_{id}\\  
The public key of voter \\v\\

\\𝕍_B,𝕍\\  
The set of all GRANDPA voters for at block \\B\\

\\GS\\  
GRANDPA protocol state consisting of the set of voters, number of times
voters set has changed and the current round number.

\\r\\  
The voting round counter in the finality protocol

\\V\_(B)\\  
A GRANDPA vote casted in favor of block B

\\V_v^(r,pv)\\  
A GRANDPA vote casted by voter \\v\\ during the pre-vote stage of round
\\r\\

\\V_v^(r,pc)\\  
A GRANDPA vote casted by voter \\v\\ during the pre-commit stage of
round \\r\\

\\J^{r,stage}(B)\\  
The justification for pre-committing or committing to block \\B\\ in
round \\r\\ of finality protocol

\\Sign^{r,stage}\_{v_i}(B)\\  
The signature of voter \\v\\ on their voteto block B, broadcasted during
the specified stage of finality round \\r\\

\\ℰ^{r,stage}\\  
The set of all equivocator voters in sub-round ‘‘stage'' of round \\r\\

\\ℰ^{r,stage}\_{obs(v)}\\  
The set of all equivocator voters in sub-round ‘‘stage'' of round \\r\\
observed by voter \\v\\

\\VD^{r,stage}\_{obs(v)}(B)\\  
The set of observed direct votes for block B in round \\r\\

\\V^{r,stage}\_{obs(v)}\\  
The set of total votes observed by voter v in sub-round ‘‘stage'' of
round r

\\V^{r,stage}\_{obs(v)}(B)\\  
The set of all observed votes by \\v\\ in the sub-round “stage” of round
\\r\\ (directly or indirectly) for block \\B\\

\\B^{r,pv}\_v\\  
The currently pre-voted block in round \\r\\. The GRANDPA GHOST of round
\\r\\

Account key, \\(sk^a,pk^a)\\  
A key pair of types accepted by the Polkadot protocol which can be used
to sign transactions

\\Enc\_{SC}(A)\\  
SCALE encoding of value \\A\\

\\T≔(A_1,...,A_n)\\  
A tuple of values \\A_i\\'s each of different type

Varying Data Types \\𝒯={T_1,…,T_n}\\  
A data type representing any of varying types \\T_1,…,T_n\\.

\\S≔A_1,…,A_n\\  
Sequence of values \\A_i\\ of the same type

\\Enc^{Len}\_{SC}(n)\\  
SCALE length encoding aka. compact encoding of non-negative interger
\\n\\ of arbitrary size.

\\Enc\_{HE}(PK)\\  
Hex encoding

</div>

</div>

</div>

</div>

<div id="footer">

<div id="footer-text">

Version 0.2.1  
Last updated 2023-03-06 12:17:00 +0100

</div>

</div>
