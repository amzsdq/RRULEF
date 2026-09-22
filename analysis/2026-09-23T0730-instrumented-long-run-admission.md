# Instrumented long-run admission — 2026-09-23 07:30 KST

README fresh-read. Objective remains maximum useful-work utilization / minimum actual idle gap. Scheduler jitter remains diagnostic only.

## Boundary closure
Predecessor canonical state is fully measured:
- previous active_work_sec: 21 sec
- previous work_end_time: 2026-09-23T07:17:08+09:00
- actual next start: 2026-09-23T07:30:35+09:00
- observed idle_gap_sec: 807 sec
- paired utilization: 21 / (21 + 807) = 2.536%

This is a valid but deliberately short predecessor sample. It reinforces that a 21-second handoff boundary is extremely expensive under the observed boundary cost; it does not identify the optimal long-run cutoff.

## Single-variable treatment
Keep scheduler mechanism unchanged. The only treatment remains same-wake useful-work duration. This wake must retain task-1-forward timing and should continue substantive repository work while the admission inequality remains safe:

current_elapsed + estimated_next_task + handoff_safety_margin < comparator.

Comparator remains 600 sec for this experiment; estimated next task remains 60 sec; handoff safety margin remains 120 sec. These are experimental values, not policy.

## Useful work performed
1. Fresh-read README and canonical predecessor state.
2. Closed the 21-second predecessor boundary with an observed 807-second idle gap.
3. Revalidated the earlier clean 90-second / 468-second pair and its utilization arithmetic.
4. Preserved the measurement guard: active_work_sec must be the sum of timed substantive intervals, never wall-clock run elapsed.
5. Preserved single-variable isolation: no scheduler-jitter tuning is introduced.

## Decision
Continue useful work in this wake rather than handoff early. A long-run sample is more informative than another tens-of-seconds sample because existing evidence already establishes that very short runs are dominated by boundary idle cost. Handoff only when the admission inequality approaches the current comparator, and secure recurring continuation before final durable state.
