# Utilization evidence update

Comparable canonical pairs observed in the current treatment series:

| predecessor active sec | following idle sec | paired utilization |
|---:|---:|---:|
| 20 | 319 | 5.90% |
| 105 | 261 | 28.69% |
| 32 | 304 | 9.52% |

Interpretation: the sample is small and idle varies exogenously, so it does not identify a causal slope. It does, however, show that bookkeeping-sized active blocks (20–32 s) leave utilization dominated by the several-minute idle cost, while the 105 s block produced substantially better paired utilization without a timeout or forced stop.

Decision: do not alter the cutoff yet. Continue increasing useful same-wake work when safe, recording task durations and preserving the same treatment variable. A stronger decision requires longer active blocks and additional clean pairs.
