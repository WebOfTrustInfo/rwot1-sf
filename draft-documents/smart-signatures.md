# Smart Signatures

### Authors

+ Christopher Allen
+ Greg Maxwell
+ Peter Todd
+ Ryan Shea
+ Pieter Wuille
+ Joseph Bonneau
+ Joseph Poon
+ Tyler Close

### Abstract

In this paper, we describe a cryptographic signature system that can be used to greatly extend the capabilities of traditional cryptographic signatures. Traditional systems are based on strictly-defined authentication and authorization mechanisms that assume a single private key can be used to produce a given signature and that a single public key can be used to verify it.

Given the evident limitations of this design, we propose an alternative that is more powerful in its capabilities due to the fact that the conditions for verification are explicitly outlined and fully-programmable. This programmable authorization system allows for broad capabilities in specifying the conditions under which a signature or set of signatures can be considered valid.

Our inspiration for this authorization system is the Bitcoin scripting language, where the authorization to spend funds is explicitly defined within a script, rather than being implicitly defined through the reference to an authorized public key. The largest benefit of explicit specification of authorization conditions is that the system is fully extensible, so new operations can be defined at any time and the only limitation on the authorization system is the set of operations that the authorization interpreters understand.

### Background

#### Traditional Message Signing and Verification

In traditional message signing systems, one generates two mathematically-linked keys, a public key and a private key, where the public key can be derived from the private key, but the reverse derivation cannot be performed.

To produce a signature for a given message, a signature generation function takes as inputs a private key and the message to be signed. A reader can then verify the signature with a known public key, which is linked to that unknown private key. This is done by a signature verification function that uses the public key, the signature, and the signed message as inputs.

Traditional signature systems are very powerful on their own, as one can verify a signature without being able to produce it. However, these longstanding cryptographic systems are very limited in scope.

#### Bitcoin Scripting

Bitcoin contains a fairly advanced authorization system. Every transaction in Bitcoin has a set of recipients, where each of the recipients is actually a script that outlines the conditions under which the coins can be spent at a future date.

Here, the scripts are the equivalent of challenges. Anyone who can meet the conditions outlined by the script is granted access to spend the funds.

These scripts can be very powerful and support various levels of complexity:

1. Scripts can require signatures that correspond to a given hash of an unknown public key. This is a traditional signature, referred to in bitcoin as a “pay-to-pubkey-hash” script.
2. Scripts can require a set of signatures to be provided that correspond to K out of N specified public keys. This is known as a multi-signature script.
3. Scripts can keep their actual redemption conditions secret and simply provide a hash of their redemption conditions. At a later date, a redeemer can provide the redemption conditions along with the signatures that allow it to meet those conditions — simultaneously providing the conditions and meeting them. If the conditions are met _and_ the hash of the conditions matches the hash provided in the script, authorization is granted.

As an example, let's take a look at a standard Bitcoin script:

```
OP_DUP OP_HASH160 <pubKeyHash> OP_EQUALVERIFY OP_CHECKSIG
```

Here, authorization would be granted if a user could provide a smart signature that contains a standard signature and a public key that together could be used as input for a Bitcoin script-compatible verification function in order to produce a "true" output.

### Proposal

#### Bitcoin’s Scripting Outside of the Blockchain

Bitcoin's smart authorization mechanism can be used in other contexts. A wide variety of resources, from API endpoints to assets on a blockchain, can be protected by an authorization system where each resource links to script-encoded conditions for access and each authorization request links to information that seeks to meet the provided conditions. Such a system would be a smart signature system.

#### Smart Verification

Let's go to the standard Bitcoin script we looked at above:

```
OP_DUP OP_HASH160 <pubKeyHash> OP_EQUALVERIFY OP_CHECKSIG
```

Now imagine we have a smart certificate that is used outside of the blockchain context and has the above script code embedded inside of it. With this, certificate validation code would go through and verify the authenticity of the script, when provided with a signature.

The certificate would be verified as follows:

1. The user's signature is pushed onto the stack, producing [SIG1]
1. The user's public key is pushed onto the stack, producing [SIG1][PUB1]
1. The user's public key is duplicated (OP_DUP) on the stack, producing [SIG1][PUB1][PUB2]
1. The top public key on the stack is replaced by a hash of itself (OP_HASH160), producing [SIG1][PUB1][PUBHASH1]
1. The smart certificate's public key hash is pushed onto the stack, producing [SIG1][PUB1][PUBHASH1][PUBHASH2]
1. The public key hashes from the user and the smart certificate are checked for equality and then popped off the stack (OP_EQUALVERIFY), producing [SIG1][PUB1]
1. The user's signature is checked against the user's public key (OP_CHECKSIG), and if it is valid, both items are popped off the stack and replaced by “true”, producing [true]
1. The certificate is validated

This process demonstrates the simplest sort of smart certificate, which is valid if its signature is valid. Basically it's the same as a self-signed certificate, except the rules for its validity are _inside_ the certificate.

More complex scripts could replicate CA-style infrastructures, web-of-trust approaches, or multisigs to create certain  kinds of smart contracts. Examples of some of these results are included in the use cases, below.

#### Implications

