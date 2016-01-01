# Rebooting the Web of Trust

These white papers were produced as part of the Rebooting the Web of Trust design workshop. On November 3rd and 4th 2015, over 40 tech visionaries came together in San Francisco, California to talk about the future of decentralized trust on the internet with the goal of writing 3-5 white papers and specs.

* **Workshop Sponsors:** Respect Network, PricewaterhouseCoopers, Open Identity Exchange and Alacrity Software
* **Workshop Producer:** Christopher Allen
* **Workshop Facilitators:** Christopher Allen and Brian Weller with graphic facilitation by Sonia Sawhney and additional paper editorial & layout by Shannon Appelcline

## What’s Next?
The design workshop and these papers are just starting points for Rebooting the Web of Trust. If you have any comments, thoughts, or expansions on these papers, please post them to our GitHub issues page: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/issues We are also planning for more gatherings on this topic in the near future, with the object being to have something notable ready for release on the 25th anniversary of PGP, in July 2016. If you’d like to be involved or would like to help sponsor these events, email: ChristopherA@LifeWithAlacrity.com

## Final Whitepapers

* [Rebranding the Web of Trust](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/final-documents/rebranding-web-of-trust.pdf)
* [Opportunities Created by the Web of Trust for Controlling and Leveraging Personal Data](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/final-documents/satisfying-real-world-use-cases.pdf)
* [Decentralized Public Key Infrastructure](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/final-documents/dpki.pdf)
* [Smart Signatures](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/final-documents/smart-signatures.pdf)
* [Creating the New World of Trust](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/final-documents/whats-the-next-step.pdf)

### Rebranding the Web of Trust
_A White Paper from Rebooting the Web of Trust_

By Shannon Appelcline, Dave Crocker, Randall Farmer, and Justin Newton

The Web of Trust. It’s the buzzword for a new model of decentralized identity. However, it’s also a phrase that dates back almost twenty-five years and has been heavily overloaded with meaning during that time. The classic definition of Web of Trust derives from PGP, but the top Google results refer to a website reputation rating system created by a Finnish internet company. Meanwhile, some use it as a big tent that includes identity authentication & verification, certificate validation, and reputation assessment, while the vibrant blockchain community is also drawing new attention to the classic concept.

To build a contemporary Web of Trust, we need to better define it. To do so, we must both understand what the classic Web of Trust was and create a model for the elements of trust that are contained within a more modern definition.

* Lead Paper Editor: Shannon Appelcline

### Opportunities Created by the Web of Trust for Controlling and Leveraging Personal Data
_A White Paper from Rebooting the Web of Trust_

by du5t, Kaliya "Identity Woman" Young (@identitywoman), John Edge, Drummond Reed, and Noah Thorp

In November 2015 Facebook's share price broke $100 USD/share, for a total valuation of $290 billion USD. This is evidence that both Facebook and the market understand the value of controlling and leveraging personal data. However, the now-conventional absorb-everything design of Facebook is a blunt one. Employing users as passive producers with no control of their own data only scratches the surface of what is possible with networks of information and identity.

Some of these constraints arise from Facebook's centralization, something that tends to worsen as an organization grows in size. There are limits to the amount of trust this sort of centralized authority can garner. This often results in punitive postures: democracies come with the expectation that citizens be forever watchful of their government; while corporations are watched over by regulatory bureaus and further deterred by class-action suits.

Decentralized systems that are engineered to prevent concentrating power as they grow avoid this. They can in fact increase their credibility as more users provide their assessments as input. Protocols and structures that are distributed and self- sovereign also offer significantly improved robustness, portability, and versatility than conventional centralized or escrowed processes — especially when combined with secure cryptography.

One of the first technologies to offer the advantages of decentralization emerged 25 years ago when the advent of PGP realized a Web of Trust that contained decentralized, cryptographically verified attestations of its users. Unfortunately, failures of UX design confined the spread of PGP to highly technical communities.

