# XDI Link Contracts: An Overview
By Drummond Reed, Co-Chair, OASIS XDI Technical Committee, drummond@respect.network

One of the challenges in a distributed peer-to-peer data network, such as a web of trust, is how any two peers can quickly and easily negotiate a data sharing agreement, i.e., a human- and machine-understandable (and enforceable) description of what data the publisher is sharing with the subscriber under what permissions and conditions. Additional challenges include:

1. How can the parties to the data sharing agreement identify and authenticate each other such that they can safely interact for the period of time it is effective?
2. How can such a data sharing agreement be portable, so the parties are not dependent on any particular app or service provider to enforce it?
3. How can such a data sharing agreement be adaptable to different security and privacy policies, so it is not obsoleted as new technologies arrive?

This paper briefly describes the solution to these problems developed by the [OASIS XDI (Extensible Data Interchange) Technical Committee] (http://www.oasis-open.org/committees/xdi/) as part of the XDI 1.0 suite of specifications for semantic data interchange.

## The Four Steps to an XDI Link Contract

### Step 1) XDI Graphs: Addressable Semantic JSON
The first step is to establish a semantic graph model that provides a standard way to persistently address any data asset (from a single data element to an entire database) in the context of any data authority, container, or context for that data asset. To do this, the XDI graph model uses the same subject-predicate-object triples model as RDF, but adds: a) a standard predicate for modeling context, and b) the requirement that all contextual predicates be unique in the scope of their parent node. This addressable semantic tree model is the heart of XDI.

The four levels of the XDI semantic tree model are summarized by the acronym REAL (Root-Entity-Attribute-Literal). They are serialized in JSON using four levels of nested JSON objects. Each of these JSON objects has a unique global address. Any node that has a reassignable (mutable) address (called an *XDI name* or *i-name*) can be mapped to a node that has a persistent (immutable) address (called an *XDI number* or *i-number*).

Following is an example XDI graph with some typical profile data for a person (Alice). Alice’s graph also includes a reference to the peer graph for another person (Bob). The i-numbers use the XDI UUID scheme, and the i-names use the “x-” prefix reserved for examples.
```
{
    "/$is$ref": [
        "(=x-alice)",
        "(=!:uuid:33ad7beb-1abc-4a26-b892-466df4379a51)"
    ],
    "<$iri>": {
        "&": "https://xdi.example.com/=!:uuid:x-bob/"
    },
    "=!:uuid:33ad7beb-1abc-4a26-b892-466df4379a51": {
        "/#friend": [
            "=!:uuid:f336a645-f5a9-41b7-ab80-ace41a8f69c2"
        ],
        "<#home><#email>": {
            "&": "alice@example.com"
        },
        "<#work><#email>": {
            "&": "alice.roth@example.net"
        },
        "<#personal><#email>": {
            "/$ref": [
         "=!:uuid:33ad7beb-1abc-4a26-b892-466df4379a51<#home><#email>"
            ]
        }
    },
    "=!:uuid:33ad7beb-1abc-4a26-b892-466df4379a51#passport": {
        "<#country>": {
            "&": "Canada"
        },
        "<#name>": {
            "&": "Alice Roth"
        },
        "<#num>": {
            "&": "1234567"
        }
    },
    "(=!:uuid:f336a645-f5a9-41b7-ab80-ace41a8f69c2)": {
        "/$is$ref": [
            "(=x-bob)"
        ]
    }
}
```
### Step 2) XDI Link Contracts: Standard Subgraphs for Authorization

The second step is to use this addressable semantic tree model to represent data sharing agreements. Each such agreement is between the publisher of the data, called the *authorizing authority*, and a party who wants to access the data, called the *requesting authority*. Because the agreement links these parties to the data covered by the agreement—and also binds them to the terms of the agreement just like a real-world contract—the XDI Technical Committee calls this XDI subgraph a *link contract*.

The root node of an XDI link contract is an XDI entity identified with the reserved class name `$do` (chosen because a link contract is a machine-readable description of what an authorizing authority permits a requesting authority to do with the described data).

A `$do` node may appear anywhere inside the subgraph of an authorizing authority node. Such a link contract is owned and controlled by that authorizing authority. Like a real-world contract, the contract terms control if the terms are fixed (no changes can be made by any party), unilateral (only the authorizing authority can make changes), or bilateral (changes require the consent of all parties).

### Step 3) XDI Permissions: Semantic Relations to Data Nodes