Embedding the script be inside the certificate ensures that the same method is used to evaluate it on all devices. Putting a refactoring of certificate policies into scripts that are executed and including a standard-tested virtual machine that executes those scripts may help avoid many of the common errors in certificate policy code in various apps and services.

The script inside a certificate can be inspected and evaluated. Like Bitcoin today, some standard scripts may emerge that are trusted at a higher level than arbitrary written scripts.

### Use Cases

At minimum we need to support existing trust models, including self-signed certificates, CA-style certificates, and PGP-style validation. In addition, we need to demonstrate flexibility for uses cases such as:

#### Short-term Delegation

* Bob has a key for website authentication, but is going on vacation. He wants website sysadmin Alice to be able to sign on his behalf while he's gone. Alice should be able to get into Bob's servers for a week, but things should revert to normal when Bob returns.
* Carol has a very secure key for signing her email. She wants to give her phone the temporary ability to sign emails with that key for the next week.

#### Limited Delegation

* Dan, Dana, Erin, Frances, and Frank are in charge of the development branch of a software project. Project leader Alice wants to give them a key that lets them release development versions of the project without allowing them to release stable versions.

#### Unbundling Delegation

* Carol uses a revocation service. She wants to give them the ability to revoke her key or her previously signed certificates without letting them authenticate keys.

#### Complex Delegation

* CFO Augustus wants to delegate authority to a department to issue a set amount of new bonds, but no more than the set amount, and with an interest rate within certain specifications.
* When Dan, Dana, Erin, Frances, and Frank release a development release, 3-of-5 of them need to sign the release. Further, Dan has a hardware token and wants to sign with 2-of-2 keys, where one key is stored on his hardward token and one is stored on his desktop computer.

### Implementation Status

At this point, self-validating certificates only exist as a rough "on the napkin" proposal: neither a specification nor a proof-of-concept has been created. The next step may be to create a proof-of-concept prototype before focusing too much a detailed specification.

### Implementation Concepts

Some possible implementation concepts:

+ __Schnorr Signatures & Script2__ – Many of the more complex signature delegations that we wish to offer (in particular Tree Signatures) require implementation of Schnorr Signatures, which Bitcoin's script language does not currently offer. Blockstream offers a [new library](https://github.com/bitcoin/secp256k1) to support Schnorr under curve secp256k1 and is working on Script2, an upgrade of Bitcoin's script, to support it.
+ __Merkelized Abstract Syntax Tree (MAST)__ - MAST is a cryptographically committed version of an abstract syntax tree that naturally maps to Lisp-like syntax and semantics. MAST-based [Tree Signatures](https://blockstream.com/2015/08/24/treesignatures/) allow for multisig scripts with sophisticated AND/OR operations, which can be supported using Bitcoin's script language by adding a single op-code: OP_CAT.
+ __Pruning__ - Unexecuted branches of the MAST can be pruned away and replaced by hashes. The verifier knows that the code was executed correctly while code not executed isn’t relevant, improving privacy.
+ __Delegation via signed code__ - To delegate control to another party, sign a secondary MAST that implements additional checks, such as a secondary public key and have the master MAST execute that code if the signature passes.
+ __Upgrades__ - We can add an operation that looks like a no-op. By definition this means "There are rules here that I don't know how to enforce"; systems have to treat that as a failure. Then we can add meaning to that operand in an upgrade. Once a supermajority is updated to enforces the rules, everyone sees the new op and can validate the script.

### Open Questions

+ __Static Context & Run Context__ - In order to perform a number of use cases, the virtual machine may need to provide a context to a script and some way to parse that context. For instance, a certificate authority-like script needs to know which domain a child script is approving access to (an internal static context), whhich domain is actually being accessed (an external static context), and even the content of a web page itself (a run context), and then must compare these values. What additional script operands are needed to parse and evaluate context?
+ __Asynchronous Oracles__ - A number of use cases may require connecting to an third-party oracle to evaluate certain conditions such as a proof-of-existence as of a certain date, proof-of-uniqueness, specific financial information, or revocation status. It could be that these oracles are pre-fetched and added to the script's context before execution. If so, how does a script tell the virtual machine what to pre-fetch? It could be that certain oracles are distributed on DHT or blockchain and thus are always static. In any case, any asynchrony has security implications including the possibility of denial of service. How do we minimize these risks?
+ __Revocation__ - There was some discussion by the team about how to do revocation. Revocation is not as simple as a failed authentication; revoking a key is distinct from all other signature operations as it implies a desire for proof of non-revocation. It could be that revocation scripts need to be separate and distinct from a validation script. Possibly a proof-of-publication oracle can support this by providing a signature attesting to the fact that a specific revocation does not exist as of some timestamp. Finally, we could only use short-lived keys and not rely on revocation at all.
* __Hierarchical Deterministic Keys__ - A number of use cases (in particular short-lived keys) may require scripts to evaluate validity of HD keys. Can we do this securely in script? What additional operands may be required?
+ __Choice of Language__ - The team has focused on a variant of Bitcoin's Forth-like scripting language. The advantage here is that we can leverage the security reviews and understanding of a widely deployed existing system. However, at some point if we add enough features to the language that are unique to smart signatures, the benefits of being derived from Bitcoin's script become less valuable. Other language approaches may offer superior features without compromising security, or offer superior tools. This team agrees that a simplified language should be a requirement, but where to draw the line is unclear.
