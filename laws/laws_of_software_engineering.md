---
title: Laws of Software Engineering
description: 
published: 1
date: 2023-12-03T01:17:37.221Z
tags: 
editor: markdown
dateCreated: 2023-12-03T01:06:56.358Z
---

# Laws of Software Engineering

## Atwood's Law
> Any application that can be written in JavaScript, will eventually be written in JavaScript.
>  - [Jeff Atwood, 2009](https://blog.codinghorror.com/all-programming-is-web-programming/)

Ultimately this law concerns software distribution: the web is the best mechanism for distributing software, JavaScript is the language of the web, hence Atwood's law. It might be updated some day to include WASM, though that's yet to be seen. Certainly the years since this blog post was published seem to have vindicated the law, though the growth of embedded systems in everything from cars to toasters runs counter to Atwood's original point.

## Brooks' Law
> Adding [human resources] to a late software project makes it later.p
>  - [Fred Brooks, 1975](https://www.indiebound.org/book/9780201835953)

This law first appeared in a classic book, [The Mythical Man-Month](https://www.indiebound.org/book/9780201835953). The central insight is that new developers require onboarding, which in turn requires time of existing developers, which in turn subtracts time from ongoing projects. Hence, a word of caution for hapless managers who attempt to speed up a project which is running off the rails: adding new resources will only exacerbate the problem.

The qualifier "late" in the statement of the law is an important one. It suggests that human resources *can* be added to projects which are not late. Hence, for example, the success of some open source software projects, which successfully incorporate thousands of developers over the course of their lifetimes.

## Choose Boring Technology
> Consider how you would solve your immediate problem without adding anything new
>  - [Dan McKinley, 2015](https://mcfunley.com/choose-boring-technology)

Though rarely cited as a law, McKinley's essay on boring technology has crystallized a resistance to pursuing cutting-edge technology stacks for their own sake.

## Conway's Law
> Any organization that designs a system (defined broadly) will produce a design whose structure is a copy of the organization's communication structure.
>  - [Melvin Conway, 1968](https://www.melconway.com/Home/Conways_Law.html)

Conway's Law is considered a driving principle of software management. Once an engineering organization is split up a certain way, its products will tend to reflect the org chart over time; it follows that org chart changes must be considered carefully. The [inverse Conway maneuver](https://www.thoughtworks.com/radar/techniques/inverse-conway-maneuver) attempts to flip the logic of this law on its head, by designing org charts that promote a desired software architecture. Arguably, the microservices revolution is an example of such a maneuver.

## Cunningham's Law
> The best way to get the right answer on the internet is not to ask a question; it's to post the wrong answer.
>  - [Ward Cunningham, 1980](https://archive.nytimes.com/schott.blogs.nytimes.com/2010/05/28/weekend-competition-schotts-law/)

Cunningham's formulation was apocryphally described in a comment on Ben Schott's blog in 2010. As stated, it describes the way people interact on the internet; it was [satirized by XKCD](https://xkcd.com/386/). More broadly, it's a supposition about human nature, i.e. that people would rather argue againt an assertion than fill in a blank.

The date of the law is highly uncertain, since it's been described second-hand and was a casual aphorism rather than a formal publication. Given that it's claimed to have bene coined in the early 1980s, it's likely it was phrased in terms of Usenet forums or similar contexts rather than more modern formats like blogs.

## Doerr's Law
> We need teams of missionaries, not teams of mercenaries.
>  - [John Doerr, 2015](https://www.svpg.com/missionaries-vs-mercenaries/)

The point of this law is that product teams should be mission-oriented: engaged, autonomous, and otherwise be tied in to the organization's larger mission. Mercenaries are motivated primarily by money, and are uninterested in the mission insofar as it doesn't impact their ability to get paid.

In the sense that this law pushes managers to empower teams, and to find ways to give them intrinsic motivation based in an organization's mission - it is on balance a good law. However, it is easy to take this train of thought too far, namely to assume that total loyalty can be assumed of employees without necessarily earning that loyalty. Colloquially, the extreme version of this thought is expecting employees to "drink the Kool-Aid" of an organization's ideology. Clearly, it's necessary for leaders to chart a moderate path.

## Fitts' Law
> The time to acquire a target is a function of the distance to and the size of the target.
>  - [Paul Fitts, 1954](https://doi.apa.org/doiLanding?doi=10.1037%2Fh0055392)

Originating in psychology and usability studies, this law studied the ease of grasping a physical target. The law is of direct importance to user interface designers today, and to the software developers who create those interfaces. It is also applicable to software interfaces: for example, it manifests in the ease-of-use of APIs.

## Gall's Law
> A complex system that works has evolved from a simple system that worked. A complex system built from scratch won’t work.
>  - [John Gall, 1975](https://www.goodreads.com/book/show/583785.The_Systems_Bible)

Originating in systems design, this law encourages software developers and product managers alike to begin with simple systems and grow towards complexity - rather than beginning with a complex system. This law is often cited as the reason for the failure of complex systems like CORBA, and is hailed as the reason for success of systems which began humbly, such as the World Wide Web.

## Goodhart's Law
> When a measure becomes a target, it ceases to be a good measure.
>  - [Charles Goodhart, 1975](https://link.springer.com/chapter/10.1007/978-1-349-17295-5_4)

Originating in economics, this law posits a pessimistic view of measuring the success of software. Once a given measure, for example lines of code, becomes reified as the measure of success, then software developers can readily maximize that measure, for example by adding a lot of superfluous comments or other unnecessary code. This law joins others which indicate the difficulty of measuring software projects, such as Hofstadter's.

## Hofstadter's Law
> It always takes longer than you expect, even when you take into account Hofstadter's Law.
>  - [Douglas Hofstadter, 1979](https://www.indiebound.org/book/9780465026562)

First coined in Hofstadter's book [Gödel, Escher, Bach](https://www.indiebound.org/book/9780465026562), this law nods at the difficulty of accurately estimating the length of software projects. It's self-referential in a way that Gödel especially would have appreciated. Indeed, advice to rising software managers commonly suggests adding a "buffer" to their estimates. This law suggests that the buffer will never be enough. Zawinski's Law may provide an explanation for this phenomenon: even when developers complete their tasks within the estimated time, software bloat will cause the project to expand and then overflow the buffer.

## Hyrum's Law
> With a sufficient number of users of an API, it does not matter what you promise in the contract: all observable behaviors of your system will be depended on by somebody.
>  - [Hyrum Wright, 2012](https://www.hyrumslaw.com)

Given enough use, there is no such thing as a private implementation. That is, if an interface has enough consumers, they will collectively depend on every aspect of the implementation, intentionally or not. This effect serves to constrain changes to the implementation, which must now conform to both the explicitly documented interface, as well as the implicit interface captured by usage. We often refer to this phenomenon as "bug-for-bug compatibility."

## Kerchkhoff's principle
> In cryptography, a system should be secure even if everything about the system, except for a small piece of information - the key - is public knowledge.
>  - [Auguste Kerckhoffs, 1883](https://www.arcsi.fr/doc/cryptomilitaire.pdf)

This principle predates modern software development by several decades, but establishes an important principle that extends beyond the domain of cryptography. It establishes a bright line between the code in a system, which is public knowledge, and the data in the system, which is private. By doing so, it discourages the common but ultimately insecure practice of "security by obscurity". This principle has found particular popularity in the open source community, which is built on the principle of publicizing source code but not the data it uses.

## Kernighan's Law
> Everyone knows that debugging is twice as hard as writing a program in the first place. So if you’re as clever as you can be when you write it, how will you ever debug it?
>  - [Brian Kernighan, 1974](https://www.goodreads.com/book/show/454039.The_Elements_of_Programming_Style)

It's commonplace to conclude that debugging is harder than writing a program; empirical studies have actually shown that "twice as hard" might be an underestimate. Kernighan looks at this phenomenon from the opposite angle, arguing that it's better to write simple code with an eye towards long-term maintainability. Compare to Knuth's optimization principle.

## Knuth's optimization principle
> Premature optimization is the root of all evil.
>  - [Donald Knuth, 1974](https://dl.acm.org/doi/10.1145/356635.356640)

Commonly attributed to Donald Knuth, some say this principle is really a popularization of a quote by Tony Hoare. As with all principles, this one may be taken to improper extremes: neglecting optimization altogether, or choosing intentionally mal-performing approaches from the outset. At one extreme, developers can spend a lot of time writing tightly optimized loops which gain small improvements in efficiency at the expense of huge reductions in maintainability. At the other extreme, developers can choose the wrong framework, or a grossly inappropriate database for the task at hand, leading to "maintainable" software which wilts under the slightest load. In the original article, Knuth himself considers some of these trade-offs; in the main he argues against a "penny-wise, pound-foolish" attitude. Compare to Wirth's Law.

## Law of Leaky Abstractions
> All non-trivial abstractions, to some degree, are leaky.
>  - [Joel Spolksy, 2002](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/)

This law points out that abstractions are imperfect. Hence, for example, SQL programmers must know a fair amount about their database server's query plans in order to understand their code's performance characteristics - the abstractions of the query language are not much help.

Taken to its logical conclusion, this law suggests that abstractions "save us time working, but they don’t save us time learning." The result is a grim conclusion, that programming is only getting more difficult as time goes on.

## Linus's Law
> Given enough eyeballs, all bugs are shallow.
>  - [Linus Torvalds, 1999](http://www.catb.org/~esr/writings/cathedral-bazaar/)

This law is attributed to Linus Trovalds but was popularized by Eric Raymond in his famous essay, The Cathedral and the Bazaar. It's something of an introduction to the open source movement. Trovalds's central argument is that increasing the number of developers on a project reduces the time to resolve bugs. For any single bug, some of those developers will inevitably have the central insight or knowledge to address the bug. Contrast this Law with Brooks's, and also compare to Kerchkhoff's.