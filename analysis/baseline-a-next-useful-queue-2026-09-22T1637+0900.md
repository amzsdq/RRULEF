# Baseline A next useful-work queue — 2026-09-22 16:37 KST

## Purpose
Keep the current wake doing substantive work after the original four-item queue was exhausted, without changing the 10-minute cutoff or scheduler mechanism.

## Fresh-read invariant
- Objective remains maximum useful-work utilization / minimum actual idle gap.
- Baseline A remains unchanged: while materially below the initial 10-minute budget, continue the next safe useful task.
- Scheduler jitter remains diagnostic only.

## Current evidence state
The prior queue completed measurement-integrity, handoff-cost, continuous-run acceptance, and adaptive-cutoff-readiness work. The latest durable run still recorded only >=47 sec of connector-backed useful work and explicitly classified itself as not cutoff-evaluable. Therefore the immediate problem is not a shortage of policy; it is obtaining longer literal same-wake execution evidence.

## Useful-work queue
1. Build a compact evidence ledger from the latest corrective/validation runs that distinguishes exact values, lower bounds, and upper bounds. This prevents false precision when computing utilization.
2. Derive a conservative same-wake utilization bound from those runs using only connector-backed intervals; do not infer missing active time.
3. Define the next measurement artifact so per-task completion timestamps can be appended during one wake, allowing active work and decision tuples to be reconstructed without counting bookkeeping as useful work.
4. Only after those are complete, reassess whether another safe substantive task fits in the remaining runtime margin.

## Decision tuple after this task
- current elapsed: still materially below 10 minutes in this wake
- estimated next task: 60–120 sec
- handoff safety margin: high
- decision: CONTINUE

No experimental variable changed.