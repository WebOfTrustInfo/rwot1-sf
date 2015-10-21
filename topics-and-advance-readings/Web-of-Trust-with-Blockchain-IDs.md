# Web of Trust with Blockchain IDs

Signed statements with a clearly defined schema can be used to have people and companies refer to one another and make attestations about their identities and their relationships.

PGP's web of trust uses a form of this, but it is fairly primitive and lacks widely accepted standards.

Blockchain ID identity statements can be used for a form of web of trust.

All parties involved in the statement, including the issuer and the subject of the statement can locally cache the statements and present them to others as needed.

Statements can be revoked using updating one's zone file on Blockstore and appending a hash of the statement to a list of revoked statements.

### Examples of Identity Statements

#### Relationships to Other People

```json
{
    "header": {
        "typ": "JWT",
        "alg": "ES256"
    },
    "payload": {
        "claim": {
            "knows": [
                {
                    "@type": "Person",
                    "id": "muneeb.id"
                }
            ]
        },
        "subject": {
            "@type": "Person",
            "publicKey": "032ecde4397fa473f1ce482cea6235eb0c20b3ce4c010a669034422800bbcd491d"
        },
        "issuer": {
            "@type": "Person",
            "publicKey": "032ecde4397fa473f1ce482cea6235eb0c20b3ce4c010a669034422800bbcd491d"
        }
    },
    "signature": "snFhetKhj3uwoVDXXKk5w7wxVpkeTBFjhE-J0s9zkqM9-ZcG7oD1_hi7fBXiLdvgwgbqQJ9VvbYQfTukaiedaQ"
}
```

#### Employment by an Organization

```json
{
    "header": {
        "typ": "JWT",
        "alg": "ES256"
    },
    "payload": {
        "claim": {
            "worksFor": [
                {
                    "@type": "Organization",
                    "id": "onename.id"
                }
            ]
        },
        "subject": {
            "@type": "Person",
            "publicKey": "02f6a64a75c4094889c181ff9e4b59a79c770523890dacebb025755900bedb768b"
        },
        "issuer": {
            "@type": "Person",
            "publicKey": "02f6a64a75c4094889c181ff9e4b59a79c770523890dacebb025755900bedb768b"
        }
    },
    "signature": "Ygif2h6hw2JjOJ2WTQhgwCkpvq1xngpBWYLiyvuX88HQPJjEtSAxGtWfaxPQK8u5TAVV7GSJ96kMBX38HR3WXA"
}
```
