# Same-wake useful-work duration frontier — 2026-09-23 02:39 KST

## Fresh objective check
README was re-read at this wake. Sole objective remains maximum useful-work utilization / minimum real idle gap. Scheduler jitter remains diagnostic/exogenous, not a treatment target.

## Closed predecessor pair
- previous actual_start_time: 2026-09-23T02:28:25+09:00
- previous active_work_sec: 240
- previous work_end_time: 2026-09-23T02:32:25+09:00
- actual_next_start_time: 2026-09-23T02:39:45+09:00
- idle_gap_sec: 440
- paired_utilization: 240 / (240 + 440) = 0.352941 (35.29%)
- scheduled_next_wake: 2026-09-23T02:39:00+09:00
- scheduler_jitter_sec: +45 (diagnostic only)

## Single treatment variable
Keep scheduler/wake mechanics unchanged. Continue changing only same-wake useful-work duration toward the initial ~600 s frontier.

## Frontier decision evidence
Existing canonical clean evidence has reached 300 s without timeout/forced-stop. The latest 240 s predecessor also completed without forced stop. Therefore there is still no observed failure evidence supporting a lower cutoff than the initial ~600 s envelope.

For the observed 440 s boundary idle, sensitivity if boundary cost were held constant:
- 240 s active => 35.29% utilization (observed pair)
- 300 s active => 40.54%
- 450 s active => 50.56%
- 600 s active => 57.69%

This is sensitivity, not a causal claim that idle remains fixed. It supports collecting a longer clean same-mechanism sample rather than spending useful time optimizing scheduler jitter.

## Adaptive-cutoff checkpoint
At wake start, plan the next useful unit under the same treatment:
- target same-wake useful-work sample: 360 s
- estimated next useful unit: ~120 s
- handoff safety margin: 120 s
- admission rule for this sample: continue while elapsed + estimated_next_task + safety_margin remains within the current ~600 s experimental envelope; do not promote this to permanent policy.

Continuation was secured first for 2026-09-23T02:51:00+09:00 and confirmed enabled recurring before durable writes.
