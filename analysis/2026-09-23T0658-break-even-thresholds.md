# Active-work thresholds at the newly observed 624 sec boundary

This keeps the same treatment variable and uses the observed 624 sec idle only as a conditional sensitivity value.

For target utilization U and fixed idle I, required active work is A = U*I/(1-U).

With I = 624 sec:
- To exceed the earlier clean 28.69% utilization comparator requires A > 251.2 sec.
- 40% requires 416 sec.
- 50% requires 624 sec.
- 60% requires 936 sec.

Interpretation: even the experiment's >=180 sec first frontier sample would yield only 22.39% if followed by another 624 sec idle gap. Thus >=180 sec remains valuable as a runtime-safety/frontier sample, but under a boundary this large it is not enough to demonstrate high duty cycle. The next evidence priority is still to obtain materially longer completed useful-work blocks without timeout/forced-stop, not to tune scheduler jitter.

No cutoff is promoted from this calculation.