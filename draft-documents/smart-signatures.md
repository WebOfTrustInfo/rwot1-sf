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

In this paper, we describe a cryptographic signature system that can be used to greatly extend the capabilities of traditional ones. Traditional systems are based on strictly-defined authentication and authorization mechanisms that assume a single private key may be used to produce a given signature and that a single public key may be used to verify it.

Given the evident limitations of this design, we propose an alternative that is more powerful in its capabilities due to the fact that the conditions for verification are explicitly outlined and fully-programmable. This programmable authorization system allows for broad capabilities in specifying the conditions under which a signature or set of signatures can be considered valid.

Our inspiration this authorization system is the Bitcoin scripting language, where the authorization to spend funds is explicitly defined within a script, rather than being implicitly defined through the reference to an authorized public key.

### Background

#### Traditional Message Signing and Verification

In traditional message signing systems, one generates two mathematically-linked keys, a public key and a private key, where the public key can be derived from the private key, but the reverse derivation cannot be performed.

To produce signatures of a given message, a signature generation function takes in a private key and the message to be signed. Meanwhile, in order to verify the signature, we verify that it was produced by some unknown private key that corresponds to a given known public key. In order to do this, we use a signature verification function where the public key, the signature, and the signed message are provided as inputs.

We can see how traditional signature systems are very powerful on their own, as one can verify signatures without being able to produce them. However, such longstanding cryptographic systems are very limited in scope.

#### Authorization Seals

Web-accessible resources like API endpoints are commonly protected by authorization conditions. While some primitive API authorization systems require revealing an app secret, more secure systems require users to present a signature corresponding to an authorized public key in order to gain access to the resource, and these are the systems we will focus our attention on.

When a resource requires a user to present a signature from an authorized public key, it is an authorization challenge that takes a specific form. Expressed another way, it is a seal that must be re-produced in order to access the resource. The challenge or seal can be defined as the following:

"Present a request, a public key, and a signature. If the public key is contained in our list of authorized keys and the public key matches the signature, it could only have been produced by a holder of the private key corresponding to the public key, so then access will be granted."

An analogy to this that mirrors something in the real world might be the following:

“Present an envelope with a wax seal on it. If the seal design is contained in our list of authorized seal designs, it could only have been produced by a holder of the corresponding seal mold, so then access will be granted.”

In traditional authorization systems, the seals or challenges are implicitly defined. A resource may simply state the public key required for authorization, assuming that users know to present a signature alongside the public key. But implicit or explicit, this is a seal nonetheless.

#### Bitcoin Scripting

A fairly advanced authorization system can be seen within Bitcoin. Every transaction in Bitcoin has a set of recipients, where each of the recipients are actually scripts that outline the conditions under which the coins can be spent at a future date.

Here, the scripts are the equivalent of the aforementioned seals or challenges. Anyone who can meet the conditions outlined by the script is granted access to spend the funds. Put another way, anyone who can produce a seal with a specified seal design is granted access to spend the funds.

Conditions for redemption in the bitcoin scripting language go far beyond the simple traditional one that requires signatures corresponding to a given public key.

As one example, seals can require signatures that correspond to a given hash of an unknown public key. These are referred to as “pay-to-pubkey-hash” scripts.

As another example, seals can require a set of signatures to be provided that correspond to K out of N specified public keys. These are known as multi-signature scripts.

As a third example, seals can keep their actual redemption conditions secret and simply provide a hash of their redemption conditions. This means that at a later date, a redeemer is able to provide the redemption conditions along with the signatures that allow it to meet those conditions, thus simultaneously providing the conditions and meeting them. If the conditions are met and the hash of the conditions matches the hash provided in the seal, authorization is granted.

### Proposal

#### Bitcoin’s Scripting Outside of the Blockchain

The smart authorization mechanism that is used in Bitcoin can be used in other contexts. A wide variety of resources, from API endpoints to assets on a blockchain, can be protected by an authorization system that has each resources come with it’s own script-encoded conditions for access, while each authorization request comes with it’s own information that seeks to meet the provided conditions. Such a system would be a smart seal system or a smart signature system.

#### Smart Verification

Imagine a smart certificate that has the following Bitcoin script code embedded in it:

```
OP_DUP OP_HASH160 <pubKeyHash> OP_EQUALVERIFY OP_CHECKSIG
```

In this case, authorization would be granted if a user could provide a smart signature that has a standard signature in it and a public key in it that can be used as input for a Bitcoin script-compatible verification function, and would produce the output “true”.

The certificate would be verified as follows:

1. The signature is pushed onto the stack
1. The public key is pushed onto the stack
1. The public key is duplicated on the stack
1. The top public key on the stack is replaced by a hash of itself
1. The public key hash contained inside of the smart certificate is pushed onto the stack
1. The top two stack items, each public key hashes, are checked for equality and then popped off the stack
1. The signature is checked against the public key, and if it is valid, both items are popped off the stack and replaced by “true”
1. The certificate is validated

This represents the simplest object, that is valid if its signature is valid. Basically it's the same as a self-signed certificate, except the rules for its validity are INSIDE the certificate.

More complex scripts could replicate CA-style infrastructures, web-of-trust approaches, or using multisig to create certain useful kinds of smart contracts.

#### Implications

Having the script be inside the certificate ensures that the same method is used to evaluate it on all devices. Putting a refactoring of certificate policies into scripts that are executed and including a standard-tested virtual machine that executes those scripts may help avoid many of the common errors in certificate policy code in various apps and services.

The script inside a certificate can be inspected and evaluated. Like Bitcoin today, there may emerge some standard scripts that are trusted at a higher level than arbitrary written scripts.

#### Existing Implementations

At this point, self-validating certificates only exist as a rough "on the napkin" proposal — there is no specification nor has a proof-of-concept been created.

#### Implementation Concepts

+ Merkelized Abstract Syntax Tree (MAST) - Cryptographically committed version of an abstract syntax tree. Naturally maps to Lisp-like syntax and semantics.
+ Pruning - Unexecuted branches of the MAST can be pruned away and replaced by hashes. Verifier knows code was executed correctly; code not executed isn’t relevant, improving privacy.
+ Delegation via signed code - To delegate control to another party, sign a secondary MAST that implements additional checks, such as a secondary pubkey, and have the master MAST execute that code if the signature passes.
+ Revocation oracles - Revoking a key is distinct from all other signature operations, as it implies a desire for proof of non-revocation. A proof-of-publication oracle can support this by providing a signature attesting to the fact that a specific revocation does not exist as of some time.
