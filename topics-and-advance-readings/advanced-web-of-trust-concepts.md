Advanced Web of Trust Concepts
==============================

By Christopher Allen - ChristopherA@LifeWithAlacrity.com

There are a number of advanced cryptographic concepts that may be relevant to #RebootingWebOfTrust

* Trust agility
* Translucency
* Minimizing disclosure
* Selective disclosure
* Self-validating certificates
* Store & Forward Perfect Forward Secrecy
* Unbundling Revocation and Other Services
* Random Thoughts

Trust Agility
-------------

A concept popularized by Moxie Marlinspike @moxie http://www.thoughtcrime.org/

Summarizing the concept from his blog post: http://www.thoughtcrime.org/blog/ssl-and-the-future-of-authenticity/

> The current problems with the CA system can be reduced to a single missing property: trust agility.

> At the moment, if you decide that you don’t trust VeriSign or Comodo or any other CA, what can you do? The very best you could do would be to remove the offending CA’s certificate from your trusted CA database, but then some large percentage of secure sites you visit would break. You could take an ideological stand to never visit any of those sites again, but in reality, there isn’t actually an appropriate response, and this is as true for browser vendors as it is for individuals.

> Essentially, at some point a decision was made to anchor trust in organizations like Verisign or Comodo, and now we’re locked into trusting them — forever.

> By contrast, there are two important elements to trust agility:

> * A trust decision can be easily revised at any time. It seems reasonable to think that we’ll need to anchor our trust somewhere. That we’ll pick some entity or group of entities to authenticate our communication. And right now, you could identify a set of organizations that you would trust to do this effectively. But what seems insane is to think that you could identify an organization who you would not only be willing to trust right now, but forever, without any future possibility of changing your mind based on that organization’s performance.

> * If we’re locked into making a single decision now that will effect us forever, what incentive is there for the trust provider we select to act in a way that will continue to warrant our trust?

> Individual users should have the option of deciding where to anchor their trust. Some instead say that better scoping would fix the “bad CA problem.” That if VeriSign did something particularly egregious and were somehow restricted to only authenticating certain sites, site owners would then be able to switch to a different CA in a separate scope (as opposed to now, where VeriSign can continue to sign certificates for your site even if you’re not their customer). This, in a way, would be a limited type of trust agility.

See also Moxie's video (starting at 25m36s): https://youtu.be/pDmj_xe7EIQ?t=25m36s

See also Moxie's Convergence project http://convergence.io/.

> With Convergence, "there is a level of redundancy, and no single point of failure. Several notaries can vouch for a single site. A user can choose to trust several notaries, most of which will vouch for the same sites. If the notaries disagree on whether a site's identity is correct, the user can choose to go with the majority vote, or err on the side of caution and demand that all notaries agree, or be content with a single notary (the voting method is controlled with a setting in the browser addon). If a user chooses to distrust a certain notary, a non-malicious site can still be trusted as long as the remaining trusted notaries trust it; thus there is no longer a single point of failure."

Translucency
------------

