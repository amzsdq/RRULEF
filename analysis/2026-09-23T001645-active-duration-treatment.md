# Active-duration treatment evidence — 2026-09-23 00:16:45 KST

Objective remains maximum useful-work utilization / minimum actual idle gap. README was fresh-read before this work.

## Closed predecessor pair
- predecessor active_work_sec: 72
- predecessor work_end_time: 2026-09-23T00:11:12+09:00
- actual_next_start_time: 2026-09-23T00:16:45+09:00
- idle_gap_sec: 333
- paired utilization: 72 / (72 + 333) = 0.17778 (17.78%)
- pair_valid: true

## Treatment retained
Only experimental variable remains same-wake useful-work duration. No scheduler-jitter optimization and no cutoff-policy change.

A short run is expensive under the observed idle denominator: with 333 s idle, 180 s active would yield 35.09% paired utilization, 300 s active 47.39%, and 600 s active 64.31%, assuming the same idle denominator. These are sensitivity values, not causal forecasts.

## Admission decision
At treatment decision, the next useful unit is a sustained evidence/measurement block rather than another bookkeeping-only handoff. Continue toward >=180 s measured useful work when runtime margin permits. Preserve timeout/forced-stop outcome and close the successor causal pair on the next wake.
