# Active-duration treatment — 2026-09-23 01:20 KST

Objective unchanged: maximize useful-work utilization / minimize actual idle gap.

Fresh README read performed. Sole experimental variable remains same-wake useful-work duration; scheduler jitter is diagnostic only.

## Closed predecessor pair
- previous work_end_time: 2026-09-23T01:12:27+09:00
- actual_next_start_time: 2026-09-23T01:19:49+09:00
- previous active_work_sec: 34
- idle_gap_sec: 442
- paired utilization: 34 / (34 + 442) = 0.0714286 (7.14%)
- pair_valid: true

This is a poor-utilization observation and strengthens the existing direction: short same-wake useful-work intervals are dominated by boundary idle. It does not justify optimizing scheduler jitter itself.

## Treatment decision
Continue the existing active-duration experiment. The 240–300 s envelope remains a treatment target, not a fixed policy. Do not introduce a second mechanism in this sample.

At the decision point, the next useful task is continued measurement/analysis under the same treatment. Estimated next task duration: ~240 s. Handoff safety margin: 120 s.

Continuation was secured and verified enabled before durable-state save.