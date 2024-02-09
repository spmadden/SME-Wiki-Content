---
title: Metrics, Metrics, Everywhere
description: 
published: 1
date: 2024-02-09T01:08:10.994Z
tags: 
editor: markdown
dateCreated: 2024-02-09T01:08:10.994Z
---

- I write code - but that's not why I have a job
 	- I have a job because I write code that has **business value**
- **Business value means shipping a new feature that users actually adore**
  - Going back to an old feature that never really worked well and really making it pop
  - Writing code with fewer bugs = fewer support tickets = less time in Jira
  - Not pissing our users off with a slow, ugly, or pretty site
  - Refactoring your code and having well-factored code to make future changes easier
  - Adding a unit test BEFORE you fix that bug so you never have to fix it
- Business value is anything that makes people want to give us money
  - We like money, so we want to generate more business value
- We need to make better decisions about our code.

1. Our code generates business value when it RUNS
   a. Not when we write it.
   b. People don't give us money to hang our code on the wall
   
2. We need to know what our code does when it runs
   a. We need to **MEASURE** that.
   
3. Basic fundamental truth about reality: Map is not the territory
   a. The map of SFO is NOT the City of SFO
   b. The way that we talk about something is not the way the thing that it is
   c. Perception is not equal to Reality
   d. Both the map and territory are in a constant state of flux
   
4. There's a gap between what we think we know, and what we actually know
	 a. **MIND THE GAP**

5. We have a mental model of what our code does, but it's not actually the code itself
   a. This is what we use when we work with our code, predict the effects of a change, track down that bug
   b. **OUR MENTAL MODEL IS OFTEN WRONG**
   c. When our mental model is wrong: it is confusion.
   d. "This code can't possibly work" (it works)
   e. "This code can't possibly fail" (it blows up)

6. There's no physical correlation for what we do
   g. We don't have a off-kilter chair to remind us we're bad carpenters

7. Given two code samples
   a. Which is faster? We don't know.
   b. **We CAN'T KNOW until we MEASURE IT.**

8. This affects how we make decisions
   a. How we allocate our resources, etc.
   b. Do we play the guess-and-check game to figure out why the app is slow/broken?
   c. Or do we instrument the system to allow us to make a better, data-driven decision?
   d. Instrumentation allows us to make & improve our mental model that allows us to make better decisions.
   
9. We use our mental model to decide what do to.
   a. A better mental model makes us better at deciding what to do.
   b. A better mental model makes more business value.

10. **BUT ONLY IF WE'RE MEASURING THE RIGHT THING.**
    a. We need to measure our code where it MATTERS.
    b. In the wild, as it's generating business value.
    c. In production. Not on your laptop, not on a test cluster.

11. Five different ways of measuring our code in production:
    1. Gauges
       1. Instantaneous value of something at a specific point in time
       2. Ex: database size
       3. Metrics.gauge("cities", {cities.size})
    2. Counters
       1.  An incrementing and decrementing value
       2. Ex: # of simultaneous open connections
       3. Metrics.counter("connections").inc() // .dec()
    3. Meters
       1.  The average rate of events over a period of time
			 2. Ex: # of requests/sec
			 3. Metrics.meter("requests", SECONDS).mark()
       4. ~~Mean rate =!= #events /elapsed time~~
			 5.  The elapsed time matters. We care about recency. Mean rate isn't actually useful.
       6. Exponentially Weighted Moving Average is much better
          1. //TODO
          2. Constant: Alpha - smoothing factor
             1.  High = insensitive to variation in underlying data
             2.  Low = very sensitive to variation in underlying data
       7. 1-minute rate
       8. 5-minute rate
			 9. 15-minute rate
			 10.  Same formula as unix-load factor rate
    4. Histograms
       1. The statistical distribution of values in a stream of data
       2. Ex: # of results returned per request
       3. Metrics.histogram("response-sizes").update({results.size})
       4. Min/Max/Mean/StdDev
            1.  Mean works for NORMALLY DISTRIBUTED DATA
            2.  Most data isn't normally distributed.
            3.  Quantiles are FAR BETTER
            4.  Median/75th/95th/98th/99th/99.9th percentile
       5.  Reservoir Sampling
            1.  Keep a statistically representative sample of stream of data/measurements as they happen.
            2.  Don't quantile over the entire stream of data, use the reservoir
            3.  Vitter\'s Algorithm R. - Vitter. J. 1985
                a.  Produces uniform samples over the entire LIFETIME of the data
            4.  Forward-decaying priority sampling
                a.  See paper
                b.  Maintain a statistically representative sample of the LAST N MINUTES
    5. Timers
       1.  A histogram of durations, and a meter of calls.
       2. Ex: # of ms to respond
       3. Metrics.timer('requests', MILLISECONDS,SECONDS).time( { FN })
          1.  Name, DurationUnit, RecencyRate
       4. Result: "At ~2000 req/sec our 99% latency jumps from 13ms to 453ms"
    6. Each has a NAME, because random numbers are really hard to figure out at 3AM

12. When instrumenting/designing a system, we need to ask ourselves two questions
    1. What does this code DO that affects it's business value?
    2. How can we measure that?

13. Rule of thumb: If it can affect the business value of your code - ADD A METRIC AND MEASURE IT.
    1. Most services/apps have some 40-50 metrics
       1. Each has 1-10 different measurements

14. Collect all that data & store it.
15. Monitor it
    1. Nagios/Zabbix/Whatever
    2. If it affects business value: Someone gets their ass woken up.

16. Aggregate it
    1. Ganglia/Graphite/Cacti/Whatever - all are horrible in slightly different ways
    2. Place current values in an historical context.
    3. See long-term patterns in the behavior of your code.
       1. This is REALLY the TRUE VALUE of the process.
       2. This allows you to go FASTER and shorten our decision-making cycle.

- OODA Loop: Applies to software just as much as fighter pilots, just with less shooting and flames (hopefully)
  - Observe - observe something about the world
  - Orient - orient it with all of our other data, emotions, tactics, thoughts - extract meaning
  - Decide - decide what to do
  - Act - act.

- If we do this faster - we will win.
  - Ship fewer bugs because your mistakes will not live as long
  - Will ship more features because you won't be working on things that don't matter
  - This makes happier uses, and happier users means more money

- We might write code
- We have to generate business value
- In order to know how well we're doing that, we need metrics to understand and gather the data.
    - DATA. DRIVEN. DECISIONS.
- Aggregate these values for historical perspective to gain long-term patterns
- The map is not the territory, we need to improve our mental model of the system to make better decisions
