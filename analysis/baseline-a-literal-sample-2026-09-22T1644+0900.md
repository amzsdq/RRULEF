# Baseline A literal sample — 2026-09-22 16:44 KST

## Fresh-read invariant
README was fresh-read at this wake. Objective remains maximum useful-work utilization / minimum actual idle gap. Scheduler jitter remains diagnostic only. Baseline A 10-minute initial cutoff is unchanged.

## Start anchors
- actual_next_start_time: 2026-09-22T16:44:21+09:00 (automation runtime start)
- previous durable work_end_time: >=2026-09-22T16:39:10+09:00
- therefore current idle_gap_sec: <=311 sec (upper bound; prior work_end is a lower bound)

## Task 1 — reconcile latest run against evidence ledger
Observed task interval is bounded by connector operations rather than a local monotonic clock, so do not manufacture exact active seconds.

Findings:
1. Latest run moved execution fidelity in the right direction: six substantive durable artifacts were completed in one wake, versus earlier bookkeeping-length wakes.
2. It still did not prospectively isolate per-task active intervals, so active_work_sec remains bounded rather than exact.
3. Its final work_end_time is only >=16:39:10, so this wake's idle gap is also an upper bound.
4. Therefore neither latest-transition utilization nor this transition should be reported as an exact point estimate.

## Decision tuple after task 1
- current elapsed: materially below 10-minute initial budget
- estimated next task: 60–120 sec
- handoff safety margin: high
- decision: CONTINUE

No experimental variable changed.
