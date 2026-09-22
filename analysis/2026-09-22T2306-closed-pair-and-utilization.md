# Closed pair and sustained-work experiment — 2026-09-22 23:06 KST

README fresh-read. Objective remains maximum useful-work utilization / minimum actual idle gap.

## Clean causal pair
- previous durable work_end_time: 2026-09-22 22:59:05 KST
- actual_next_start_time: 2026-09-22 23:06:53 KST
- idle_gap_sec: 468
- prior active_work_sec: ~90
- paired utilization: 90 / (90 + 468) = 16.13%

This pair is clean because the prior run explicitly durably recorded its final work_end_time. It replaces the previous run's intentionally unpromoted 574-sec pseudo-gap.

## Interpretation
The current single experiment variable remains same-wake active-work extension. Wake-lead tuning is not introduced in this sample.

At an observed idle cost of 468 sec, hypothetical utilization if idle stayed equal:
- active 180 sec -> 27.78%
- active 300 sec -> 39.06%
- active 468 sec -> 50.00%
- active 600 sec -> 56.18%

These are diagnostic break-even values, not policy cutoffs. The result strengthens the case that ~90-sec useful-work runs are too short when each handoff can incur several minutes of real idle.

## Decision
Continue useful bounded repository work within the same wake rather than handoff merely to collect another idle sample. Preserve the current scheduler mechanism during this experiment so only active-work duration is being varied. Before eventual handoff, secure the same recurring continuation first and durably record a final work_end_time.
