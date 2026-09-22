# Cutoff decision evidence — 2026-09-23 06:08 KST

## Objective
Maximize useful-work utilization / minimize actual idle gap. Scheduler jitter remains diagnostic only.

## Variable discipline
Only same-wake useful-work duration remains under evaluation. No scheduler mechanism is changed.

## Fresh predecessor pair
- previous active_work_sec: 63
- previous work_end_time: 2026-09-23T05:55:46+09:00
- actual next start: 2026-09-23T06:07:50+09:00
- idle_gap_sec: 724
- paired utilization: 63 / (63 + 724) = 8.0051%
- physical ordering: valid
- predecessor forced stop: false

## Evidence table retained
- 12s active / 822s idle -> 1.44%
- 28s active / 679s idle -> 3.96%
- 32s active / 550s idle -> 5.50%
- 63s active / 724s idle -> 8.01%
- earlier clean: 105s active / 261s idle -> 28.69%

Idle gaps are exogenous/noisy, so this is not a causal duration curve. It is sufficient to reject voluntary handoff in the tens-of-seconds region while safe useful work remains: the boundary idle cost is several times larger than useful work in every recent short sample.

## Decision record for adaptive-cutoff comparison
At this wake, the decision variables are recorded as:
- elapsed_sec_at_decision: 0 at initial decision point
- estimated_next_task_sec: 120
- handoff_safety_margin_sec: 120
- decision: continue useful work; do not voluntarily hand off in the short-duration region

No claim is made that 600s, 720s, or any longer cutoff is optimal. A frontier value becomes evidence only after observed completed work and an observed work_end_time. Timeout/forced stop is retained as failure cost.
