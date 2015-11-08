# Distributed Permanent Identifier Registry

by Juan Benet, Christopher Allen, Noah Thorp, Harlan T Wood, Markus Sabadello, Drummond Reed, Duke Dorje

## Introduction

Today we trust people's root keys.  What if the root key is compromised? What if there is an algorithmic break and all keys become easily crackable overnight? We should be able to keep some global identifier which we bind to root keys (or some other useful value).

Instead of using a public key as an identifier, we use a Token (for example, a UUID, or a strongly random string).  The Token can be mapped to various attributes, endpoints, etc.  A range of recovery mechanisms are required for various scenarios in which the Token needs to be recovered (eg from an attacker). To update the value (e.g. public key) a new value can be registered through multiple widely trusted parties: eg EFF, state institution, my neighbor.

Each node in the network has its own copy of the dictionary, with whatever identifiers it cares about, or syncs from parties it trusts.

Some nodes may have greater trust (such as the EFF, Swiss government, Google, a best friend, etc). Increasing the cost of updating the registry increases the cost of attacking the mappings in the network.
 
Nodes in the network update their Registry. Each node assembles its own view of mappings in the network. A node recognizes Mappings in the Distributed Registry for Mappings that are below the Threshold of Conflict. Over time the widely trusted nodes in the network may change. 

## Terms

- Token (T): a permanent identifier (eg UUID) which can be rebound to a Value (V) over time.
- Value (V): a value -- such as a public key (or a hash of one), bounded in size.
- Size of Value: an upper bound on the size of a Value, upgradeable network parameter.
- Mapping (M): a record establishing a mapping T->V.
- Node: a process maintaining a set of mappings called a Distributed Registry
- Update Protocols: use-case specific protocols to update a mapping
- Distributed Registry - a list of mappings gathered from multiple nodes that are determined to be below the protocols Threshold of Conflict. 
- Registry - a table of Mappings stored on a Node and updated based on its trust in other nodes
- Threshold of Conflict - a protocol that defines network consensus of which mappings should be included in a node's Distributed Registry.

## Registration of Mappings

Can an attacker discover a Token registration and then propagate a Token faster than a good actor?

1. A registrant makes an initial claim of a Token and Value Mapping to a node. A node may have requirements for registration including format of the Token (e.g. length). A registrant may choose a Token name that is likely to be probabilistically unique when registered (e.g. a UUID).
1. The node broadcasts the provisional claim Mapping to the network
1. If the the Mapping has not been broadcast by other nodes which it trusts then the node marks the mapping as claimed.

## Constraints

- peer-to-peer network with no gated entry (anyone can participate)
- maintain a network global set of mappings T -> V
- Tokens (T) MUST be uuids (probability bound on accidental collision)
- mapping MUST be mutable
- nodes learn about mapping mutations through peer-to-peer comm (a sync)
- mapping updates MUST be able to happen over different protocols[0]
- a fraction of honest nodes exists who (would) verify mappings through expensive protocols
- but there is a higher-level federated consensus around names -- to be useful, a mapping MUST be widely accepted

**Why mapping MUST be able to happen over different protocols**

A range of “Sync Protocols” can which have different security and liveness properties, i.e. protocols range in cost, so can have syncs which are lively and cheap (e.g. a blockchain) which may lower security guarantees than others which are much more expensive (government id physical visit with biometric checks).

## Individual Verification

Nodes are individually responsible for verifying that a certain Token Update is valid, and this is (purposely) left up individual nodes to define. For example, one class of nodes could be government agencies with a (physically expensive) custom protocol for updating a mapping. 

It MUST be possible for every node in the network to connect to every single other node and individually verify a mapping update -- through whatever means the verifier finds acceptable. For example, a Government Authority might associate a Token with a specific citizen and ONLY allow updates by that citizen through a special-purpose protocol (updates could require physical visit, etc).

## Global Federated Consensus

In a sense, what we require is a registry driven by a global federated consensus...

## Proof Requirements

- want to prove disagreement propagates quickly (lower bound on number of expensive syncs) 
  (i.e. if a few nodes periodically run expensive syncs, attacks (disagreement) can be surfaced quickly)
- want to prove most nodes can store few mappings (resolving through the network)
