---
title: thread_pool_size
description: 
published: 1
date: 2023-09-20T23:01:04.734Z
tags: 
editor: markdown
dateCreated: 2023-09-11T02:04:14.343Z
---

#### Number of Threads for an optimized thread pool

-   $N_{cpu}$ = Number of Available CPUs
-   $U_{cpu}$ = Target utilization of those CPUs (0 <= $U_{cpu}$ <= 1)
-   $W_c$ = Ratio of Wait time / Compute time

Following the formula: $N_{threads} = N_{cpu} * U_{cpu} * (1 - W_c)$

You can determine the number of CPUs using Runtime:

``` java
int N_CPUS = Runtime.getRuntime().availableProcessors();
```
