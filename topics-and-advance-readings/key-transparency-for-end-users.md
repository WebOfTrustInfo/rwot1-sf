Key Transparency for End Users
==============================

By Joseph Bonneau - jbonneau@cs.stanford.edu

Many people have proposed "running a Certificate Transparency log for user keys" as a way to improve trustworthiness of centralized key servers, as deployed by apps like TextSecure, iMessage or WhatsApp. It isn't quite as simple as forking the CT code though: user certs have different privacy expectations and different performance requirements. CONIKS is a proposal to solve these problems using several improvements to the basic CT design. It has been adapted (with some modifications) as CoName by Google and Yahoo for their E2E encryption projects.

TITLE: CONIKS: Bringing Key Transparency to End Users

Paper: http://www.jbonneau.com/doc/MBBFF15-coniks.pdf

ABSTRACT: We present CONIKS, an end-user key verification service capable of integration in end-to-end encrypted communication systems. CONIKS builds on transparency log proposals for web server certificates but solves several
new challenges specific to key verification for end users. CONIKS obviates the need for global third-party
monitors and enables users to efficiently monitor their own key bindings for consistency, downloading less than
20 kB per day to do so even for a provider with billions of users. CONIKS users and providers can collectively
audit providers for non-equivocation, and this requires downloading a constant 2.5 kB per provider per day. Additionally,
CONIKS preserves the level of privacy offered by today’s major communication services, hiding the list of usernames present and even allowing providers to conceal the total number of users in the system.
