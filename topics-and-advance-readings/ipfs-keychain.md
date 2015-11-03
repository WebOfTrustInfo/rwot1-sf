
# Notes on the IPFS Keychain (or the Web Keychain)

(These are just short notes, becuase the idea is very simple, and obvious. It does not take much to understand it. But like SFS naming, it is _subtly powerful_).

_Abstract:_  _**The Keychain**_ is a datastructure for cryptographic artifacts, on top of IPFS. The Keychain allows users to place public keys, signatures, certificates, and all sorts of proofs directly on top of IPFS, creating a merkle-graph of artifacts. This way, one artifact contains merkle links to artifacts used to produce it or necessary for its verification -- e.g. a signature links to the raw data and to the key. This enables easy retrieval and verification of all necessary pieces of data. Moreover, entire swaths (graphs) of artifacts can be retrieved pre-emptively and stored locally for fast access, and even disconnected operation.


### What is IPFS? How is it useful?

IPFS is a new hypermedia distribution protocol, with Merkle Links and with Key Links! Think HTTP but with content-addressed and key-addressed links -- so content can be verified for integrity and authenticity. In short, think Git + BitTorrent + the Web. Learn more about IPFS at [the IPFS website](https://ipfs.io) or [at this seminar talk](https://www.youtube.com/watch?v=HUVmypx9HGI).

IPFS provides several useful properties:

- a decentralized, peer-to-peer distribution system
- content-addressed and key-addressed links (URIs)
- subnet, disconnected, or offline operation
- support for a wide variety of transports
- targetting web, mobile, and IoT use cases
- provides a very simple JSON-friendly data model (cbor)
- But most importantly: **IPFS is a transport for arbitrary merkle datastructures.** This means a huge merkle DAG of objects, where files, cryptographic artifacts, websites, repositories, cryptocurrencies, and more, can all link to each other through permanent, cryptographic links.


### What is The Keychain, then?

**The Keychain** is a datastructure that rides on top of IPFS. It is a PKI-over-IPFS, where all of the artifacts (keys, signatures, certificates) are first-class IPFS objects with merkle-links to the artifacts used to produce them or needed to verify them. It can include all sorts of cryptographic artifacts, like signatures, certificates, proofs, and so on.


### Examples

Consider objects like these:

```js
// a signature
{
  // the key used to sign the signature
  "key": "/ipfs/Qmbatr97vqpmrXg6tubdpUBwJrLzvYPHe9vS7xc9b7y3nk",

  // the target object signed
  "target": "/ipfs/Qmbatr97vqpmrXg6tubdpUBwJrLzvYPHe9vS7xc9b7y3nk",

  // the signature bytes
  "sigdata": "<raw-signature-over-target-hash>"
}
```

The links can be used to retrieve and verify the other artifcats. Protocols can thus only _require_ transmitting (or embedding) small links -- or single objects -- but get the entire power of distributing an entire chain of artifacts.

This is particularly important in storage or bandwidth constrained environments, like blockchains. Protocols can prepare all the artifacts in a merkle graph, add them to IPFS, ensure the survival of the data, embed the link in the blockchain, and disappear.

### How does this improve on status quo?

Today, artifacts will include hashes of relevant other artifacts, but no easy, decentralized way to resolve that hash to the other artifact. IPFS and its tooling makes all of this a pleasant experience.

### What about other data?

The Keychain coexists with other data and datastructures in IPFS and can link to them directly, using the same kind of links.

### Self Description -- Links to the algorithms themselves

By being able to link artifacts to anything in IPFS, the Keychain also makes it easy to link directly to the algorithms used to create artifacts. These links could be to _the actual code_ used to generate and verify them. This code could be in many languages. This enables users or agents to fetch the code necessary to run a protocol, enabling a much faster system upgrade as new algorithms are adopted. (And with a pure language and VM sandboxing, this can be automated).

### Survival of Data

The [IPFS Content Model](https://github.com/ipfs/faq/issues/47) leaves it up to protocols layers on top to guarantee survival of data. Other tools and protocols can be used on top to ensure its survival: IPFS nodes publicly accessible, [ipfs-cluster](https://github.com/ipfs/notes/issues/58), and [Filecoin](http://filecoin.io). This can be as simple as making the data available through an IPFS node available to the network, as straight-forward as using one of today's cloud storage systems, or as robust as hiring a large network of agents to back things up. The choice matters less because IPFS addresses do not include location, so the system can be upgraded over time (e.g. start with an IPFS node in front of S3, and then upgrade to a federation of interested parties, or to a large decentralized network).

### Encryption

Objects in IPFS can be encrypted, so objects need not be accessible to the public-- they can be held in private and revealed only to select users.

### Applications

- **Key Signing:** Keychain makes key-signing easier as all of the artifacts can be tracked and accessed via IPFS.
- **Key Hierarchies:** Keychain makes it easy to model hierarchies of keys, with signatures of the children always pointing to the parent (signers). That way the hash of a single signature can "pull out" the entire graph going all the way to the root key.
- **Certificate chains:** Certificates can link to their parents.
- **Web of Trust:** collecting and being able to crawl all of the signatures can make the Web of Trust much easier to account for and resolve.
- **Proof Schemes:** Protocols requiring proofs can make proofs that link to the related (and often necessary) other artifacts, such as keys, agreed-upon randomness, commitments, and so on.

and many more. Basically, any protocol that includes _producing_ and _distributing_ cryptographic artifacts could benefit from using IPFS and The Keychain.
