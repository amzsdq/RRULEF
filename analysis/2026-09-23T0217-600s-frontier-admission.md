# 600s frontier admission — 2026-09-23 02:17 KST

## Fresh baseline
README fresh-read this wake. Objective remains maximum useful-work utilization / minimum actual idle gap. Scheduler jitter remains diagnostic only.

## Closed predecessor pair
- previous_work_end_time: 2026-09-23T02:06:54+09:00
- actual_next_start_time: 2026-09-23T02:17:00+09:00
- idle_gap_sec: 606
- previous_active_work_sec: 210
- paired_utilization: 210 / (210 + 606) = 0.257353 (25.74%)

## Single-variable experiment
Only same-wake useful-work duration remains the treatment variable. Wake mechanism and jitter handling are unchanged.

Observed safe duration evidence includes a 300s run with timeout_or_forced_stop=false. There is still no measured timeout frontier near the nominal 600s Baseline-A budget. With the just-observed 606s boundary idle held only as a sensitivity reference:
- 210s active => 25.74% utilization
- 300s active => 33.11%
- 450s active => 42.61%
- 600s active => 49.75%

This does not prove 600s is safe, but it makes a near-600s sustained useful-work sample the highest-information next treatment while keeping all other mechanisms fixed.

## Admission decision
At wake start, target a sequence of small useful tasks and continue while cumulative useful work remains below the current ~600s baseline and the estimated next task plus 120s handoff margin does not create material timeout risk. Do not lower the cutoff merely because scheduler jitter is large.

Continuation was re-armed first for 2026-09-23T02:28:00+09:00 and kept enabled/recurring before this durable write.
