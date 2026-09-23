# 600-second frontier treatment admission

Fresh README read performed at this wake.

## Evidence
- Canonical verified active frontier: 480 s.
- Following observed idle gap for that predecessor: 251 s.
- Paired utilization: 480 / (480 + 251) = 65.663475%.
- Timeout/forced-stop evidence for the 480 s predecessor: none recorded.
- Existing `frontier-600` run is admission/decision evidence only; it does not prove a completed 600 s block.

## Single-variable treatment
Only same-wake useful-work duration is varied.

Fixed controls:
- estimated next task: 120 s
- handoff safety margin: 120 s
- comparator: 600 s
- scheduler mechanism: unchanged
- scheduler jitter: diagnostic only

## Decision
A completed, directly supported 600 s useful-work block remains the next informative treatment. Do not lower the frontier, and do not claim 600 s completion from target metadata. At each completed small-task boundary, continue while the accumulated directly observed useful-work duration plus the next-task estimate and safety margin remains inside the runtime-risk envelope. Secure the recurring continuation before handoff.

## Measurement constraint
This connector surface does not expose trustworthy per-task wall-clock boundaries for the current turn. Therefore this wake must not manufacture `active_work_sec`, `work_end_time`, `run_elapsed_sec`, or handoff overhead from API latency or scheduler timestamps. Repository work performed here is useful work, but duration remains unscored unless directly observed.
