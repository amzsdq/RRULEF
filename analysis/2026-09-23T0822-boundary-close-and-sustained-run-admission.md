# 2026-09-23 08:22 KST — boundary close and sustained-run admission

Fresh-read README objective: maximize useful-work utilization / minimize actual idle gap. Scheduler jitter remains diagnostic only.

## Closed predecessor boundary
- predecessor actual_start_time: 2026-09-23T08:14:28+09:00
- predecessor active_work_sec: 75
- predecessor work_end_time: 2026-09-23T08:15:43+09:00
- actual_next_start_time: 2026-09-23T08:22:16+09:00
- idle_gap_sec: 393
- paired utilization: 75 / (75 + 393) = 0.1602564103 = 16.026%
- pair_valid: true
- timeout_or_forced_stop on predecessor: false

This is another valid short-run boundary sample. It reinforces that repeated ~minute-scale handoffs pay a large boundary cost, but it does not estimate the optimal cutoff.

## Experiment control
Only experimental variable remains same-wake useful-work duration. Scheduler mechanism, measurement semantics, estimated_next_task_sec=60, handoff_safety_margin_sec=120, and comparator_sec=600 remain unchanged.

Short-run evidence is saturated. Highest-information next observation is a fully instrumented sustained wake toward the current 600-second comparator, while preserving the admission inequality current_elapsed + estimated_next_task + safety_margin < comparator before starting another task.

Continuation was secured as the same enabled recurring reservation before durable-state write.
