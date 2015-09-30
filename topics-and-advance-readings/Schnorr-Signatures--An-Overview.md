Schnorr Signatures: An Overview
===============================
By Christopher Allen - <ChristopherA@LifeWithAlacrity.com> & Shannon Appelcline - <ShannonA@skotos.net>

Digital signatures have been around since Whitfield Diffie and Martin Hellman first described them in 1976. Early implementations based on the prime-number based RSA algorithm were dominant in the ‘90s. In recent years discrete logarithm and elliptic curve approaches have become more popular because they allow for improved computational efficiency and smaller key size without diminishing security.

In the discrete logarithm space, ElGamal-based signature schemes have been the most deployed — thanks in large part to the National Institute of Standards and Technology (NIST) releasing their patented DSA under a royalty-free license when implementing the FIPS 186 standard in '93. Even Bitcoin as adopted a variant of DSA: the elliptic-curve based ECDSA, which uses the secp256k1 elliptic curve.

However, DSA isn’t the only answer for modern digital signatures. Schnorr signatures are an alternative that’s less widely used — primarily because they were under patent until 2008. Schnorr signatures offer numerous benefits over traditional methodologies, including:

* Strong Security. They have a stronger security proof.

* Nice Simplicity. They’re considered the simplest form of digital signature.

* Fast & Efficient. They can be implemented in blindingly quick ways on Intel hardware.

* NIKE (aka "Non-Interactive Key Exchange"). A Diffie-Helman secret between two parties can be created without any additional round-trips.

Schnorr signatures can also be added together in a very simple manner, which creates a number of interesting multisignature (aka "multisig") possibilities. These multisigs look exactly like a single signature, which means among other things that these mulitisig approaches have high privacy and low accountability:

High privacy. Third parties can’t see the participants, and only the participants can see the policy.

Low accountability. For an M of N multisig that only requires some parties to sign, you can’t see who the signors are. For example, in a 3 of 5 multisig, you can see that 3 of the allowed parties signed, but not who they are.

This high privacy is seen as an almost-universal win, but the low accountability has both advantages and disadvantages. It supports the implementation of group and ring signatures, both of which depend on anonymity, but it might be a deficit when used for financial multisigs. Fortunately, some recent implementations of Schnorr signatures are beginning to demonstrate new ways to adjust these cryptographic choices.

Much of the recent deployment of Schnorr signatures has come thanks to stream of non-NIST-based cryptographic work: in the early ‘00s, Daniel J. Bernstein and his team were working on Curve25519 (2006). This elliptic curve offers a number of advantages over curve secp256k1 including CM field discriminants, ladders, completeness, and indistinguishability from uniform random strings. Curve25519 also has a birationally equivalent Twisted Edwards Curve that can be implemented very efficiently on Intel hardware.

Bernstein applied his elliptic curve work to Schnorr signatures after their patent expired in order to create a new signature standard: EdDSA (2011), the Edwards-curve Digital Signature Algorithm. The recommended curve for EdDSA is Bernstein’s Curve25519; using it results in a variant of EdDSA called Ed25519. It combines the speed, security, and simplicity of Schnorr signatures with the size advantages of Elliptic Curve Cryptography, using all non-NIST algorithms, producing an enviable system for digital signatures.

Since its creation, Ed25519 has been implemented in a few different toolkits. Bernstein produced the first implementation for SUPERCOP. He then created the NaCl crypto library (2012) and the shorter and simpler TweetNaCl (2013), which is intended to be an auditable “crypto library in 100 tweets”.  Meanwhile, user-oriented software has begun to appear based on Ed25519, including the OpenBSD OpenSSH 6.5 (2014) and the miniLock file encryption software (2014).

Though Curve25519 researchers have initiated much of the recent work on Schnorr signatures, it’s also entering the Bitcoin world thanks to Greg Maxwell and Pieter Wuille who created a fork of the secp256k1 source library called secp256k1-zkp. Their Schnorr signature code allows Bitcoin multisigs to support more signers and to be less costly than the Threshold ECDA signature scheme that was introduced in 2014.

