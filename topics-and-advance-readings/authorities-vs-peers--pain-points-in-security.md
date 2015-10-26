Authorities vs. Peers: Pain Points in Security
==============================================

By Christopher Allen - <ChristopherA@LifeWithAlacrity.com> & Shannon Appelcline - <ShannonA@skotos.net> with the the help of the #RebootingWebOfTrust Community www.WebOfTrust.info

The *Rebooting Web of Trust Designshop* reimagines the models that we use for privacy, security and transparency on the Internet. We wish to move away from the problems created by the centralization of trust on the Internet — though centralized authorities such as Certificate Authorities and DNS Registrars — and instead implement peer-to-peer based systems, as inspired by the classic PGP and the more recent peer-to-peer decentralized tools such as Bitcoin.

However, both centralized authority-based services as well as peer-to-peer decentralized security have their own challenges. Identifying these pain points and solving them is one of the main ways that we can successfully create a new Web of Trust.

Pain Points of Authorities
--------------------------

DNS Registrars and Certificate Authorities (CAs) offer examples of centralized authorities of trust on the Internet — and they also offer examples of problems with that centralization as well. Anyone who has tried to move a domain or renew a certificate can personally identify many of the pain points in these systems.

### Purchase Pain

**Authorities are bureaucratic.** Certificates and domains are crucial parts of doing business on the internet. Unfortunately, that importance isn’t represented in many authorities’ business models. It might take days or weeks to move a domain or to acquire an extended validation certificate. The process also tends to be non-transparent and customer support is often limited or non-existent.

        Pain Points: temporary lose of services (customers), wasted time (customers)

*(This is a pain point that’s improved in recent years, thanks to increased automation, but that’s in turn led to other problems.)*

**Authorities are incentivized toward profit, not service.** The centralization of trust in online authorities requires the creation of independent infrastructure, and that has a cost. As a result, most CAs and registrars are looking for a return on their investment. Unfortunately, the drive to maximize profit by increasing price and lowering operational costs has repercussions that cause pain for customers.

To start with, putting any price on a certificate or record only increases security by a small amount, based on the frictional cost of the fee. However, authorities also try to oversell their customers. Purchasing or renewing a domain name is an obstacle course where you have to constantly dodge past add-ons and extensions that the registrars try to make sound required and obvious. Meanwhile, CAs offer arbitrary lists of varying costs items without much explanation; the widely disparate prices at different CAs makes things even more confusing.

        Pain Points: confusing products (customers), decision fatigue (customers), unnecessary sales (customers)

**Authorities fail to offer follow-up services as promised.** After they’ve sold their products authorities often become very reluctant to provide follow-up services, because they no longer have a profit incentive. Many CAs don’t properly revoke certificates, while domain registrars won’t transfer domains without extensive bureaucratic wrangling. Getting CAs to reissue certificates was also a problem until recent issues with Heartbleed and SHA1, but even now only some CAs make this sort of reissuance easy.

        Pain Points: poor follow-up support from authorities (administrators, customers)

**Authorities overly bundle services.** Even when they only manage to sell you a single product, authorities still tend to bundle numerous services together that do not necessarily belong together. CAs offer the best example. The main purpose of a certificate in the world of Internet commerce is to protect against man-in-the-middle attacks. However, CAs also prevent sybil attacks with the friction they introduce due to monetary and time costs, which prevents abusers from getting an infinite number of certificates. CAs also bundle certification and validation into their products. Finally, CAs accept revocation requests and distribute that information to others. Not all of these services need to be bundled together.

Bundling so many different services increases the costs of certificates and simultaneously reduces the time and effort being spent on the real security issues.

        Pain Points: unnecessary cost (customers)

**Authorities’ additional offerings don’t necessarily increase security.** Thanks in large part to the profit motivation of authorities, administrators forced to purchase certificates often feel like they’re being scammed. And, there’s real support for their belief: for many years CA verification were based on little more than a phone call and some simple information look-up. The result was a process that some administrators saw as near pointless and not contributing to security. It felt like authorities were doing the least possible to achieve certification, which defeated the purpose.

The differentiation of DV, OV and  EV (Domain, Organizational and Extended Validation) certificates has created better security value because of specific requirements for each. For example, a DV certificate is guaranteed to at some point have been associated with the machine it’s certifying, while an OV certificate verifies the organization exists and is operational. However, EV certificates reveal the continued problem of overselling, as most end-users won’t recognise the difference between a lock and a green bar.

        Pain Points: feeling of security theater (administrators), feeling of unnecessary work (administrators)

