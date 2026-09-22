# Run 12 empirical boundary ledger — 2026-09-22 17:08 KST

## Purpose
Do useful empirical work under unchanged Baseline A instead of creating another cutoff/readiness policy artifact.

## Fresh-read invariant
README was fresh-read at wake start. Objective remains maximum useful-work utilization / minimum actual idle gap. Baseline A's 10-minute comparator is unchanged. Scheduler jitter is diagnostic only.

## Evidence used
Latest durable run (`runs/2026-09-22T1657+0900.md`) records:
- actual start: 16:57:11 KST (exact)
- prior work end: >=16:45:28 KST (lower bound)
- resulting idle gap: <=703 sec (upper bound)
- work end: >=16:58:11 KST (lower bound)
- run elapsed through secured handoff: >=60 sec
- 4 successful substantive durable artifacts
- no timeout/forced stop

The evidence index records the earlier 10-run comparator: 323 sec active, 1470 sec idle, 18.0% aggregate utilization, 8–72 sec active/run, no observed forced stops.

## Derived empirical facts
1. The latest run improved execution fidelity relative to many early samples, but `>=60 sec` is still only >=10% of the 600-sec initial comparator. It therefore cannot falsify or validate a 10-minute cutoff.
2. No observed forced-stop evidence currently supports shortening the comparator.
3. The dominant known loss remains boundary exposure: the 10-run comparator has 1470/323 = 4.551 idle seconds per recorded active second.
4. Because prior `work_end_time` can be a lower bound, later `idle_gap_sec` must remain an upper bound. Treating it as exact would bias utilization downward with false precision.
5. The next high-value evidence is not another policy decision. It is a same-wake sequence whose useful tasks are timestamped closely enough to show how far execution can safely approach the comparator.

## Decision tuple after this task
- current elapsed: materially below 10-minute comparator
- estimated next useful task: 90–180 sec
- handoff safety margin: high
- decision: CONTINUE

No experimental variable changed.
