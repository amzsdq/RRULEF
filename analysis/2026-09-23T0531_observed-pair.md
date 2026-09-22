# Observed pair — 2026-09-23 05:31 KST

README fresh-read. Objective remains maximum useful-work utilization / minimum actual idle gap. The experiment variable remains same-wake useful-work duration; scheduler jitter is diagnostic only.

## Closed physical pair
- previous work_end_time: 2026-09-23T05:19:48+09:00
- previous active_work_sec: 28
- actual_next_start_time: 2026-09-23T05:31:07+09:00
- idle_gap_sec: 679
- paired utilization: 28 / (28 + 679) = 3.96%
- scheduled_for: 2026-09-23T05:30:00+09:00
- scheduler_jitter_sec: +67

This is the first post-reanchor pair with a non-zero observed predecessor duration. The boundary is physically valid because previous work_end_time precedes actual start.

## Interpretation
The 28-second predecessor is far too short relative to a 679-second handoff boundary cost. This does not establish a new cutoff; it establishes that voluntary handoff at tens-of-seconds useful-work duration is strongly dominated whenever safe useful work remains. At the same 679-second boundary cost, hypothetical utilization would be 30.63% at 300 seconds active work and 46.91% at 600 seconds active work. These are sensitivity values only.

## Admission decision
Continue the same experiment variable. Do not tune scheduler lead from this sample. At each bounded unit record elapsed time, estimated next-task time, and handoff safety margin; continue while the next safe useful unit fits the current runtime-risk envelope. Preserve observed-only duration measurement.
