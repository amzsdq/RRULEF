# Useful-work queue while active-duration observability is unavailable

## Basis
README objective remains maximum useful-work utilization / minimum actual idle gap. The current runtime cannot directly observe trustworthy `active_work_sec`, so repeated frontier re-verification is not useful work.

## Concrete work queue
Use future wakes on the first unfinished item, without re-proving the 480s frontier unless contradictory evidence appears:

1. Audit run records for measurement-schema consistency and identify fields that are directly observed vs inferred.
2. Build a compact evidence table from valid paired runs: active_work_sec, following idle_gap_sec, paired utilization, timeout/forced-stop.
3. Check whether existing valid samples support any adaptive-cutoff hypothesis without changing more than one experimental variable.
4. Remove or quarantine misleading records that encode scheduler jitter as a target metric or imply unobserved active duration.
5. Keep `state/latest-run.json` as the single current checkpoint; avoid adding analysis files unless they contain new experimental information.

## Guard
Do not infer active useful-work duration from commit timestamps, connector latency, scheduler timestamps, filenames, or whole-turn wall time. Record task results/counts when duration is unobservable.

## Why this improves utilization
It converts wakes from repeated status verification into bounded repository maintenance/analysis tasks that can produce reusable evidence while preserving measurement integrity.
