# Building a web of trust for decentralized e-commerce platforms (e.g. OpenBazaar)

By [Michael Folkson](https://twitter.com/michaelfolkson), (https://michaelfolkson.com/).

OpenBazaar is a decentralized network for peer-to-peer online commerce. Cryptographic keys establish an identity, digital signatures prove an identity agreed to the contract and a cryptographic hash of the contract acts as a tamper-proof record of the contract. Products are paid for using multi-signature escrow contracts with arbiters digitally signing transfer of funds to the seller or back to the buyer in case of disagreement over the quality or specifications of the goods delivered.

The upside of bypassing centralized services such as eBay, Kickstarter or Uber is that no third party can charge excessive fees, impose restrictive policies, prohibit Bitcoin payments or present a single point of failure in the storing of users’ personal data. However, the downside is that no organization is responsible for maintaining the integrity of the system and guard against Sybil attacks and fake ratings.

Webs of trust (such as the PGP web of trust) have historically been used to bind cryptographic keys and an identity. However, they can also potentially be used to build broader reputation or trust systems for users of platforms such as OpenBazaar so that they can assess the likelihood of promises made on the marketplace being fulfilled.

Dionysis Zindros proposes one particular web of trust solution in his paper ‘A pseudonymous trust system for a decentralized anonymous marketplace’. His aim is to “construct a means to measure trustworthiness between individuals in a commercial setting where goods can be exchanged between agents”. There are at least three types of participants on a platform such as OpenBazaar. Vendors might scam buyers by not delivering goods, buyers might falsely claim they didn’t receive the goods and arbiters might not resolve conflicts in a neutral manner.

In Zindros’ solution, each node on the network can vouch for the trustworthiness of other nodes. This “direct trust” may be based on real life associations or through dealings on other online platforms such as eBay. It is represented as edges with a source, target and a weight. If a user is not connected to a node by an edge, trust can be assessed indirectly through the trust other connections have in this particular node. Every user has different sets of connections so the “projected trust” in the node will most likely be different for each user.

Unlike projected trust, global trust in a node will be consistent across users. A node will build up this global trust through proof-of-burn and proof-of-timelock mechanisms.

This web of trust solution is vulnerable to man-in-the-middle attacks where an honest vendor is impersonated for the purposes of building up trust. It is currently difficult to guard against such attacks though the physical delivery of the product may be used to verify that there is no man-in-the-middle.


OK Turtles file

##### Q: What Is A Protocol?

A __protocol__ is *a description of a fixed pattern of behavior*.

A protocol ***is not:***

- A platform.
- An implementation.
- A network.

Or any other "thing". Protocols are how the _things_ themselves behave.

##### Q: Why Are You Telling Me This?

Because the Internet needs blockchains, and it needs to be able to access them securely from mobile devices. At the same time, it would be unwise for the entire Internet to rely on any _specific_ blockchain.

##### Q: Why Does The Internet Need Blockchains?

Because blockchains are how you do digital property on the Internet in a secure and decentralized fashion.

##### Q: OK...? Why is that important?

It's important and relevant for all the following applications:

- Identity
- Security
- Communication (aka: Identity + Security)

This Design Shop is all about identity. If you want to be able to *actually own* your identity online, then you need blockchains.

No individual owns their online identity today. Companies and governments own your online identity, and this applies to individuals as much as it does to other companies and groups.

Since blockchains make individual ownership of digital property possible, they make it possible for you to actually own (and therefore have control) of your online identity.

##### Q: OK... So What's This About A "Generic Thin Client Protocol?"

Blockchains are difficult to run on most end-user devices.

A _thin client_ (or a _light client_) refers to software that downloads only a portion of the blockchain [[1]](https://en.bitcoin.it/w/index.php?title=Thin_Client_Security&oldid=56863). This gives clients some ability to verify for themselves the authenticity of information within it.

The Internet needs a __blockchain agnostic__ and __technique agnostic__ thin client specification.

Agnosticism is essential because:

- Any blockchain may become abandoned by the Internet community.
- The “ideal blockchain” is unknown and may not exist.
- Non-agnostic protocols promote potentially harmful centralization.

Although most thin client techniques are derivatives of Satoshi’s original [Simplified Payment Verification (SPV)](https://en.bitcoin.it/wiki/Thin_Client_Security), it turns out there’s more than one way to skin a thin client. And so, in order to define a flexible thin client standard, we must find out just how different they can be.

![](https://okturtles.com/other/images/Thin-Client-land-2.jpg)