### Security Pain

**Authorities are obvious targets for attacks.** Unfortunately, authorities have the potential to be big targets. Even if an authority is trustworthy, that doesn’t mean that it’s secure. A break-in could compromise an entire authority and every certificate they’ve ever issued. To look at it another way: every CA is a potential point of failure for the entire internet.

        Pain Points: broken security (authorities, users), potential for data theft (users)

**Authorities failures cascade.**
Broken security at a single intermediary CA certificate can cascade to the need for tens of thousands of sites to replace their certificates because they’re wholly dependent on the CA above them in their chain.

        Pain Points: need to replace certificates (authorities, users)

**Authorities disclose unecessary information.** Validation is one of the many products bundled into a typical certificate. However, validation also tends to bundle a lot of information of its own — not all of which is necessary in all situations. This means that casual use of certificates can expose excessive information. This also makes the possibility of authority insecurity that much worse.

        Pain Points: information exposure (users)

**Authorities are subvertible.** Centralization itself causes some problems, such as the fact that authorities can be subverted by other agencies. Governments and corporations have already taken advantage of this, using centralized authorities as levers to influence large groups of people. Domain names and websites alike have been snatched away due to shaky claims of ownership. The broad abuse of DMCA notices is another example of powerful actors targeting authorities to the deficit of other Internet users.
	    Pain Points: loss of services or even livelihood (users)

### Non-Centralization Pain

**Authorities have become a web.** The strengths of centralization have been somewhat lost with the proliferation of authorities. You wouldn’t want to put all of your trust in a single authority, but most browsers trust over a hundred root certificates from over fifty organizations. This means that the average user is forced to trust the assessments of companies whose motives are not the same or are unknown. In other words, centralized authorities have practically become a web of trust, but without the advantages of such a web.

Worse, this dramatically increases the chance of security problems: if your browser trusts 100 certificates that each have a 1% chance of a breach over the course of  year, the chance that you’re exposed to a breach over the course of a year [1-.99^100] is 63%!

        Pain Points: broken security (users), lack of trust (users)

Pain Points for Web of Trust
----------------------------

Before the advent of Bitcoin several years ago, PGP offered us our earliest lessons about the issues that arise from peer-to-peer privacy. It still continues to be a great starting point.

### Use Pain

**Key management is awful.** The thing that’s always held PGP back is its key management scheme. Users must both understand how to exchange big, unwieldy, non-human-readable keys and how to do it in a way that doesn’t violate security. Key servers offer one solution but come with centralization concerns. Fortunately, innovation in wallets  from the Bitcoin community — such as paper wallets, use of QR codes, and HD keys — and the introduction of secure, decentralized human-readable identifiers from the Namecoin community demonstrate it is possible to do better.

        Pain Points: bad usability (users)

**Authority-less trust can be irrecoverable.** Because it has no authorities, PGP doesn’t give you any recourse if you lose your authentication information. Lose a private key? Lose the password you use to store your private key? You’re out of luck, with no one to support you. Fortunately, the Bitcoin cryptography community is again offering solutions for these problems, such as the use of hierarchical keys for key management, the introduction of escrow and threshold keys, or the creation of new sorts of trusted third-party services.

        Pain Points: lack of third-party backup (users), lack of reliability (users)

### Security Pain

**Direct trust isn’t the same thing as indirect trust.** With PGP it’s meaningful to directly link with a person: you exchange keys with someone you know and you thereafter have absolute faith that they’re who they said they were. However this direct trust changes into something else when you’re talking about the friend-of-a-friend or the friend-of-a-friend-of-a-friend. Instead of direct trust, you have a path made up of indirect trust and you must have faith that each of those relationships was both meaningful and entered into in good faith. Some argue that anything beyond direct trust in PGP is meaningless, or only good for unsecure introductions.

        Pain Points: lack of trust (users)

**Key compromise is totally revealing.** The loss of a private key will typically endanger anything ever sent with that key, including everything sent prior to the loss of the key. Meanwhile, you have to keep that old, broken key forever to unlock old documents. These problems are reflections of PGP’s larger issues with key management, but they’re security problems that arise from the usability issues.

        Pain Points: endangerment of past communications (users)

**Backwards compatibility can kill security.** PGP has been around for a long time, and some implementations of it aren’t secure any more. Unfortunately, many current PGP tools are required to maintain compatibility with older, broken versions. You certainly wouldn’t want to lose access to old files encrypted under a previous style of PGP, but in a world where upgrades are so automated as to be painless, it seems like there should be a better option than maintaining compatibility with outdated security methods.

        Pain Points: insecure security (users), potential for data theft (users)

