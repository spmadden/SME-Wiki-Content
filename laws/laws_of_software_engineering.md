---
title: Laws of Software Engineering
description: 
published: 1
date: 2023-12-03T01:11:57.454Z
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