# Handoff-overhead accounting correction

## Objective
Maximize useful-work utilization and minimize actual idle gap. Baseline A remains unchanged at the 600-second initial comparator.

## Empirical correction
The 17:49 run reported `handoff_overhead_sec <=503`, but that interval started at the last *bounded useful-work endpoint* (17:51:45), not at an observed handoff decision timestamp. Under README's definition, handoff overhead starts at the handoff decision. Therefore 503 seconds is not a valid handoff-overhead estimate; it is only an upper bound on a mixed interval containing uninstrumented useful work, connector latency, and bookkeeping.

Treating that mixed interval as handoff overhead would optimize the wrong component and could cause premature stopping of useful work.

## Measurement rule for the next sample
Do not change cutoff or scheduler mechanism. Record exactly one additional timestamp: `handoff_decision_time`. Then compute:

`handoff_overhead_sec = durable_handoff_complete_time - handoff_decision_time`

Keep `work_end_time` tied to the last actual useful-work endpoint, even when useful work continues after earlier checkpoints.

## Decision
No evidence supports changing the 600-second comparator yet. Continue same-wake useful work while elapsed + estimated next task + safety margin remains below the comparator, and measure the handoff phase separately when it actually begins.