In fact, the Bitcoin community appears to be currently on the leading edge of Schnorr multisig development. Maxwell and Wuille are looking for ways to make Schnorr multisig more accountable. They’re also trying to solve usability issues, as M of N Schnorr multisigs currently require too many round trips.

Polycheck Signatures offer one intriguing possibility. They implement M of N multisigs as mathematical formulas; the formulas can be manipulated to zero out some of their factors, removing some signers from the (literal) equation.

However, Pieter Wuille’s Tree Signatures appear to offer even more capabilities. Tree signatures implement M of N multisigs as a Merkle tree filled with N of N multisigs; together, this combined structure represents many additional options for multisigs, as as "Either A and B signed, or 2 out of C, D and E signed".

Though these methodologies offer some changes to Schnorr multisig accountability and usability, the hunt for the perfect way to widely adopt Schnorr signatures continues. In order to reach this goal, we’ll need to answer a number of questions:

* What specific identity problems can only be solved by adopting Schnorr signatures? Which problems, when addressed, will have the biggest impact on the community?

* Should our identity work switch from secp256k1 to make use of the non-NIST Ed25519? Or should we instead use secp256k1 for better compatibility with existing bitcoin-based crypto?

* What are the tradeoffs? What exactly are the differences between Bitcoin’s secp256k1-zkp and EdDSA? What do we loose by choosing Schnorr on secp256k1 vs Ed25519?

* Can we parallel the development approach and APIs of NaCl, TweetNaCl, and TweetNaCl-js, but with secp256k1-zkp?

* Can Tree Signatures be brought to Ed25519? Can HD ("Hierarchical Deterministic") keys be brought to Curve25519?

* What other opportunities with Schnorr signatures should be be exploring? Group and ring signatures? What libraries and languages should we be targeting first?

References
----------

Bernstein, Daniel J. “A state-of-the-art Diffie-Hellman function”. 2006. http://cr.yp.to/ecdh.html.

Bernstein, Daniel J. “Curve25519: new Diffie-Hellman speed records”. February http://cr.yp.to/ecdh/curve25519-20060209.pdf.

Bernstein, Daniel J., et al. “Ed25519: high-speed high-security signatures”.  September 2011. http://ed25519.cr.yp.to.

Bernstein, Daniel J., et al. “High-speed high-security signatures”. September 2011. http://ed25519.cr.yp.to/ed25519-20110926.pdf.

Bernstein, Daniel J., et al. “TweetNaCl: A crypto library in 100 tweets “. September 2014. http://tweetnacl.cr.yp.to/tweetnacl-20140917.pdf.

Maxwell, Greg. “A Crypto-detour”. SF Bitcoin Devs Seminar: A Deep Dive with Bitcoin Core Developer Greg Maxwell. April 2015. https://www.youtube.com/watch?v=TYQ-3VvNCHE&feature=youtu.be&t=21m50s.

Kobeissi, Nadim. “miniLock”. Hackfest 2014: Nadim Kobeissi presented "miniLock - Advances in Usable Cryptography"‬. November 2014. https://www.youtube.com/watch?v=izHUQ73i-5U&feature=youtu.be&t=24m5s.

Schnorr, Claus-Peter. “Efficient identification and signatures for smart cards”. Advances in Cryptology — CRYPTO ’89. 1990.

Seurin, Yannick. “On the Exact Security of Schnorr-Type Signatures in the Random Oracle Model”. January 2012. https://eprint.iacr.org/2012/029.pdf.

Wuille, Pieter. SF Bitcoin Devs Seminar: Key Tree Signatures. August 2015. https://www.youtube.com/watch?v=gcQLWeFmpYg.

‪Wuille, Peter. “Tree Signatures”. August 2014. https://blockstream.com/2015/08/24/treesignatures/.
