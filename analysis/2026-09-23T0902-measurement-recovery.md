# Measurement recovery — 2026-09-23 09:02 KST

## Fresh invariant
README was fresh-read. Objective remains maximum useful-work utilization / minimum actual idle gap. Scheduler jitter remains diagnostic only. Baseline A's 600 s is an initial comparator, not a fixed rule.

## Current defect
The latest durable state has `active_work_sec=null` and `work_end_time=null` because exact task timestamps were unavailable. This correctly avoids fabricated utilization, but repeated null boundaries now prevent the experiment from learning from future wakes.

## Recovery without changing treatment
The sole treatment variable remains same-wake useful-work duration. Scheduler mechanism, estimated next task (60 s), handoff safety margin (120 s), and comparator (600 s) remain fixed.

For future work, use explicit task-boundary timestamps captured at the moment each substantive repository operation is begun/completed when such timestamps are directly available. Aggregate only completed useful tasks. Do not use connector latency or whole-turn wall time as active work. If exact task-boundary timing is unavailable, keep the duration null rather than infer it.

## Admission
Current runtime start is 09:02:24 KST. At checkpoint, the next useful task remains safe under the fixed admission inputs (estimated task 60 s + safety margin 120 s versus the 600 s comparator). Continue substantive repository work rather than hand off solely because another analysis artifact exists.

## Experiment integrity
- changed variable: same-wake useful-work duration only
- estimated_next_task_sec: 60
- handoff_safety_margin_sec: 120
- comparator_sec: 600
- scheduler_jitter optimization: false
- timeout_or_forced_stop: false at checkpoint
