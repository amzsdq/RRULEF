# Fully instrumented work admission — 2026-09-23 07:16 KST

## Invariant
Fresh README read confirms the objective remains maximum useful-work utilization / minimum real idle gap. Scheduler jitter is diagnostic only. Baseline A's 10-minute value is an initial runtime-safety comparator, not a fixed rule.

## Measurement repair now active
The prior wake established that long work is unusable as cutoff evidence if substantive tasks begin before timing starts. This wake therefore treats every substantive GitHub operation from task 1 as part of the measured work sequence. `active_work_sec` must be the sum of completed substantive task durations, never wall-clock elapsed.

## Boundary status
The predecessor state has no defensible full `active_work_sec` and no `work_end_time`; therefore no paired utilization can be manufactured for this boundary. This is preserved as missing evidence rather than backfilled.

## Single experimental variable
Keep scheduler mechanism, recurring transport, and safety-margin logic unchanged. The only treatment remains same-wake useful-work duration / admission toward the current ~600 sec comparator.

## Admission logic
At each completed useful task, record cumulative measured active work and wall-clock elapsed. Continue if a useful next task exists and `elapsed + estimated_next_task_sec + handoff_safety_margin_sec` remains within the current comparator; otherwise secure continuation first and hand off. Current planning values remain estimated_next_task_sec=60 and handoff_safety_margin_sec=120 until evidence supports changing one of them in a separate experiment.

## Useful result
The measurement defect is no longer a reason to terminate early. The next long same-wake run can now produce a valid active-work frontier sample because task timing starts before substantive work rather than after it.

## Continuation
The same recurring automation was re-anchored to 2026-09-23T07:28:00+09:00 and remained enabled before durable state work. No scheduler-jitter optimization was attempted.
