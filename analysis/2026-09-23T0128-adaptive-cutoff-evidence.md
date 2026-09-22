# Adaptive-cutoff evidence checkpoint — 2026-09-23 01:28 KST

This file records evidence for future adaptive-cutoff comparison without changing the current experiment variable.

## Observed facts
- Latest predecessor active_work_sec: 151
- Latest real idle_gap_sec: 188
- Latest paired utilization: 44.54%
- timeout_or_forced_stop on predecessor: false
- Current experiment: baseline-a-active-work-duration

## Decision fields for future comparison
Checkpoint A:
- elapsed_sec_at_decision: approximately 140s of run/tool work
- estimated_next_task_sec: 120
- handoff_safety_margin_sec: 120
- decision: CONTINUE

Checkpoint B:
- elapsed_sec_at_decision: approximately 220s
- estimated_next_task_sec: 150
- handoff_safety_margin_sec: 120
- decision: CONTINUE

Rationale: both checkpoints remain materially below the initial 600s baseline budget and no timeout/forced-stop evidence has appeared in the predecessor. Early handoff would add another boundary and expose the system to another real idle interval. No adaptive cutoff is activated yet; these fields are only evidence for later comparison.

## What would justify handoff
A handoff becomes preferable when elapsed time plus estimated next useful task plus safety margin approaches the empirically safe runtime envelope, or when a timeout/forced-stop signal appears. The safe envelope is not yet estimated tightly enough to replace Baseline A.
