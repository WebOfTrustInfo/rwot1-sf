# First Encounters with PGP

The first time I came across PGP, I was reading a blog post on the topic of identity with bitcoin public keys. The ideas discussed in the post compelted me to the point of searching around for the writers contact info. But instead of the typical name and email address I expected, all I found was a pseudonym and PGP fingerprint. I could figure this out I thought. That morning at the local breakfast spot I was talking to my friends about my encryption plans for the day. When the man sitting next to me at the restaurant overheard. A fellow PGP user, on his way to a python convention. He gave me his business card and said that if I ever figured out PGP I should try to send him an encrypted message.

PGP skills are a badge of honor. But the outside perception is that the only people willing to work for it are nerds and criminals.

> In the words of Phil Zimmerman: 
*"Privacy is as apple-pie as the Constitution."*

This is a contradiction. Everyone expects privacy, but no one values it enough to invest time into it. As for why Johnny can't encrypt, I'm not sure why PGP is so complicated. But if PGP was truly intended for people to be able to take privacy into their own hands, it's fallin short of its goal. To this day, I still have yet to have anyone sign my PGP key, although few have tried.  

As someone born in the early days of PGP, my discovery of finding it and learning about it only after cryptocurrency is a bit backwards from most people. In comparison with the wealth of choices that exist in Bitcoin API, it seems as if nothing is out of the box ready with PGP.  When trying to integrate a simple key PGP sign and encrypt code snippet into a web app, I found that even the most popular PGP tool kit OpenPGP.js could be outdated. And until Keybase.io gets a more robust API. Developers are left wondering if PGP is really the best way to go. If message encryption is going to strive, its has to compete with free social media platforms. 

Web-of-trust models, applied to social media have done quite well. Twitter has been credited with an underlying web-of-trust model in the follower-follower "like" and "comment" relationship. Facebook and Linkedin both leverage the FOAF (Friend-Of-A-Friend) web-of-trust model. The next generation of personal encryption tools need to put real social interactions first, and become a more universal tool for communication and reputation.

<br>
##### 1. Reputation:
PGP has four levels of trust that the user can assign to another users' public key: Unknown, marginal, full, and ultimate. But since the trust rating a user gives to public keys in their network is not publicly available to everyone else, reputation in signing keys is limited to a binary confirmation of signed or not signed once it's on the server. Ideally, the user should have the ability to set the degree to which people could specify their trust. Who can rate me, and how specific can they be? A more robust reputation system would include the ability to endorse a person after a mutual signing of keys:

    "This is the same Alice I've known since 1999, when we started college together. 
    She has read her fingerprint to me in person."
    [expand for the full signed statement]
    Signed by g0449... twitter/malgorithms, github/malgorithms, etc.

<br>
##### 2. Identity-valdation:
Everything about security comes down to trust. How well can I trust that this public key is actually held by the proper owner? Currently PGP relies on the users for validating the identity of the people in their network. Usually this takes place face-to-face. But the ability to authenticate thru third parties while linking their online identities is a significant amount of value added. Keybase currently has the most developed implementation:

    // ♥ keybase id kidblondie
    ✔ public key fingerprint: 8A3D DB0E 024E 98A5 4C72 C204 E565 3818 E15F DC6E
    ✔ "anarchoass" on twitter: https://twitter.com/anarchoass/status/5895362344...
    ✔ "kiaraRobles" on github: https://gist.github.com/6f5e17b8d03cbabec21d

<br>
##### 3. Decentralization
Given the innovation of the blockchain as a decentralized database I can imagine how a similar protocol could be used to maintain the identity and reputation information on a decentralized blockchain. Putting identity and reputation on a blockchain will ensure that the information comes from a specific user, to the intended recipient, and neither the message or the reputation they've established with each other has been tampered with.

If the goal of the web-of-trust is to establish and ensure the correct identity association with asymmetric cryptographic keys I think its more than achieved its goal. Nevertheless now that it has, we're compelled to ask what can be improved? The obvious solutions to mainstreaming web-of-trust communication includes making better software. The list includes more secure crypto for the browser, PGP encrypted messaging in mobile apps, and the capacity use our private keys for more than messaging. A more ambitious goal expands the meaning of the web-of-trust to include reputation, identity-validation, and decentralization.

<br>
References
----------

- ["ArXiv.org Cs ArXiv:1508.04868." [1508.04868] From Pretty Good To Great: Enhancing PGP Using Bitcoin and the Blockchain. N.p., n.d. Web. 04 Oct. 2015.](http://arxiv.org/abs/1508.04868)
- ["Does Social Contact Matter? Modelling the Hidden Web of Trust Underlying Twitter∗." Marketing to the Social Web How Digital Customer Communities Build Your Business (2009): 207-17. Web.](http://www2013.org/companion/p981.pdf)
- ["Keep Web of Trust - Allow Endorsements." Weblog post. GitHub. N.p., n.d. Web. 04 Oct. 2015.](https://github.com/keybase/keybase-issues/issues/637)
