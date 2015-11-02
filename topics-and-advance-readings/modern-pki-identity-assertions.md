# Modern PKI: Identity Assertions Forming Trust Networks

Current public key infrastructure for personal communication is limited, hard to use, and harder to use correctly. User adoption is very low, even in relation to the userbase already using OpenPGP-based software for communication.  A PKI can and must be created which does not require expert-level knowledge of public-key encryption to use properly.

A PKI's job is to store and retrieve public keys and their respective global identity bindings: identifiers of personal location or accounts controlled by the key's owner and associated with that key.  The key is queried via a bound identity attribute (e.g. email address), and the PKI will also return all certificates asserting the validity of these identity bindings.

The method of creating certificates to validate a key-identity binding may be used in a general-purpose way to bind more types of global identities than just the email addresses and domain names most commonly bound by PGP and X.509 respectively.  Furthermore, the signed certificate key assertions can do more than simply determine key validity. They can be generalized into assertions on any topic, thereby generating a trust network.

## Overloading Of the Term 'Key'
A note should be made here about the term 'key'.  Commonly 'key' refers to cryptographic keys in the sense of a public/private keypair, or just the public key portion.  OpenPGP also defines another definition for 'key', a 'PGP Key'.  A PGP key contains one or more cryptographic keys (keypairs or public keys), global identity in the form of one or more email addresses, as well as a complete set of certificates signed by other keys to indicate relative validity of the key/email binding.

This particular agglomeration makes the email identity binding the de facto standard identifier, effectively limiting OpenPGP-based communication to email.  Nowadays there is a multiplicity of channels of textual communication, and limiting oneself to a single channel is not ideal.  This is not a limitation of public key cryptography, but simply of the interchange format: a PGP Key consists by definition of the binding of cryptographic keys and email addresses.  Splitting this atom opens the way to the secure use of a panarchic set of communication channels which utilize a PKI-style method of acquiring secure credentials as a transparent, flexible underlying protocol layer.

## Cryptographic Signing as Formalized Assertion

An assertion binding a set of global identifiers to a key can be formalized by generating a certificate -- a statement of the assertion which is cryptographically signed.  In the case of validity, the assertion is the key itself, and some canonical representation is then signed.  The result is a certificate.

### X.509 Domain Assertions
In X.509, an assertion is made associating a key with a global identifier, most commonly a domain name.  The assertion takes the form of a Certificate Signing Request, which asserts a relationship between a public key, the domain name requested, and personal identifying information including business name, address, and email address.

This CSR is itself validated by being signed by a key which is trusted.  A key is trusted if it is in a certificate chain from the trusted root key of a Certificate Authority. This is a top-down, authority-based approach to determining whether a certificate is valid, and has been fairly successful at centrally administering a scarce global identity asset, the domain naming system.  However, it is expensive, some argue without good purpose, which in turn limits the use of secured communication on the web.

### OpenPGP Identity Assertions
PGP followed a fundamentally different path in determining the validity of such an identity binding (excluding the more hierarchical PGP Universal Server). When creating a PGP key, an assertion is made associating the key with a global identifier: an email address.  Since there is no default central authority in PGP, validity of this assertion is determined via a web of trust.

In this model, a PGP key can be used to generate a certificate asserting the validity of another key, which is an assertion that the key actually belongs to the owner of the associated email address, called "signing a key".  The certificate is then stored within the PGP key being validated.  To determine whether a particular public key's identity assertion is valid a user would check whether the key includes a signature that a) they themselves signed or b) anyone they know signed.  (This is a slight simplification.)  The only information we get from querying the key's signatures is whether, from our point of view and current keychain, us or someone we know claims the keypair is valid.

## Validity Network Graph
### PGP Keys
A PGP key is essentially a partial description of a graph: a single node and its edges. The node is the keypair and the edges are the set of available validity certificates -- the minimum amount of information to be able to combine with one's own key graph ("keychain") to be able to utilize a Web of Trust method to derive basic validity information.

This method of storing a PGP Key, transmitting, and then recombining into a full network graph is a product of its time, circa 1992.  It is more suited to passing one's keys back and forth on diskette than the era of ubiquitous fast internet. While we can learn from and be grateful for what has come before, the scale and constraints we are now designing for are fundamentally different.

### Blockchain
The blockchain is revolutionary in part because it is a single public record that is not destroyable (given enough nodes over a large enough geographic area), tamper-resistant (given a diverse enough pool of miners), and permanent.  It is a method of maintaining a single unified data state.

