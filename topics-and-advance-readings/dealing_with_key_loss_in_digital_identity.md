# Dealing with private key loss or compromise in digital identity systems

By Christian Lundkvist [@ChrisLundkvist](https://twitter.com/chrislundkvist) \<christian.lundkvist@consensys.net\>

## Introduction

If an identity is tied to a single persistent private key, then loss
or compromise of the private key will mean total loss of the
identity. Since key compromise and/or loss do happen there needs to be
a way to recover from this in order to have a persistent digital
identity. See [here][definitions] for definitions used.

## Key revocation and rotation

If the user of the identity suspects that a key is or may be
compromised the user can rotate their key by submitting a new key to
the system, signed by the old key. After this the old key can be
revoked. An example of how key revocation can work in Ethereum is
[here][keyrev].

## Key loss

To deal with the case where a user completely loses control of the key
a multisig system can be put in place where the user preemptively
selects `N` "delegate" identities that are empowered to allow the key
of the identity to be changed if `N` delegates provide their
signatures. An example of this kind of key reset mechanism is
[here][keyreset].

## Timeouts and dealing with takeover attempts

In the previous [example][keyreset] of a decentralized key reset
procedure a timeout was introduced where the original key can stop a
key rotation from taking place using a timeout. There can be a contest
period where the old key can stop the key rotation if the key rotation
was initiated by an attacker that had been able to access the old key.

## Questions

* What are good timeout procedures to balance ease of key rotation with protection from attackers?
* How to deal with UI/UX challenges of decentralized key recovery procedures?


definitions: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/shared_terminology_for_digital_identity_systems.md
keyrev: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/pki_tools_in_evm_blockchains.md
keyreset: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/Key-revokation-of-lost-and-stolen-keys.md
