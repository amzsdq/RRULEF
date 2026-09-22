# Sustained-work next sample — 2026-09-22 22:57 KST

README fresh-read. Objective remains maximum useful-work utilization / minimum actual idle gap.

## Evidence carried forward
Previous durable pair (22:36:19 -> 22:47:43):
- idle_gap_sec = 684
- prior active_work_sec ~= 180
- paired utilization = 20.83%
- timeout_or_forced_stop = false

The current experiment changes one variable only: extend same-wake useful work. Wake-lead mechanics are held constant for this sample.

## Decision
A 300-second active sample would still yield only 30.5% utilization if the next idle repeats at 684s. A 480-second sample would yield 41.2%; 600 seconds would yield 46.7%. The 50% break-even active duration is 684 seconds. These are diagnostics, not new fixed cutoffs.

The useful next observation is therefore not another short measurement-driven handoff. Continue bounded useful work toward the existing Baseline-A region while recording task durations, but preserve enough handoff margin to avoid losing unfinished work to runtime timeout.

## Handoff state
Same recurring automation was re-anchored before this durable write to 23:04 KST and returned enabled=true with RRULE:FREQ=HOURLY. No second scheduler mutation is planned in this handoff.

Next run should close the causal pair from the final work_end_time recorded by this run, then compare realized utilization against the short-window samples.
