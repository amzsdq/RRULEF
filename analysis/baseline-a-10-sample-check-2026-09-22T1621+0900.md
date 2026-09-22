# Baseline A — 10-sample execution check

## Result
The current bottleneck is not evidence that the 10-minute cutoff is too high or too low. The baseline has not actually been exercised near its stated cutoff.

Across the 10 comparable runs from 15:50 through 16:18 KST:
- total active_work_sec: 323
- total observed idle_gap_sec: 1470
- aggregate utilization: 323 / (323 + 1470) = 18.0%
- active work per run range: 8–72 sec
- timeout_or_forced_stop: 0 observed

## Interpretation
Every sampled run handed off after far less than the initial 10-minute budget. Therefore these samples mainly measure repeated short-run handoff + wake gaps, not the performance of Baseline A's intended continuous-work behavior.

Changing the cutoff now would confound the experiment. The next useful correction is not a new policy variable: execute the existing Baseline A literally. When elapsed/active work is far below 10 minutes and another safe useful task exists, continue in the same wake rather than ending after measurement bookkeeping.

## Experimental consequence
Keep the 10-minute initial cutoff unchanged until there are runs that actually approach it or until runtime evidence shows a smaller safe ceiling. Record each small task duration and the decision tuple (elapsed time, estimated next-task duration, safety margin). Only after comparable execution exists should an adaptive cutoff be A/B tested.

## Objective impact
At the observed aggregate, 82.0% of active+idle transition time is idle. Reducing repeated premature handoffs is directly aligned with the invariant objective and does not require optimizing scheduler jitter.