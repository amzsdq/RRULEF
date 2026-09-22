# Idle-conditioned active target — 2026-09-22 22:35 KST

## Purpose
Continue the same sustained-work experiment; no mechanism change.

The just-closed direct idle pair is 296 s, materially above the retained post-anchor mean 178.15 s. Because jitter is exogenous and not optimized, this is not used to alter wake scheduling. It is useful for understanding how much active work is needed to amortize the observed boundary.

For paired utilization U=A/(A+296):
- A=60 s -> 16.85%
- A=180 s -> 37.82%
- A=296 s -> 50.00%
- A=300 s -> 50.34%
- A=480 s -> 61.86%
- A=600 s -> 66.96%

Thus the >=180 s milestone remains valuable as a direct test against recent 30-60 s windows, but with this particular idle exposure it does not reach 50% paired utilization. Roughly 296 s active is required merely to break 50% for this pair.

## Decision tuple after task
- current elapsed: still well below 600 s comparator
- estimated next useful task: <=120 s
- handoff safety margin: positive
- decision: CONTINUE

No threshold changed. This analysis prevents incorrectly treating 180 s as a universal utilization target; the correct target depends on actual following idle.
