# Frontier promotion gate — 2026-09-23 14:34 KST

## Objective
Maximize useful-work utilization and minimize actual idle gap. Scheduler jitter remains diagnostic only.

## Fresh state
- README Baseline A: continue valid same-wake work while safe; 10 minutes is an initial comparator, not a fixed rule.
- Verified frontier: 480 s active work, followed by 251 s actual idle gap, paired utilization 0.65663475, no forced stop.
- Next treatment target: 600 s.

## Promotion gate
The 600 s treatment may be promoted only when all of the following are present in one directly observed completed run:
1. `active_work_sec >= 600` from direct task-boundary timing, not a target/admission value.
2. `work_end_time` is directly recorded.
3. `timeout_or_forced_stop = false`.
4. The following wake records `actual_next_start_time`, allowing `idle_gap_sec = actual_next_start_time - work_end_time`.
5. Paired utilization is then computed from the observed active interval and observed idle gap.

Until those conditions exist, 480 s remains the verified frontier. Repository arithmetic, filenames, commit latency, connector latency, scheduled wake time, and scheduler jitter cannot promote it.

## Operational consequence
Do not spend future wakes re-deriving the 480→600 sensitivity. If direct timing is unavailable, perform other bounded substantive repository work. If direct timing becomes available, prioritize the 600 s treatment because it is the next experiment that can change the frontier.

## Single changed variable
Same-wake useful-work duration only. Keep estimated next-task duration and handoff safety margin unchanged for this treatment.
