# Distributed multi-ledger model for financial industry

By Pavel Kravchenko

There are a few problems that financial institutions have while applying blockchain ideas to their needs, such as limited scalability, trust needed to (semi-)anonymous validators, low speed of transaction settlement, limited privacy of trading positions, absence of AML and KYC mechanisms. All this issues are consequences of the trustless nature of existing blockchain implementations such as Bitcoin, Ethereum and (partially) Ripple that work under the assumption that there should not be a central party that controls the system. This implies the presence of a single blockchain/ledger and global consensus over it. While we fully agree on the need for decentralized financial infrastructure, we believe that techniques that are used in Bitcoin etc are not directly applicable to it. Ideas and mechanisms that are described in this paper are rather simple - 1) each entity has its own ledger(s) that contains its transactions and balances 2) there is no global shared ledger at all 3) there is no global consensus 4) there are no designated validators - financial institutions (gateways and other trusted parties) are validators. To simplify things you can imagine the existing state of the things when each business and individual has its own financial ledger and they are updated individually and then apply the blockchain data structure, cryptographic techniques and a standard set of communication protocols to it. Basically we are describing the financial internet.

The financial industry needs a unified and standard set of open-source protocols to trade and store information about accounts (for easy and provable audit) and settlement. These protocols should be able to support processing of hundreds of thousands transactions per second, have built-in AML/KYC mechanisms and identification techniques, protection of information about trading positions, provable finality of a trade, minimal trust to third parties.

Bitcoin (or Ethereum) blockchain cannot be considered suitable for financial industry because of the 1) anonymity of validators 2) longest chain rule that allows anonymous actors to change the past (51% attack) 3) low transaction speed 4) the requirement for all details of all transactions to be replicated to all participants indiscriminately and without encryption 5) built-in coin
Semi-trusted systems (like Ripple) consensus mechanism doesn’t provide information for the user  whether the rest of the network agrees with user’s UNL state and similarly, achieving global consensus about each transaction and changes of the protocol is hardly imaginable.

In addition to that:
- final users don’t have a way to analyze/prove situations that caused problems (forks).
- financial institutions face privacy problems when working on the same blockchain - all their trading positions are public.
- situation with KYC vs privacy is not clear - from one side there is no identity information attached to a public key, from the other - blockchain is open to everybody to analyze graph of transactions

### Model and protocol of asset emission, registering and trading

1. Each entity (user or financial institution) has it own ledger that may be public or private.
2. There are no designated validators. Validators = gateways/banks/regulators. 
3. The validators are responsible solely for promising never to sign a transaction that would result in a double-spend and for validating that the business rules associated with the transaction were implemented correctly. Validators that operate in some regulated environment are legally punishable for their actions. Validators that represent non-regulated entities (i.e. merchants that issue loyalty points for their customers) risk only trust of their customers.
4. All validators can establish trusted relationships with other validators by exchanging/certifying public keys with each other. This will allow their users to pay/exchange currencies.
5. Process of establishing trust (between validators, validators and regulators, validators and users) is beyond scope of the system. 
There are no anonymous parties in the system. Each public key can be traced down to its owner (but it doesn’t imply presence of global address book). 6. Validators’ public keys are either self-signed or signed by the central authority in central jurisdiction. Signed transaction could be proven legally binding.
7. There is no global identity provider or identity storage. Users are registered with certain validator and correspondence between username (such as john@citi.com) and public key is stored in a database that validator (i.e. Citi) maintains. Validator provides limited access to this database to other validators/users. 
8. There is no need in presence of a single central authority. Network is based on trusted p2p relationships between validators (financial institutions). Trust means ability to provide credit to each other. But at the same time any kind of relationships (hierarchical) can be established using the same set of protocols.
9. DDoS attack is not applicable, since everybody knows who is initiating (or co-signing) the transaction. 
10. Validators don’t obligatory share state of their ledgers with each other and don’t achieve consensus within the whole set of validators. 
11. Since all entities are identified, built-in coin is not needed.

Questions to discuss:

- This model is essentially Web of Trust between public organizations. How does trust scaling differs from Web of Trust in PGP case? 
- What are the implications of having fully hierarchical PKI that has only one root for one region?
- Is there a way to monitor double spending attempts without breaching privacy of the ledgers?


