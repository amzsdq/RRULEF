# Sustained-work admission — 2026-09-23 08:42 KST

Objective: maximize useful-work utilization / minimize actual idle gap.

Fresh README read confirms scheduler jitter is diagnostic only. Baseline A's 600 s budget is an initial comparator, not a fixed rule.

## Closed predecessor boundary
- previous work_end_time: 2026-09-23T08:34:27+09:00
- previous active_work_sec: 33 s conservative observed minimum; incomplete measurement
- actual_next_start_time: 2026-09-23T08:42:06+09:00
- observed idle_gap_sec: 459 s
- paired utilization: not promoted to a clean cutoff sample because predecessor active_work_complete=false

## Admission decision
Keep exactly one experimental variable: same-wake useful-work duration.
- elapsed at initial admission: 0 s
- estimated next task: 60 s
- handoff safety margin: 120 s
- comparator: 600 s
- admission sum: 180 s
- action: continue substantive work; do not early-handoff merely to collect another short sample.

The recent evidence already makes repeated tens-of-seconds handoffs low-information. The next useful evidence is a fully instrumented sustained wake approaching the existing comparator without changing scheduler mechanism, estimated-task assumption, or safety margin.

Measurement rule for this wake: timestamp substantive task boundaries from task 1; active_work_sec is the sum of completed substantive task durations, never wall-clock run elapsed.
