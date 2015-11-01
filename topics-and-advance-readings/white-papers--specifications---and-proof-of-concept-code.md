White Papers, Specifications & Proofs of Concept
================================================

by Christopher Allen - ChristopherA@LifeWithAlacrity.com

Our goal for this initial #RebootingWebOfTrust design workshop is to:

* Focus on the creation of the next generation of decentralized web-of-trust based identity systems.
* To generate 5 technical white papers on topics decided by the group that will have the greatest impact on the future"

To this end, I thought it would be useful to define what is a ***white paper***, and as some people desire to go beyond this, what is a ***specification*** and ***proof of concept code***.

White Papers
------------

Ultimately, the best white papers provide information to solve a problem that will be useful to the reader.

Very early on, a great white paper needs establish who the audience is, and attract readers from that audience to it. We don't want to waste the time of those who don't need this white paper. This should be done in the title, subtitle, or in first paragraph.

A white paper should begin by introducing a pain point. Readers should be connected with sympathy and understanding of that pain though use of a story "the use case". A use case should describe when and where that pain point occurs (aka "the problem"). The white paper should justify why that particular problem should be solved, or why it is worthy of the effort to solve it.

Next, the white paper should objectively explore alternative ways to solve the problem, or how this problem has, or has not, been solved in the past by various solutions.

Ideally (but not always) it should logically lead the reader toward a new solution that is worthy of further investigation (aka "a solution").

This solution should be presented, along with costs and risks to implement that solution.

Finally, the readers should become convinced that the problem is solvable, become engaged in helping solve the problem, and have a path to participate in solving the problem.

A good white paper should not be too long. A good rule of thumb is the 3-30-3 rule. Within 3 seconds a reader should be able to decide if they are interested (title, first sentence), then 30 seconds to decide if the white paper is worthy of their attention, and within 3 minutes the essential points of the problem and proposed solution. This often means effective headlines and infographics are important. Everything beyond that in the white paper is to support those already convinced and lead them to the path of further participation.

Specification
-----------------

Presuming that someone that is already engaged to participate in a particular solution (say by a white paper), a specification describes the externally visible behaviors of a system that implements that solution.
* What the developers need in order to build the system.
* What the testers need in order to validate the system.
* What other stakeholders need to know in order to approve the cost to implement the system.

A specification must define the functional interfaces through which external entities (the actors) can interact with the system (both input and output), as well as how as a result of those interactions, there is a change of state.

Proof of Concept Code
-------------------------------

Proof of concept code is a minimal implementation of a specification, that has been created to explore if there are unanticipated technical issues, logistical problems, vulnerabilities or other weaknesses of that specific implementation approach or that of the specification itself.

Proof of concept implementation are typically not expected to be efficient, reliable under all conditions, or scalable, but are expected to validate functional interfaces and state changes in a system.

Proof of concept code ideally should never be shipped to customers, and often is significantly refactored or rewritten from scratch before a deployment. The belief is that a good proof of concept will address problems when they are small scale and low impact before the problems impact larger systems, reducing costs of final implementation.
