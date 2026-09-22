# Clean boundary experiment v2 — 2026-09-22

## Objective
Maximize useful-work utilization / minimize true idle. Baseline A remains 600 sec; scheduler jitter remains diagnostic only.

## Fresh-read basis
README was fresh-read at run start. Prior overlap analysis showed that durable-save completion is not a valid substitute for useful-work end when the next wake can start concurrently.

## Single variable under test
Boundary placement only. No cutoff or scheduler-mechanism change.

For the next causal pair, record four distinct instants:
1. `actual_start_time` — first substantive action in this run.
2. `useful_work_end_time` — instant the last substantive task ends.
3. `handoff_decision_time` — instant the run decides not to start another substantive task.
4. `durable_handoff_complete_time` — continuation confirmation plus durable state persistence complete.

Derived quantities:
- `idle_gap_sec = next_actual_start_time - useful_work_end_time`, only if non-negative.
- `handoff_overhead_sec = durable_handoff_complete_time - handoff_decision_time`.
- `handoff_overlap_sec = max(0, durable_handoff_complete_time - next_actual_start_time)`; diagnostic, never counted as idle.

## Decision rule retained
After each bounded substantive task, record elapsed time, estimated next-task duration, and remaining margin to the 600-sec comparator. If elapsed is below 600 sec and there is no concrete timeout/forced-stop risk, continue immediately. Do not stop merely to improve measurement cleanliness.

## What counts as substantive work in this experiment
Fresh repository inspection, empirical reconciliation, measurement correction, and implementation of durable experiment state count when they directly advance the utilization experiment. Pure status narration does not.

## Current empirical conclusion
The observed 142-sec overlap invalidated a run-level durable-save marker as an idle boundary, but it does not justify reducing the 600-sec comparator. The next useful datum is a causally ordered pair using `useful_work_end_time`, not another proxy.
