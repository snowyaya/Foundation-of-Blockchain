# Foundations of Blockchain
-- Those notes were taken while learning basic concepts of blockchain.
-- The lecture is from [Tim Roughgarden](https://www.youtube.com/playlist?list=PLEGCF-WLh2RLOHv_xUGLqRts_9JxrckiA)

### L1

#### I. Overview
[L1 Notes from Tim Roughgarden](https://timroughgarden.github.io/fob21/l/l1.pdf)

#### Blockchain Stack
- Layer 0: the internet
- Layer 1: consensus layer + a computer layer (60% of this tutorial)
- Layer 2: scaling layer (20% of t his tutorial)
- Application layer (20% of this tutorial)

#### Consensus Protocols
- Blockchain is a new global computing paradigm, not owned by anyone
- Not about digital money
- Principles over protocols

#### II. Digital Signature Schemes

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
