# Active-duration treatment — 2026-09-22 23:50 KST

Objective remains maximum useful-work utilization / minimum real idle gap. Scheduler jitter is diagnostic only.

## Clean pair
- previous_work_end_time: 2026-09-22T23:45:27+09:00
- actual_next_start_time: 2026-09-22T23:50:31+09:00
- idle_gap_sec: 304
- previous_active_work_sec: 32
- paired_utilization: 32 / (32 + 304) = 0.095238 (9.52%)
- previous_scheduled_next_wake: 2026-09-22T23:50:00+09:00
- scheduler_jitter_sec: 31 (diagnostic only)

## Treatment discipline
The sole treatment variable remains same-wake useful-work duration. No cutoff rule, jitter policy, or wake mechanism is changed in this run.

The 32-second predecessor run is materially too short relative to the observed 304-second idle cost. With idle held constant only as a leverage calculation, 304 seconds of active work would be required for 50% paired utilization, 456 seconds for 60%, and about 709 seconds for 70%. These are not new cutoffs; they show why terminating after bookkeeping-sized work is inefficient.

## Admission decision
At this checkpoint the run is still far below the 10-minute baseline budget. The next useful task is to preserve the clean measurement chain and continue the active-duration treatment rather than hand off immediately. A continuation wake has nevertheless been secured first as failure protection. No scheduler-jitter optimization is attempted.
