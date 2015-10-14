# Building a web of trust for decentralized e-commerce platforms (e.g. OpenBazaar)

By [Michael Folkson] (https://twitter.com/michaelfolkson), (http://michaelfolkson.com/).

OpenBazaar is a decentralized network for peer-to-peer online commerce. Cryptographic keys establish an identity, digital signatures prove an identity agreed to the contract and a cryptographic hash of the contract acts as a tamper-proof record of the contract. Products are paid for using multi-signature escrow contracts with arbiters digitally signing transfer of funds to the seller or back to the buyer in case of disagreement over the quality or specifications of the goods delivered.

The upside of bypassing centralized services such as eBay or Uber is that no third party can charge excessive fees, impose restrictive policies, prohibit Bitcoin payments or present a single point of failure in the storing of users’ personal data. However, the downside is that no organization is responsible for maintaining the integrity of the system and guard against Sybil attacks and fake ratings.

Webs of trust (such as the PGP web of trust) have historically been used to bind cryptographic keys and an identity. However, they can also potentially be used to build broader reputation or trust systems for users of platforms such as OpenBazaar so that they can assess the likelihood of promises made on the marketplace being fulfilled.

Dionysis Zindros proposes one particular web of trust solution in his paper ‘A pseudonymous trust system for a decentralized anonymous marketplace’. His aim is to “construct a means to measure trustworthiness between individuals in a commercial setting where goods can be exchanged between agents”. There are at least three types of participants on a platform such as OpenBazaar. Vendors might scam buyers by not delivering goods, buyers might falsely claim they didn’t receive the goods and arbiters might not resolve conflicts in a neutral manner.

In Zindros’ solution, each node on the network can vouch for the trustworthiness of other nodes. This “direct trust” may be based on real life associations or through dealings on other online platforms such as eBay. It is represented as edges with a source, target and a weight. If a user is not connected to a node by an edge, trust can be assessed indirectly through the trust other connections have in this particular node. Every user has different sets of connections so the “projected trust” in the node will most likely be different for each user.

Unlike projected trust, global trust in a node will be consistent across users. A node will build up this global trust through proof-of-burn and proof-of-timelock mechanisms.

This web of trust solution is vulnerable to man-in-the-middle attacks where an honest vendor is impersonated for the purposes of building up trust. It is currently difficult to guard against such attacks though the physical delivery of the product may be used to verify that there is no man-in-the-middle.

OpenBazaar is not currently using a web of trust solution.

Questions to discuss:

* How should webs of trust be phased in when they require strong network effects?

References
----------

Sanchez, Washington. “Decentralized Reputation in OpenBazaar”. 2015 https://blog.openbazaar.org/decentralized-reputation-in-openbazaar/.

Zindros, Dionysis. “A pseudonymous trust system for a decentralized anonymous marketplace”. 2014. https://gist.github.com/dionyziz/e3b296861175e0ebea4b.
