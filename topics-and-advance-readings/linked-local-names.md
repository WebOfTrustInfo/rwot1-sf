Linked Local Names: An Overview
=====

How do you identify someone online? Traditionally, the answer has been to use a centralized naming system. Trusted authorities act as the root of a global name space that connects names with public keys to certify who people are.

Unfortunately, this classic setup has problems. The earliest complaints focused on the x.509 standard and said that it was overly complex and overly formal. However, as the internet grew, people soon realized that there was a bigger problem: in a global name space, names quickly failed as a means of unique identity. If someone is verified by a certificate authority (CA) as Christopher Allen, who are they, really? Is it the psychic medium? The UCSF assistant professor? The security technologist? A traditional certificate can’t tell you. CA-based systems also require validation and revocation which recent SSL attacks like HeartBleed have proven have not adequately deployed or scaled to meet security requirements. Other aspects in the centrality of architecture in CA-based systems have also made them vulnerable to new forms of attacks.

In 1996, Ronald L. Rivest & Butler Lampson specified a different sort of system: linked local names, which they called “A Simple Distributed Security Infrastructure”. SDSI was intended to put the power of certificate authority in everyone’s hands. Each individual attaches personal labels to public key credentials, creating “local names”. More importantly, individuals could also connect to the local names created by other people. Thus you might have a local name for Christopher Allen that you label “Christopher”. It in turn could be used to create a more complex chain like “Christopher’s Shannon’s wife”. This would refer to a person labeled “wife” by the person labeled “Shannon” by the person labeled “Christopher” who is labeled by you: you define Christopher who defines Shannon who defines wife.

That same year, Carl Ellison was also working on local names and how to avoid the use of global certificate authorities. He eventually combined his work with SDSI in an IETF work group that defined the simple public-key infrastructure (SPKI). It takes an orthogonal look at these problems by linking authorizations to keys instead of just names. It also does away with CAs by creating webs of certificates between individuals and allows for the creation of cryptographic Access Control Lists (ACLs).

SDSI/SPKI has continued to expand in the years since Ellison’s RFCs, as seen in Ninghui Li’s 2000 paper “Local Names In SPKI/SDSI”. However, the SPKI RFCs never deployed—the specifications remain troubled by some of the same issues as older systems, particularly when representing complex information in a semantic graph. Finally, usage was limited in part due to an inability for anyone to monetize the infrastructure itself.

Marc Stiegler independently addressed the problem of global name spaces by expanding on Zooko’s Triangle — a list of requirements for global naming. It suggests that global names must be memorable, securely unique, and (obviously) global. Taking away any one criteria produces a more limited sort of identifier, such as a key (which is not memorable) or a nickname (which is not securely unique). Stiegler’s equivalent of the local name is a PetName (which is not global). Nick Szabo also worked on some proofs to demonstrate a solution for Zooko's Triangle can be created.

OpenID similarly tacked the topic of how people could identify and authenticate themselves to a relying party without having to use a single central authority. The OpenID community's original solution was to use a resolvable global name in the form of URL, and more recently, in OpenID Connect, an email address. This global name was then resolved to an associated OpenID identity provider to provide an authentication assertion (which may also include various identity attributes).

Although some large identity providers, such as Google, Wordpress, and Flickr, offer OpenID service, the OpenID community has not yet been able to achieve adoption beyond a few large identity providers. This challenge has been especially acute because the primary alternative to OpenID has become the social logins provided by the large social networks like Facebook and Twitter that already have very large namespaces and users that authenticate with these networks regularly.

More recently at OASIS, the XDI Technical Committee has developed an addressable semantic graph model and graph interchange protocol that supports all these forms of identifiers and identifier resolution. Although early work on XDI identifiers was focused on centralized XDI identifeir registries (called i-name and i-number registries), more recent work has prioritized specifying how the XDI protocol can be used for fully decentralized identifier assignment, resolution, and authentication.

