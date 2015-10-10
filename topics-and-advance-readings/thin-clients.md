# The Need For A Generic Thin Client Protocol

By [Greg Slepak](https://twitter.com/taoeffect), attending on behalf of the [okTurtles Foundation](https://okturtles.com/).

##### Q: What Is A Protocol?

A __protocol__ is *a description of a fixed pattern of behavior*.

A protocol ***is not:***

- A platform.
- An implementation.
- A network.

Or any other "thing". Protocols are how the _things_ themselves behave.

##### Q: Why Are You Telling Me This?

Because the Internet needs blockchains, and it needs to be able to access them securely from mobile devices.

##### Q: Why Does The Internet Need Blockchains?

Because blockchains are how you do digital property on the Internet in a secure and decentralized fashion.

##### Q: OK...? Why is that important?

It's important and relevant for all the following applications:

- Identity
- Security
- Communication (aka: Identity + Security)

This Design Shop is all about identity. If you want to be able to *actually own* your identity online, then you need blockchains.

No individual owns their online identity today. Companies and governments own your online identity, and this applies to individuals as much as it does to other companies and groups.

Since blockchains make individual ownership of digital property possible, they make it possible for you to actually own (and therefore have control) of your online identity.

##### Q: OK... So What's This About A "Generic Thin Client Protocol?"

Blockchains are difficult to run on most end-user devices.

A _thin client_ (or a _light client_) refers to software that downloads only a portion of the blockchain [[1]](https://en.bitcoin.it/w/index.php?title=Thin_Client_Security&oldid=56863). This gives clients some ability to verify for themselves the authenticity of information within it.

The Internet needs a __blockchain agnostic__ and __technique agnostic__ thin client specification.

Agnosticism is essential because:

- Any blockchain may become abandoned by the Internet community.
- The “ideal blockchain” is unknown and may not exist.
- Non-agnostic protocols promote potentially harmful centralization.

Although most thin client techniques are derivatives of Satoshi’s original [Simplified Payment Verification (SPV)](https://en.bitcoin.it/wiki/Thin_Client_Security), it turns out there’s more than one way to skin a thin client. And so, in order to define a flexible thin client standard, we must find out just how different they can be.

![](https://okturtles.com/other/images/Thin-Client-land-2.jpg)

Other known thin client techniques are:

- [Proof of Transition](https://blog.okturtles.com/2015/06/proof-of-transition-new-thin-client-technique-for-blockchains/)
- [VerSum](https://people.csail.mit.edu/nickolai/papers/vandenhooff-versum.pdf)

And there are very likely others. We do not know how many there might be and what they all might look like (yet), but by studying the existing ones it may be possible discern a commonality between them, and that in turn can be used to specify a generic protocol that can wrap all possible techniques.

Such a protocol, if standardized and adopted, would allow any software to communicate securely with any blockchain. That would be highly valuable and useful.

##### Further Reading

- [DNSChain's (New-And-Not-Yet-Implemented) Security Model](https://github.com/okTurtles/dnschain/blob/master/docs/Security-Model.md)
