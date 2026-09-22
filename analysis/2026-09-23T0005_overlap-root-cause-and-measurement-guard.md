# Overlap root-cause / measurement guard — 2026-09-23 00:05 KST

## Fresh-read invariant
README.md still defines the objective as maximum utilization / minimum real idle gap. Scheduler jitter is diagnostic only. Baseline A's 10-minute budget remains an initial value, not a fixed rule.

## Observation
The durable predecessor reports:
- actual_start_time: 2026-09-23T00:02:53+09:00
- work_end_time: 2026-09-23T00:05:47+09:00
- active_work_sec: 174
- scheduled_next_wake: 2026-09-23T00:07:00+09:00

This automation run began at approximately 2026-09-23T00:04:48+09:00, before the predecessor's durable work_end_time. Therefore the executions overlap in wall-clock time. A scalar latest-run pointer can be overwritten by a run whose start predates the predecessor endpoint.

## Consequence
For utilization, `previous_work_end_time -> actual_next_start_time` is only a causal pair when actual_next_start_time >= previous_work_end_time and the selected predecessor is the latest completed non-overlapping run. Negative gaps must remain invalid; clamping to zero would fabricate utilization.

## Minimal guard (measurement only; no policy change)
For the current active-duration experiment:
1. Keep the experiment variable unchanged: same-wake useful-work duration.
2. When an execution overlaps a predecessor, do not use that predecessor/run pair for idle-gap or paired-utilization inference.
3. Preserve the completed run as evidence, but the next clean pair must anchor to the latest completed endpoint that precedes the next actual start.
4. Do not optimize scheduler jitter to solve this; overlap is treated as a measurement/concurrency condition.

This is not a new optimization policy. It is a validity condition required by the README's causal definition of idle_gap_sec.

## Next useful work
Obtain a directly measured >=180-second useful-work block without timeout/forced stop, then close a clean non-overlapping successor pair before drawing adaptive-cutoff conclusions.