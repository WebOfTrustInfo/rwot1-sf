Avoiding Confused Deputy Attack Using Capabilities
==================================================

By Tyler Close - tyler.close@gmail.com

The Web has been a fertile field for vulnerability research not just because of programmer mistakes, but most significantly because the Web was the first popular platform for multi-party security. Unlike past client-server platforms, Web users interact with servers that link to other servers. When creating a new platform for multi-party interactions on blockchain technology, we should apply the lessons learned about how multi-party security is different from client-server security. The key insight is that it is crucial to be precise about where an exercised permission comes from. A more thorough explanation is offered at:

TITLE: ACLs Don't

SOURCE: http://waterken.sourceforge.net/aclsdont/current.pdf

ABSTRACT: The ACL model is unable to make correct access decisions for interactions involving more than two principals, since required information is not retained across message sends. Though this deficiency has long been documented in the published literature, it is not widely understood. This logic error in the ACL model is exploited by both the clickjacking and CrossSite Request Forgery attacks that affect many Web applications.
