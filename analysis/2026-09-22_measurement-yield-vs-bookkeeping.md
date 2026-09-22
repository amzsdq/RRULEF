# Measurement yield vs bookkeeping — 2026-09-22 20:07 KST

## Fresh baseline
README was fresh-read. Baseline A remains the comparator: continue useful work below ~600 sec, secure continuation before timeout risk, and optimize actual idle gap / useful-work utilization rather than scheduler jitter.

## Evidence audit
The latest durable run (`runs/2026-09-22T1954+0900.md`) closed the second corrected causal idle sample at 570 sec, but explicitly left `active_work_sec` and `handoff_overhead_sec` unasserted. It also records four substantive units before final save.

Across the recent sequence, measurement quality improved (bad mixed boundaries -> direct endpoint -> two clean idle samples), but useful-work accounting is still too weak to compare actual utilization because active work is not measured directly.

## Bottleneck
The current bottleneck is no longer the idle-gap formula. It is measurement yield per wake:
- repeated policy/audit documents consume execution time;
- exact active-work duration is still missing;
- therefore utilization remains hypothetical even after clean idle samples exist.

## Next experiment candidate (not activated in this run)
Change one variable only: task-duration instrumentation.
For each substantive unit, capture `task_start`, `task_end`, and `duration_sec`; sum durations into `active_work_sec`. Do not change the 600-sec cutoff or wake mechanism in the same experiment.

This directly tests the objective because it converts utilization from a sensitivity calculation into an observed metric.

## Decision
No cutoff change. No scheduler-mechanism change. Preserve the two clean idle samples (91 sec, 570 sec) and prioritize observed active-work measurement on the next clean run.