With an addressable semantic tree model, permissions can be represented by XDI relations between the `$do` node and the XDI subgraph(s) containing the data that is the object of the permission. This can be thought of as the graph-based equivalent of an [ACL](https://en.wikipedia.org/wiki/Access_control_list), but with much richer and more extensible semantics. For example, the following XDI statement (using i-names for simplicity) is how a link contract from Alice could provide permission to read (`$get`) her home phone number.


Subject | Predicate | Object
------- | --------- | ------
=x-alice#friend$do | $get | =x-alice<#home><#phone>

The XDI Technical Committee defines a standard set of XDI predicates for graph operations.

Operation | Description
--------- | -----------
$get | Read statements in a subgraph
$set | Write statement to a subgraph
$add | Add statements to a subgraph
$mod | Update a literal value
$del | Delete statements from a subgraph
$connect | Instantiate a link contract
$send | Send an XDI message
$push | Publish an XDI message to subscribers
$do | Authorize other operations

XDI developers can specialize the $do operation to extend the XDI operation vocabulary to encompass any operation for which a link contract needs to control permission.

### Step 4) XDI Policies: Semantic Logic Trees for Authorization

The final step is to express the set of policies that an requesting authority must satisfy in order to be authorized under a link contract. This is the XDI equivalent of [XACML](https://en.wikipedia.org/wiki/XACML), the XML-based policy expression language published by the OASIS XACML Technical Committee. In fact, XDI link contracts can reference external policies and policy engines like XACML to make policy evaluations. Alternatively, policies can be expressed and evaluated directly in XDI.

XDI policies may specify any set of terms and conditions relevant to making an authorization decision, including requirements for identification, authentication, encryption, digital signatures, synchronization, and termination of the link contract. They can also govern privacy by specifying authorized uses of shared data.

XDI policies may also bind the authorizing authority. For example, a link contract may require that the authorizing authority sign and encrypt XDI messages containing data updates that are pushed to a requesting authority.

XDI policies are specified in the `$do$if` branch of a link contract. Policies may be combined into a boolean logic tree of arbitrary complexity using `$and`, `$or`, and `$not` statements. In the following example, Alice’s graph has added a link contract that gives Bob `$get` access to her home email address provided Bob’s XDI request satisfies two policy conditions:

1. Alice’s graph asserts that Bob is a friend of Alice.
2. Bob’s XDI message has a valid signature.

Note that the i-number UUIDs have been shortened to x-alice and x-bob for readability.
```
{
    "/$is$ref": [
        "(=!:uuid:x-alice)"
    ],
    "<$iri>": {
        "&": "https://xdi.example.com/=!:uuid:x-bob/"
    },
    "=!:uuid:x-alice": {
        "/#friend": [
            "=!:uuid:x-bob"
        ],
        "<#home><#email>": {
            "&": "alice@example.com"
        },
        "<#work><#email>": {
            "&": "alice.roth@example.net"
        },
        "<#personal><#email>": {
            "/$ref": [
                "=!:uuid:x-alice<#home><#email>"
            ]
        }
    },
    "(=!:uuid:x-alice/#friend)": {
        "=!:uuid:x-alice#friend$do": {
            "/$get": [
                "=!:uuid:x-alice<#home><#email>"
            ]
        }
    },
    "(=!:uuid:x-alice/#friend)(=!:uuid:x-alice#friend$do$if$and/$true)": {
        "{$from}": {
            "/$is#friend": [
                "=!:uuid:x-alice"
            ]
        },
        "{$msg}": {
            "<$sig><$valid>": {
                "&": true
            }
        }
    }
}
```
## Negotiation of XDI Link Contracts

Although any XDI authority may write a link contract directly into its graph to grant permissions to any other XDI authority, in practice link contracts are produced via an exchange of XDI messages between the requesting and authorizing authorities. This is the machine equivalent of how most real world contracts are negotiated. This exchange of messages has enough permutations that it is being defined in a separate specification from the XDI Technical Committee called *XDI Connections 1.0*.

## Conclusion

Building on the “flat” RDF semantic graph model, XDI defines an addressable semantic tree of data. This semantic tree enables a special type of subgraph, an XDI link contract, that can standardize how any two peers can arrive at an interoperable, portable data sharing agreement. This agreement can authorize any operation that can be defined with an XDI relation and can govern any data that can be referenced with the XDI graph model, including pointers to any Web-addressable resource. A link contract can also be governed by policies written in XDI or in any Web-addressable policy engine. The XDI protocol will also specify how link contracts can be negotiated between arbitrary peers, enabling a fully decentralized web-of-trust.

## Questions for the Web-of-Trust Group

* How can we best can we use link contracts and XDI graphs to facilitate your web-of-trust needs?

* Link contracts are currently express policy statements, enforced by legal agreements and law. How best can we adapt them to use more cryptography to enforce the contracts? Are there smart contract and ring and threshold signature possibilities?

* Link contracts have additional value when supplemented by proof-of-existence. How best can we anchor link contracts in blockchain to add PoE?

## References

Joseph Boyle, Drummond Reed, Markus Sabadello. "XDI Core 1.0 Working Draft 06" (voted to become Committee Specification Draft 01). OASIS XDI Technical Committee. October 2015. http://xdi.org/xdi-spec-docbook/xdi/xdi-core-1.0/xdi-core-1.0-wd06.xml

Richard Cyganiak, David Wood, Markus Lanthaler. "RDF 1.1 Concepts and Abstract Syntax". W3C Recommendation. February 2014. http://www.w3.org/TR/rdf11-concepts

Dan Brickley, R.V. Guha. "RDF 1.1 Schema". W3C Recommendation. February 2014. http://www.w3.org/TR/rdf-schema

Antoine Zimmerman. "RDF 1.1: On Semantics of RDF Datasets". W3C Working Group Note. February 2014. http://www.w3.org/TR/rdf11-datasets

Erik Rissanen. "eXtensible Access Control Markup Language (XACML) Version 3.0". OASIS Standard. January 2013. http://docs.oasis-open.org/xacml/3.0/xacml-3.0-core-spec-os-en.pdf
