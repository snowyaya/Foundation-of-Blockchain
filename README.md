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


### L2 - Byzantine Broadcase in the Synchronous Model via the Dolev-Strong Protocol

**=> Synchronous model. Dolev-Strong protocol (for BB, SMR), tolerates any # of dishonest nodes.**

#### Recap of the SMR problem
- clients submit transactions to one or more nodes.
```
|__ clients: users of blockchain
|__ nodes: machines running the blockchain protocol
```
- Each node maintains local history (append-only data structure)

#### Goal
- a protocol (a event-dirven code) taht satisfies:
```
|__ consistency: all nodes agree on the same history
|__ liveness: every submitted transactions eventually added to all nodes histories
```

#### Plan
- solve first under a bunch of assumptions, relax assumptions one-by-one

#### Assumptions (to be relaxed)
- permissioned
```
|__ permissioned: a priori known set of nodes {1, 2, 3, ...} (known IP addresses)
|__ permission setting: you need permission to be one of the nodes participating in the protocol
|__ permissionless: anyone can join and contribute to that protocol, such as bitcoin and ethereum
```
- PKI (public key infrastructure)
```
|__ each node i has a pki/ski pair, pki known to all nodes upfront
```
- Sychronous
```
|__ all nodes share a global clock, time steps 0, 1, 2, 3, ...
|__ all message sent at time t arrive by time t+1 (in some arbitrary order)
```
- All honest nodes
```
|__ all nodes run inherited protocol, no (intended or unintended) deviations
```

#### Solution via Round-Robin Leaders
- Idea: nodes take turns as "leaders"
```
|__ leader sends ordered list of transactions it knows about to all others nodes (plays the role of a "block")
|__ when node receives most recent leader's ordered list, amends it to local history

```

- Note: satisfies consistency + liveness

#### Faulty/Byzantine Nodes
- Definition: a node that is not honest is called faulty
- Types of faulty nodes
```
|__ crash fault (run honestly until some failure time, then stop entirely - no more messages sent)
|__ omission fault (may selectively withhold messages it's supposed to send)
|__ Byzathine fault (can behave arbitrarily, though still can't break cryptography) 

```

- Canchicalpoly: send conflicting messages to different nodes
- New assumption 4: for known parameter f , <= f nodes are Byzatine,  other >= n-f nodes are honest

####  The Byzatine Broadcast Problem
- Idea: stick with the rotating leaders approach
- Subroutine: Byzatine broadcase (BB)
```
|__ one node is the sender (known to all up front)
|__ Sender has a private input  v_* E V
```
- Goals
```
|__ termination: reach honest nodes eventually halts with some value, v_i E V
|__ agreement: all honest nodes choose the same value v_i
|__ vallidity: if sender is honest, all honest v_i's equal v_*
```

#### SMR Reduces to BB
- SMR Protocol: given a Byzantine broadcast subroutine
```
|__ take turns as leader (e.g., round-robin)
|__ run BB protocol (with sender = current leader), agree on a transaction list L
|__ each node appends L to its local history
```

- Why is the reduction correct?
```
|__ BB agreement => SMR consitency (every time step, all honest nodes add the same transaction list)
|__ BB validity => SMR liveness (if honest node knows about a transaction, eventually all become the leader/sender, validity => all honest nodes add that transaction)
```

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
