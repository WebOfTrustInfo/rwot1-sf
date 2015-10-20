# Secret Handshake : Key Exchange as a Capability System

By Dominic Tarr - dominic.tarr@gmail.com

_originally published July 10, 2015, at http://dominictarr.github.io/secret-handshake-paper/shs.pdf)_

Secret Handshake is a key exchange with the properties of a capability system -
a conceptual framework for the construction of decentralized access control systems.

Capability Systems are an alternative model of operating system security design.
Historically, Capability Systems lost out to Access Control Lists (ACL).
However, these ideas are due to be reconsidered, because Capability Systems are viable
in cryptographic decentralized systems, but ACLs are not.

Security systems are about granting and denying access to resources.
In the physical world, we can observe a variety of approaches to security
that are analogous to both ACLs and Capability Systems. For example,
a your car has registration papers, which are like an access control list.
These are probably administered by an organization which is administered by your government.
Centralized Authority all the way up. If you cannot prove that you own or
otherwise have the right to be driving a given car
you may be arrested for possession of a stolen vehicle. On the other hand,
the car key is analogous to a capability. If you possess the keys to the car,
you can start it and drive away. If you give the keys to another driver
then they have the same capability to access the car that you do.

Enforcement of the ACL requires a centralized authority (police, etc)
but enforcement of the capability can be built into the car itself,
and access to the vehicle can be transferred by simply handing the keys over.

Secret Handshake differs from most key exchange protocols because it assumes
that you already know the key you wish to communicate with, and how you
established that key (i.e. by the web of trust) is outside of it's scope.

This enables us to use that public key as a cryptographic capability.
This has several interesting security effects. Firstly, it becomes harder
to abuse the system - for example, in many other protocols (ssh, TLS, noise),
the server's public key is sent to the client in the first message pass,
if the client neglects to pin that key, they permit a man in the middle attack.
However, in Secret Handshake, since the key is an cryptographic access token,
you cannot establish a connection without preselecting that key, and so man-in-the-middle
is prevented at the cryptographic layer, not at the implementation layer.

The server can be sure of this by auditing the protocol, without inspecting the client application.

## The Protocol

The core design of the protocol is as follows (see the original paper for full details)

Alice (`A`) is the client, who dials the phone, and Bob (`B`) is the server who answers it.
Alice begins by generating an ephemeral key (`a`), which will only be used for this connection.
At this point, Alice knows that she wants to communicate with Bob, and what IP address he has,
but since neither party has confirmed the identity of the other this pass is marked `? -> ?`,
Alice sends her ephemeral public key to Bob.
```
? -> ? : a_p
```
Bob then responds with his ephemeral public key (`b`). Neither know for sure who they are talking to yet.
```
? <- ? : b_p
```
Alice and Bob can then derive a shared secret `a*b` which is used to encrypt further passes in the key exchange.

This is Alice's most important step, in one pass, she proves to Bob that she knows who he is,
and also that she really is Alice, and then Bob just needs to acknowledge that.
To prove her identity, she signs the shared secret `Sign(A, a*b)`, and combines that with her public key
`A_p`, and encrypts that with a double diffie-helman, `Box[a*b|a*B](A_p, Sign(A, a*b))`.

```
? -> B : Box[a*b|a*B](A_p, Sign(A, a*b))
```

If Bob receives this message, he can open it and see Alice's signature, but nothing is revealed if she dialed a wrong number
(accidental man-in-the-middle). Bob knows the ephemeral secret is fresh, because he recently created `b`,
and so he also knows that `Sign(A, a*b)` is fresh, and that this is Alice. Given that this message was boxed
to him, he also knows this was not a wrong number.

Bob now knows he is talking to Alice, but Alice doesn't know it's really Bob yet. If Bob doesn't want to talk to Alice,
he can drop the call, and Alice won't know whether it was a wrong number or not. If he chooses to accept Alice's call,
he sends back confirmation of his identity by signing Alice's proof, and encrypting it back to Alice.

```
h := A_p, Sign(A, a*b)
A <- B : Box[a*b|a*B|A*b](Sign(B, h))
```

Alice and Bob may then commence a streaming bulk encryption protocol based on their triple diffie-helman shared secret
`a*b|a*B|A*b`.


