# Overlap causal correction — 2026-09-22

## Objective
Preserve the only invariant: maximize useful-work utilization / minimize true idle.

## Fresh evidence
The prior boundary pair was:
- prior run actual start: 18:35:39 KST
- prior run durable work-end marker: 18:46:20 KST
- next run actual start: 18:43:58 KST
- observed overlap: 142 sec

The overlap is not idle and must not be clamped to zero or counted in utilization.

## Causal diagnosis
The previous `work_end_time` was a durable-save/commit completion marker after the continuation had already become eligible. That marker therefore measures the tail of an old run while a new run may already have begun. It is not a valid mutually-exclusive useful-work boundary.

This means the experiment currently has two distinct quantities:
1. **useful_work_end_time** — end of the last substantive task whose duration belongs to the run.
2. **durable_handoff_complete_time** — completion of wake confirmation + state persistence.

Only (1) is eligible for the next run's idle-gap numerator boundary. (2) is handoff tail/overlap diagnostics.

## Single-variable experiment for next clean pair
Do not change the 600 sec cutoff. Do not tune scheduler jitter. Change only boundary placement:
- timestamp `useful_work_end_time` immediately when substantive work stops;
- secure/confirm continuation after the handoff decision;
- timestamp `durable_handoff_complete_time` separately;
- next run computes `idle_gap_sec = actual_next_start_time - useful_work_end_time` only when causal ordering is valid;
- if the next run begins before durable handoff completes, record `handoff_overlap_sec` separately rather than corrupting idle.

## Why this matters
A continuation becoming runnable before durable persistence is complete can be good for availability, but the measurement model must not interpret concurrent handoff tail as negative idle. Separating useful-work end from durable handoff completion preserves the objective without introducing a new policy.