On 8 June 2015, XDI.org, the public trust organization for XDI infrastructure, chartered the XDI Registry Working Group for this purpose. The charter invites industry experts to join a collaborative open standard effort to implement secure, reliable, and persistent decentralized naming and authentication by using new approaches such as blockchain technologies.

This is just one of many possibilities of new technologies: dnschain hopes to solve security issues with classic DNS by using the blockchain.  Onename.com wants to decentralize identity for bitcoin payments and IPFS.io imagines a peer-to-peer web. New algorithms such as the 25519 elliptic curve allows for new capabilities Schnorr Group Signatures and Shamir Secret Sharing.

So, there’s plenty of interest in local names as tools to reap the rewards of decentralization. The biggest obstacle is combing through all of this disparate work to find out what’s worked and what hasn’t. Then, we can we push forward toward new, more polished implementations of these recurring security themes.

References

3D. “The Problem(s) with OpenID”. ID-Corner: The Identity Corner. August 2007. http://idcorner.org/2007/08/22/the-problems-with-openid/. 

Allen, Christopher "Revokable Self-Signed TLS Certificates" https://github.com/ChristopherA/revocable-self-signed-tls-certificates-hack/blob/master/README.md

Bernstein, Daniel J., et al. “Ed25519: high-speed high-security signatures”.  September 2011. http://ed25519.cr.yp.to. 

Ellison, Carl M. “Establishing Identity without Certification Authorities”. Proceedings of the Sixth USENIX UNIX Security Symposium. July 1996. http://irl.cs.ucla.edu/~yingdi/pub/papers/Ellison-OldFriend-USENIX-Security-1996.pdf. 

Ellison, Carl M. “RFC 2692: SPKI Requirements”. 1999. https://tools.ietf.org/html/rfc2692. 

Ellison, Carl M., et al. “RFC 2693: SPKI Certificate Theory”. 1999. https://tools.ietf.org/html/rfc2693. 

Ellison, Carl M. “SPKI/SDSI Certificates”.  http://world.std.com/~cme/html/spki.html. 

Ferdous, Md. Sadek & Audun Jøsang. “Entity Authentication & Trust Validation in PKI using Petname Systems”. Theory and Practice of Cryptography Solutions for Secure Information Systems (CRYPSIS). May 2013. http://folk.uio.no/josang/papers/FJ2013-CRYPSIS.pdf. 

Ferdous, Md. Sadek, Audun Jøsang, Kuldeep Singh, and Ravishankar Borgaonkar. “Security Usability of Petname Systems”. Proceedings of the 14th Nordic Conference on Secure IT Systems. October 2009. http://folk.uio.no/josang/papers/FJSB2009-NordSec.pdf. 

Li, Ninghui. “Local Names in SPKI/SDSI”. Computer Security Foundations Workshop, 2000. CSFW-13. Proceedings. 13th IEEE. July 2000. https://www.cs.purdue.edu/homes/ninghui/papers/names_csfw00.pdf. 

Rivest, Ronald L. & Butler Lampson.  “SDSI - A Simple Distributed Security Infrastructure”. October 1996. http://research.microsoft.com/en-us/um/people/blampson/59-sdsi/acrobat.pdf. 

Sakimura, N., et al. “OpenID Connect Core 1.0”. http://openid.net/specs/openid-connect-core-1_0-final.html. 

Stiegler, Marc. “An Introduction to Petname Systems”. February 2005, et al. http://www.skyhunter.com/marcs/petnames/IntroPetNames.html. 

Stiegler, Marc. “Petname Systems”. August 2005. http://www.hpl.hp.com/techreports/2005/HPL-2005-148.pdf. 

Szabo, Nic. "Secure Property Titles with Owner Authority". 2005 http://szabo.best.vwh.net/securetitle.html

Wilcox-O’Hearn, Zooko. “Names: Distributed, Secure, Human-Readable: Choose Two”. October 2001. Archived at http://web.archive.org/web/20011020191610/http://zooko.com/distnames.html. 
