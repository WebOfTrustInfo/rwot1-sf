A cool hack with XDI graphs, blockstore, link contracts, and cryptographic identifiers
--------------------------------------------------------------------------------------
Markus Sabadello, Vienna, October 19th 2015

XDI Graphs
----------

XDI (eXtensible Data Interchange) is a semantic graph technology for modeling, accessing, and linking any data online. It is similar to RDF insofar as it is also based on triples describing a graph of nodes that represent resources (called "contexts" in XDI), properties that connect resources (called "relations" in XDI), and literals. Unlike RDF which uses opaque URIs (mostly HTTP) as identifiers and which constructs all semantics purely from the graph structure, XDI identifiers use an abstract syntax where semantics are established not only from graph structure, but also from the identifiers themselves. For example, in RDF an identifier for a person may be **http://danubetech.com#markus**, whereas in XDI, an identifier for a person would be **=markus**. XDI often assigns two or more identifiers to a resource, e.g. while **=markus** is considered a "reassignable XDI name", a corresponding "permanent XDI number" such as **=!:uuid:91f28153-f600-ae24-91f2-8153f600ae24** may also be assigned. Simply by parsing the identifiers, some limited semantics can already be extracted ("=" stands for person, "!" stands for permanent).

Since XDI identifier syntax does not use domain names and IP addresses, XDI also needs its own framework for registration and discovery. Given an XDI identifier, an "XDI endpoint" can be discovered which contains an XDI authority's graph. XDI endpoints and their graphs may be controlled by persons, organizations, or things. Given this information, participants of an XDI network (called "XDI peers") can begin to interact, connect, and exchange arbitrary data using the XDI messaging protocol.

Example XDI semantic graph data:

	=markus/#friend/=christopher
	=markus<#email>/&/"markus@danubetech.com"

Blockstore
----------

Historically, XDI infrastructure began by using a centralized registry model. Since this was independent of DNS and had its own commercial component, this infrastructure has been subject to criticism by various communities. After this model collapsed in late 2014, the non-profit XDI.org formed a group called the XDI Registry Working Group to begin developing a distributed blockchain-based solution. Initially, we built a PoC based on simple OP_RETURN Bitcoin transactions, where given an XDI name, its corresponding XDI number and XDI endpoint can be looked up.

