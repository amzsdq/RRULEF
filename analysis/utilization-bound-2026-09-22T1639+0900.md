# Conservative utilization bound — 2026-09-22 16:39 KST

## Inputs
Latest validation evidence supplies active_work_sec >=47 and preceding idle_gap_sec <=465. Both are bounds, not exact values.

## Bound
For utilization U = active / (active + idle), U increases with active and decreases with idle. Therefore substituting the minimum known active work (47) and maximum known idle gap (465) gives a conservative lower bound:

U >= 47 / (47 + 465) = 47 / 512 = 0.091796875, or >=9.18%.

This does not imply actual utilization was 9.18%; actual active work may be larger and actual idle gap may be smaller. The only defensible conclusion from these bounds is that this transition's utilization was at least 9.18% under the recorded inequalities.

## Optimization implication
The bound is still consistent with the earlier diagnosis: wakes that terminate after tens of seconds expose the system repeatedly to multi-minute idle gaps. No scheduler-jitter optimization is inferred. The controlled variable remains unchanged; obtain literal longer same-wake Baseline A samples before testing adaptive cutoff.

## Decision tuple after this task
- current elapsed: still below the 10-minute initial budget
- estimated next useful task: 60–120 sec
- handoff safety margin: high
- decision: CONTINUE
