# Foundations of Blockchain
- Those notes were taken while learning basic concepts of blockchain.
- The lecture is from [Tim Roughgarden](https://www.youtube.com/playlist?list=PLEGCF-WLh2RLOHv_xUGLqRts_9JxrckiA)

### L1

#### I. Overview
[L1 Notes from Tim Roughgarden](https://timroughgarden.github.io/fob21/l/l1.pdf)
[L1 Slides](https://timroughgarden.github.io/fob21/slides/F21L1.pdf)

#### Blockchain Stack
- Layer 0: the internet
- Layer 1: consensus layer + a computer layer (60% of this tutorial)
- Layer 2: scaling layer (20% of t his tutorial)
- Application layer (20% of this tutorial)

#### Consensus Protocols
- Blockchain is a new global computing paradigm, not owned by anyone
- Not about digital money
- Principles over protocols

#### II & III. Digital Signature Schemes

#### Consensus
- Keep multiple machines ("nodes") in sync, even in the face of an unreliable network, malicious attacks.

#### Permanent Assumptions
- The Internet exists
- Cryptography exists

#### Definition of a DSS (defined by 3 algorithms)
- Key generation algorithm (maps random seed => (pk, sk) pair)
- Signing algorithm (maps msg+sk => msg+sig)
- Verification algorithm (maps msg+sig+pk => "yes/no")

#### Assumptions ("ideal signature")
- Don't know sk => impossible to generate valid msg+sig

#### IV. The SMR Problem
- SMR stands for State Machine Replication
- Clients submit transactions to nodes
- Each node maintains a local appendable-only data structure (in an ordered sequence) 
- Keep all nodes in sync; identical local histories

#### Definition
- a protocal = code to be run by each node (local computations, receive messages from other nodes + clients, send messages to other nodes)

#### Goal
- Consistency: all nodes agree on history (i.e., same transactions sequence)
- Liveness: every valid transactions submitted eventually added to history 


### L2 Byzantine Broadcase in the Synchronous Model via the Dolev-Strong Protocol

**=> Synchronous model. Dolev-Strong protocol (for BB, SMR), tolerates any # of dishonest nodes.**

#### Recap of the SMR problem
- clients submit transactions to one or more nodes.
```
-- clients: users of blockchain
-- nodes: machines running the blockchain protocol
```
- Each node maintains local history (append-only data structure)





### L3
**=> Synchronous model. Without PKI (public key infrastructure), nodes 67% honest. (Hexagon proof)**

### L4
**=> Asynchronous model. Definition. FLP impossiblity result.**

#### 

### L5
**=> Asynchronous model. Finish proof of FLP impossiblity.**

### L6
**=> The portially Synchronous model. Need 67% honest.**

### L7 
**=> The Tendermint protocal + its aprovable gurantees**

#### Two main types of protocol
1. Tendermint is built on top of BFT (Byzentine fault tolerance) protocol, invented in 1980s. Others, such as Cosmos, Terra, Algorand, Facebook DM, are also using that consensus.
2. Bitcoin and Ethetreum -> longest-chain protocols
3. Some protocol favors "safety" => refers to BYT; Some protocol favors "liveness" => refers to longest chain
