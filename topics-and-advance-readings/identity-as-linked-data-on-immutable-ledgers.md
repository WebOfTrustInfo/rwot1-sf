# Identity as Linked Data on Immutable Ledgers

By

- Tim Daubenschuetz, @timdaub, \<tim.daubenschuetz@gmail.com, tim@bigchaindb.com\>
- Trent McConaghy, @trentmc0, \<gtrent@gmail.com, trent@bigchaindb.com\>


## Motivation

Content creators on the Web are getting a raw deal. They get a fraction of a cent for an ad played on YouTube, and nothing on Facebook, for filling these sites with traffic-driving content. It’s hard to make a living when you’re
a creative. Licensing is hard; the UX is terrible, so lawyers and middlemen extract the most value. In the music
industry, more money flows into the pockets of distributors than creatives. Consumers are often happy to pay for their
content. Instead, they're forced to sit through ads or miss out on income due to ad-blockers.


## The COALA IP Working Group

To address these problems, COALA IP (Coalition Of Automated Legal Applications, Intellectual Property) was
formed to design and implement a free and open specification for handling digital licensing of intellectual property. Its
goals are to establish open, free, and easy ways to claim attribution, add metadata, license works, mediate IP disputes,
and authenticate claims of others. Furthermore, there should be global agreement at the data level without the need for centralized
control.

A recent, more concrete, endeavor of the group has been to write a specification for handling digital licensing of
intellectual property on immutable ledgers. It's an effort to transform the implementation-agnostic [Rights Reference Model](http://doi.org/10.1000/284)
of the [Linked Content Coalition](http://www.linkedcontentcoalition.org/index.php) into a free and open guideline. It
outlines technologies that could be leveraged for implementation and structure of a specification for all involved parties: creators, rights holders, consumers, developers, etc. The protocol is to be technology-opinionated, but ledger-agnostic.


## The COALA IP Protocol

The COALA IP protocol is essentially two parallel technical efforts:

1. It's a community-driven effort to find and define a minimally-viable set of data for licensing intellectual property
   (using RDF schema definitions)
2. It's a free and open messaging/communication protocol for license-transactions


At its core, the RDF schema defines ontology over six main entities that form and their interconnections. The
ontology as well as all entities have been derived from the LCC's RRM:

- **Place:** A localizable, physical place (e.g. an address, a city, a country, ...)
- **(digital/physical) Manifestation:** A perceivable creation (e.g. a print of a photograph of a certain scene)
- **Creation:** A distinct, abstract creation whose existence is revealed through one or more manifestations (e.g. The idea
  to photograph a certain scene)
- **Right:** A transferable entity connected to a manifestation that entitles the owner to do something in relation
  to a Creation (e.g. a permission to display a Manifestation publicly)
- **RightsAssignment:** A transfer of a Right (e.g. Transferring the permission to display a Manifestation publicly)
- **Assertion:** A claim made about the truth or falsehood of assertions made in the ontology (e.g. A statement vouching
  for the validity that a certain Party is the original author of a Creation)
- **Party:** An individual or a group of individuals representing right holders, licensors, users and so on...(e.g. a human being
  or a group of human beings)


Since finding a minimal viable set of properties that describe each of the entities' features is difficult without having
domain-specific industry knowledge, COALA IP's plan is to open this process up to the community, thereby letting the community define
and derive domain-specific RDF schema. As soon as saturation for changes in schema emerge, further formalization is planned
to take the them to an international standards organization appropriate.

Key technologies used to achieve this endeavor are:


- **[JSON-LD](https://www.w3.org/TR/json-ld/):** A recently emerged RDF serialization format, that brings Linked Data to the
  JSON data structure
- **[IPLD](https://github.com/ipfs/specs/tree/master/ipld):** A data structure to merkle-link JSON objects in order to
  retrieve them with merkle-paths, providing cryptographic integrity-checking of the data as well as content-addressable
  storage
- **[ILP](https://github.com/interledger/rfcs):** A set of specifications for sending (at this point only: fungible) digital
  assets across different ledgers


## The Missing Link: Identity

At the point of writing this position paper (almost) all pieces of the specification are in place, except for a crucial one:
Identity (the so called "Party" entity mentioned in the previous section).

Members of the COALA IP working group would like to actively participate in design-workshops of the Web of Trust working
group to discuss identity solutions that fulfill the following systematic requirements:

- An Identity's identifier must be resolvable within the Internet
- An Identity's properties must enable other Identities to validate the cryptographic integrity of an Identity's signed data
- An Identity must have at least one persistent unique public identifier that is both human- and machine-readable
- An Identity's identifier should have multiple designations (e.g. compare to [IBAN designations](http://www.isbn.org/about_isbn_standard))
- An Identity participates in a global trust network, having it's trustworthiness continuously evaluated by other
  participating Identities


In order to be compliant with the current state of the COALA IP protocol, the following requirements should be fulfilled:

- Is an Identity resolved within the Internet, then it's data can be integrity-checked cryptographically (compare: content-addressed
  storage provided by IPFS and IPLD is favored)
- Preferred serialization formats of an Identity object are JSON, JSON-LD or IPLD
- A resulting specification regarding Identity management respects the immutability of data


Additionally, some philosophical requirements the COALA IP group would like to address:

- A digital Identity solution must not be based on any proprietary technology


## Attribution

This paper couldn't not have been written without the tremendous efforts from collaborators and employees of the following projects:

- The Linked Content Coalition
- IPFS
- The Interledger Protocol
- RDF, JSON-LD and all related Semantic Web and Linked Data standards and implementations
- The COALA IP working group
- BigchainDB