A public blockchain is equivalent to a public notary. The certificate is timestamped and thereafter part of the public record.  A consensus mechanism is in place to guard against bad actors / miners in the blockchain, and the cost of notarizing (miner's fee) guards against spam.

Timestamping certificates also allows for the possibility of progressive trust, where a key's interactions over time provide a context and reputation from which to make trust determinations.

### Store Edges, Not Nodes
Within the graph of all transactions in a blockchain system such as Bitcoin, what is actually stored in the blockchain is the edges of the graph, not the nodes; the relationships only, not the entities relating with each other.  The nodes can be inferred and calculated from the sum of the edges. A wallet UI presents to the user a derived balance from the sum of all transactions.

In the same way, a service retrieving certificate-based identity attributes with a blockchain-like storage system would persist only the certificates regarding an attribute about a key. Validity information for that key can be rehydrated by traversing the graph, filtering for certificates referencing the key being queried.

Graph traversal is fairly time consuming. An Ethereum Virtual Machine based blockchain can be utilized which allows transactions to execute bytecode that can store information in actual data structures.  For instance, a hash table can be built up allowing constant time lookup of certificates for a given key.


## Validating Identity Binding
Initial ownership validation of the identifier bound to the uploaded public key was not part of older PKIs.  PGP Global Directory is a PKI which now verifies the email address on the uploaded key via the now-familiar method of emailing a one-time link to the email address.  The [keybase](http://keybase.io) service goes further and supports verification of ownership over multiple social accounts by publishing a message signed with the private key.  Their tooling supports a low-friction method of encrypting a message to a user referenced by their account identifier, such as twitter handle, github username, or email.

It addresses the modern online landscape:
* Identity online may be referenced from accounts on multiple services.
* Encryption keys should be easily discovered and fetched, referenced by any of these online identities.
* Encryption and decryption should be seamless, as though communicating with the individual, with the keys as an almost-invisible protocol layer. There is still a long way to go for this last piece.

### Revocation
Since blocks are timestamped, more temporal dynamics are possible.

On the one hand, key revocation can be enacted in the usual way where a user signs the revocation certificate with the key to be revoked. The approximate moment when the user's revocation was written into the blockchain is public knowledge.  Instead of discounting all communications ever made with that key as would happen in traditional revocation, the system can apply a drop-off of trust values from a point of time relative to information indicated in the revocation certificate of whether the key was compromised and for how long.

On the other hand, in the case where a user has lost access to the key, revocation by attrition is possible.  Trust values based on last known certification or use of the key would naturally drop off over time where no one was using the key. As the user interacts with a new key, his network would naturally accrue certificates validating the new key associated with his online identities.


## More Than Valid/Invalid
The original PGP Web of Trust was a mechanism for making a simple deduction from the signatures available: the key is either valid or invalid -- either actually associated with the individual who owns the bound global identifiers or not.

However, splitting up the keypair from the identifiers being bound allows for some new and useful dynamics. Other users can generate certificates validating specific identifier-binding assertions, and they can indicate a gradient trust rating of any particular assertion. Users can certify any statement/assertion, and other users can also make assertions about that assertion, again indicating a gradient trust rating.  These assertions and trust ratings, and the graph of interdependent relationships can combine to give a finely nuanced graph of general trust relative to any node or set of nodes, providing useful information from which to make determinations of worth relative to the opinions of those you already trust.

## Hierarchical PKI
The hierarchical model has many benefits especially within hierarchical structures.  It also has drawbacks for contexts outside of a hierarchical structure where person-to-person communication is considered private and sacrosanct.  An Ethereum Virtual Machine based approach to solving the public communication context does not preclude a more centralized and control-oriented solution applied to an organization or corporate structure.

### Same Smart Contracts, Different Chain
There are multiple blockchains with varying tradeoffs that run the Ethereum Virtual Machine.  These implementations share the same executable bytecode, but differ in the method of achieving consensus, and address different needs.

The main Ethereum chain is the ideal solution for the public use case. It provides a single set of publically-accessible verifiable data without any centralized control, and thus it does not depend on the continued existence of a company, university, domain name, corporate entity, or foundation.

The needs of a corporation vary from that of the general public. An organizational hierarchy demands  control over its infrastructure. Often required is tight permissioned access, running within the corporate datacenter or cloud, ability to manually revoke keys when an individual leaves an organization, manually rotate keys if a user loses or leaks his private key, and enforce data policies such as key rotation.  All of these are possible using other self-hosted blockchain implementations.  One of the main benefits here is that smart contract code vetted by the open source community can be utilized directly. Upon initialization, for instance, a master CA key could be specified which allows administrative override, whereas in the public version, no such key would be specified.

But do we now have a return to the familiar old world of siloed data as a barrier to interoperability?  One way of overcoming interop issues is communicating as separate networks with open access. Read access to individuals' public keys can be ubiquitous without compromising security.  DNS could indicate where to query for a particular corporation's key data.  The HTTP Keyserver Protocol defines SRV records to be used to indicate the keyservers for a domain.  Also the trusted admin key (essentially an in-house Certificate Authority) could act as trusted introducers or meta-introducers between individuals in different blockchains.

## Future Work

This is a nascent area in the modern context, and this paper has barely scratched the surface of what is possible.  There are many avenues to explore regarding usage and implementations.  Regardless, there will be developed a protocol or set of protocols that allow secure communication seamlessly, without expert knowledge or any manual intervention required, and work on this has already begun.
