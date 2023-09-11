#### Number of Threads for an optimized thread pool

-   \$N\_{cpu}\$ = Number of Available CPUs
-   \$U\_{cpu}\$ = Target utilization of those CPUs (0 \<= \$U\_{cpu}\$ \<= 1)
-   \$W_c\$ = Ratio of Wait time / Compute time

Following the formula: \$ N\_{threads} = N\_{cpu} \* U\_{cpu} \* (1 - W_c)\$

You can determine the number of CPUs using Runtime:

``` java
int N_CPUS = Runtime.getRuntime().availableProcessors();
```
