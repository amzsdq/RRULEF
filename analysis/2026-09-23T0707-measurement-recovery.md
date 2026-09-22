# Measurement recovery — 2026-09-23 07:07 KST

## Fresh-read invariant
README objective remains maximum useful-work utilization / minimum real idle gap. Scheduler jitter is diagnostic only.

## Previous-run boundary
Previous canonical state ended useful work at 2026-09-23T07:03:00.133615+09:00. This wake's externally observed automation start is 2026-09-23T07:07:33+09:00, so the boundary idle gap is approximately 272.866 sec.

The predecessor's full `active_work_sec` is null because its early tasks were not individually timestamped; only `active_work_sec_observed_min=61.898` is defensible. Therefore this boundary MUST NOT be converted into a paired utilization value. Doing so would fabricate precision.

## Useful finding
The dominant measurement defect is now clear: doing substantive work before opening per-task timing makes a long wake unusable as cutoff evidence even when the work itself is useful. This is an instrumentation defect, not evidence against long same-wake work.

## Next-run protocol (measurement only; no scheduler-mechanism change)
At wake start, timestamp every substantive task boundary from task 1. Maintain a running sum of completed task durations. Use that sum for `active_work_sec`; never substitute wall-clock run elapsed. Continue useful tasks while the admission check remains safe. This changes only measurement completeness, not cutoff or wake mechanism.

## Handoff
Continuation was secured first for 2026-09-23T07:18:00+09:00 as the same enabled recurring automation. No attempt was made to optimize scheduler jitter.
