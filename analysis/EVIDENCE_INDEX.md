# RRULEF evidence index

Purpose: reduce repeated rediscovery and keep future wakes focused on useful work. This is an index, not a new policy.

## Canonical objective
- `README.md` — fresh-read every wake; invariant objective, Baseline A, measurement definitions.

## High-value empirical evidence
- `analysis/baseline-a-10-sample-check-2026-09-22T1621+0900.md` — 10 comparable runs: 323 sec active, 1470 sec idle, 18.0% aggregate utilization, 8–72 sec active/run, zero observed forced stops.
- `runs/2026-09-22T1644+0900.md` — recent execution-fidelity sample; >=67 sec to secured handoff, 5 durable analysis artifacts, still not near cutoff.
- `analysis/run11-premature-handoff-economics-2026-09-22T1657+0900.md` — derived idle:active ratio 4.551:1 and boundary-cost interpretation without assuming jitter improvement.

## Current decision state
- `analysis/adaptive-cutoff-readiness-2026-09-22T1634+0900.md` — adaptive cutoff not ready because baseline cutoff has not been exercised adequately.
- `analysis/baseline-a-decision-record-2026-09-22T1644+0900.md` — keep Baseline A unchanged pending literal evidence.
- `analysis/run11-objective-compression-2026-09-22T1657+0900.md` — stop multiplying policy artifacts; focus on long same-wake useful work.

## Measurement helpers
- `analysis/continuous-run-acceptance-criteria-2026-09-22T1634+0900.md`
- `analysis/baseline-a-next-measurement-2026-09-22T1644+0900.md`

## Minimal fresh-read set for next wake
1. `README.md`
2. latest file under `runs/`
3. this index

Read other analysis only when a concrete decision requires it. This reduces repeated connector overhead and leaves more of each wake for useful work.

## Current unresolved evidence gap
Obtain at least one literal same-wake Baseline A sample that continues safe useful tasks substantially closer to the current 10-minute comparator, or observes a concrete runtime-risk signal before then. Until that exists, changing cutoff would confound execution fidelity with cutoff selection.

## Decision tuple after this task
- current elapsed: still below initial comparator
- estimated next task: 90–180 sec
- handoff safety margin: positive
- decision: CONTINUE
