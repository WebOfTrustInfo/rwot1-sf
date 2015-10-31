# Attempts at common terminology for Digital Identity systems

By Christian Lundkvist [@ChrisLundkvist](https://twitter.com/chrislundkvist) \<christian.lundkvist@consensys.net\>

## Introduction

This note is an attempt to come to consensus about common terminology
when discussing digital identity systems. Often discussions about
digital identity suffers from a lack of precise arguments where the
people discussing have different internal definitions of what identity
means in the context. Thus there is a lot of conflation of identity vs
reputation vs biometric IDs etc. I invite everyone to critizise the
terminology used here and suggest better terms where appropriate, or
to point out errors or other areas that should be covered.

I will try to be general and to not introduce language specific to any
particular implementation or technology stack. In the examples I will
cover specific implementation stacks such as PGP, Ethereum, Blockstack
or a CA-based centralized approach.

## Names and keys

A **cryptographic name** (or just **name**) is a cryptographic hash,
number or (potentially human-meaningful) string that acts as a global,
unique, persistent identifier for the purpose of interactions with
cryptographic systems such as blockchains, messaging platforms or
authentication systems. The well-known [Zooko's triangle][zookos]
states that such names can have two of the three properties Decentralized,
Secure, and Human-meaningful. Blockchains such as [Namecoin][] showed
that it was possible to have systems where all three properties hold
up to byzantine fault tolerance.

The cryptographic name is publicly tied to one or more private/public
key pairs - the private keys are the core of the identity and are used
to sign messages such as transactions on a blockchain, encrypted
point-to-point messages, or messages or certificates enabling access
control. We denote the private key holder the **agent** or **user** of
the name, or simply the **keyholder**. The keys associated to the name
do not neccessarily need to be persistent, they could be swapped out
using a key revocation or key rotation system that links the name to
the keys.

The public key(s) are tied to the name through a publicly accessible
secure registry. This registry could be a centrally managed trusted
system such as a certificate authority or a physically decentralized
(but logically centralized) system like a blockchain. Names can also
be tied to keys through a non-centralized system of certificates, as
advocated in the [SPKI][] proposal. Note that in the SPKI proposal
global unique names are achieved by adding namespaces onto local
names.

### Examples

#### Public keys

The simplest form of a name is the public key corresponding to a
private key (or the hash of a public key). In this case no registry or
certificate is needed to bind the name to the key, the public key
itself is the name. One downside of this scheme is that since the name
is the public key it's not possible to switch out the corresponding
private key while keeping the name persistent in the case of key loss
or compromise.

#### PGP

Using our terminology the names in the PGP system are public keys. It
is tempting to say that names in PGP are email addresses. However,
anyone can generate a PGP keypair and sign a PGP certificate tying a
given email address to that key, and this makes email addresses not
unique in the PGP system. Using the terminology below, an email
address is instead an attribute connected to a specific key.

#### Blockchain ID

In Blockchain ID the cryptographic name is unique but also
human-meaningful. A longer description of the system is
[here][blockchainIdNames].

#### Ethereum-based identity systems

The flexibility of the Ethereum smart contract system allows most kinds
of naming systems to be utilized (public-key, human-meaningful, random
hash, etc). So the question becomes one of selecting desirable
properties. Human-meaningful naming systems have the problem of
[namesquatting](https://forum.namecoin.info/viewtopic.php?f=2&t=2387),
that Namecoin tries to solve by paying fees for names which is
difficult to do in a decentralized fashion. Instead a
non-human-meaningful random hash cryptographically linked to public
keys could be a better cryptographic name to use.

#### Other systems

* X.509?
* PEP?

## Attributes

A name can be linked to a set of **attributes**. An attribute is a
piece of data that's cryptographically associated with a
name. Attributes tie a name together with (mainly) external data and
anchors the name into a context outside of the cryptographic realm of
the name and its associated private and public
keys. Attributes can refer to data like First Name, Last Name, and
photo for a name representing a person, or they can be a tax
identification number or accounting information for a name
representing a corporation. Attributes allow humans to put
cryptographic names in a social context and is the main way humans
will relate to identities. As an example, the Facebook system
identifies users by their Facebook ID (the number acting as the unique
identifier of their profile). Very few users would use this number to
identify their friends, they instead relate to their friends on
Facebook by their Name, Profile Picture etc. Attributes can be either
public, or stored encrypted and be selectively revealed.

### Global vs Local attributes

Many attributes will only be relevant in certain contexts. Thus
attribute data could be external to the name and possibly maintained
by third parties. The name could have links to externally maintained
attribute stores. Even basic things like Name, Profile picture etc
could potentially be tied to external entities, and the user can
choose to update the information either by changing the data held by
the external attribute store, or by changing which attribute store is
linked to.

### Nyms/Usernames as attributes

Usernames/Nyms are special attributes as they are supposed to map onto
identities in a one-to-one fashion in the context where they're
used. Here there may be Nym registries that are localized, for
instance tied to a company, or decentralized like Namecoin or
registries on a blockchain like Ethereum. If the cryptographic name of
the identity is a human-meaningful one this can be used directly as a
username.

### Examples

#### Schema.org

The Schemas outlined in [schema.org/Person][schemaperson] give a good example of attribute data for a human person:

```json
{
"@type": "Person",
"name": "Christian Lundkvist",
"givenName": "Christian",
"familyName": "Lundkvist",
"description": "Blockchain nerd",
"address": [
        {
            "@type": "PostalAddress",
            "streetAddress": "49 Bogart St",
            "addressLocality": "Brooklyn, NY",
            "postalCode": "11206",
            "addressCountry": "United States"
        }
    ]
}
```

#### PGP

In the basic implementation of PGP the attributes are email addresses and attached User ID strings.

#### Blockchain ID

The [Blockchain ID][blockchainIdAttr] attributes are based on the schema.org attributes above but enhance them with additional attributes for things like social media accounts etc.

## Claims/Attestations

A **claim** or **attestation** is a statement about a name or an
attribute of a name, signed by (a key associated to) another
name. This is a very general notion that can apply in many different
contexts. Some attestations could be about relationships between
identities: Company ABC makes an attestation that Person XYZ is
employed there, and Person XYZ can make the corresponding attestation
about Company ABC. There will need to be some standardization around
how to format these attestations in order to maintain
compatibility. The [JSON Web Token][jwt] standard could be a good
starting point for this. In this standard the name making the claim is
called the **issuer**, and the subject of the claim is called the
**subject**.

Attestations are very close to the "web-of-trust" of PGP but could be
more granular and contain more information. A simple example of an
attestation is a "link", i.e. a simple two-way mutual connection
between two identities, signed by both of the identities. One could
also imagine a one-way simple attestation similar to the "follow" used
by Twitter.

Attestations could also be used for reputation systems, e.g. you can
have an attestation giving 1-5 stars in an online shopping context.

### Examples

#### PGP

PGP attestations embody the original notion of a web-of-trust. The
attestation is of the unidirectional type where one PGP identity signs
the public key of another PGP identity. The implied sentiment in the
attestation is "I attest that the user of this key is also the user of
this email address.".

#### schema.org attestations

The [schema.org/Person][schemaperson] specs have various attestations regarding
relationships between people. In the spec there are the fields
`knows`, `follows`, `relatedTo`, `sibling`, `spouse`, `parent`.

In the spec these attestations are also attributes, i.e. my identity
has an attribute that I know someone.

```
{
"follows": [person0, person1],
"knows": [person2]
}
```

The schema.org spec does not have any cryptographic anchoring of the
relationship, so it needs to be augmented with cryptographic
signatures. This can be done either by adding signatures to the
attestation schema (using JSON web tokens), making it in effect a
certificate as is done by the [BlockchainID
Token][blockchainIdToken]. Another way that can be used in
Ethereum-based systems is to embed the attestation in a smart contract
directly on the blockchain. The transactions that put the data in the
smart contract provides the cryptographic anchoring in this case.

#### JSON Web Token (JWT)

A JWT is a JSON data structure containing a **claim**, together with a
**subject** which is the subject of the claim and an **issuer**, which
is the entity that issued and signed the token. Often in our
discussions around user-owned identitiy the subject and issuer will be
the same entity. The JWT can be digitally signed and/or encrypted. An
example from the Blockchain ID spec:

```
  {
        "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJFUzI1NiJ9.eyJjbGFpbSI6eyJrbm93cyI6W3siQHR5cGUiOiJQZXJzb24iLCJpZCI6Im11bmVlYi5pZCJ9XX0sInN1YmplY3QiOnsiQHR5cGUiOiJQZXJzb24iLCJwdWJsaWNLZXkiOiIwMzJlY2RlNDM5N2ZhNDczZjFjZTQ4MmNlYTYyMzVlYjBjMjBiM2NlNGMwMTBhNjY5MDM0NDIyODAwYmJjZDQ5MWQifSwiaXNzdWVyIjp7IkB0eXBlIjoiUGVyc29uIiwicHVibGljS2V5IjoiMDMyZWNkZTQzOTdmYTQ3M2YxY2U0ODJjZWE2MjM1ZWIwYzIwYjNjZTRjMDEwYTY2OTAzNDQyMjgwMGJiY2Q0OTFkIn19.snFhetKhj3uwoVDXXKk5w7wxVpkeTBFjhE-J0s9zkqM9-ZcG7oD1_hi7fBXiLdvgwgbqQJ9VvbYQfTukaiedaQ",
        "data": {
            "header": {
                "typ": "JWT",
                "alg": "ES256"
            },
            "payload": {
                "claim": {
                    "knows": [
                        {
                            "@type": "Person",
                            "id": "muneeb.id"
                        }
                    ]
                },
                "subject": {
                    "@type": "Person",
                    "publicKey": "032ecde4397fa473f1ce482cea6235eb0c20b3ce4c010a669034422800bbcd491d"
                },
                "issuer": {
                    "@type": "Person",
                    "publicKey": "032ecde4397fa473f1ce482cea6235eb0c20b3ce4c010a669034422800bbcd491d"
                }
            },
            "signature": "snFhetKhj3uwoVDXXKk5w7wxVpkeTBFjhE-J0s9zkqM9-ZcG7oD1_hi7fBXiLdvgwgbqQJ9VvbYQfTukaiedaQ"
        },
        "chainPath": "2643afc402f51102d49ee70496354b53f753978c127656ab10fb24a699a842e6",
        "encrypted": false
    }
```


## Identity

An **identity** is the totality of a cryptographic name together with
its associated attributes and attestations. 

### Examples

#### PGP

A PGP identity is a public key together with the associated email
address(es) and corresponding web-of-trust attestations from other
keys.

#### Blockchain ID

The Blockchain ID system uses a human-meaningful name together with
attributes and attestations stored in a distributed storage system
like a DHT and hashed into a blockchain.

#### The uPort Identity system (Ethereum-based)

The [uPort][] system now being built at ConsenSys will use a
non-human-meningful random hash name embedded in an Ethereum
contract. This contract contains hashes of attribute information
stored in IPFS, along with reputational attestations stored in the
contract itself. This gives the flexibility to do key revocation, key
rotation and [decentralized key resets][decentralizedkeyrecovery]
while maintaining a persistent cryptographic name. The reputational
attestations can be read and processed by other smart contracts.

#### Other systems

* X.509
* PEP

[namecoin]: http://namecoin.info/
[uport]: https://medium.com/@ConsenSys/uport-the-wallet-is-the-new-browser-b133a83fe73#.hr4dlj5pi
[blockchainidtoken]: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/Web-of-Trust-with-Blockchain-IDs.md
[zookos]: https://en.wikipedia.org/wiki/Zooko%27s_triangle
[spki]: ftp://ftp.isi.edu/in-notes/rfc2693.txt
[blockchainidnames]: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/Secure-Naming-on-the-Blockchain.md
[blockchainidattr]: https://github.com/blockstack/blockchain-id-js/blob/master/docs/profile.md
[schemaperson]: http://schema.org/Person
[decentralizedkeyrecovery]: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/Key-revokation-of-lost-and-stolen-keys.md