Today, decentralized Webs of Trust remain as important as ever. Now is the time to extend them to be usable by everyone who has access to digital networks, in particular to marginalized populations that can benefit from the technology. It is a fortunate tragedy that there is no shortage of real-life examples of the need for decentralized Webs of Trust in the world today. A large spectrum of individuals — from marginalized persons like stateless refugees and victims of human trafficking to members of the informal or unregulated economy — urgently need to participate in otherwise privileged economic and political fora, but they face technical, economic, and political barriers to entry.

The essential problem is to connect burgeoning new technological developments with unmet consumer needs, and vice-versa. In this paper, we present five use cases: from two relatively simple cases of managing selective disclosure to the most extreme case of establishing government-verifiable credentials from nothing for a stateless refugee.

Each case identifies basic technical implementation needs, presents a brief solution sketch, and outlines potential user experience. Afterward, we discuss common themes and summarize future prospects.

* Lead Paper Editors: du5t, Kaliya "Identity Woman" Young (@identitywoman)

### Decentralized Public Key Infrastructure
_A White Paper from Rebooting the Web of Trust_

by (alphabetical by last name) Christopher Allen, Arthur Brock, Vitalik Buterin, Jon Callas, Duke Dorje, Christian Lundkvist, Pavel Kravchenko, Jude Nelson, Drummond Reed, Markus Sabadello, Greg Slepak, Noah Thorp, and Harlan T Wood

Today’s Internet places control of online identities into the hands of third-parties. Email addresses, usernames, and website domains are borrowed or "rented" through DNS, X.509, and social networks. This results in severe usability and security challenges Internet-wide. This paper describes a possible alternate approach called decentralized public key infrastructure (DPKI), which returns control of online identities to the entities they belong to. By doing so, DPKI addresses many usability and security challenges that plague traditional public key infrastructure (PKI). DPKI has advantages at each stage of the PKI life cycle. It makes permissionless bootstrapping of online identities possible and provides for the simple creation of stronger SSL certificates. In usage, it can help “Johnny” to finally encrypt thanks to its relegation of public key management to secure decentralized datastores. Finally, it includes mechanisms to recover lost or compromised identifiers.

* Lead Paper Editor: Greg Slepak, Drummond Reed

### Smart Signatures
_A White Paper from Rebooting the Web of Trust_

by Christopher Allen, Greg Maxwell, Peter Todd, Ryan Shea, Pieter Wuille, Joseph Bonneau, Joseph Poon, and Tyler Close
Abstract

Traditional cryptographic signature systems are based on strictly-defined authentication and authorization mechanisms that assume a single private key can be used to produce a given signature and that a single public key can be used to verify it. Given the evident limitations of this design, we propose an alternative with more powerful capabities, based on the ability to explicitly outline and fully program conditions for verification. These conditions would then be used to determine when a signature or set of signatures can be considered valid.

Our inspiration for this authorization system is the bitcoin scripting language, where the authorization to spend funds is explicitly defined within a script, rather than being implicitly defined through the reference to an authorized public key. The largest benefit of explicit specification of authorization conditions is that the system is fully extensible, so new operations can be defined at any time, with the only limitation being the set of operations that the authorization interpreters understand.

* Lead Paper Editors: Christopher Allen, Ryan Shea

### Creating the New World of Trust
_Final Notes from Rebooting the Web of Trust_

What's Next? On November 3rd and 4th, the Rebuilding the Web of Trust design workshop looked at the future of decentralized trust on the internet with the goal of producing 3-5 white papers and specs. Those papers were polished for release in December, leaving the question: what's next?

Our major goal is to produce something notable for the 25th anniversary of PGP, in July 2016. This should be a working proof-of-concept that can help the Web of Trust to reach a broader audience. It should be something that's both usable and used and it needs to be compelling.

If we can meet this goal, we can make our design ideas into reality.

* Lead Paper Editor: Shannon Appelcline

* What’s Next Support: Christopher Allen, Brian Weller, Sonia Sawhney

## License

All of the contents of this directory are licensed [Creative Commons CC-BY](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/final-documents/LICENSE-CC-BY-4.0.md) their contributors.
