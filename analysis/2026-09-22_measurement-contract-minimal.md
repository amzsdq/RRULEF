# Minimal measurement contract — 2026-09-22

Objective remains maximum useful-work utilization / minimum actual idle gap. This is measurement instrumentation, not a new policy.

For the next same-wake sample, record only directly observed timestamps:

- `run_start_time`: timestamp immediately before first substantive task.
- For every completed substantive task: `task_start_time`, `task_end_time`, and `duration_sec = end-start`.
- After each task: `run_elapsed_sec`, `estimated_next_task_sec`, and `handoff_safety_margin_sec`.
- `handoff_decision_time`: timestamp only when the decision to stop substantive work is actually made.
- `handoff_complete_time`: timestamp after recurring wake is confirmed enabled and durable state is committed.

Derived values:

- `active_work_sec = sum(task durations)`; connector waiting/bookkeeping is not silently counted as useful work.
- `handoff_overhead_sec = handoff_complete_time - handoff_decision_time`.
- On the next wake, `idle_gap_sec = actual_next_start_time - previous work_end_time`.

Baseline A comparator remains 600 sec. Continue another useful task while the current run remains below the comparator and there is no concrete timeout/forced-stop risk. Do not infer a timeout risk merely from elapsed connector latency. No scheduler-jitter optimization is introduced.
