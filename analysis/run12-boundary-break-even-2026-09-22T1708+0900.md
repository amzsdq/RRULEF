# Run 12 boundary break-even calculation — 2026-09-22 17:08 KST

## Inputs
Indexed comparator: 323 sec active and 1470 sec observed idle across 10 comparable runs.

## Break-even framing
Suppose continuing useful work within the current wake avoids one future handoff boundary with idle gap g, but creates expected lost-work cost L because a longer run has some chance of forced termination. Same-wake continuation is favorable on utilization grounds whenever avoided idle plus avoided handoff overhead exceeds expected lost useful work and recovery cost.

The current evidence cannot estimate L because the indexed sample reports no forced stops and lacks literal near-cutoff runs. Therefore assigning a numeric timeout probability now would be fabricated.

What can be measured is the scale g already observed: mean observed idle gap in the 10-run set is 147 sec. Thus a continuation decision that safely absorbs a 60–120 sec useful task can plausibly avoid exposure to an idle boundary whose historical mean is larger than that task duration, without claiming the next gap will equal the mean.

## Consequence
The economically relevant missing number is not scheduler jitter. It is the forced-stop/lost-work cost curve as same-wake elapsed approaches the runtime limit. Until that curve has observations, premature handoff remains the directly observed controllable loss and 600 sec remains an unvalidated comparator rather than a tuned optimum.

## Decision tuple
- elapsed: below comparator
- estimated next bounded task: 60–120 sec
- safety margin: positive
- decision: CONTINUE

No experimental variable changed.
