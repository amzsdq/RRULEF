# Active-duration treatment — 2026-09-23 01:25 KST

Objective remains maximum useful-work utilization / minimum real idle gap. Scheduler jitter remains diagnostic only.

## Fresh baseline read
README was re-read at this wake. Baseline A continues useful tasks while accumulated useful work is below the initial ~10-minute budget, unless timeout risk makes handoff safer. The 10-minute value is not a fixed rule.

## Clean predecessor pair
- previous_work_end_time: 2026-09-23T01:22:20+09:00
- actual_next_start_time: 2026-09-23T01:25:28+09:00
- idle_gap_sec: 188
- previous_active_work_sec: 151
- paired_utilization: 151 / (151 + 188) = 0.4454277286 (44.54%)
- previous_scheduled_next_wake: 2026-09-23T01:25:00+09:00
- scheduler_jitter_sec: 28 (diagnostic only)

## Treatment discipline
The sole experiment variable remains same-wake useful-work duration. No wake mechanism, scheduler-jitter policy, or additional cutoff mechanism is changed.

The clean predecessor improves materially over the immediately preceding 34s/442s pair, but 151 seconds remains far below the initial 10-minute useful-work budget. Holding the observed 188-second idle only as a leverage calculation, 188 seconds active work yields 50% utilization; 282 seconds yields 60%; 439 seconds yields 70%; and 752 seconds yields 80%. These are sensitivity values, not policy thresholds.

## Admission checkpoint
At the first checkpoint, elapsed useful-work budget consumption is still far below the baseline envelope. Estimated next useful task: ~120 seconds. Handoff safety margin retained: 120 seconds. Decision: continue useful work rather than terminate after bookkeeping. A same recurring continuation was secured first as failure protection and verified enabled before durable-state write. No jitter optimization was attempted.
