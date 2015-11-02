# Distributed Receptor-Based Computing
By Arthur Brock @ http://artbrock.com & http://ceptr.org 

The MetaCurrency Project’s requirements for decentralization combined with a commitment to leveraging organizing principles of living systems led us to invest a lot of time in the past 5 years developing Ceptr. Ceptr is a rebuild of much of the computing stack optimized for decentralized sense-making, computation and composability. This means semantics baked into the lowest levels of memory storage, self-describing protocols which let anything talk with anything else, blockchain-like abilities for decentralized data storage and computation.

Our approach addresses many issues people are tackling in a variety of projects (web of trust, blockchain, semantic web, decentralized applications, federated identity, ease of interoperability, rapid code evolution with massive reuse, mesh networks, etc.) through a unified approach.  We know providing such a different approach creates barriers to adoption and understanding, but we also know that applications in Ceptr will be able to be developed faster, easier and should significantly outperform projects which have been cobbled together from more traditional tools.

There’s a lot of things we’ve worked out pretty well, like:  

* Lightweight virtual machines (receptors) for distributed applications/computing 
* Configurable byzantine fault tolerance options for distributed data storage with intrinsic data integrity in signed chains
* Deeply integrated semantics: semantic memory, semantic stacks, and a generalized parsing and pattern matching system via our semantic tree regular expression engine
* Built-in code repository for sharing vocabularies, code and protocols
* Optimization for rapid evolution and easy deprecation (of code, vocabs, protocols, etc.)
* Pluggable, self-describing protocols (Ceptr protocols are not textual descriptions for human protocol developers, but pluggable semantic code. A receptor can install a protocol to read a message after receiving the message it didn’t know how to read.)
* Network-wide event subscription (through persistent “listeners”)
* Massive interoperability, reusability, mashability, and composability
* Ensuring fractal coherence (This needs a paper of its own to explain why it’s important.)

Some of Ceptr is operational, some is barely operational code-scaffolding, and some is yet to be built (especially these next topics). And we could use some support designing good implementation strategies for some of these things.

**Hierarchal Deterministic Keys and Key Management:** Since every agent that wants to communicate on the Ceptr Network gets its own address and keys for signing & encryption, we’d love ideas for making it easy for people to manage a lot of keys. Also, in many configurations we’d like to use hierarchal keys (e.g. a master receptor and with synched slave instances, an agent/person and the receptors they create (whether a standalone receptor or sharded peers). 

**Capabilities-Based Security:** Any tips, tricks, techniques or warnings about using capabilities-based security tokens + authorized users (Ceptr messages are always signed/authenticated by source), building appropriate chains, enforcing at appropriate times/sequences.
Lightweight Signing & Multi-Party Signatures: Every network message in Ceptr is signed. We’d like to keep that as light as possible. We also would like build a few multi-party signature scenarios into our BFT algorithms.

**Resource Balancing in Distributed Systems with Diverse Capacities:** When you have a handful of receptor instances with different resources (CPU, GPU, bandwidth, storage, network centrality, etc.), are there existing tools algorithms for “load balancing” based on these capacity differentials?

## Ceptr Identity and Web of Trust

**Network addresses** in Ceptr are permanent IDs associated with the agent (person, program, or legal entity) communicating on the network. These UUIDs have a history and are accountable for their activities. Addresses are not temporary, reassigned, or segmented for routing. 

We use a **progressive trust** approach, where people are able to self-assert into the network as an anonymous client. Later they may upgrade via a triangulation/vouching process to create a trusted peer address. When they register their address (from a sparse UUID space) on the network, they must publish a public key (to a sharded DHT), and may provide a public key-server address, revocation-server address, and identity server address. Identity information can be selectively shared via capacity-based tokens. 

Nodes on the network can configure their own **thresholds for serving or routing traffic** (whether to service requests from anonymous clients, or addresses with a history of spamming – based on activity/reputation metrics built into the Ceptr routing protocols. For example, to extend battery life and preserve bandwidthy I'd probably set higher filtering thresholds on Ceptr running on my mobile phone than my cloud server or my plug computer at home.

Since every Ceptr Network message is signed with the public key of the sender you can authenticate the message source. **Confirming the sender's identity** can be done by means of their authorized identity service(s). We expect Ceptr to have a rich ecosystem of capabilities-based identity services from peers and trusted authorities, ranging from validating a pseudonym to confirming government issued passport/citizenships/voter registration or financial/credit reporting. Users can control access via capabilities tokens and manage rights and restrictions on shared information via smart contracts. 
