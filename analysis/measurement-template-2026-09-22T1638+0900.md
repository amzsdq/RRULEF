# Same-wake measurement template — 2026-09-22 16:38 KST

Purpose: make a future literal Baseline A wake reconstructable without treating control-plane bookkeeping as useful work. This is a measurement artifact, not a new policy.

## Start
- actual_start_time:
- previous_work_end_time:
- exact_idle_gap_sec (only if both anchors exact):

## Task ledger
For each substantive task append one row immediately after completion.

| task | task_start | task_end | duration_sec | useful output | elapsed_at_decision_sec | next_task_estimate_sec | handoff_safety_margin | decision |
|---|---|---|---:|---|---:|---:|---|---|
| 1 | | | | | | | | |
| 2 | | | | | | | | |
| 3 | | | | | | | | |

Rules for measurement only:
- duration_sec uses observed timestamps where available; otherwise mark a bound rather than inventing precision.
- active_work_sec is the sum of substantive task durations, excluding wake scheduling, status prose, and durable bookkeeping unless that bookkeeping itself is the substantive task.
- while elapsed is materially below the current 10-minute initial budget, a safe next useful task fits, and useful work exists, record CONTINUE and execute it.

## End
- active_work_sec:
- work_end_time:
- run_elapsed_sec:
- tasks_completed:
- timeout_or_forced_stop:
- handoff_decision_time:
- handoff_secured_time:
- handoff_overhead_sec:
- scheduled_next_wake:

## Decision tuple after creating this template
- current elapsed: materially below 10 min
- estimated next useful task: 60–120 sec
- handoff safety margin: high
- decision: CONTINUE