The general concept of Translucency, popularized by the book [Translucent Databases](http://www.wayner.org/node/46) by Peter Wayner, is to encrypt data while it is stored on the server. From the FAQ:

> Q: What are translucent databases? A: A term for databases that must protect some information while revealing other data. In other words, a phrase to capture how the database must exist somewhere between translucency and opacity.

> Q: Do they encrypt things? A: Yes, but only some things and then only in a careful way. Standard encryption algorithms lock data away in an inscrutible pile of bits. Only the person with the right key can make sense of the information. Translucent databases use the same algorithms in a more controlled fashion. Some of the information is turned into an inscrutible pile of bits, but other parts can be read, understood and acted upon by the database engine.

> Q: So what's scrambled beyond recognition? A: Anything you want. The database administrator usually chooses personal or sensitive information. Social security numbers or credit card numbers are ideal choices. Passwords are another choice.

> Q: But are they really beyond all recognition? A: Actually, no. The book describes how to control the scrambling so that useful work can be done with the result. In some cases, you can still compare the information to see if it matches other scrambled entries. In others, you can add or multiply the data too. All of this work is done behind a curtain of encryption so the privacy is still protected.

> Q: So why would I use something like this? A: Databases come with good security already, but nothing is perfect. Sometimes someone leaves a backdoor open. The operating system, not the database itself, is often the culprit. Sometimes clerks, bosses and everyone in between abuse their legitimate access. Translucent databases provide a way to work with sensitive information in a more secure way.

> Q: Are there advantages? A: The security mechanism of translucent databases is much simpler. Translucent databases don't require heavily tested operating systems running the in the most secure mode to protect the information. They can save administrative costs by making life easier for system administrators. The mechanism also runs faster in many cases because there's no need for a complicated security layer to evaluate every request.

> Q: Isn't hardware cheap? A: Yes, but it's not just about speed and cost. Translucent databases also make ideal satellite databases placed in remote sites or branch offices. They can accomplish all of their tasks without the extra security. There's no need to lock away the database or check out all of the staff. The translucent database strips away the sensitive information.

> Q: Are they perfect too? A: Nothing is perfect, but translucent databases can withstand some attacks that would cripple a regular database. If a hacker breaks in or an employee turns traitor, the information is still secure. There are still ways that information can leak out, but they're significantly fewer and harder to exploit.In many ideal situations, the database administrator can publish the root password and remain sure that the sensitive information will stay locked up.

There are a number of variants of translucency, including have the keys to decrypt data on the server being held by the client, or using some form of multi-signature or threshold encryption.

Minimizing Disclosure
---------------------

The concept of minimizing disclosure is to reveal only the amount of information about the certificate holder that is needed for the relying party to make a decision, and no more. The classic example is that when you wish to enter a bar in the US to buy a drink, you currently offer a credential that reveals your full name, address, identifying numbers, birthday, etc. This even though all the bouncer legally needs to do is verify that you are over 21. A minimum disclosure credential would offer only the age information.

There are a number of approaches to minimizing disclosure:

* Progressive Disclosure: With progressive disclosure, only the minimum information is offered. For instance, the first request for the holder's age would only result in that the issuer does have a claim regarding the holder's age — the info exists. A second request might reveal that they are older than 13, a third over 18, a fourth over 21, the fifth the actual age in years, the sixth a birth year, and the last a birthday. By policy, a relying party would never ask more than  needed to make a decision about the credential holder.

* Relying Party Profiles: If a relying party desires a credential from someone, they present a profile representing their authority to make such a request. By policy, such profiles only are authorized if they minimize disclosure. Example of this approach:
   * YOTI https://www.yoti.com/

* Attribute Certificates: These are digital certificates that enable relying parties to confirm attributes about the holder other than the identity. For instance, instead of presenting a single credential with many attributes, only the most basic credential is presented, sufficient to confirm identity. Separate attribute certificates are now bound to that credential. Another way to think about it is that attribute certificates are attributes that are outside a traditional digital certificate rather than bound inside one.

* Selective Disclosure: (see next section)

* Potentially [Homomorphic Cryptography](http://searchsecurity.techtarget.com/definition/homomorphic-encryption) could also be used for minimizing disclosure. This is a very computationally intensive method that allow complex mathematical operations to be performed on encrypted data without ever compromising the encryption.

Selective Disclosure
--------------------

Another approach to minimize disclosure; this is a cryptographic zero-knowledge and blinding techniques to prevent the relying parties from linking attribute certificates with the same person. There are a number of variations, many patented, including:

  * Ben Laurie's Selective Disclosure for Laymen: http://www.links.org/files/selective-disclosure.pdf
  * Jason Holt's Blinded Credential Sets: https://eprint.iacr.org/2002/151.pdf
  * U-Prove: http://research.microsoft.com/en-us/projects/u-prove/
  * Identity Mixer - How it Works: http://www.zurich.ibm.com/idemix/howitworks.html
  * IRMA - I Reveal My Attributes: https://www.irmacard.org/scientific-publications/
  * ABCTrust - Attribute Based Credentials for Trust https://abc4trust.eu/
  * Selective Trust using HD Keys: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/Selective-Disclosure-of-Identity.md

Self-Validating Certificates
----------------------------

Bitcoin's non-Turing complete, Forth-like language known as [Script](https://en.bitcoin.it/wiki/Script) could be thought of as a form of digital signature system. Greg Maxwell and Christopher Allen have proposed that this may allow for a new form of self-validating certificate, where the bytecode for verifying the certificate is signed and embedded inside the certificate itself.

This technique may offer some useful security properties, as well as allowing for some sophisticated smart contracts opportunities.

Imagine a certificate that has this bytecode embedded in it:

```
OP_MY-HASH
OP_MY-SIGNATURE
OP_VERIFY
```

The OP_MY-HASH would tell the virtual machine to create a new hash of this object and push it on the stack. OP_MY-SIGNATURE would create the digital signature for this object and push it on the stack. OP_VERIFY would pop both of those values and return 0 if they are equal.

This represents the simplest object, that is valid if its signature is valid. Basically it's the same as a self-signed certificate, except the rules for its validity are INSIDE the certificate.

More complex scripts could replicate CA-style infrastructures, web-of-trust approaches, or using multisig to create certain useful kinds of smart contracts.

Having the script be inside the certificate ensures that the same method is used to evaluate it on all devices. Putting a refactoring of certificate policies into scripts that are executed and including a standard-tested virtual machine that executes those scripts may help avoid many of the common errors in certificate policy code in various apps and services.

The script inside a certificate can be inspected and evaluated. Like Bitcoin today, there may emerge some standard scripts that are trusted at a higher level than arbitrary written scripts.

At this point, self-validating certificates only exist as a rough "on the napkin" proposal — there is no specification nor has a proof-of-concept been created.

Store & Forward Perfect Forward Secrecy
---------------------------------------

PFS (Perfect Forward Secrecy) is a feature of protocols like TLS that offers assurance that if a long-term private key is compromised, the adversary can't also compromise all prior encrypted sessions that used that compromised key even if they've been archived by the adversary. See http://vincent.bernat.im/en/blog/2011-ssl-perfect-forward-secrecy.html & https://lwn.net/Articles/572926/

However, it is much more difficult to offer PFS with store and forward systems like email, as unlike TLS they rarely make a direct connection between the message sender and the recipient.

There are a number of methods for doing this, all with problems.

* Short-lived keys: a series of keys are created, with short expiration dates. The private key is deleted as soon as it expires.

* One-use keys: Each key is used once, then discarded after use. A directory of public keys is available where keys are deleted after use.

* End-to-End Transport: The store and forward agent of the sender delivers directly to the agent of the recipient, without any intermediaries.

These ideas about perfect forward secrecy in PGP were proposed at https://tools.ietf.org/html/draft-brown-pgp-pfs-01

Alternatively, it may also be possible to offer a form of PFS by creating one-use HD (Hierarchical Deterministic) keys and a chain path.

* Hierarchical Deterministic Keys: BIP32 & Beyond
https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/hierarchical-deterministic-keys--bip32-and-beyond.md

* Cryptographic Identifies section of "A Cool Hack…" https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/0499f9c1352220cd471af9fdc7553eb94ddc5709/topics-and-advance-readings/cool-hack-xdi-blockstore-bip32.md

* Decentralized Authentication with Blockchain Auth https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/d662c0e41c8493feb997da264cee38d0fae842c2/topics-and-advance-readings/Decentralized-Authentication-with-Blockchain-Auth.md

* Selective Disclosure of Identity with Hierarchical Deterministic Keys and JSON Web Tokens
https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/d662c0e41c8493feb997da264cee38d0fae842c2/topics-and-advance-readings/Selective-Disclosure-of-Identity.md

Unbundling Revocation & Other Services
--------------------------------------

Earlier this year Christopher Allen demonstrated that it may be useful to unbundle revocation services from certification services:

> In the traditional X.509 Public Key Infrastructure (PKI), Identity Certificates are used to demonstrate ownership of a public key, and are signed by a Certificate Authority (CA) who asserts that the authority has verified that the information in the Identity Certificate is correct. This CA Certificate is, in turn, signed by another Certificate Authority that asserts that the CA Certificate itself is valid. Ultimately this certificate "chain" leads to the "root" certificate with a well known public key that is considered to be strong and uncompromised.

> This is the real power of PKI over other identity protocols —- Identity Certificates are “self-authenticating” and you don't need any network operations to validate a certificate chain.

> A challenge is that Identity Certificates are typically intended to persist for a long period of time, and thus are valid until their expiration date, or until they are terminated through “revocation”.

> Unfortunately, Identity Certificates may become compromised before they expire. This may happen due to a compromise by exposure of the the user's private key, but can also happen due to bugs in software or other exploits. In addition, Certificate Authority’s keys may also be compromised through exposure of private keys and/or bugs. Finally, the "root" key itself may become compromised.

> Theoretically, each time an Identity Certificate is presented, not only is the signature checked on that key and of all the Certificate Authorities above it, each key is to be checked to see if the Certificate Authority has issued an early “revocation” of that certificate in a Certificate Revocation List (CRL). Unfortunately, this part of the Public Key Infrastructure has never really worked. In order to validate an Identity Certificate you would need to connect to the CA to get the list of CRLs, which may be themselves be compromised or be subject to denial-of-service attacks. Thus requiring CRL validation of Identity Certificates removes many of the advantages of “self-authentication” of certificates, so few use them.

> Instead most applications using PKI implement some form of CA Certificate “pinning”. In a somewhat simplified explanation, when an Identity or CA Certificate (or sometimes the public key or hash of the key) is first seen, that Certificate is “pinned” to the host in a “pinset”. The presumption is that this initial validation is correct, and any subsequent changes may be an attack that require additional validation. Often these “pinsets” are hard-coded into software, requiring an update to the software itself if there is a compromise in one of the keys.

> Another solution could include implementing Webs-of-Trust, PGP-style, but this approach has not seen much activity.

> Finally, another approach is to replace CRLs with some type of service that are more distributed and less subject to a denial-of-service attack. The Online Certificate Status Protocol (OCSP) protocol has been used and does help with revocation of CA Certificates, but is not very effective in compromised server private keys. In addition it has privacy issues (CAs can learn your browsing habits), and it also has scaling and performance issues.

> In 2013 Mozilla reported that of 1774 CRL servers, ~1/2 did not respond to requests, and for that those that did report offered over 2.66 million revoked certificates taking up ~98MB. For OCSP Mozilla reported 1,292 servers with a response time of ~200ms per certificate, and every certificate in the chain needs to be checked! Now in 2015, due to Snowden revelations and Google “HTTPS Everywhere” SEO changes we are being asked to use TLS for every server on the internet, so the scaling challenges today are even greater!

> There are some possible solutions on the horizon, CRLsets & OCSP stapling (basically certificate pinning approaches applied to OCSP), and a new Certificate Transparency proposal from Google. Unfortunately these approaches are unproven, are not decentralized, and may also have other undiscovered issues.

> The underlying technology of Bitcoin that is known as the blockchain has some interesting properties when thinking about the revocation problem.

> Fundamentally the blockchain is a decentralized, consensus-based, time-stamped ledger. It is used in Bitcoin for financial transactions — in a sense a double-entry bookkeeping system where virtual coins are moved off one account and moved onto another, in such a way that no one can double-spend those coins.

> The beauty of this system is that there are hundreds of thousands of copies of these ledgers, all of which are updated within 10 minutes of each other. The blockchain is also very good for something called “proof-of-existence” at a particular time. This is because of how important it is to have all transactions properly in order to prevent double-spending.

> A lot of thought has been put into making this system reliable, safe against attack, and fast. There is no “root” in the blockchain, instead it functions as a decentralized authority with no center. The system is very heterogeneous, meaning that there are many redundant versions of the code, APIs, and services making denial-of service and other technical compromises more difficult.

> The blockchain is not an identity system. Each account (a Bitcoin address) has a private key associated with it that only exists until that account is spent (has a zero balance), and then that key is thrown away. This is very unlike X.509 PKI use of keys which may be kept for years.

> I would like to take advantage of these throw-away keys. I propose that one possible solution to the Revocation Problem is to consider using blockchain technology as a solution.

For more information on this proof-of-concept, see: https://github.com/ChristopherA/revocable-self-signed-tls-certificates-hack

One lesson learned from from this hack is the general idea that there may be other aspects of current cryptographic services are traditionally considered to be a single service, that in fact could be unbundled into separate services. For instance, why do we have to have ICANN be the only one that can mediate domain name disputes? Other communities may decide to have EFF be a more fair mediator, so users can choose. Thus we could unbundle this subtle portion of a naming service to enable pointing to user or community choice of mediation, rather than a single arbitrary one.


Random Thoughts
---------------

* Eigentrust++ from the peer-to-peer world looks very interesting http://www.cc.gatech.edu/~lingliu/papers/2012/XinxinFan-EigenTrust++.pdf
  * Reportedly NEM altcoin (New Economy Movement) is now using Eigentrust++ http://nem.io/

* For master keys, should we be looking at increasing from 256 byte to 512? The 25519 curve has a double-sized companion 41417 http://eprint.iacr.org/2014/526.pdf

* Or maybe we should move to having master keys use quantum resistant math. Eduarda Freire's thesis on multilinear map-based HD keys claims to be proven secure: http://eprint.iacr.org/2014/526.pdf, Programmable Hash Functions in the Multilinear Setting http://link.springer.com/chapter/10.1007/978-3-642-40041-4_28, and Forward Secure Non-Interactive Key Exchange by David Pointcheval, Olivier Sanders http://link.springer.com/chapter/10.1007%2F978-3-319-10879-7_2
