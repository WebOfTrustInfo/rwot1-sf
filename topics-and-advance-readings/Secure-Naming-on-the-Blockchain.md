# Secure Naming on the Blockchain

*by Muneeb Ali [@muneeb](https://twitter.com/muneeb) \<muneeb@onename.com\>, Ryan Shea [@ryaneshea](https://twitter.com/ryaneshea) \<ryan@onename.com\>, and Jude Nelson [@judecnelson](https://twitter.com/judecnelson) \<jcnelson@cs.princeton.edu\>*

Note: This document uses a few sections from a paper that is currently under peer-review. Please contact the authors if you want a copy of the full paper pre-print.

### Introduction

The Domain Name system (DNS) and Public-key infrastructure components like certificate authorities (CAs) are critical components of today's Internet. Security of most online communication and web traffic depends on the security of these systems. Current PKI systems usually require trusting a central party like Verisign and [DNS has many security issues](http://web.mit.edu/6.033/www/papers/dnssec.pdf) e.g., DNS cache poisoning. 

Crypotocurrency blockchains are a potential alternative to traditional DNS and PKI systems that can provide better security and decentralization guarantees. The technology is relatively new and evolving rapidly, little production data or experience is available to guide design tradeoffs. In this paper, we summarize our experience with running a large-scale production deployment of a naming system on top of a cryptocurrency (Namecoin), and discuss how our experience informed the
design of a new blockchain-based naming and PKI system called Blockstore. 

### Background on Namecoin

[Namecoin](https://namecoin.info/) provides a blockchain-based key/value store and is
originally credited for solving the [Zooko's Triangle](https://en.wikipedia.org/wiki/Zooko%27s_triangle) since it
provides a) human-readable names, b) without requiring central or trusted
parties, and c) users can securely own the names with their private keys.
Namecoin is one of the first forks of Bitcoin and is the oldest cryptocurrency
blockchain that is still operational.

The main motivation for starting Namecoin was to create an alternate DNS-like
system which uses a blockchain as the primary ledger for storing information on
registered domain names, instead of relying on ICANN DNS. Namecoin is derived from
Bitcoin code, and keeps most functionality identical to Bitcoin, with the exception of
support for registering key/value pairs.

Namecoin supports multiple namespaces, with same rules for pricing and name
expiration for all namespaces. By convention, the *d/* namespace is used for domain
names which are mapped to .bit domain name.  For example, to register yahoo.bit, one
must register the key *d/yahoo* and then put the value as the IP
address of the Yahoo! website. The key registration process works as follows: 

**Pre-order:** A user first announces the hash(key) without
revealing what is it that she is trying to register. This is done by the
*name_new* operation in a new transaction and pre-orders the name.

**Reveal:** After the *name_new* transaction has been confirmed by
the network i.e., everyone has confirmed that they have seen and accepted the
*name_new* transaction, the user can reveal what was the key she was actually
trying to register in a *name_firstupdate* operation. The user can include the
value of the key/value pair in this operation as well.

**Update:** The value associated with the key can be updated by a
*name_update* transaction. It also happens to renew the key registration by
another fixed amount of time (currently 36,000 blocks).

#### Lessons from Namecoin

The security of name ownership on a blockchain is tied to the security of both the underlying blockchain and the software powering it. There are three security issues to take into consideration:

1. Cost of attack for taking over 51% mining power
2. Software vulnerabilities
3. Network attacks

For details on these security concerns and other experiences from a large-scale production deployment on Namecoin see [this post](http://blog.onename.com/namecoin-to-bitcoin/). Further, the pricing policy for name registrations is very important for enabling a spam-free namespace. See [this paper](http://randomwalker.info/publications/namespaces.pdf) for a detailed discussion of pricing mechanisms and analysis of Namecoin namespaces.

### Design of Blockstore

Blockstore enables human-readable name registrations on the Bitcoin blockchain, along with the ability to store associated data in external datastores. You can use it to register globally unique names, associate data with those names, and transfer them between Bitcoin addresses. Anyone can perform lookups on those names and securely obtain the data associated with them.

Blockstore uses the Bitcoin blockchain for storing name operations and data hashes, and a Kademlia-based distributed hash table (DHT) and other external datastores for storing the full data files outside of the blockchain.

<img src="https://s3.amazonaws.com/onenameblog/openname-bitcoin-dht-diagram-4.png" width="650"/>

Blockstore is designed to implement Namecoin-like functionality in the layer above the blockchain. It leverages the blockchain to achieve consensus on the state of the system at the time of each block discovery, but otherwise offloads its control logic and state to an external process.  Critically, Blockstore embeds a *virtual blockchain* within the blockchain's transactions, which any peer can audit to determine whether or not one Blockstore peer has processed the same name operations as another.  In doing so, Blockstore keeps its control plane (the virtual blockchain), its data plane (external storage), and its external storage providers logically separate from one another.  We believe this is a significant improvement over alt-coin designs, because it allows the developers of each component to evolve and innovate independently for the benefit of all.

#### Blockstore Implementation

The current reference implementation of Blockstore is in Python and is released as GPLv3 [open-source code](https://github.com/blockstack/blockstore). In the current implementation users can:

+ define namespaces and set parameters for those namespaces
+ register names that can be owned by a Bitcoin address
+ securely associate hashes of data with names
+ store hash-data pairs (key-value pairs) in a DHT or any other storage system
+ transfer names from address to address
+ renew names so they don't expire
+ support SPV-like light clients

In the future, it will support the ability to:

+ revoke names (to allow users to recover from name theft)
+ reset name ownership (to allow users to recover from either name loss or theft)
+ pay name registration fees to miners instead of having them burned (once OP_CHECKLOCKTIMEVERIFY becomes standard)

The easiest way to get started with Blockstore is:

> pip install blockstore

#### Additional resources

+ [Blockstore design decisions](https://github.com/blockstack/blockstore/wiki/Design-Decisions)
+ [Blockstore usage docs](https://github.com/blockstack/blockstore/wiki/Usage)
+ [Blockstore name and namespace operations](https://github.com/blockstack/blockstore/tree/master/blockstore/lib/operations)

### Other Blockchains

There are several other implementations of blockchain-based naming sytems, including BitShares and a few smart contracts on Ethereum.

+ [BitShares Named Accounts](https://bitshares.org/technology/transferable-named-accounts/)

Existing Ethereum contracts unfortunately do not have the same level of sophistication that Blockstore has, but one could conceivably write more powerful contracts with better designs.

+ [An overly simplistic (and insecure) naming contract](http://ether.fund/contract/06735/namecoin)
