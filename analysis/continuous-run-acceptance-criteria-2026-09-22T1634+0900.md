# Continuous-run acceptance criteria — 2026-09-22 16:34 KST

## Purpose
Determine whether a run is valid evidence for Baseline A without changing the 10-minute cutoff or scheduler mechanism.

## Valid literal Baseline A sample
A run is cutoff-evaluable only when all observable conditions hold:

1. Multiple sequential useful tasks are performed in the same wake when useful work remains.
2. Each completed small task has a duration or a conservative timing bound grounded in observable connector/runtime timestamps.
3. After each small task, the decision tuple is retained: current elapsed time, estimated next-task duration, and handoff safety margin.
4. If elapsed time is materially below the initial 10-minute budget, next-task estimate fits comfortably, safety margin is high, and useful work exists, execution continues rather than handing off.
5. A handoff before the budget is justified only by an actual blocker, exhausted useful queue, or credible runtime-risk boundary; bookkeeping completion alone is not justification.
6. active_work_sec does not count waiting/idle time or control-plane bookkeeping as useful work merely to inflate utilization.
7. timeout_or_forced_stop and incomplete-work loss are recorded rather than silently discarded.

## Classification of current evidence
- The earlier 8–72 sec wakes are useful idle-gap observations but are not valid evidence about whether a 10-minute cutoff is optimal, because they did not exercise that cutoff.
- The 16:25 corrective wake is directionally better because it completed three substantive durable analysis artifacts sequentially, but its recorded useful-work lower bound was only >=57 sec. It therefore remains an execution-fidelity sample, not a cutoff-limit sample.

## Consequence
Do not tune the 10-minute value from premature-handoff samples. First obtain runs that actually consume a substantial fraction of the available same-wake work budget without timeout. This prevents optimizing a parameter that the runtime has not yet exercised.