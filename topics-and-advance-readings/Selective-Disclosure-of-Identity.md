# Selective Disclosure of Identity with Hierarchical Deterministic Keys and JSON Web Tokens

Identity information can be packaged together, as it is with traditional forms of identification like passports and driver's licenses, or it can be fragmented and selectively disclosed.

Identity fragmentation and selective disclosure has huge benefits for privacy. If a service only requires a singly piece of information on a user, like a liquor site that needs to know if a user is of age, the service can ask the user to present a statement of age that has been self-attested AND has been attested to by a party that the service trusts, whether that be a DMV, a corporation or an individual. This allows the person to prove he/she is of age without revealing his/her identity.

### Signed Identity Tokens

With [v3 of the Blockchain ID schema](https://github.com/blockstack/blockchain-id/wiki/Profile-Schema-v3), [user profile information](https://github.com/blockstack/blockchain-id-js/blob/master/docs/profile.md) is split up into individual signed statements that are expressed as JSON Web Tokens and packed up in a ["token file"](https://github.com/blockstack/blockchain-id-js/blob/master/docs/token-file.md). The tokens are each individually signed with different keys, so that each identity statement has a different issuing cryptographic identity. Then, to reconstruct the profile, the user presents all of the tokens and presents proof that he/she signed those tokens.

### Hierarchical Deterministic Key Derivation

The way we do this is have each Blockchain ID username registered be tied to a hierarchical deterministic public key. Then, for each token presented, the derivation path (aka the chain path which is expressed as a hash) is provided that leads from the parent HD public key to the descendant HD public key (via unhardened key derivation) that has an accompanying public key that matches the issuer. Each derivation path has a very high amount of entropy, ensuring that the descendants cannot be discovered via brute force derivations from the master key. The chain path is required.

### Identity Resolution

A name is securely linked to a zone file in Blockstore. The hash of the zone file is stored in the OP_RETURN field of the update transction, and the data itself is stored in the DHT. The zone file contains instructions for the client to resolve the user's token file, which contains tokens that can be combined to reconstruct the user's profile. Individual tokens can be encrypted or omitted from the main file in order to make sure they are not associated with the user's central identity.

### Interesting Implications

+ individual identity statements can be presented by an anonymous user, then the user can later identify oneself by simply presenting a hash
+ the "double spend" problem of identity proofs is solved whereby users cannot share their keys that have been verified to be "over 21" because sharing an unhardened descendant key of a master public key means that the master public key will be shared as well

### Resources

+ [JSON Web Tokens](http://jwt.io/)
+ [Blockchain ID Profile Schema v3](https://github.com/blockstack/blockchain-id/wiki/Profile-Schema-v3)
+ [Reconstructed Profile Example](https://github.com/blockstack/blockchain-id-js/blob/master/docs/profile.md)
+ [Profile Token File Example](https://github.com/blockstack/blockchain-id-js/blob/master/docs/token-file.md)
+ [Zone File Example](https://github.com/blockstack/blockchain-id-js/blob/master/docs/zone-file.md)
