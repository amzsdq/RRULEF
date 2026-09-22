# RRULEF 02:03 — rearm failure correction + 600s admission

## Fresh objective
README fresh-read. Optimize actual idle gap and useful-work utilization; scheduler jitter remains diagnostic only.

## Closed predecessor pair
- previous work_end_time: 2026-09-23T01:55:27+09:00
- actual_next_start_time: 2026-09-23T02:03:24+09:00
- idle_gap_sec: 477
- previous_active_work_sec: 150
- paired_utilization: 150/(150+477) = 0.2392344498 (23.92%)

## Rearm failure diagnosis
The prior handoff requested 01:54 even though the scheduler write completed after 01:54. That made the requested DTSTART stale at write time. This is a handoff correctness failure, not evidence about scheduler jitter. The immediate correction is to require the selected DTSTART to still be future-dated at the scheduler write, without adding a jitter-optimization mechanism.

## Single experiment variable
Keep the experiment variable unchanged: same-wake useful-work duration.

The last clean sustained sample reached 300s without timeout/forced-stop. Current predecessor boundary idle is 477s. If boundary idle were held constant only for sensitivity analysis:
- 150s active => 23.92%
- 300s active => 38.61%
- 450s active => 48.54%
- 600s active => 55.71%

This does not prove the future idle distribution, but it shows why short 150s runs are expensive under observed boundary cost. There is still no timeout evidence justifying lowering the initial ~600s envelope.

## Admission decision
Continue toward a sustained ~600s useful-work sample without changing wake/jitter mechanisms. At each task boundary record elapsed, estimated next-task duration, and handoff safety margin. Stop before the runtime-risk frontier if the next task would consume the safety margin.
