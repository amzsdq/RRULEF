# Instrumentation recovery — executable next step

Fresh README read at this wake confirms the invariant remains maximum useful-work utilization / minimum actual idle gap. Scheduler jitter is diagnostic only.

## Current blocker in evidence, not execution
The predecessor canonical state has `work_end_time=null` and `active_work_sec=null`, so the current boundary cannot be paired without fabrication. This does **not** justify another short wake or another sensitivity memo.

## Useful work completed this wake
1. Fresh-read README and canonical state.
2. Verified that the canonical state itself identifies exact task-boundary timing as the missing measurement surface.
3. Converted that observation into an executable measurement protocol rather than changing the experiment.
4. Secured the same recurring continuation before durable-state write.

## Measurement protocol for the next directly observable task boundary
- Record `task_start_time` immediately before a substantive GitHub operation when the runtime exposes a trustworthy timestamp.
- Perform the substantive operation.
- Record `task_end_time` immediately after completion when directly observable.
- Add only completed, directly observed intervals to `active_work_sec`.
- If either boundary is unavailable, leave the duration null; do not substitute connector latency, scheduled time, or whole-turn wall time.
- Continue useful work in the same wake while the elapsed-time + estimated-next-task + safety-margin budget remains safe.

## Experiment integrity
Changed treatment variable: none beyond the already-selected same-wake useful-work duration.
Fixed: estimated next task 60 s; handoff safety margin 120 s; comparator 600 s; scheduler mechanism.

The next high-value evidence remains a sustained same-wake run with completed-task timing, not another sub-minute handoff sample.