---
title: SPM's Laws of Software Engineering
description: 
published: 1
date: 2024-12-31T21:30:30.909Z
tags: 
editor: markdown
dateCreated: 2024-12-31T19:20:49.527Z
---

# SPM's Laws of Software Engineering

These are a collection of rules/laws/axioms I've come to follow during my career as an Engineer.  Each has a story behind it.  These are all compatible with [SPM's Rules of Engagement](/laws/spms-roes) in spirit, if not to the letter.


## The 1st Axiom: Nearly all problems in Engineering are People Problems, not Science Problems.

> Science is easy.  People are hard.  Engineering is done to improve the lives of people - your customers.

### Axiom 1.1: People are Fickle

> fickle /fĭk′əl/ (adj): Not fixed or firm; liable to change; unstable; of a changeable mind; not firm in opinion or purpose; inconstant; capricious.
> See also: unstable, inconstant, ambiguous, erratic, ambivalent, impulsive, impermanent
> {.is-info}

### Axiom 1.2: Schedule, Budget, Staffing, and Prioritization are the hardest problems you'll never solve.
> The best design in the world will always be overridden by the "Magic 4":
> * We don't have the schedule because...
> * Other tasks hare higher priority because...
> * We don't have spare staffing because...
> * We don't have spare budget because...

| Layer | Name           | Unit                                         | Example                                         |                    Reliability                     |        Diagnostic Effort        |       Correction Effort        | 
|:-----:|----------------|----------------------------------------------|-------------------------------------------------|:--------------------------------------------------:|:-------------------------------:|:------------------------------:| 
|  10   | Politics       | Organizations / Governments / Prioritization | Policies / Laws /                               |   `Lowest` < Most of your problems happen here.    | `Lowest` < Easiest to diagnose  | `Highest` < Hardest to correct | 
|   9   | Money          | Dollars                                      | Salary / Postage Stamp                          |                       `<-->`                       |             `<-->`              |             `<-->`             | 
|   8   | People / Users | FTEs                                         | The Animal (Human, Dog, Lizard, etc.)           |                      `<---->`                      |            `<---->`             |            `<---->`            |
|   7   | Application    | User Interface/Interaction                   | GUI / CLI / Pen                                 |                     `<------>`                     |           `<------>`            |           `<------>`           |
|  6*   | Protocol       | Data                                         | SSL/TLS Connection / Ciphering / Language       |                    `<-------->`                    |          `<-------->`           |          `<-------->`          |
|   5   | Session        | Data                                         | TCP Connection / Conversation                   |                   `<---------->`                   |         `<---------->`          |         `<---------->`         |
|   4   | Transport      | Segment / Datagram                           | TCP Segment / UDP Datagram / Package / Envelope |                  `<------------>`                  |        `<------------>`         |        `<------------>`        |
|   3   | Network        | Packet                                       | IP Addresses / Mailboxes                        |                 `<-------------->`                 |       `<-------------->`        |       `<-------------->`       |
|   2   | Data Link      | Frame                                        | Ethernet Switches / WAPs / Mail Truck           |                `<---------------->`                |      `<---------------->`       |      `<---------------->`      |
|   1   | Physical       | Symbol                                       | Cat6A / Wifi / Post-Office                      | `Highest` < The least of your problems happen here | `Highest` < Hardest to diagnose | `Lowest` < Easiest to correct  |

> Reliability (adj): Such that either information will reach its destination, even if it requires retransmission, or the sender will be told that it didn't.
{.is-info}


## The 1st Law: Know Who Your Customer Is

> If you're improving the lives of your customers, you need to know who your customer is and you need to know what their problems are.  Maintain a good and continuous understanding of your customers and their problems.  Both are fickle (see Axiom 1.1) and guaranteed to change and fluxuate over time.

## The 2nd Axiom: Changes add Complexity.
> Fact: 100% of all bugs in software are introduced through software changes.
> {.is-warning}

> Fact: 100% of all bugs in software are corrected through software changes.
> {.is-warning}

> Omnipotence (n): Infinitely Powerful  (omni-potentia)
> Omniscience (n): Infinitely Knowing   (omni-scientia)
> Omnibenevolence (n): Infinite Well-Meaning (omni-bene-volition)
> {.is-info}

> Fact: Omnipotence, Omniscience, and Omnibenevolence are divine attributes and reserved for `$yourChosenDeities[..]`

### Axiom 2.1: Changes are your Friend!
> Embrace change.  People change.  Understanding changes.  Your requirements change.  You live in an ever-changing world where entropy always increases.  Learn to love it, because change is the only constant in this universe.  Embrace refactorings into simpler, more robust, more usable implementations.

### Axiom 2.2: Change is your Enemy!
> 

## The 2nd Law: Minimize Complexity


## The Law: Growth is Essential
> Always be working towards something larger, bigger, better, faster.

## The  