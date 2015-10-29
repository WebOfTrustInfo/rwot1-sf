Hierarchical Deterministic Keys: BIP32 & Beyond
===============================================
By Christopher Allen - <ChristopherA@LifeWithAlacrity.com> & Shannon Appelcline - <ShannonA@skotos.net>

When Bitcoin debuted it revealed one characteristic that was very different from the world of traditional PKI: a proliferation of keys. As used in PGP, in X.509 certificates used by TLS, and in other protocols, the number of private keys are few and they they do not expire for many years.

Instead, to maximize privacy Bitcoin rapidly cycles through keys, discarding old keys from past transactions as soon as the public key is revealed and the coins are spent. Since each address is hashed from a public key, this means that a Bitcoin user needs to deal with a large lot of keypairs. The traditional answer for this problem has been wallets — which collect and manage keys so that users don’t have to.

The earliest Bitcoin wallets still faced challenges. That’s because the Bitcoin Core and early clients generated each key randomly. Unfortunately, this methodology requires careful (and constant) backups to ensure continued access to all funds. It also opens some privacy loopholes; because new key generation wasn’t trivial, single keys were often reused when they shouldn't have been. Transactions could be correlated if they used the same address (and thus keypair) for change, requiring even more keys.

A bit over two years ago, this standard methodology began to change with the advent of BIP32, which laid out a new model for Hierarchical Deterministic Keys (HDKs).

* **Deterministic** means that keys are no longer created randomly, but instead generated as part of a linked chain. Regular backups are no longer required as long as the private-key seed that created the chain is safe. This makes key management very simple, and even allows easy caching the master key in a paper wallet or cold storage--only having child keys stored on more vulnerable computer hardware.

* **Hierarchical** means that the chain of keys is ranked so that lower-rank keys cannot reveal information about their higher-ranked brethren. This also allows selective sharing of public keys for auditing purposes.

BIP32 implements HDKs using the secp256k1 curve to create an ordered tree of 512-bit extended keys — each of which contains both a 256-bit public key and a 256-bit chain code. Below the root of the tree are extended child keys that are derived from a parent public key, a parent chain code, and an index number. New-style HD wallets are then be used to hold these extended keys.

One of the advantages of BIP32 is that new child public keys can be created exclusively from the child’s extended key (its public key + its chain code), allowing for considerable expandability without ever knowing any private key. Of course, the parent’s private key can also be used to create this derivation (and to determine child private keys).

This leads to an obvious drawback: if a child’s private key is leaked and combined with the child’s chain code, that can be used to reveal all the private keys of the children. Worse, if the child’s private key is combined with the parent’s chain code, it can be used to figure out the private key of the parent!

To resolve this, HD wallets can use an alternative hardened derivation of HDKs, which combine the parent’s private key (rather than its public key), the parent’s chain code, and an index number. Though this hardened derivation sacrifices one of the important elements of HDKs (the ability to generate children without a private key), it’s important for the security of the most important keys in a hierarchy. Since hardened and normal derivations can be combined in a wallet, it’s become standard to use hardened derivations for the root and the specific key levels of an HD wallet.

A number of additional Bitcoin Improvement Proposals have built on the ideas of HDKs.

**BIP39** describes a methodology for generating word lists that can be used to easily recreate the root of a HDK hierarchy.

**BIP43** expands on the structure that was introduced for HD wallets in BIP32. It suggests that the first tier should always be used to define a “purpose”, which describes the structure of the other tiers and the keys in the hierarchy.

**BIP44** then offers a default structure (“purpose”) for HD wallets, to help standardize their usage. Combining the ideas from BIP32 and BIP43, it lays out the following organization:

    m / purpose' / coin_type' / account' / change / address_index

Each of these divisions represents a new level of the keypair hierarchy, with tiers marked with a ' being levels that are hardened. The standard format for BIP44 is then:

    m/44'/0'/0'/0/0

This means:

* Purpose: 44 (aka BIP44), hardened

* Cointype: 0 (0 for Bitcoin, but could be others), hardened

* Account: 0 (user account), hardened

* Change: 0 (addresses for change), unhardened to allow creation of child keys

* Address Index: 0 (the first key)

The Future
----------

Though BIP44 nicely brings together much of the previous work on HDKs, there is still considerable room for expansion of HDK's capabilities.

We can  improve the core functionality of HDKs:

* **Different Curves:** HDKs should be possible with curves other than secp256k1. They would be particularly useful with curve 25519. There also has been some interesting provably secure concepts by Eduarda Friere for HD keys that use quantum-resistant lattice cryptography, some of maybe can be brought into elliptic curves.

* **HDK Security:** There’s been some research into preventing key leakage when multiple keys are revealed. Using M of N multisignatures might resolve the security issues that rise up when both a key and a chain code are revealed. Gutoski and Stebila propose a different technique. These approaches need more examination and analysis.

We can use it for better key management:

* **Improved Delegation:** HDKs give us considerable ability to delegate actions out to the cloud without sacrificing security — such as by only giving a child key to an iPhone. The key could then be discarded if the phone was lost or compromised, without having to recreate a root key. We could even have each session have its own key.

* **Rotation & Revocation:** Child keys can be rotated. Parent keys can revoke child keys.

There’s also the opportunity to use HDKs for more than Bitcoin transactions, taking the advantages of hierarchy, ease-of-key-creation, and ease-of-storage into additional fields:

* **One-Time Auth:** Parts of the HDK structure could be used to create one-time authentication keys for various web sites. You could log into Google two billion times without ever repeating yourself!

* **Independent Signatures:** HDKs provides the ability to use different hierarchical branches for encryption and for signing so that the same key is not used for both.

* **Hierarchical Identity:** Parts of the HDK structure could be specifically designated for identity. Techniques for storing master keys (paper wallets, BIP38 phrases, cold storage, etc.) can be used to protect identity.

* **Increased Privacy:** Pseudo-anonymous branches can be revealed later to belong together under the same parent. One-time signatures can used with group and ring signatures for additional privacy.

Each of these topics deserves more attention — to see what improvements they could create for the Web of Trust and to determine what their repercussions would be.

References
----------

Antonopoulos, Andreas M.  “Chapter 4: Keys, Addresses, Wallets”. Mastering Bitcoin. 2015. http://chimera.labs.oreilly.com/books/1234000001802/ch04.html#hd_wallets.

Freire, Eduarda and Simoes Veloso. “Non-Interactive Key Exchange and Key Assignment Schemes”. 2014. http://www.isg.rhul.ac.uk/~kp/theses/EFthesis.pdf.

Gutoski, Gus and Stebila, Douglas. “Hierarchical deterministic Bitcoin wallets that tolerate key leakage”. Cryptology ePrint Archive. 2015. https://eprint.iacr.org/2014/998.pdf

Palatinus, Marek, Pavol Rusnak, Aaron Voisine, and Sean Bow. “BIP39: Mnemonic Codes for Generating Deterministic Keys”. 2013. https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki.

Palatinus, Marek, and Pavol Rusnak. “BIP43: Purpose Field for Deterministic Wallets”. 2014. https://github.com/bitcoin/bips/blob/master/bip-0043.mediawiki.

Palatinus, Marek, and Pavol Rusnak. “BIP44: Multi-Account Hierarchy for Deterministic Wallets”. 2014. https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki.

Wuille, Pieter. “BIP32: Hierarchical Deterministic Wallets”. 2012. https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki.
