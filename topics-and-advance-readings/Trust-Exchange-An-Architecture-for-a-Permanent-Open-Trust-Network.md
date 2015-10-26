# Trust Exchange: An Architecture for a Permanent Open Trust Network

By [Harlan T Wood](https://twitter.com/harlantwood)

In 1963 J.C.R. Licklider, director of the Information Processing Techniques Office at The Pentagon's Advanced Research Projects Agency, proposed an "[Intergalactic Computer Network](https://en.wikipedia.org/wiki/Intergalactic_Computer_Network)", which he envisioned as an electronic commons open to all.  This bold vision planted the seeds for ARPANET, and eventually for the network of networks known as the Internet.  Today we need an equally bold vision -- an open interoperable commons for the permanent storage, sharing, and searching of what is perhaps the most important information of our time: Trust.

## Desired Features

What is meant mean by a "Permanent Open Trust Network"?  Here we refer to a permanent digital archive for trust, reputation, and ratings information, which has the characteristics:

1. Anyone can contribute _claims_ (collectively representing any type of trust or reputation data: ratings, vouches, "likes", reviews, [h-reviews](http://microformats.org/wiki/h-review), etc)

1. Claims are in an open format that is sufficiently flexible to represent multiple claim types

1. Claims are immutable, and cryptographically signed by a private key belonging to the claimant

1. A claim can target any person or entity, commonly a public key (if available) or a URL

1. Claims can be easily shared, selectively or publicly, or may remain private

1. A _trust network_ emerges for each claimant, which is actually a cascading network of the trust networks they are most closely connected to

1. Information within such a trust network is easily discoverable and  searchable

## Trust Exchange Architecture

Trust Exchange is an emerging protocol being developed at by my colleagues and I at [Citizen Code](http://www.citizencode.io/), which seeks to address the feature set above, incorporating other open source components wherever possible, and building the remaining pieces from scratch.

For a gentle introduction, see Noah Thorp's excellent article [Decentralized Cooperation needs Decentralized Reputation](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/DecentralizedCooperationNeedsDecentralizedReputation.md); or for the more technically minded, see the early work on an open source [reference implementation](https://github.com/citizencode/trust-exchange).

Here we address the technical components implied by the features listed above, and indicate the external software, or internal directions intended by Trust Exchange.

### Extensible & Interoperable

Trust Exchange aims for maximum extensibility and ecosystem compatibility:

1. Pluggable datastores: the reference implementation currently supporting a graph database, a document database, and partially supporting IPFS
1. Data architecture supports interoperability with JSON-LD, RDF, XDI](http://xdi.org/), [IPLD](https://github.com/ipfs/ipfs/issues/36), among others
1. Open architecture for multiple cryptographic hashing, signing, and encryption  algorithms

### Flexible Trust Atom Format

The format for storing open "Trust Atoms" is capable of subsuming existing heterogeneous rating formats.  Examples to illustrate this are enumerated below.

An example of a "like" as a Trust Atom:

```json
{
  "source": "multihash-QmWdprFxhCWzjJ6D9Tw9tj5FyWFauhYuGtDQigVvwfteNv",
  "target": "http://maidsafe.net/",
  "content": "like",
  "timestamp": "2015-08-11T22:32:23.207Z"
}
```

An example of a "vouch" as a Trust Atom, where the (hash of the) public key of the target is known:

```json
{
  "source": "multihash-QmWdprFxhCWzjJ6D9Tw9tj5FyWFauhYuGtDQigVvwfteNv",
  "target": "multihash-QmdzVM8y31dVmvwa4bQ5Nuwu6HVXK7mGootcWdnbtp98cZ",
  "content": "CoffeeScript",
  "value": 0.95,
  "timestamp": "2015-08-11T22:32:23.207Z"
}
```

An example of a "4 (out of 5) star rating" as a Trust Atom:

```json
{
  "source": "multihash-QmWdprFxhCWzjJ6D9Tw9tj5FyWFauhYuGtDQigVvwfteNv",
  "target": "https://en.wikipedia.org/wiki/The_Terminator",
  "value": 0.8,
  "raw_value": 4,
  "maximum": 5,
  "rating_type": "5-star",
  "timestamp": "2015-08-11T22:32:23.207Z"
}
```

### Cryptographically Signed Claims

Claims are cryptographically signed by a private key belonging to the claimant.  For example:

```json
{
  "source": "multihash-QmWdprFxhCWzjJ6D9Tw9tj5FyWFauhYuGtDQigVvwfteNv",
  "target": "http://ipfs.io/",
  "value": 0.9,
  "content": "content addressable graph infrastructure",
  "timestamp": "2015-08-11T22:32:23Z",
  "+hash": "multihash-QmaGJwJRTrYGChugJrdzUqq7CxwsvNyYuhUPZFvxuJUgtM",
  "+signature":"7de52c8bd7ec15fa117dca2ca9d6e474746316508337856f0b2e42617670a113845c0f98c34b833869ae47757659fb7051cf13c38c3cd3cba40cb89735c6a48c"
}
```

In order to compute the `+hash`, and from that the `+signature`, we must first determine the `canonical JSON`. For the example above, that is:

```json
{"content":"content addressable graph infrastructure","value":0.9,"source":"multihash-QmWdprFxhCWzjJ6D9Tw9tj5FyWFauhYuGtDQigVvwfteNv","target":"http://ipfs.io/"}
```

The `+hash` is created by applying a hashing function to the `canonical JSON`, which provides a permanent identifier (address) of this Trust Atom, eg:

```
multihash-QmemzKk3wiXjNVNrtdj7Mos11dNYzMFbxkfNQJ6W25CwLb
```

The creator of the `Trust Atom` can then sign this hash with the private key corresponding to the public key embedded in the Trust Atom itself, forming the `+signature` attribute.

### Permanence: Content addressable nodes and trees

For a permanent archive, content addressing based on the cryptographic hash of the data (or tree of data) is preferable to server- or domain-based addresses, conferring benefits including automatic deduplication, caching, and cryptographic verification of content.

Trust Exchange builds on the foundations being laid by the [InterPlanetary File System](https://ipfs.io), a promising emerging technology which "provides a high throughput content-addressed block storage model, with content-addressed hyperlinks. This forms a generalized Merkle DAG, a data structure upon which one can build versioned file systems, blockchains, and even a Permanent Web."

### Discovery and Search

At the level of data nodes, the need for indexing, search, and discovery is similar to other platforms.  IPFS is [moving in promising directions](https://github.com/ipfs/archives/issues/8) with distributed indexing, especially with the use of [CRDTs](https://en.m.wikipedia.org/wiki/Conflict-free_replicated_data_type) (Conflict-free replicated data types).

### Related Tools & Future Directions

A suite of tools is required to meaningfully complete the Trust Exchange ecosystem, including:

1. **Translators**: given a Trust Atom format able to represent existing trust information, we enable an open source ecosystem of tools able to copy trust information from a user's siloed data sources and translate it into this interoperable open format.

1. **Trust Atom Crawlers**: given your known trust network, crawlers can update and index trust information into your "personal cloud" of Trust Atoms.

1. **Trust Network Analysis**: given the raw data of Trust Atoms, insight and recommendations can be gleaned from algorithmic crunching of this data.  This area is a rich opportunity for an ecosystem of both free and commercial tools.

1. **Private Sharing**: a user must be able to share any Trust Atom or collection thereof with an individual or group, transparently discovering public keys, encrypting and decrypting, as easily as sharing content on a social network is today.

These tools require further research and development; components will be sourced from existing open source libraries wherever possible.

## Toward an Intergalactic Trust Network

Just as Licklider envisioned an Intergalactic Computer Network, and Juan Benet an InterPlanetary File System, we need open, interoperable trust network protocols and systems built for the permanent storage of the data that is the foundation of the ultimate social network: the trust information of humanity.