### Centralization Pain

**Centralization can be hidden.** Though peer-to-peer networks are built to avoid centralization, hidden centralization is frequent and can open the network up to all of centralization’s pain points. Most obviously, a PGP key server is a centralized service that can cause problems. Less obviously, PGP is based on email addresses, which is in turn are based on the centralized domain name service.

        Pain Points: hidden problems (users)

Shared Pain Points
------------------

Finally, a number of problems appear in both classic centralized schemes and newer peer-to-peer schemes; they represent some of the most fundamental pains in security.

### User Experience Pain

**Trust is too complex.** Certificates offer the best example of this. You have wildcard certs and extended validation certs and single-name certs. You have SHA-1 and SHA-2. There’s a confusing medley of options. Similarly, PGP has a lot of complexity thanks to many key types and sizes. None of this is standard-operating procedure for the average administrator or the average internet user, so the whole topic goes right over their heads.

        Pain Points: bad usability (users), confusing products (users)

**Trust is poorly integrated.** Unfortunately none of these trust schemes have ever been well-integrated into their individual ecosystems. The complexity of PGP mail clients (and their separate key management tools) has been a prime cause of PGP not receiving mainstream acceptance. Similarly, certificate management has almost no integration with web server management; administrators have to perform arcane steps on the command line, then go out to third parties in order to generate new certificates.

        Pain Points: bad usability (administrators)

**Trust is poorly explained.** Complexity and integration issues could be resolved by better documentation, but none of the CAs or registrars seem economically incentivized to go that route. Similarly, documents on PGP are get so wound up in key management that it’s rare for them to present a simple, meaningful explanation of their system.

        Pain Points: lack of understanding (users)

**Systems are brittle.** Linking security systems into other services often makes those services more brittle and less reliable. The system being secured can fail during key rotation or due to problems with master key backup. A mail client with a PGP plug-in might crash if the client becomes out of date or if the plug-in does. Integration with Paypal payment services was recently threatened for sites that didn’t upgrade their certificates to SHA-2. There are generally more points of failure for a system with integrated security, which is another reason that people are less willing to use these systems. Newer mechanics like threshold keys and escrow keys may offer more reliability solutions, but are unproven.
	    Pain Points: System unreliability (administrators, users)

**The number of keys and certificates is increasing.** The average corporation has to manage thousands of CA certificates. If you add SSH keys and PGP certificates, that number might double. Tools for managing these disparate keys and certificates, and their lifecycle, are not easy to use, nor allow for easy integration.

        Pain Points: Too many keys (administrators)

### Security Pain

**Key rotation is difficult.** Because the friction of creating keys and certificates is high, users don’t follow best practices for key rotation. The same keys and certificates are used for too long. Web admins desire CA certificates that don’t expire for 4 or 5 years. Many of us in the PGP community still use keys from a decade ago. Re-encrypting old data with new keys may add a reliability risk as well as security risk. The Bitcoin community fortunately does better: it typically throws away a key when it has been used once.
	    Pain Points: Weak security (users)

**Trust revocation is difficult.** The trust offered by CAs and PGP is too often de facto irrevocable. CAs theoretically can invalidate certificates, but most historically respond poorly to such requests. Revoking a PGP certificate across a web of trust can be even more problematic.
	    Pain Points: lack of support when things go bad (administrators)

**Privacy is weak.** Generally, CAs and peer-to-peer services alike give out too much information. For CAs, this is a general problem of bundling too many different services together. However, domain registries are even worse: they require users to pay additional fees to keep their private information private. Similarly, in PGP the very act of key signing reveals information about social networks. If you care about privacy, then both systems have issues.

        Pain Points: information exposure (users)

### Transparency Pain

**Decisions making is not transparent.** Transparency is primarily a problem for CAs and other authorities. Their rules and how they’re applied are often totally opaque. The authorities might be making deals with governments,  other organizations, or peers that might undermine their security, and there’s no way to know.

However, PGP has shown that peer-to-peer systems can have transparency problems as well. There are very few implementations, thus only a few people can make changes to PGP itself, while PGP is also hard to interact with because there isn’t the diversity of administrative tools that you’d find for more modern software. Bitcoin’s wallets show that significant diversity and competition can offer innovation that PGP’s limited choices can not. However Bitcoin also has hidden centralities that are not transparent, such who has the authority to make a hard fork.

        Pain Points: unknown policy (users)
