# Cutoff experiment trigger — 2026-09-22 16:41 KST

## Purpose
Specify when evidence is sufficient to change exactly one variable: the initial 10-minute cutoff. This does not change the cutoff now.

## Trigger evidence
A cutoff experiment becomes meaningful only after literal Baseline A produces repeated same-wake samples that:
1. execute sequential useful tasks rather than ending after bookkeeping;
2. consume a substantial fraction of the current budget;
3. record exact or explicitly bounded task durations and final work_end_time;
4. record each decision tuple (elapsed, next-task estimate, safety margin);
5. show whether timeout/forced-stop risk appears as the budget is approached.

## Candidate one-variable test once triggered
Hold wake mechanism, measurement definitions, and useful-work queue semantics fixed. Change only cutoff duration for a bounded A/B comparison. Compare aggregate useful-work utilization, idle-gap exposure count, incomplete-work loss, and timeout/forced-stop incidence. Scheduler jitter remains diagnostic and is not optimized.

## Current decision
NOT TRIGGERED. Existing validation wakes remain far below the current budget, so changing cutoff would confound execution-fidelity failure with cutoff quality.

## Decision tuple
- elapsed: still safely below current budget
- estimated next useful task: 60–120 sec
- safety margin: high
- decision: CONTINUE