Example Bitcoin [transaction](https://testnet3.toshi.io/api/v0/transactions/b6ce84b395a9c8f146fd75f5cd980dea6efbac4601f346ee19f0e39a16c7f48d) with XDI name registration (some details removed for brevity):

	{
	  "hash":"b6ce84b395a9c8f146fd75f5cd980dea6efbac4601f346ee19f0e39a16c7f48d",
	  "version":1,
	  "outputs":[
	    {
	      "amount":1638,
	      "spent":false,
	      "script":"OP_RETURN 584449030337e7d205564ff2b0586299627488dfea35c4abf1d15e173accf46c8a10ca26 OP_RETURN 3d91f28153f600ae2491f28153f600ae24 OP_RETURN 68747470733a2f2f78646930332d61742e64616e756265636c6f7564732e636f6d2f636c2f253542 OP_RETURN 2533442535442532312533417575696425334139316632383135332d663630302d616532342d3931 OP_RETURN 66322d383135336636303061653234",
	      "script_hex":"6a24584449030337e7d205564ff2b0586299627488dfea35c4abf1d15e173accf46c8a10ca266a113d91f28153f600ae2491f28153f600ae246a2868747470733a2f2f78646930332d61742e64616e756265636c6f7564732e636f6d2f636c2f2535426a282533442535442532312533417575696425334139316632383135332d663630302d616532342d39316a0f66322d383135336636303061653234",
	      "script_type":"unknown"
	    }
	  ]
	}

After this, we started to look at Blockstore, which offers a higher-level set of name registration operations based on the Bitcoin blockchain as well as a pluggable external storage system such as the well-established Kademlia DHT. We therefore created a second PoC where we "preordered" and "revealed" the **.xdi** namespace within Blockstore's "testset" environment. Within this namespace, we registered an XDI number with a record that contains not only the associated XDI endpoint, but also various forms of Proof-of-Ownership.

Example Blockstore blockchain record for XDI number **=!:uuid:91f28153-f600-ae24-91f2-8153f600ae24**, which because of length limitations is encoded to the key **_eux8n200r9u7vvhl2s78igyq9wdg.xdi**:

	# blockstore-cli get_name_blockchain_record _eux8n200r9u7vvhl2s78igyq9wdg.xdi
	[
	    {
	        "address": "1FgeuAw6MFY6VVqFGcza4kB18WFuLpEkLY",
	        "first_registered": 377454,
	        "last_renewed": 377454,
	        "revoked": false,
	        "sender": "76a914a1119ed24038b2b89e16e309c92ac2c3ef8016fa88ac",
	        "sender_pubkey": "02de282d770f9e0de9ce6bbb41774c3da0e79350a067b5acda9bb596b4c530ecfe",
	        "value_hash": "86cc5e2b695c518459de751c8e7059562a01710f"
	    }
	]

Example Blockstore DHT information:

	# blockstore-cli get_name_record _eux8n200r9u7vvhl2s78igyq9wdg.xdi
	{
	    "name": {
	        "formatted": "=!:uuid:91f28153-f600-ae24-91f2-8153f600ae24"
	    },
	    "endpoint": "https://xdi03-at.danubeclouds.com/cl/%5B%3D%5D%21%3Auuid%3A91f28153-f600-ae24-91f2-8153f600ae24",
	    "registrar": "+!:uuid:02f30164-997d-4184-b949-5ca1ab1eda7a",
	    "secret": "$6$Yds8Rr4X$YKL7z0CYtNMXE9do/y2ZshUaoADH1BvyXqr/Cf0b2drGt6FZBjfVi",
	    "signature": "CAQ8AMIIBCgKCAQEAh2BVeQPj3lWDjx9n1HfXWsCOtyF2oEtVxVWrrQnGK1lihhBF5GSkQV149H/nqRvyBwdg8vG4J7UMaeYGbSpz/OKfF8Jr2o4rHi3qSFzW2/UXAtEdiwis/N6lJcHGepBscJuu0fHSI/IHdMpHYurTy4AAQihNIc41ZHcwqUAoGkaZbb38d733TGwj17PvBI0XtHV+6Xqt",
	    "v": "1"
	}

This PoC is available at http://xdi.space/.

Link Contracts
--------------

Once XDI identifiers and their associated XDI endpoints are known, it becomes possible to access, connect, and modify data in the XDI network. In order to control which operations are possible, XDI link contracts are used. Link contracts are established between "authorizing authorities" and "requesting authorities". They contain sets of permissions that are granted if a certain policy is satisfied. Policies can express a variety of conditions such as membership in a group, or requirements for authentication, signatures, encryption, etc.

The following is an example of an XDI link contract issued by =julia to =romeo that allows =romeo to read =julia's e-mail address if he presents a valid signature:

	(=julia/=romeo)$do/$get/=julia<#email>
	(=julia/=romeo)($do$if$and/$true){$from}/$is/=romeo
	(=julia/=romeo)($do$if$and/$true){$msg}<$sig><$valid>/&/true

In the early days of XDI, we had been assuming that every XDI authority has one or more associated key pairs (we have mostly been using 2048 bit RSA), which can be obtained from an XDI endpoint, which in turn can be discovered given the XDI name or number of the authority.

For example, a public signing key associated with =romeo is expressed as follows:

	=romeo$msg$sig$keypair<$public><$key>/&/"MIIBIjANB...cwIDAQAB"
	=romeo$msg$sig$keypair/$is#/$rsa$2048

When =julia receives a request from =romeo to retrieve her e-mail address, the following steps happen:

1. =julia's XDI endpoint parses the incoming message and finds a signature as well as the identifier of the sender =romeo.
2. Given the XDI identifier, =julia discovers =romeo's XDI endpoint.
3. From =romeo's XDI endpoint, =julia retrieves (and caches) =romeo's public signing key.
4. =julia validates the signature on =romeo's message, evaluates the link contract policy, and grants access.

Cryptographic Identifiers
-------------------------

Recently, we started experimenting with "cryptographic XDI numbers", which are XDI identifiers that are constructed directly from a public key. This can eliminate the XDI discovery step as well the need for a-priori relationships or round trips between the XDI peers, and therefore enables immediately secure XDI connections (this is also known as a [NIKE](https://eprint.iacr.org/2012/732.pdf) technique). The first generation of cryptographic XDI numbers is based on Ed25519 32 bit public keys and uses the [cid-1 XDI scheme](https://github.com/projectdanube/xdi2-crypto-ec25519).

Example cid-1 cryptographic XDI number:

	=!:cid-1:x3Yps9M3Cc5yBtrdR1dcjfddBtFa2VLDpYhgnHbwztsdaeH9e4w

After this, we looked at hierarchical deterministic keys as pioneered by the [BIP-32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) proposal, where key pairs can have verifiable tree relationships. This enables interesting scenarios where e.g. an XDI authority can have a discoverable extended key pair, and this XDI authority can enroll XDI agents such as smartphone apps which have key pairs derived from the XDI authority's key pair. XDI link contracts can then be established between XDI authorities that accept the other authority's key, or one derived from it.

In order to organize the tree of key pairs, a schema similar to the one described by [BIP 44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) should be put in place. For example, the following levels may make sense:

m / purpose' / identity system' / account' / account-endpoint' / agent-type' / agent(') / session

* m (hardened) is the master key pair, created from a seed
* purpose (hardened) is set to constant 9, meaning keys used for personal identity services
* identity system (hardened) is set to constant 120 (ASCII for 'x'), meaning XDI
* account (hardened) is an abstract root of one's personal identity, which is not actually represented in XDI
* account-endpoint (hardened) is used to create extended public key XDI numbers identifying an XDI authority with an associated XDI endpoint
* agent-type (hardended) describes the type of XDI agent that may have more or less cryptographic abilities, e.g. 0=non-delegatable (hardened key), 1=delegatable (non-hardened key), 2=agents that can only sign, 3=agents that can only encrypt
* agent (hardened or non-hardened depending on agent-type) is used to create public key XDI numbers identifying XDI agents such as a smartphone app or IoT device
* session (non-hardened) optionally for app-specific purposes such as creating messaging sessions

Based on this approach, we are now working on the [cid-2 XDI scheme](https://github.com/projectdanube/xdi2-crypto-secp256k1).

Example cid-2 cryptographic XDI numbers:

	Seed:
	crazy horse battery staple
	
	Account #1 endpoint #1 (key path m/9'/120'/1'/1'):
	=!:cid-2:xpub6F9Ytjev4vdChPvABxd645LspyrQhQqMajajMBSpmvizubb7JXHr3hmWmeUnoehaks1LZjnsBbWfxPDFEUTGedzKxYRS1WjYvjDXJZQk3ur
	
	Agent type #1 agent #1 (key path m/9'/120'/1'/1'/1'/1):
	=!:cid-2:1GpKLiTq79fFgdHLvFyAz2tdpzSjtcGs2M

Given these XDI numbers, we set up a PoC where one XDI peer creates a link contract that allows another XDI peer to access data from any of its agents.

	SEED -----
	          |  m/9'/120'/1'/1'
	          |
	          |            ___________________ 
	          |           |                   |
	          |  register | Blockstore        | lookup
	          |    ---->  |___________________|  <----
	          v   |                                   |
	 ___________________                         ___________________
	| =romeo's endpoint |                       | =julia's endpoint |
	| =!:cid-2:xpub6F9Y |  ==================>  | LINK CONTRACT     |
	|___________________|                       |___________________|
	
	          |
	          |  m/9'/120'/1'/1'/1'/1
	          v
	 ___________________
	| =romeo's agent    |
	| =!:cid-2:1GpKLiTq |
	|___________________|

Example link contract at =julia's XDI endpoint:

	(=julia/=romeo)$do/$get/=julia<#email>
	(=julia/=romeo)($do$if$and$or/$true){$from}/$is/=!:cid-2:xpub6F9Ytjev4vdChPvABxd645LspyrQhQq...
	(=julia/=romeo)($do$if$and$or/$true){$from}/$is#derived$key/=!:cid-2:xpub6F9Ytjev4vdChPvABxd645LspyrQhQ...
	(=julia/=romeo)($do$if$and/$true){$msg}<$sig><$valid>/&/true

Example XDI message from =romeo's XDI agent to =julia's XDI endpoint:

	(=!:cid-2:1GpKLiTq79fFgdHLvFyAz2tdpzSjtcGs2M)/$send/=romeo[$msg]*!:uuid:1234
	=romeo[$msg]*!:uuid:1234/$is()/(=julia)
	=romeo[$msg]*!:uuid:1234/$do/(=julia/=romeo)$do
	=romeo[$msg]*!:uuid:1234<$sig>/&/"bc40b0958be89..."
	=romeo[$msg]*!:uuid:1234$do/$get/=julia<#email>

The message's sending XDI peer is =romeo's XDI agent identified by the cryptographic XD number **=!:cid-2:1GpKLiTq79fFgdHLvFyAz2tdpzSjtcGs2M**. Since =julia's link contract is set up to grant access to any of =romeo's derived keys, =romeo could use a different XDI agent or change keys without the need to inform =julia of this change.

Acknowledgements
----------------

This work is heavily based on input by Christopher Allen as well as the XDI.org Registry Working Group. Thank you
also to the Blockstore team for their support in developing the PoC.
