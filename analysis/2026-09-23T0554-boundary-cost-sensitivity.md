# Boundary-cost sensitivity — 2026-09-23 05:54 KST

## Scope
Single experimental variable remains same-wake useful-work duration. Scheduler jitter mechanism is unchanged and is not optimized here.

## Fresh baseline definition
README defines the objective as maximum utilization / minimum actual idle gap, with 10 minutes only an initial timeout-avoidance heuristic.

## Newly closed predecessor pair
- predecessor active_work_sec: 12
- predecessor work_end_time: 2026-09-23T05:41:01+09:00
- actual_next_start_time: 2026-09-23T05:54:43+09:00
- idle_gap_sec: 822
- paired utilization: 12 / (12 + 822) = 0.014388 = 1.44%
- physical ordering: valid

This is a third post-reanchor non-zero pair in which tens-of-seconds useful work is dominated by boundary idle cost. It strengthens the conclusion that voluntary handoff after only tens of seconds is inefficient while safe useful work remains.

## Sensitivity only — not a new cutoff policy
For an observed boundary gap G, utilization from W seconds of useful work is W/(W+G). Using the three recent valid observed gaps 550s, 679s, and 822s gives median G=679s.

At G=679s:
- W=120s -> 15.02%
- W=300s -> 30.64%
- W=600s -> 46.91%
- W=720s -> 51.47%

Useful work required to reach a target utilization if boundary cost remained 679s:
- 50% -> 679s
- 60% -> 1018.5s
- 70% -> 1584.3s

These are sensitivity calculations, not permission to exceed runtime safety. The evidence says to keep extending useful work while safe, not to adopt 1018.5s or 1584.3s as cutoffs.

## Decision
Continue Baseline-A-style same-wake work rather than voluntarily handing off after a short task. At each task boundary, compare observed run elapsed + estimated next task + handoff safety margin against the runtime-risk frontier. Keep one-variable discipline: do not alter scheduler-jitter handling while probing useful-work duration.
