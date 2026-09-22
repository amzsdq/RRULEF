# Evidence priority for the active-duration experiment

The repository now has three directly relevant completed-work regimes:

1. 61 sec active / 594 sec following idle = 9.31% utilization.
2. 63 sec active / 624 sec following idle = 9.17% utilization.
3. Earlier clean comparator: 105 sec active / 261 sec following idle = 28.69% utilization.

Because idle differs substantially, these observations do not estimate a causal duration-response slope. Their information value is asymmetric:
- Repeating another 30–70 sec active block adds little; that region is already known to be boundary-cost dominated.
- A >=180 sec completed-work block adds new runtime-frontier information and tests whether the treatment can escape bookkeeping-sized runs without forced stop.
- A sample progressively closer to the nominal 600 sec comparator is higher value after >=180 sec is demonstrated safe, but should not be inferred safe in advance.

Therefore the next-task admission priority is substantive bounded work that extends the current wake, not additional scheduler analysis. Scheduler jitter remains diagnostic only. The experiment remains single-variable.