# Observed pair + adaptive-cutoff checkpoint

- README fresh-read at this wake; objective remains maximum utilization / minimum actual idle gap.
- Experimental variable remains same-wake useful-work duration only. Scheduler jitter is diagnostic, not optimized.
- actual_next_start_time: 2026-09-23T05:40:49+09:00
- predecessor work_end_time: 2026-09-23T05:31:39+09:00
- predecessor active_work_sec: 32
- idle_gap_sec: 550
- paired_utilization: 32 / (32 + 550) = 0.054983 (5.50%)
- predecessor pair is physically valid and observed-only.

## Decision checkpoint

- run_elapsed_sec at checkpoint: 12
- estimated_next_task_sec: 120
- handoff_safety_margin_sec: 120
- decision: CONTINUE useful work; a voluntary handoff after only tens of seconds is dominated by the observed 550-second boundary cost.
- No scheduler-jitter mechanism change in this experiment.
- Continuation was secured before durable state write, with the same recurring reservation enabled and moved to 05:53 KST.

## Interpretation

Two consecutive post-reanchor non-zero predecessor samples (28s then 32s) both show very low utilization because boundary idle dominates. This does not identify the optimal cutoff yet, but it strongly rejects tens-of-seconds voluntary handoff as an efficient operating point under current boundary costs. Continue extending observed same-wake useful-work duration without projecting future completion timestamps.
