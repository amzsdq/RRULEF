# Active-duration frontier admission — 2026-09-23 01:53 +09:00

Objective: maximize useful-work utilization / minimize real idle gap. Scheduler jitter remains diagnostic only.

Fresh README result: Baseline A's 600 s budget is an initial timeout-avoidance estimate, not a fixed rule. The sole treatment variable remains same-wake useful-work duration.

Canonical predecessor available at wake:
- previous work_end_time: 2026-09-23T01:37:25+09:00
- previous active_work_sec: 300
- previous timeout_or_forced_stop: false
- previous requested wake: 2026-09-23T01:45:00+09:00

Current wake actual start: 2026-09-23T01:52:57+09:00.
Therefore the clean predecessor pair is:
- idle_gap_sec = 932
- paired utilization = 300 / (300 + 932) = 0.2435064935 (24.35%)

Interpretation: this is not evidence to optimize scheduler jitter. It is evidence that a 300 s useful-work interval can be dominated by the boundary idle cost. Holding this observed idle cost fixed only as sensitivity analysis, 600 s useful work would yield 600/(600+932)=39.16%, an absolute +14.81 percentage-point utilization improvement. No timeout/forced-stop was observed at 300 s, so the measured safety frontier is still above 300 s and below/at an unknown runtime limit.

Admission decision for this wake:
- elapsed at first decision: ~10 s
- estimated next useful task block: 120–180 s
- handoff safety margin: 120 s
- action: CONTINUE sustained useful work; do not lower cutoff because of scheduler jitter.
- experiment isolation: do not change wake mechanism, jitter handling, or safety margin in this sample; only extend useful-work duration toward the 600 s baseline frontier if runtime remains healthy.

Continuation was secured first as the same enabled recurring reservation before durable evidence was written.
