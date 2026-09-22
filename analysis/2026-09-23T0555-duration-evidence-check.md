# Same-wake duration evidence check — 2026-09-23 05:55 KST

## Variable discipline
Only same-wake useful-work duration is under evaluation. No scheduler-jitter mechanism change is introduced.

## Comparable observed evidence retained
Recent post-reanchor pairs:
- 28s active / 679s idle -> 3.96% utilization
- 32s active / 550s idle -> 5.50% utilization
- 12s active / 822s idle -> 1.44% utilization

Earlier clean observed evidence includes:
- 105s active / 261s idle -> 28.69% utilization

The idle gaps are not controlled, so the utilization differences are not a clean causal estimate of duration alone. However, every tens-of-seconds block is economically dominated by boundary idle cost, while the 105s block demonstrates that materially longer same-wake work can amortize a boundary substantially better without a recorded forced stop.

## What can and cannot be concluded
Can conclude: voluntary handoff after only tens of seconds should not be treated as a desirable operating point while safe useful work remains.

Cannot conclude: 10 minutes, 12 minutes, or any longer value is proven optimal. The previous projected-duration bug invalidated claims that were not based on observed completion timestamps.

## Next discriminating evidence
Keep extending observed same-wake useful work under the existing runtime safety envelope. Record each completed task duration and only close a frontier sample with an observed work_end_time. A timeout/forced-stop event is a failure-cost observation, not evidence to be discarded.
