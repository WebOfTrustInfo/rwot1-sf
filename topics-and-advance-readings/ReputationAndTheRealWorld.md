Web Reputation Systems and the Real World
=========================================

By Randy Farmer - randy.farmer@pobox.com - co-author with Bryce Glass of *Building Web Reputation Systems* (2010 Tor Books http://www.amazon.com/Building-Reputation-Systems-Randy-Farmer/dp/059615979X)

*This essay originally appeared as a chapter in [The Reputation Society: How Online Opinions Are Reshaping the Offline World](http://mitpress.mit.edu/books/reputation-society) from MIT Press, and is also published on the author's blog at http://buildingreputation.com/writings/2014/06/web_reputation_systems_and_the.html*

Digital Reputation
------------------

> *When anticipating the future of society and technology, it is advisable to look to the past for relevant successes and failures. Randy Farmer shares some of the signposts, warnings, and potential solutions he has encountered over two decades of building reputation systems.*

Digital reputation is rapidly expanding in real-world influence. Bryce Glass and I have studied hundreds of online reputation systems, including dozens that we helped develop. As we noted in the preface to Farmer and Glass (2010a, ix), “Today’s Web is the product of over a billion hands and minds. Around the clock and around the globe, a world full of people are pumping out contributions small and large: full-length features on Vimeo; video shorts on YouTube; comments on Blogger; discussions on Yahoo! Groups; and tagged-and-titled Del.icio.us bookmarks.”

Given the myriad contexts in which reputation is being used, it may be surprising to the reader that there is not yet any consensus on this field’s fundamental terminology. We therefore define reputation as “information used to make a value judgment about an object or a person.” But we acknowledge the special role of the reputation(s) of a person and therefore suggest a special term for this: karma. A good example of karma from real life is your credit score.

Reputation System Evolution and Challenges
------------------------------------------

### Preweb Reputation Systems

Modern digital and web reputations are deeply rooted in pre-Internet social systems. In this essay and others in this volume, examples are drawn from real-world models like the credit scoring industry’s measures of creditworthiness and its flagship reputation score, FICO, which was created by Fair Isaac Corporation. There are many industries that rate their members and suppliers. Cities get ratings for their bonds. Products have received the Underwriters Laboratories (UL) or the Good Housekeeping seals of approval. *Consumers Digest* published five-star ratings long before anyone had access to computers in the home.

But not all real-world reputation systems have been successful or continued in the same form over time. Looking closely at these systems and how they have evolved may save the developers of digital reputation systems millions of dollars by identifying possible best practices and helping to avoid dead ends.

### Web Reputation Systems

As recently as fifteen years ago, it was unlikely that you could gather enough information for a consensus about the quality of some obscure item from your coworkers, friends, and family. Your ability to benefit from reputation was limited by the scope of your social circle.

Now, thousands of strangers are publishing their opinions, which are aggregated into digital reputation. Want to buy an antique chess set? Look for a good seller feedback score on eBay. Figure out what movie to rent from Netflix? Five-star ratings and reviews will point you in the right direction. Want to find out what charities your friends are into? Look at their “likes” on Facebook.

On the surface, using digital reputation systems seems better and easier than tapping your social circle. However, there are some interesting -- and even troublesome -- side effects of reducing reputation to digital scores created from the input of strangers:

* Digital reputation scores are limited in the subtlety of their inputs. Only numbers go in, and those numbers usually come from simple user actions, such as “Marked an Item as Favorite.” But these actions don’t always accurately represent the sentiment that was intended, such as when marking something as a favorite is used for convenience to tag objectionable or novel items.

* Aggregated numerical scores capture only one dimension of a user’s opinions. For example, eBay’s seller feedback score was eventually enhanced with detailed seller ratings that reflect features of a transaction with scores called “Item as described,” “Communications,” “Shipping time,” and “Shipping and handling charges.”

* Another class of weaknesses in digital reputation is manipulation by stakeholders. A cadre of fraudulent New York electronics vendors reportedly used to invade Yahoo! Shopping every Christmas, building up false good-reputation for sales by cross-rating each other with five stars (Hawk 2005).

In order for digital reputation to come out of its early experimental period, we -- that is, the community of web reputation designers and developers -- need to acknowledge and address these technical, social, and potentially political issues. We need to work together to mitigate foreseeable risks based on historical lessons and to avoid a high-visibility economic or political event that will thrust these problems into the public domain -- with people demanding immediate and perhaps illadvised action.

### Digital Reputation Is Not Classical Reputation

Social networks borrow and redefine the metaphor of connecting to a friend to create an edge in a digital graph of inter-person relationships. Unfortunately, the term “friend” online has lost its real-life subtlety: if you are active on Facebook, you will likely have many “friends” that you are connected to but that you wouldn’t think of as close friends in real life. The same kind of oversimplification occurs when we attempt to quantify real-world socially defined reputation.

In designing reputation systems, we generally use numerical scores (ratings) together with small snippets of text (evaluations). But compared to real-world reputation, these computational models are almost too simple to merit even using the same word. Real-life reputation is subtle and dynamic, with personal and cultural elements. Most of the time, it is inherently nonnumerical. On the other hand, a digital reputation’s representation of value is typically numerical, globally defined for all, simple to calculate, and often publicly displayed -- clumsy, in comparison.

It is the utility provided by digital reputations that makes them so worthwhile. Software uses digital reputations to sort and filter the unmanageably huge morass of content on the web so that a human can make the final selection: where to eat, what to watch, from whom to buy. It is that last interaction -- with a choice made by a thinking human being -- that imbues the reputation score with its real power.

As reputation systems increase in real-world influence, the importance of who keeps, calculates, and displays the scores will become a greater societal discussion. Online reputation systems have been deployed for more than a decade, and many of the challenges that reputation systems will face are already known. By articulating these weaknesses, systems designers and researchers can address them head on, or at least enter the fray with their eyes wide open.

### Karma Is Hard

Though digital reputations for objects are often a poor imitation of the social reputations they attempt to mimic, karma is even more challenging. We have previously detailed a dozen ways in which karma differs from object reputation (Farmer and Glass 2010b).

Incentives are one example. Because karma is reputation for a user, increasing one’s karma score is often considered a strong incentive for participation and contributions on a site. This incentive can create trade-offs between the goals of the site and the desire for the rewards granted with high karma. We can see evidence of this desire, for instance, when collusion or fake user accounts are used by individuals to increase their karma. A related design challenge is finding a trade-off between rewards for a high quantity of participation instances versus rewards for providing high quality of contributions.

As a harbinger of possible future karma dilemmas, consider the legal and business debates that have evolved around credit -- such as use of FICO and other credit scores -- in the hiring process (as discussed later in this chapter and in chapter 6 of this volume). This practice has emerged because the classical job references reputation system has dried up as the result of litigation. When real-life reputation systems falter, it seems likely that more and more uses will be found for digital karma.

### If Reputation Has Real-World Value, Then Methods Matter

The power of reputation systems to provide real, actionable information, crowdsourced from large numbers of people and clever algorithms, will only increase over time. Every top website is using reputation to improve its products and services, even if only internally to mitigate abuse. In short, reputation systems create real-world value. Value often translates to wealth, and where there is wealth, the methods for creating that wealth become optimized -- often to the point of exploitation. Ever since people have trusted the written opinions of others, shady contractors have been generating false letters of recommendation to exploit the unwary.

The new wealth of digital reputation is created in large part by software. This software is usually written under extreme time pressure and without much design discipline, which leads to two challenges. First, reputation system bugs become corporate liabilities. Bad reputation model design or even simple coding errors can lead to inaccurate results that may significantly damage the value of an entity or business.

Second, reputation system abuse becomes lucrative. As a score increases in influence, the cost to manipulate that score is less than the value created. Spammers and hackers learned this more than fifteen years ago, and current reputation systems are already under constant attack. SEO (search engine optimization) is already a billiondollar business created solely to influence search ranking reputation. Likewise, public relations and marketing agencies may create buzz and social networking attention by creating façades of seemingly unbiased individuals.

Potential Solutions
 -- -- -- -- -- -- -- -- -- -

Given the difficulties surrounding digital reputation and the problems of abuse and unreliable code, one wonders who would be brave enough to propose and build a next generation reputation system. There are lessons from previous systems that can help eliminate -- or at least mitigate -- the risks.

### Limit Reputation by Context (Especially Karma)

The FICO credit score is most appropriately used to represent the context named “creditworthiness” and is built exclusively out of inputs that are directly related to the borrowing and repayment of money. The nature of the input matches the nature of the output. We typically run into trouble when the score is used for noncreditworthiness tests, such as preemployment screening. In fact, according to the National Consumer Law Center, using credit scores for preemployment screening is an unreliable indicator of productivity (H.R. 3149). It is also discriminatory, as certain minority groups statistically have lower FICO scores without necessarily being less productive. Likewise, a corporate executive’s excellent eBay buyer feedback has nothing to do with his or her credit score or with the number of experience points for his or her World of Warcraft character. Keep the contexts apart.

Tip: Don’t cross the streams. Good digital reputations should always be contextlimited -- the nature of the inputs should constrain the use of the reputation scores that are output.

### Focus on Positive Karma

Numerically scoring a person via karma can have a strong personal and emotional effect (see chapter 1 in this volume). Unlike object reputation, with karma it is a best practice to avoid publicly displayed negative scoring, direct evaluation of the person, and comparison of karma scores on leaderboards. Instead, build karma out of quality related indirect inputs, such as scores for the person’s helpfulness or ratings of objects created by the person. Avoid direct rankings and comparisons, except for competitive contexts. Karma leaderboards can demoralize regular participants and discourage participation by new community members.

Though most object reputation is intended to be displayed publicly, some of the most useful karma scores are either corporate (used internally by the site operator to determine the best and worst users in a context) or private (displayed only to the user). Private karma can still be used as a very strong incentive: just ask any blogger how obsessively they check their blog’s visitor analytics.

Tip: Focus on multifaceted positive karma. Avoid direct rankings and comparison of people, except where competition is desired. Reserve negative karma for egregious cases of misconduct; even then, look for alternatives.

### Focus on Quality over Quantity

When designing reputation systems for applications and sites, an easy method is often desired to motivate users to take some action. Usually that action is users creating content. The quickest model to build is in broad use across the web today: participation gives users points for taking actions -- usually more points for actions that are more desirable. Sometimes the points are redeemable (a virtual currency); other times, they simply accumulate indefinitely. These points are often displayed as a karma score and are sometimes used in competitive forms such as leaderboards.

If these points are a currency or lead to special recognition such as privileged feature access, they often either (1) never catch on because of contextual irrelevance or (2) lead to abuse, as described earlier. Purely participation-based systems often end up in one of these two states, unless they continually evolve to become more relevant and mitigate abuse. A good example of this is when Digg abandoned its leaderboards because all of the top contributors were using bots and friends to manipulate their rank.

When digital karma increases real-world influence or monetary value, abuse will only accelerate. The reputation scores that have the most lasting and trusted real-world value are those based primarily on quality evaluations by other users.

Tip: The best web content karma scores are generated not from participation-based points but from quality evaluations of one’s contributions written by other users.

Quality evaluations provide increased protection against simple forms of reputation abuse, as it is more difficult to generate large volumes of fraudulent indirect feedback. eBay protects their seller feedback scores by limiting the scope of user ratings to a single sales transaction, not an overall evaluation of an ongoing history of business with a seller. Yelp is almost the opposite -- the business may be evaluated historically, which makes it easier to manipulate. FICO’s creditworthiness score is also indirect karma -- creditors report only specific transaction facts, not subjective and nonstandardized opinions of the consumer’s relationship overall. By tying karma to the quality evaluations of a person’s actions instead of rating the person directly, the score is more reliable and easier to interpret.

### Mitigate Abuse through Metamoderation

As any reputation score increases in influence -- especially if that influence has realworld side effects -- the incentives to abuse the reputation model can grow to exceed the costs of manipulating the score, which leads to increased abuse and decreased utility value of the reputation score (and of the corresponding site or sites as a whole). The reputation score can eventually become untrustworthy.
If the community generating the content is sufficiently large -- perhaps when moderation costs exceed a certain percentage of the operating budget, such as 5 percent -- metamoderation reputation systems have been shown to be effective tools in cleaning up the worst content. The technical news site Slashdot uses such a metamoderation scheme to combat indirect input abuse by randomly selecting rated items for a second level of cross-check -- in effect, “rating the raters” (as discussed in chapter 7).

In Farmer and Bryce (2010a), we detail a Yahoo! Answers case study in which an internal reputation system allowed automatically determined trustworthy users to instantly remove content from the site. This approach effectively and completely shut down the worst trolls. Response time to remove content that violated terms of service (TOS) fell from eighteen hours (using paid moderation) to thirty seconds (with reputation-based metamoderation) and saved $1 million per year.

Tip: If users are creating and evaluating your mission-critical content, consider using reputation-based moderation and metamoderation techniques to enable your community to cross-check your content, identify the best content, and deal with abuse.

New Solutions, New Problems
 -- -- -- -- -- -- -- -- -- -- -- -- -- -

Future reputation system designers will hopefully apply narrow context to their data, ensure that publicly displayed karma is generated based on quality of actions and contributions, and mitigate abuse through reputation mechanisms such as metamoderation. But whenever a new technology comes into prominence, techno-optimists emerge who see it as a possible solution to contemporary social ills. So it should come as little surprise that many people have high hopes for the socially transformative power of digital reputation systems.
Though exciting possibilities, these trends require critical evaluation through the filter of experience. Important new problems to address are also likely. Lessons taken from the social evolution of other real-life institutions may apply to digital reputation systems as they increase in real-world influence.

### The Naming of Names

This chapter’s numerous admonitions to limit reputation to appropriate contexts raise the question: what are these contexts? Certainly reputation contexts within a single website can be narrowly and 100 percent locally defined. eBay seller feedback is a good example: its name describes its inputs and purpose adequately. But outside the web, the most influential reputations aren’t built solely out of single-supplier input.

What about cross-site, cross-company, and other globally shared contexts such as creditworthiness? How will data be shared across various boundaries? (See chapters 16 and 17 in this volume.) Who, if anyone, will manage the taxonomy of reputation contexts?

Looking at the credit score industry, we can see a proven model: the reputation system operator (such as Fair Isaac Corporation, which created the FICO scores) creates the context, defines the model, and specifies the data format and API for inputs in exchange for sharing the reputation results. The creditors supply credit history information for their customers in exchange for the right to access the creditworthiness reputation scores of all others, which they use to optimize their business practices.

Is this ad hoc method of identifying reputation contexts sufficient? What are the possible problems? If cross-domain reputation contexts aren’t standardized in some fashion, it seems likely that consumer confusion will result. We see some early evidence of this when comparing the five-star ratings of various product and service sites.

For example, why are the reviews on Netflix so different from Yahoo! Movies? It seems likely that the answer is that the context of those who wish to decide what movie to see at the theater for $20–$50 is significantly different from the context of selecting a DVD, delivered in a few days as part of a $9.99 all-you-can-eat watch-at-home subscription. Other factors may include selection bias and known patterns of abuse on movie sites (in which some ad agencies post fake positive reviews of first-run films). Even though the formats of the reviews are virtually identical, merging these two databases while ignoring their contexts would produce confusing results.

Nonetheless, on the week it was released, Facebook’s global “Like” system became the most visible cross-site reputation system on the web. We can expect more companies to follow their lead in producing interfaces for integration of reputation systems into applications of all kinds, from websites to social games and mobile phones.

The questions remain: should there be an effort to shape or identify the taxonomy of shared reputation contexts? Should there be a set of suggested practices or even requirements for calculations associated with the important real-world impact of reputation scores -- e.g., a set of branded guidelines that build consumer trust in these models? In short, do we need a “Good Housekeeping Seal of Approval” for reputation systems?

### Privacy and Regulation

As online reputation’s influence in the real world increases, we will face problems of privacy and regulation. These issues have to date generally been deferred with web reputation systems -- perhaps because the inputs were single-sourced and under the umbrella legal shield of the site’s TOS.

Generally, allowing users to completely opt out of a service by deleting their account is seen as sufficient privacy protection, and thus far has limited the potential real-world legal exposure of the host site. In short, the TOS defines the context for inputs and reputation, to which the user agrees, and walking away from the data is the escape clause.

But we are already seeing this perceived corporate protection eroding on sites such as eBay, where some sellers’ primary income is threatened by the actions of the hosting company on behalf of certain buyers (Cardingham 2008). Even if the company thinks it is protected by its TOS and “safe-harbor” provisions, most reputation systems depend on the actions of other users to create their scores. These three-party transactions are complicated and confusing, and get worse when users share data.

Once inputs and scores cross domains, information privacy crops up. It’s not enough to opt out of a data source -- users need to get their data corrected at (or entirely removed from) the data aggregators. Think about a major dispute with a specific credit card company; perhaps a card was stolen and used to rack up a large sum. After the creditors’ laborious flagging process, aggregators must be notified of disputed items and must temporarily remove them from creditworthiness scores, but not all aggregators respond at the same rate or have the same policies. On the Internet, reputation spreads rapidly, and traditional simple binary notions of private versus public information can fail us. Existing legal codes do not grant the right to control the dissemination of this increasingly critical data; they need to be updated (Solove 2007).

One way to facilitate thoughtful government regulation of reputation systems is to establish an industry group to define best practices and conventions for managing the privacy and control of data shared in reputation systems. Industry self-policing may be in the best interests of all involved.
The Rise of Online Karma as Offline Power

As more reputation moves online, more karma systems will follow, providing users with incentives to make high-quality contributions to web content, to identify users that don’t comply with the rules, and to enhance contributors’ personal brand. Craig Newmark, founder of Craigslist.org, in the foreword to this book reflects the thinking of many reputation system optimists: the idea that public karma for users may partially displace other forms of political and economic influence.

This idea -- that digital reputation, specifically karma, will increase to enable the intelligentsia to rise from the ashes and take their rightful place among the powerful -- is appealing to technical people. The Platonic ideal of the Philosopher King has been with us for more than two millennia. Has its time finally come? Will reputation systems enable us to truly identify the people, products, and ideas that will best solve our problems, or even allow us to govern wisely? Science fiction authors have suggested this for many years (e.g., Card 1985; Stiegler 1999). How far can online reputation take us?

Conversations with proponents of this position suggest that “. . . we then just combine all the relevant reputations into an overall GoodCitizen or SmartPerson karma.” As inputs, they then suggest combining factors like credit score, large readership for social media messages and/or blog posts, or strong endorsements on LinkedIn.com.

The largest initial challenge of this model is that good reputation has limited context. Naïvely combining scores from diverse contexts makes the calculation about no context at all. Next, combining scores from multiple sources has the “weakest-link” problem: the security weaknesses or abuses of the least-safe contributor site damage the integrity of the karma as a whole.

Even if one could solve context and weakest-link problems, the basic problem remains that any global SmartPerson karma represents too simple a metric to be used to evaluate a person for a complex role. Such karma may represent traits like popularity or industriousness, but be insufficient to represent one’s capacity to lead a large group of fellow citizens. Modern democratic elections could be considered to be reputation systems with a binary result, isElected. This binary result is not very fine-grained karma and is highly correlated with the amount of money spent on a campaign.

As noted earlier, paying for higher digital reputation already happens with movie and business reviews. Likewise, individuals, businesses, and political parties try to purchase influence via SEO, advertising, and other methods.
If money can buy digital karma, the idea of karma displacing money as influence in politics is not realistic. What remains are different questions: can online karma (and object reputation) be a productive political force in real life? Can it improve the information we use to select our leaders, and bring more justice to our laws?

When reputation scores are limited to appropriately narrow contexts, they can serve an increasing role within those contexts. Being a creator or critical analyst of the web already plays an increasing role in world politics. Recognized web influencers (bloggers, CEOs, etc.) regularly appear before Congress and parliaments worldwide. California’s 2010 elections featured two high-tech CEOs nominated for senator and governor, and in 2009 the Pirate party won a seat in the Swedish parliament.

In the near term, especially given its contextual nature, it seems likely that digital karmas will have a political influence similar to that of traditional endorsements by interest groups such as trade associations and charitable foundations. Online, distributed versions of these organizations are already forming. For example, sellers on eBay have formed the Internet Merchants Association, and combined the leverage of their high seller feedback ratings with their aggregated funding to influence the company and related regulatory bodies.

### Karma as Currency

What about the idea of converting karma into something you can spend, like money? A romantic notion: reputation given for good acts gets transformed into currency that you can later pay to others to reward their good acts.
Cory Doctorow, in his science fiction novella Down and Out in the Magic Kingdom (see chapter 18 in this volume), coined the term “Whuffie” to represent karma as a transferable currency: “Whuffie recaptured the true essence of money: in the old days, if you were broke but respected, you wouldn’t starve; contrariwise, if you were rich and hated, no sum could buy you security and peace” (Doctorow 2003, 10). A derivative of this idea has been implemented by the Whuffie Bank, which uses traffic at social media sites such as Twitter to model influence and create a score. Basically, if you get talked about, you gain Whuffie, and you transfer Whuffie when you talk about others. There is a separate mechanism to explicitly grant Whuffie to another user, presumably as a gift or a payment for some product or service rendered.

There are several problems with this model. First, it suffers from the same universal context problem previously defined, only worse: there is no clear way to reliably set an exchangeable numerical value based on user actions across contexts. If one decides to create a different currency for each context -- say a science Whuffie and a sports Whuffie and a political Whuffie -- then an accounting and exchange nightmare is created. How much science Whuffie trades for a given amount of political Whuffie? Does the market float? It quickly becomes an untenable mess.

Second, this example turns popularity (something that is already reinforced on social networks, leaderboards, and search rankings) into a currency. By extension, the Whuffie Bank could make the pop star of the month the Philosopher King of the Internet. This problem is systemic to any use of karma as currency. It isn’t likely to export to real life because popularity and attention often aren’t accurate measures of intelligence, trustworthiness, political savvy, technical training, or anything else that might be useful.
Third, it is unclear whether and how reputation can fulfill the traditional currency function of being a “store of value.” As described by Doctorow, any loss of respect would cause a speedy corresponding loss of Whuffie -- suggesting a continuous perperson currency revaluation. At Internet speeds, a single scandal could wipe you out in a matter of hours. Karma seems far too fragile to become a significant currency.

In short, Whuffie -- global reputation as currency -- crashes on the rocks of complexity. The universal context problem suggests that there can be only a few truly global currencies. However, there may be scope for experimenting with reputation as local currency.

### Overcoming Challenges Together

Though many reputation contexts will be limited to a single vendor or site, some providers will want to combine scores across all available sources, such as IP address blacklists for email. (Chapter 17 refers to these contexts as constrained reputations and universal reputations, respectively.)
The taxonomic, privacy, and regulatory challenges facing future digital reputation systems have already been articulated in this volume. How do we minimize the duplicated effort in technology development, policy and taxonomy design, industry standards, reputation modeling, and user interface best practices?

Either we continue reputation system development ad hoc, letting large corporations establish single-vendor-centric de facto standards and practices for cross-context (“universal”) reputation, or we use another approach: open standards and open software.

Probably the greatest contributions to the adoption of HTTP and HTML as the backbone data standards for the web were two open source projects: the Mozilla web browser and the Apache web server. These applications provided the stable frameworks required for others to build a new class of Internet software. Though these applications weren’t bug-free, they were the focal point of the effort to produce a reliable system.

In an attempt to provide an open, stable, and common infrastructure for reputation systems development, I have started -- with the help of many people -- the Open Reputation Framework project. Our hope is to make the Open Reputation Framework a home for reputation platform implementations, freely released intellectual property, and resources for modeling reputation systems, including a toolkit based on the reputation grammar described in Farmer and Glass (2010a). Online forums at this site -- or others like it -- as well as broader societal discussions offline are needed to foster the evolution of best practices for privacy, regulation, reputation taxonomy, and related issues. Open and well-lit places for discussion may be a prerequisite to guiding the development of reputation systems in a positive direction.

References
----------

Card, O. S. 1985. Ender’s game. New York: Tor Books.

Cardingham, C. 2008, October 24. Man sued for leaving negative feedback on eBay. Retrieved from: http://www.money.co.uk/article/1001771-man-sued-for-leaving-negative-feedback-on-ebay.htm.

Doctorow, C. 2003. Down and out in the Magic Kingdom. New York: Tor Books.

Farmer, R., and B. Glass. 2010a. Building Web Reputation Systems. Sebastopol, CA: O’Reilly.

Farmer, R., and B. Glass. 2010b. On karma: Top-line lessons on user reputation design [web log post.]. Building reputation systems: The blog. Retrieved from: http://buildingreputation.com/ writings/2010/02/on_karma.html.

Hawk, T. 2005, November 29. PriceRitePhoto: Abusive bait and switch camera store [web log post]. Thomas Hawk’s digital connection. Retrieved from: http://thomashawk.com/2005/11/ priceritephoto-abusive-bait-and-switch-camera-store.html.

H.R. 3149. 2010. Equal Employment for All Act. 111d Cong. Retrieved from: http://www.open congress.org/bill/111-h3149/show.

Solove, D. J. 2007. The future of reputation: Gossip, rumor, and privacy on the Internet. New Haven: Yale University Press.

Stiegler, M. 1999. Earthweb. Riverdale, NY: Baen.
