# Boundary-elimination empirical sample — 2026-09-22 18:13 KST

Objective: maximum useful-work utilization / minimum actual idle gap. Baseline A comparator remains 600 sec; no cutoff or scheduler variable changed.

## Direct observations

- run_start_time: 2026-09-22T18:13:37+09:00 (automation runtime timestamp)
- task_1_start_time: 2026-09-22T18:13:37+09:00
- task_1_end_time: 2026-09-22T18:13:54+09:00 or earlier
- task_1_duration_sec: <=17 sec wall-clock bound; README fresh read + prior-run/measurement-contract fresh reads + continuation secured
- scheduled_next_wake: 2026-09-22T18:25:00+09:00
- recurring/enabled confirmation: 2026-09-22T18:13:54+09:00
- timeout_or_forced_stop: false

Because connector completion timestamps are only available as observed response times rather than task-internal timestamps, the task duration is retained as a bound rather than promoted to exact active_work_sec.

## Decision after task 1

- run_elapsed_sec: <=17 sec
- estimated_next_task_sec: 60 sec
- handoff_safety_margin_sec: >=523 sec relative to the 600-sec comparator
- decision: CONTINUE. The margin is strongly positive and there is no concrete timeout/forced-stop signal.

## Substantive result

The previous run handed off at only 28 sec despite a stated positive 572-sec comparator margin, solely because instrumentation had not started at its first task. This sample removes that reason: instrumentation is active from run start, so early voluntary handoff is not justified by the measurement contract. The correct Baseline-A action is to continue useful work in this same wake while the safety margin remains positive.
