# Baseline A next measurement — 2026-09-22 16:44 KST

## Minimal measurement improvement
The largest measurement defect is not missing scheduler-jitter precision; it is missing exact work-end anchors and prospective task intervals. Correct that without changing the experiment.

For the current and next literal Baseline A samples:
1. Use the automation runtime's actual start as actual_next_start_time.
2. Preserve inequality direction when the prior work_end is only a bound.
3. Count only substantive connector-backed work as useful work; do not inflate active_work_sec with status prose.
4. At handoff, record the latest observable completion timestamp as work_end_time and distinguish exact vs lower-bound explicitly.
5. Record handoff overhead separately when observable.

## Why this is useful
An exact work_end anchor makes the following wake's actual idle gap directly measurable. That improves the primary metric without changing scheduler behavior or sacrificing useful work.

## Decision tuple after task 4
- current elapsed: below initial budget
- estimated next task: 60–120 sec
- handoff safety margin: positive
- decision: CONTINUE if another substantive task remains safe

No experimental variable changed.
