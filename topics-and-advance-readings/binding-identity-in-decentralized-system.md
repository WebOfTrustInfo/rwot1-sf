#Binding Identity in a Decentralized System

*by Wayne Thayer [@wthayer](https://twitter.com/wthayer) \<wthayer@gmail.com\>*

Server authentication and code signing certificates have historically bound a physical identity – typically an organization – to the certificate via an authority (CA). This binding benefits relying parties who don’t have an existing relationship with the organization by making it more difficult to impersonate the organization.

There are numerous difficulties with this process of identifying a physical entity:
+	It’s error prone – CAs rely on the accuracy and freshness of data sources such as corporate filings to verify organization identity. The task of determining that a certificate requestor is an authorized representative of the organization has become has become increasingly difficult as organizations move away from land lines and centralized offices.
+	It’s expensive and time consuming – the standard for Extended Validation (EV) certificates [1] was created in part due to concerns about the inconsistency and weakness of CA’s organization validation (OV) practices. The resulting 8-step EV process is reliable, but also complex, time consuming, and often expensive due to the need to engage an attorney or accountant, or even perform a physical site visit. 
+	Names are not unique – ‘Acme Inc.’ can be incorporated in Delaware and registered with a local government in a different state or country. This led to the inclusion of jurisdiction information in EV certificates, but it’s difficult to properly interpret that information. The situation for individuals is even worse. Individuals and unregistered businesses aren’t allowed to obtain EV certificates because publishing a unique identifier for an individual creates legitimate privacy concerns.

More recently, the identity component has been dropped from certificates. Since their introduction in the early 2000s, Domain Validated (DV) server certificates have become ubiquitous due to their low cost (now sometimes free) and simple validation process. These certificates are great when the relying party is confident they know and trust the site they’re connecting to. They also provide a low level of protection from phishing [2]. It has also become common practice for platform vendors to use certificates without validated identity information for signing code. In some cases, the platform vendor signs the code as part of their approval process (e.g. Apple) or accepts self-signed certificates (e.g. Android).

An additional problem with identity in certificates is the difficulty in presenting the information in a way that allows relying parties to easily make an informed decision. Many Web browsers display the verified organization in the address bar for EV certificates, but not for OV certificates. Mobile browsers often omit this information to preserve screen real estate. Google is discussing [3] the removal of special EV indicators in favor of a warning for any site not using TLS and otherwise configured securely.

Reputation is one solution to verifying identity in a decentralized system. However, as described in Noah Thorpe’s paper, this is a difficult problem. Reputation also disadvantages new entities. Microsoft has combined reputation with validation in Windows by granting code signed with an EV certificate a neutral reputation when published, but then quickly adjusting the score using their reputation algorithms [4].

There are valid and valuable use cases for binding verified physical identities in a decentralized web-of-trust system. Is this really a problem, and if so, should we ignore it, integrate traditional CA verification methods, or find a new way to solve it?

###References:
[1] https://cabforum.org/wp-content/uploads/EV-V1_5_7.pdf

[2] http://news.netcraft.com/archives/2015/10/12/certificate-authorities-issue-hundreds-of-deceptive-ssl-certificates-to-fraudsters.html

[3] https://www.chromium.org/Home/chromium-security/marking-http-as-non-secure

[4] http://blogs.msdn.com/b/ie/archive/2012/08/14/microsoft-smartscreen-amp-extended-validation-ev-code-signing-certificates.aspx
