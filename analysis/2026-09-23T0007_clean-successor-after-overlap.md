# Clean successor after overlap — 2026-09-23 00:07 KST

## Fresh-read invariant
README.md still defines the objective as maximum useful-work utilization / minimum real idle gap. Scheduler jitter remains diagnostic only; the 10-minute budget remains an initial baseline, not a fixed rule.

## Closed causal pair
Durable predecessor:
- work_end_time: 2026-09-23T00:06:10+09:00
- active_work_sec: 82

Current actual start:
- actual_next_start_time: 2026-09-23T00:07:05+09:00

Therefore:
- idle_gap_sec = 55
- paired_utilization = 82 / (82 + 55) = 0.598540 = 59.85%
- pair_valid = true

This is the first clean successor after the overlap-invalid sample. It confirms the measurement guard works without clamping negative idle and without changing the optimization mechanism.

## Interpretation
The 59.85% sample is materially better than prior short-run samples because the realized idle denominator happened to be only 55 seconds. It is not evidence that scheduler jitter should be optimized, nor sufficient evidence to set a new cutoff. The controlled experiment variable remains same-wake useful-work duration.

## Admission decision
At decision time, the useful next task is still the directly measured >=180-second useful-work block. The continuation has been secured first. Do not change cutoff, wake mechanism, or jitter handling in the same experiment. A >=180-second block without timeout/forced stop followed by a clean successor pair is the next evidence needed for adaptive-cutoff comparison.
