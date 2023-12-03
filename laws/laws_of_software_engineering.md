---
title: Laws of Software Engineering
description: 
published: 1
date: 2023-12-03T01:06:56.358Z
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