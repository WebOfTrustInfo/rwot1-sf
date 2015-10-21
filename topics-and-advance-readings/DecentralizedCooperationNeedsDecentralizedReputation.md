# Decentralized Cooperation needs Decentralized Reputation
White Paper By [Noah Thorp](http://twitter.com/noahthorp)

We are in the midst of a techno-cultural trend that re-envisions ownership, protocols of trust, organizational decision making, and ecosystems of work. This zeitgeist can broadly be called decentralized collaboration.

In the United States, organizations are atomizing into flexible services and autonomous, purpose-driven small businesses. [Deloitte reports](http://dupress.com/articles/business-ecosystems-come-of-age-business-trends/) the ecosystems of value creation that are emerging create both competitive and collaborative advantage. Several forces are driving this change.

Freelance work represents a significant driver. Today, freelancers and gig workers make up 34% of the US work force. In keeping with these trends, Intuit and MBO Partners optimistically predict that by 2020 freelancers will represent 43-50% of the work force. Although these numbers may be inflated, there is strong evidence that autonomous work forces are expanding.

Organizational functions are unbundling to empower this atomized economy of freelancers and worker hives. Small ventures are freed to focus on core value by leveraging services like Zen Payroll, Zen99, and Zenefits for accounting; Clerky for legal support; gig work through Lyft, Uber, and Thumbtack; WeWork and Impact Hub for co-working. Crowd funding has reached mainstream participation through Kickstarter, Angel List, Mosaic Solar Financing, and Crowdfunder.

Of more disruptive significance is the introduction of truly decentralized technologies. Significantly disruptive models include decentralized commerce ([Open Bazaar](https://openbazaar.org/), [Silk Road](https://en.wikipedia.org/wiki/Silk_Road_(marketplace))), file storage ([IPFS](https://ipfs.io/), [Maidsafe](http://maidsafe.net/)) and asset tracking ([Ethereum](https://www.ethereum.org/), [Bitcoin](https://www.bitcoin.com/)). Decentralized blockchain solutions for governance, truth, and trust are poised to create resilient, censorship resistant networks empowering a new generation of beneficiaries.

Large scale decentralized cooperation depends on decentralized reputation. Cryptocurrencies enable decentralized financial transactions, but what technology decentralizes the reputation data necessary for the full spectrum of commerce and collaboration?

Arriving at such a solution is an interdisciplinary endeavor. It requires investigation into the interface between private keys, reputation data structures, reputation data interpretation, and social interpretation of reputation data.

## The Challenge of Decentralized Reputation at Scale

Advice from our personal networks reduces our search time for new products, services, ideas, and collaborators dramatically. This benefit is magnified as we move from our in person network to online graphs. But these graphs are currently primarily provided by centralized services such as Google, Facebook, Twitter and the like.

In a centralized world, we rely heavily on familiar brands that we trust to provide reputational information for services we have no previous direct interaction with. Reputation services like Yelp store ratings and provide the context necessary for interpreting reputational information. There are several reasons to create alternative centralized reputation services.

Centralized services have a biased incentive structure for interpreting reputation data and disproportionate power to modify it. For instance, movie ticket provider [Fandango](http://fivethirtyeight.com/features/fandango-movies-ratings/) is incentivized to pump up movie ratings to sell more tickets and they can set ratings high to do so. This demonstrates how reputation data is subject to censorship, distortion, and deletion.

Effectiveness of searching is diminished when data is closed to alternate interpretations for novel uses. For example 28,902 IMDB users rated cult classic movie [Plan 9 From Outer Space](http://www.imdb.com/title/tt0052077/) an average of 4 out of 10. If you were looking for the best sci-fi B Movies of all time the rating system at IMDB is apparently useless. Averaging ratings in this case removes information needed to discover bizarre cult films.

Company bankruptcy can lead to massive community data loss.

The amount of redundant, non-reusable work spent by users on rating things is astounding. Large quantities of user generated data is siloed, non-reinterpritable, and impermanent. This represents a significant loss of value to the users who created this content.

A new era of peer to peer collaboration can be enabled through decentralized reputation services. If executed well a scalable, decentralized, interoperable reputation network can make economic ecosystems considerably more productive.

It is worth noting a few barriers to participation in growing reputation systems. Users fear durable negative reputation and this limits participation. Participants are also afraid of being categorized in unfair ways (e.g. the [Peeple app](http://arstechnica.com/business/2015/10/yelp-for-people-app-if-it-exists-disappears-from-the-internet) phenomenon). Fear of retribution for recording negative ratings limits contribution of potentially valuable data. Other adoption factors include cost of participation, availability of relevant data (a network effect), and confidence in accuracy.

To maximize usefulness, decentralized reputation system must be:

1. Interoperable
1. Interconnected
1. Compatible with permissionless and anonymous accounts
1. Contextual
1. Chronological
1. Resilient (censorship resistent, immutable, decentralized)
1. Re-interperatable (raw data is open to user and use specific re-interpretation)
1. Not feared
1. Compatible with the spectrum of identity

## The Need for Progressive Permissionless Reputation

Permissionless access to decentralized systems serves several needs. For one, permissionless decentralized ledgers like Bitcoin grant access to electronic transactions for individuals that would not be able to acquire bank accounts due to lack of government identification, minimum bank balances, or poor credit scores. The low bar for account access enables progressive reputation accumulation. On these grounds, permissionless account access is a potential boon to those with untrustworthy banks, refugees, the homeless, and the poor.

Permissionless accounts also mean an increase in network size and network contributions. Wikipedia demonstrates the strong value of permissionless contribution - 29% of constructive contributions are made with only the recording of the contributors IP address.

## Preserving the Spectrum of Anonymity

Kaliya Hamlin (Identity Woman) defines the [spectrum of identity](http://www.identitywoman.net/the-identity-spectrum) like this:

- Anonymous
- Pseudonymous
- Self-asserted
- Socially validated through a social graph
- Verified by a validated third party
- Mix and match

The exposure of reputation, account, and transaction data progressively remove anonymity and create a reputation profile. For example, bitcoin accounts are subject to progressive reduction of anonymity through each transaction, buying and selling communication, and through account verification (AML/KYC compliance) with services like CoinBase.

The chain of identity reputation creation looks something like this:

1. A pseudonym is created when an actor is known to be unique and has recurring data associated with its actions
1. A profile is created when discrete data is progressively associated with a pseudonym. Reputation is implicitly created through the aggregation of pseudonym and profile data.
1. Value potential is created when a pseudonym is linked to a physical person, place, or thing.
1. Value is created (or destroyed) when information linked to a person place or thing is interpreted and leads to a change of information or in the physical world.

Virtual anonymity is decreased as information is progressively associated with a unique identity.

Physical anonymity is decreased as information about physical identity is increased.

Because of these factors it is important to investigate the interaction between reputation and the progressive loss of anonymity.

## Interpreting Decentralized Reputation Data

Attribution: the synthesis of ideas here is heavily influenced by the insights of Harlan Wood and Matt Schutte.

In order to preserve the utility of reputation information for multiple purposes, it must be available in its raw form. The availability of this raw data enables many interpretations, using diverse algorithms, fit for specific decision making purposes.

The certainty of any given rating is proportional to the:

- Relevance of the data to the interpreters decision making
- Agreeance of progressively aggregegated information
- Diversity of information sources
- Reputation provider's reputation profile. The reputation provider profile trust graph can be recursively evaluated as it is in Google's page rank algorithm.
- Discounting of spurious data by trusted meta-raters

In a decentralized network the aggregation of reputation may be queried across many data storage sources. This data will likely be assembled by crawlers that provide standard data and standard algorithms for interpretation. Confidence in decentralized reputation data may be provided by cross referencing multiple reputation aggregation providers. This interpretation may include both public and private data sources. These providers may themselves be rated using hashes for both the data they ingest and the algorithms they use to interpret the data.

Reputation shifts over time. This makes the time stamping of reputation data essential. A bad rating followed by a good rating from the same pseudonym is likely to mean the opposite of a good rating followed by a bad rating from the same pseudonym.

Default algorithms should be tolerant of bad ratings for many reasons. Reputation and trust are not constant values. In human terms trust evolves through interaction. For instance, broken trust can lead to greater trust through reconciliation. A system that cannot adequately model this subtlety is eliminating potential value that can be realized by a network through reputation queries.

In the Trust Exchange solution I advocate, reputation is inferred by querying through friend of friend relationships to aggregate and interpret reputation. Reputation systems demonstrate their effectiveness relative to our ancestral in person reputation networks particularly in cases where reputation data comes from distant associations. The utility of a reputation system is dependent on both the aggregation of sufficient data and the minimization of reputational distortion across network hops.

With this reasoning, an open interoperable data sharing, with low reputational distortion can dramatically magnify the social gains from network value creation.

## Technical Requirements

Harlan Wood, Joel Dietz, and I are contributing to a very early stage open source protocol solution to the challenges described above. The protocol is called [TrustExchange](https://github.com/citizencode/trust-exchange/blob/master/README.md)

Trust Exchange specifies simple storage of reputation information in a data format called Trust Atoms. Trust Atoms are signed by a private key to associate them with a rater and are queried through a trust network that is also described by Trust Atoms. Trust Atoms can be aggregated by a reputation aggregator across many reputation storage locations including blockchains like Ethereum and distributed file systems like IPFS. TrustAtoms are raw data interpreted by the interpreters choice of reputation algorithm.

The current version of the Trust Atom JSON format flexibly accommodates tags, numerical ratings, and arbitrary content. It is suitable for rendering existing reputation data in an interoperable format.

When converting reputation system data from many existing sources into Trust Atoms, a binding for contextual content gives reputation evaluation algorithms more information on how to interpret a given Trust Atom. For example star rating systems of movies vary across websites and require calibrated interpretation. Including a source specific context gives sufficient information for a rating algorithm. The context referenced should also describe how to accurately generate TrustAtom for the context.

Here is a Trust Atom format extended to include a context to assist reputational evaluation algorithms.

```
{
  source: <hash of public key of the rater (person or organization)>
  target: <hash of public key, or URL of the entity being rated>
  value: <a numeric value in the range 0..1>
  content: <description or tags relating to rating>
  context: <link to a context description>
  timestamp: <date/time of creation>
  +hash: <cryptographic hash of canonical JSON version of this trust atom>
  +signature: <cryptographic signature of hash, signed with the private key of source>
}
```

For more details see the [Trust Exchange Github README](https://github.com/citizencode/trust-exchange/blob/master/README.md).

## Related Questions

- What is a suitable format for describing a Trust Atom context?
- How can entities that do not have a private key be rated? For example, how would we rate the movie "Plan 9 From Outer Space"?
- Who pays for the storage of Trust Atoms?
- How do we formally address the reduction of anonymity inherent in sharing Trust Atom information?
- What are the primary vectors for attacking decentralized reputation systems?
- What are the primary methods for gaming decentralized reputation systems?
- Who are the winners and losers for each point in the spectrum of anonymity?

## References

- Deloitte Center for the Edge, [Business Ecosystems Come of Age](http://dupress.com/articles/business-ecosystems-come-of-age-business-trends), 2015
- MBO Partners, [The Succesful Independent Contractor: A Workforce Trend for The Future](http://careeradvisoryboard.org/public/uploads/2014/06/Career-Advisory-Board-MBO-Executive-Summary_FINAL.pdf), 2014.
- Intuit, [The Intuit 2020 Report](http://http-download.intuit.com/http.intuit/CMO/intuit/futureofsmallbusiness/intuit_2020_report.pdf), 2010
- Wikipedia, [IPs Are Human Too](https://en.wikipedia.org/wiki/Wikipedia:IPs_are_human_too), 2015
- Arvind Narayanan and Vitaly Shmatikov, [Robust De-anonymization of Large Datasets (How to Break Anonymity of the Netflix Prize Dataset)](http://arxiv.org/pdf/cs/0610105v2.pdf), 2008
- [TrustExchange](https://github.com/citizencode/trust-exchange/blob/master/README.md)
- Kaliya Hamlin [The Identity Spectrum](http://www.identitywoman.net/the-identity-spectrum), 2010
- Walt Hickey, [Be Suspicious of Online Movie Ratings Espescially Fandango](http://fivethirtyeight.com/features/fandango-movies-ratings/), 2015
