Lightning Network and Web of Trust ==================================

By Joseph Poon <joseph@lightning.network>

The Bitcoin Lightning Network is a smart contract technology using Bitcoin payment channels which allows for scalable high-volume micropayments without delegating full custody of funds to trusted third parties.

Bitcoin allows anyone to send value without a trusted depository or custodian. However, due to limitations to block confirmation, transactions require up to one hour. Additionally, individual micropayments below several cents are not worthwhile on the Bitcoin blockchain as the on-blockchain transaction fees are several cents. Lightning Network conducts net settlement of funds between two participants which allows one to conduct an unlimited amount of transactions off-blockchain, but eventually settling the transactions on-chain.

Funds are placed into a two-party, multisignature "channel" bitcoin address. This channel is represented as an entry on the bitcoin public ledger. In order to spend funds from the channel, both parties must agree on the new balance. The current balance is stored as the most recent transaction signed by both parties, spending from the channel address. To make a payment, both parties sign a new exit transaction spending from the channel address. All old exit transactions are invalidated by doing so.

The Lightning Network does not require cooperation from the counterparty to exit the channel. Both parties have the option to unilaterally close the channel, ending their relationship. Since all parties have multiple multisignature channels with many diferent users on this network, one can send a payment to any other party across this network.

By embedding the payment conditional upon knowledge of a secure cryptographic hash, payments can be made across a network of channels without the need for any party to have unilateral custodial ownership of funds. The Lightning Network enables what was previously not possible with trusted financial systems vulnerable to monopolies—without the need for custodial trust and ownership, participation on the network can be dynamic and open for all.

Applications include pay-per-megabyte internet, machine-initated high-volume programmatic payments, and paying for media (e.g. pay-per-article).


New Challenges to WoT Key Exchange
----------------------------------

New innovations and development in key exchange and trust systems are becoming increasingly necessary for new developments in decentralized financial systems. Traditionally, financial infrastructure has used hierarchical systems which have been sufficiently functional for a banking model where there are only several trusted counterparties. However, with development in decentralized systems like Bitcoin, it's necessary for individuals to conduct key exchange without central entities.

The Lightning Network in particular requires direct communication between endpoints. Payments are routed across a network of participants and receipt of funds are proven by knowledge of some preimage with a previously shared hash. As a result, proof-of-payment can only be established with a signed message establishing that knowledge the preimage for hash H is actual payment. This receipt must be signed by the recipient before payment is made if one wishes to be able to proof the purpose of a payment. As this requires digitally signing a document before payment, the participants must have some kind of key exchange to validate that the recipient is who they claim to be.

These types of payments are direct peer-to-peer payment without trusted custodians, so the trust models are somewhat more complex and may be similar to a web-of-trust type system.

Incorrect key exchange due to attacks from adversaries results in payment to incorrect parties. Direct, immediate, tangible financial loss can result from improper key exchange. This problem is exacerbated by the need for many parties to send funds to many other parties.

As a result, systems like the Lightning Network will be in need of key-exchange and discovery which is not only functional for a handful of trusted parties (which are currently somewhat mitigated by cert-pinned identities), but to also be useful for a group of individuals or small merchants to receive payments and prove payments reliably. These types of emerging financial systems may be used other applications of communication and digital identity.

Questions
---------

1. What kinds of identities & indentifiers are ideal for the use case of requiring signed receipts/proof-of-payment? Canonicalization of identity, whether to include hostnames vs. pubkeys as the root identity, UX, etc.

2. What kind of identifier features are necessary? E.g. scriptable revocation of keys

3. Are there any examples or implementations of architectures to use for identity? Are identity documents/certificates preferable over simple pubkeys?

4. It's possible that people will overload these systems for messaging and reputation systems, what are some implications for doing so? How does one make reputation sybil resistant?

5. Historically, users are very bad at maintaining private keys, are there advantages for a WoT based on multiple-signators?

6. Are centralized directories a worthwhile tradeoff? How to minimize trust in a single entity (E.g. namecoin) over models with centralized identifiers (e.g. OpenID)?

7. What would be a secure user experience flow for establishing trust for someone buying a cup of coffee at an independent coffee shop? At an online newspaper?


References
----------

[1] The Bitcoin Lightning Network paper http://lightning.network/lightning-network-paper.pdf

[2] Summary http://lightning.network/lightning-network-summary.pdf

[3] Video https://www.youtube.com/watch?v=8zVzw912wPo
