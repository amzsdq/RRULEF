# 600s frontier admission — 2026-09-23 01:45 KST

Objective remains maximum useful-work utilization / minimum actual idle gap.

Fresh README confirms the 600s Baseline-A budget is an initial timeout-avoidance estimate, not a fixed rule. The only experiment variable remains same-wake useful-work duration.

Predecessor durable sample:
- active_work_sec: 300
- work_end_time: 2026-09-23T01:37:25+09:00
- timeout_or_forced_stop: false
- next scheduled wake had been 01:45

Current actual start: 2026-09-23T01:44:43+09:00
Closed predecessor pair:
- idle_gap_sec: 438
- paired_utilization: 300 / (300 + 438) = 0.4065 (40.65%)
- pair_valid: true

Interpretation:
The 300s sample completed without timeout, but the following boundary cost was 438s, so stopping at 300s produced poor paired utilization. With the same observed 438s idle held constant only as a sensitivity reference, 600s active work would yield 57.80% utilization. This does not assume idle is controllable; it shows why measuring a longer safe active interval is high-value.

Admission decision:
- continue the same active-duration experiment toward the 600s frontier when useful work is available;
- do not change wake mechanism, jitter handling, or other policy in this experiment;
- record elapsed time, estimated next task duration, and safety margin before admitting each additional task;
- a timeout/forced stop is failure-cost evidence; a clean sample near 600s is evidence that the prior 300s stopping point was premature.
