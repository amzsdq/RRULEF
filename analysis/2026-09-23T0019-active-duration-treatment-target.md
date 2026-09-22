# Active-duration treatment target — 2026-09-23 00:19 KST

Objective remains maximum useful-work utilization / minimum real idle gap. Scheduler jitter is diagnostic only.

Fresh canonical predecessor:
- previous work_end_time: 2026-09-23T00:17:59+09:00
- previous active_work_sec: 74
- previous requested next wake: 2026-09-23T00:21:00+09:00

This wake began before the previously requested boundary, so the predecessor-to-start pair must be treated as overlap-invalid rather than coercing negative idle to zero. It is not admitted to utilization evidence.

Single experimental variable remains same-wake useful-work duration. The next useful treatment target remains a directly measured >=180 s useful-work block without timeout/forced stop, followed by a clean non-overlapping successor so its real idle gap can be paired. No cutoff, jitter, or wake mechanism is changed in this experiment.

Decision record:
- elapsed_sec_at_decision: 13
- estimated_next_task_sec: 180
- handoff_safety_margin_sec: 120
- action: continue useful work / preserve treatment target
- rationale: the current evidence is dominated by short active blocks and variable exogenous idle; obtaining a sustained block is more informative than adding another policy.
