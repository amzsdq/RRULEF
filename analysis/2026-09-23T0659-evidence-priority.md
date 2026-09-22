# Evidence priority for the active-duration experiment

Directly relevant completed-work regimes now include:

1. 61 sec active / 594 sec following idle = 9.31% utilization.
2. 63 sec active / 624 sec following idle = 9.17% utilization.
3. Earlier clean comparator: 105 sec active / 261 sec following idle = 28.69% utilization.
4. Historical sustained sample: approximately 180 sec active / 684 sec following idle = 20.83%, timeout_or_forced_stop=false.

Because idle differs substantially, these observations do not estimate a causal duration-response slope. Their information value is asymmetric:
- Repeating another 30–70 sec active block adds little; that region is already known to be boundary-cost dominated.
- The first ~180 sec safety/frontier sample already exists and did not force-stop.
- A materially longer completed sample, around 300 sec and then progressively toward the nominal 600 sec comparator if safe, now has higher information value.

Therefore the next-task admission priority is substantive bounded work that extends the current wake beyond the already-demonstrated ~180 sec region, not additional scheduler tuning. Scheduler jitter remains diagnostic only. The experiment remains single-variable.