# Boundary integrity audit — 2026-09-22 19:26 KST

Baseline A comparator remains 600 sec. No cutoff or scheduler-mechanism change in this experiment.

## Fresh observations
- actual_start_time: 2026-09-22T19:26:46+09:00
- canonical README was fresh-read at run start.
- preceding durable run state: ac480b513362e6e3d02d29911f2f3e6b1cc4b42f.
- preceding substantive sample: d5b67ab0f0d71bff8a1ceaa6dc2a92d7476a0395.

## Integrity finding
The preceding sample explicitly required the final useful_work_end_time to be captured immediately before handoff bookkeeping, but the subsequent run-state commit did not contain that timestamp. Therefore this wake cannot honestly compute the requested cross-run idle_gap_sec. Substituting the durable commit time would reintroduce the already-identified mixed-boundary error.

This is a measurement defect, not evidence that the 600-sec comparator is wrong.

## Substantive work performed
1. Fresh-read README and revalidated the objective and Baseline A.
2. Inspected the latest durable run state and substantive sample.
3. Verified that no valid previous useful_work_end_time exists in the latest boundary pair.
4. Preserved the pair as invalid-for-idle rather than manufacturing a value.
5. Defined the minimum valid next pair: a directly captured useful_work_end_time followed by the following wake's directly observed actual_start_time.

## Decision ledger
At this point elapsed runtime is well below 600 sec, timeout/forced-stop evidence remains absent, and the next useful task is bounded: persist this integrity result and continue toward a directly captured endpoint. Early handoff is therefore not justified by Baseline A.

## Measurement status
- active_work_sec: not inferred from wall-clock time
- previous useful_work_end_time: unavailable
- actual_next_start_time for previous pair: 2026-09-22T19:26:46+09:00
- idle_gap_sec: not asserted
- timeout_or_forced_stop: false so far
- experimental variable: useful-work boundary placement only

## Required next boundary
Immediately before handoff bookkeeping begins, capture useful_work_end_time as a direct timestamp and make it durable. The following wake must consume exactly that endpoint before doing other substantive work. Do not use commit completion time as a proxy.
