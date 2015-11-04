Day One Summary
===============

(unedited notes of interim report outs by #RebootingWebOfTrust teams)

### 1a. A FRAMEWORK FOR SMART SIGNATURES

Bitcoin has extended idea of a signature for smart contracting and other ideas. So how can it be extended?

It can be used for the delegation of keys, with signature that limits their use through programmatic rules

Came up with specific uses
- Delegating access to server
- Delegating a limited key to certain devices
- Creating conditions on software releases
- Defining user-specific revocation

### 2a. DPKI: IDENTIFIERS

Identity should be an immutable key
Multiple methods of discovery
Identity stored in a registry
- Creates multiple sorts of keys

### 2b. DPKI: SECURITY

Want an SIF. Security Internet, Finally.
Minimum number of techniques to create maximum amount of security

Two techniques
- Thin Clients
- Convergence + Block Chains

How many doors do you have to knock on to compromise a system? A metric for decentralization.

2c. DPKI: PRIVATE KEYS

Any system of DPKI must manage private keys for users in a way that's semi-automatic yet secure

Methodology:
- Break up key into shards on multiple devices

### 3. WHAT DO WE MEAN BY TRUST?

- The PGP term Web of Trust is overloaded

- Classic PGP is just Decentralized Key Validation

- We need a new term or to redefine Web of Trust

- Rename or Reclaim?

## 4. QUICK SPEC FOR KEYS MISUSED ON THE BLOCK CHAIN

## 5. SYBIL-RESILIENT REPUTATION AGGREGATION

Use Case:
- Decentralized commerce platform
- Sybils can transact with each other to build up reputation
- Can't stop Sybil creation, but can it make it more costly and make users more transparent to see validity

Sybil-Resilient:
Consumers can detect "bad" behavior
- Best we have current is user reviews, but they're taken avantage of
- Need something better

System would bounce back when there's a Sybil attack

Reputation Aggregation:
- How we aggregate events is important to allow users to detect bad behavior

Result:
- Let users route themselves to actors who behave in ways that causes them to trust

### 6. SATISFYING THE REAL WORLD: WEB OF TRUST USE CASES

Three themes
- Selective Disclosure
  - Ex) Proving age without showing rest of info
- People who don't have identity
  - Ex) Refugee
  - Ex) Someone with pieces of an identity (e.g., victim of domestic violence who has shed part of identity)
- Augumenting different identities
  - Ex) If don't have enough ID for a bank account, how do you get to bigger stuff?
