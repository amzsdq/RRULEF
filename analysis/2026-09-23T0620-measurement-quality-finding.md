# Measurement quality finding — 2026-09-23 06:20 KST

## Objective
Maximize useful-work utilization / minimize actual idle gap. Scheduler jitter remains diagnostic only.

## Fresh-read baseline
README Baseline A continues useful work below the initial ~10 minute budget; 10 minutes is explicitly not a fixed rule.

## Finding
The current canonical state at wake start contains `active_work_sec: 0` while its decision text says to `continue-useful-work-short-region-rejected`. This means the run record closes before the continued useful work is actually measured. Repeating such wakes can optimize measurement/analysis overhead instead of useful work and cannot establish a longer safe-work frontier.

This is not evidence that the 10-minute baseline is optimal. It is evidence that recent very-short completed-work pairs (12s/28s/32s/63s) are insufficient to test the intended variable: same-wake useful-work duration near the runtime-safety frontier.

## Single-variable experimental decision
Do not change scheduler mechanism or jitter handling. Keep the experiment variable as same-wake useful-work duration. The next valid frontier evidence must come from actually completed useful work, not a planned/projected duration. A state write may record only elapsed completed work at write time; it must not claim future work.

## Decision inputs
- elapsed_sec_at_decision: measured during the run, never projected
- estimated_next_task_sec: 120
- handoff_safety_margin_sec: 120
- target comparison: initial 600-second Baseline A versus a later adaptive cutoff only after valid completed-work samples exist

## Operational implication
Short voluntary handoffs in the tens-of-seconds region remain poor candidates because observed boundary idle gaps are hundreds of seconds. However, no numeric cutoff above or below 600 seconds is promoted until an actually completed longer run is observed without timeout/forced stop.
