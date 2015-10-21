# Secure Naming on the Blockchain

*by Muneeb Ali [@muneeb](https://twitter.com/muneeb) \<muneeb@onename.com\> and Ryan Shea [@ryaneshea](https://twitter.com/ryaneshea) \<ryan@onename.com\>*

Note: This document uses a few sections from a paper that is currently under peer-review. Please contact the authors (Muneeb Ali, Ryan Shea, Jude Nelson) if you want a copy of the full paper pre-print.

### Blockchain Naming Systems

+ Namecoin
+ Bitcoin + Blockstore
+ Other Blockchains

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

### Bitcoin + Blockstore

Blockstore enables human-readable name registrations on the Bitcoin blockchain, along with the ability to store associated data in external datastores. You can use it to register globally unique names, associate data with those names, and transfer them between Bitcoin addresses. Anyone can perform lookups on those names and securely obtain the data associated with them.

Blockstore uses the Bitcoin blockchain for storing name operations and data hashes, and the Kademlia-based distributed hash table (DHT) and other external datastores for storing the full data files outside of the blockchain.

<img src="https://s3.amazonaws.com/onenameblog/openname-bitcoin-dht-diagram-4.png" width="650"/>

#### Blockstore Capabilities

Blockstore is extremely sophisticated in it's abilities. For example, it can:

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

#### Additional resources

+ [Blockstore design decisions](https://github.com/blockstack/blockstore/wiki/Design-Decisions)
+ [Why to use Blockstore over Namecoin](http://blog.onename.com/namecoin-to-bitcoin/)
+ [Blockstore usage docs](https://github.com/blockstack/blockstore/wiki/Usage)
+ [Blockstore name and namespace operations](https://github.com/blockstack/blockstore/tree/master/blockstore/lib/operations)

### Other Blockchains

There are several other implementations of blockchain-based naming sytems, including BitShares and a few smart contracts on Ethereum.

+ [BitShares Named Accounts](https://bitshares.org/technology/transferable-named-accounts/)

Existing Ethereum contracts unfortunately do not have the same level of sophistication that Blockstore has, but one could conceivably write more powerful contracts with better designs.

+ [An overly simplistic (and insecure) naming contract](http://ether.fund/contract/06735/namecoin)
