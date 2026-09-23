# Boundary-cost operationalization — 2026-09-23 13:31 KST

## Objective
Maximize useful-work utilization / minimize actual idle gap. Scheduler jitter remains diagnostic only.

## Fresh-read constraint
Baseline A says continue valid tasks inside the same wake while cumulative useful work remains safely below the runtime-risk boundary; 10 minutes is an initial comparator, not a fixed law.

## Problem found
Recent work correctly identified an observability deadlock, but merely deferring the 600 s treatment does not itself increase utilization. The repository already contains enough evidence to make one operational change without pretending to have a new timing measurement: avoid creating a handoff merely because an analysis artifact or checkpoint was completed.

Existing boundary-frequency analysis shows why: every avoidable boundary purchases another idle exposure. Its 178.15 s mean-idle calculation is descriptive rather than predictive, but the structural result does not depend on treating that mean as causal: for a fixed amount of useful work, more handoff boundaries cannot reduce boundary count.

## Single-variable operational treatment
Changed variable for the next comparable run:
- BEFORE: artifact/checkpoint completion may terminate the wake.
- TREATMENT: artifact/checkpoint completion is only a natural measurement point; immediately start the next safe useful repository task unless the admission check predicts insufficient runtime safety margin.

Everything else remains fixed: same recurring continuation mechanism, same jitter treatment, same objective, no scheduler-jitter optimization.

## Admission record required at each natural task boundary
Record, when observable:
- run_elapsed_sec
- estimated_next_task_sec
- handoff_safety_margin_sec
- decision = CONTINUE or HANDOFF
- reason

Do not fabricate elapsed time when the execution surface cannot expose it. In that case continue only bounded, reversible repository work and preserve the 480 s verified frontier; do not claim a 600 s completion.

## Expected information gain
This treatment tests the directly actionable implication of the evidence: whether suppressing analysis-driven premature boundaries increases useful work per wake without increasing timeout/forced-stop failures. A later run with direct timing can quantify the effect; until then this file is an operational treatment specification, not a result.
