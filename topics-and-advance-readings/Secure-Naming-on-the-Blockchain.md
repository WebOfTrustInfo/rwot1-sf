# Secure Naming on the Blockchain

### Blockchain Naming Systems

+ Namecoin
+ Bitcoin + Blockstore
+ Other Blockchains

### Namecoin

From [namecoin.info](https://namecoin.info/):

Namecoin was the first fork of Bitcoin. It was first to implement merged mining and a decentralized DNS. Namecoin squares Zooko's Triangle!

#### Additional Resources

+ [Namecoin Wiki](https://wiki.namecoin.org/index.php?title=Welcome)

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
