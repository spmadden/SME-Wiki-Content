---
title: SPM's Laws of Software Engineering
description: 
published: 1
date: 2025-01-01T00:12:25.915Z
tags: 
editor: markdown
dateCreated: 2024-12-31T19:20:49.527Z
---

# SPM's Laws of Engineering

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

...which brings us to the first law.

## The 1st Law: Know Who Your Customer Is

> If you're improving the lives of your customers, you need to know who your customer is and you need to know what their problems are.  Maintain a good and continuous understanding of your customers and their problems.  Both are fickle (see Axiom 1.1) and guaranteed to change and fluxuate over time.

## The 2nd Axiom: Engineers are "People", and are therefore the problem.

### Precept 2.1: 100% of all software is written by Humans.
> Yes, even AI-assisted code.  AIs were created by humans, and therefore have human fallibility.
> {.is-info}

> Therefore, all software has bugs.  Some bugs are more impactful than others.

### Precept 2.2: All Humans are Stupid.  Some Humans are Effective.
> Humans make errors. Smart Humans make stupid errors.  Really effective humans make really effective errors.

![dunning-kruger-3-3919728747.webp](/dunning-kruger-3-3919728747.webp)

... which brings us to the 2nd law.
## The 2nd Law: Plan for humans to introduce errors - including your own.
> An error doesn't become a mistake until you refuse to correct it.  

> This includes ALL interactions with humans, both interpersonally and programmatically.  Accepting input from a human?  Validate it.  Producing output for a human?  Validate it (because they should be validating it as well).
> {.is-warning}

## The 3rd Axiom: Everything is a System.
> Nothing exists in a vacuum.  Everything interacts with everything else.
> {.is-warning}

> A system can be subdivided into smaller systems.  When two systems interact, new behaviors can emerge and the resultant system is "more than the sum of it's parts".
> {.is-info}

### Precept 3.1: Systems can be Modeled.
> Model (n): A simplified schematic description or representation of something, especially a system or phenomenon, that accounts for its properties and is used to study its characteristics. Typically used to build an understanding of a larger, more complex system.
> {.is-info}

> Humans build mental-models of systems to understand how to interact with that system and predict that system's behavior.
> {.is-info}

> The word "Oven" implies a very particular mental model - a box who's inside temperature can be increased by external controls.  You would not expect that the act of turning the temperature knob on the front would cause a rocket engine hidden underneath to ignite and launch the box high into an orbital altitude.  The first time this happened would forever change your mental model of the word "oven". (...and create a great story to tell at parties!  "No shit, there I was...")

### Precept 3.2: All Models are Wrong.
> Since a model is, by definition, a simplified representation of a system, it is lossy with respect to that system and cannot (with 100% accuracy) represent the inner-workings and behaviors of the system.  If it could, it wouldn't be a simplification.

### Precept 3.3: Some Models are Useful.
> The act of "Learning" is training a mental model to respond in the way the system responds. 
> {.is-info}

> Flight Training is the act of learning how the system called an "aircraft" interacts with the system called "the atmosphere".  It's not likely that you have a machine that controls the atmosphere, however the aircraft likely has controls to interact with it.  Understanding how the controls manipulate the system called "aircraft" is critical to predicting how the two systems will interact as a result.

### Precept 3.4: Models must be re-evaluated for correctness when the system changes
> Some changes to the system do not invalidate the model.  Other changes do. Every change must be evaluated to determine the impact on both the system and the model.

> For example changing an analog dial on the oven to a digital button is unlikely to invalidate your mental model of the oven.  However, discovering a rocket engine on the bottom will likely do so.

### Precept 3.5: Interactions between systems lead to emergent behaviors
> Emergence (n): Emergence occurs when a complex entity (system) has properties or behaviors that its parts do not have on their own, and emerge only when they interact in the larger context. 
> {.is-info}

### Theorem 3.5: "Emergencies" (Emergence-es) are the result of insufficiently detailed models
> Emergency (n): The quality of being emergent; sudden or unexpected appearance; an unforeseen occurrence.
> {.is-info}

... which brings us to the 3rd law.
## The 3rd Law: Evaluate every change to determine which are relevant and which are not.
> You will not be able to adjust your mental model of the system unless you understand the changes to the system.

## The 4th Axiom: Changes add Complexity

### Theorem 4.1: Changes are your Friend!
> Embrace change.  People change.  Understanding changes.  Your requirements change.  You live in an ever-changing world where entropy always increases.  Learn to love it, because change is the only constant in this universe.  Embrace refactorings into simpler, more robust, more usable implementations.

### Precept 4.2: 100% of all bugs in software are corrected through software changes.

### Theorem 4.3: Changes are your Enemy!
> Change frequently invalidates your mental model of the system. It is critically important to understand the changes, to understand how your mental model of the system must change to adapt to the latest system state.

### Precept 4.4: 100% of all bugs in software are introduced through software changes.

### Theorem 4.5: The magnitude of the systemic change is proportional to the magnitude of the required model change.
> * A Large System Change often necessitates a Large Model Change (but not always)
> * A Small System Change does not often necessitate a Large Model Change (but sometimes it does).

... which brings us to the 4th and 5th laws.
## The 4th Law: Minimizing Complexity in your Systems Minimizes the Complexity in your Mental Models

> * This is the basis of the phrase "Keep It Simple, Stupid".
> * A simple system is easier to understand.
> * Interactions between systems are often complex and therefore difficult to predict.

> Every interaction between two systems/entities is an opportunity for a mismatch/error to be introduced.
> {.is-warning}

## The 5th Law: Effective Change Management is Critical to Managing Mental Models
> * Establish a baseline, sufficiently correct model of the system.  (This is likely to take a long time.)
> * Track the small changes against the baseline.  (These are likely to be quick.)

## Axiom 5: Humans are Mortal.
Shocker, I know.
### Axiom 5.1: Time is a finite currency that can either be "spent" or it can be "invested".
> Spend (v): To throw away; squander. 
> {.is-info}

> Invest

## The 5rd Law: Forward Progress 
> Always be working towards something larger, bigger, better, faster.

## The  