# Baseline A continuous-work execution plan — 2026-09-22 16:25 KST

## Purpose
Convert the prior execution-integrity finding into substantive work that can occupy the same wake instead of repeatedly handing off after bookkeeping. This does not change the cutoff or introduce a new experimental variable.

## Fresh-read constraints
- Invariant objective: maximize utilization / minimize actual idle gap.
- Baseline A initial cutoff remains 10 minutes.
- Scheduler jitter is diagnostic, not an optimization target.
- While safely below the budget, continue useful work in the same wake.

## Useful-work queue
These tasks are ordered so each produces durable evidence and can be completed independently:

1. **Measurement integrity audit**
   - Inspect recent run records for internally inconsistent timestamps/durations.
   - Flag cases where active_work_sec is claimed more precisely than connector timestamps justify.
   - Output: evidence table and correction recommendations; do not rewrite historical observations unless objectively wrong.

2. **Handoff-cost decomposition**
   - From comparable runs, separate useful work, observed idle gap, and known handoff overhead.
   - Estimate how much utilization could improve purely by eliminating premature handoffs, without assuming scheduler jitter improves.
   - Output: lower/central bounds using only observed data.

3. **Continuous-run acceptance criteria**
   - Define the minimum evidence needed to call a run a valid literal Baseline A sample: multiple sequential useful tasks, per-task duration evidence, decision tuple, no premature handoff while safety margin is high.
   - This is measurement hygiene, not a new scheduling policy.

4. **Adaptive-cutoff readiness check**
   - Only after valid continuous Baseline A samples exist, determine whether there is enough evidence to test one cutoff variable.
   - Until then, retain 10 minutes unchanged.

## Decision rule for this run family
At each completed small task, record elapsed time, estimated next-task duration, and safety margin. If safely below the 10-minute initial budget and another queue item is available, start it immediately. Handoff is justified by approaching the runtime-risk boundary, an actual blocker, or exhaustion of useful work—not by completion of bookkeeping alone.

## Why this is useful work
The first 10 comparable samples showed 323 sec active versus 1470 sec idle (18.0% aggregate utilization) while individual runs only used 8–72 sec of active work. The dominant actionable defect is therefore premature handoff, and this queue supplies substantive work to prevent another bookkeeping-only wake.