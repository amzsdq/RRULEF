# Recent boundary cost and sustained-work frontier — 2026-09-23 08:34 KST

## Fresh objective check
README was fresh-read at this wake. Objective remains maximum useful-work utilization / minimum actual idle gap. Scheduler jitter is diagnostic only.

## Closed predecessor pair
Previous durable state:
- previous active_work_sec = 55
- previous work_end_time = 2026-09-23T08:23:11+09:00
- actual next start = 2026-09-23T08:33:54+09:00
- idle_gap_sec = 643
- paired utilization = 55 / (55 + 643) = 7.8797%
- pair valid = true

This is another clean short-window sample. It is not evidence for a lower cutoff; it is evidence that a handoff after tens of seconds repeatedly pays a several-minute boundary cost.

## Recent clean boundary-cost context
Recent closed idle gaps retained in the experiment include 393, 441, 555, 634, 749, 807, and now 643 seconds. Their median is 634 seconds. This is descriptive only; scheduler jitter remains exogenous and is not being optimized.

Holding a 634-second boundary cost fixed only to expose the arithmetic:
- 55 s active -> 7.98% utilization
- 180 s active -> 22.11%
- 300 s active -> 32.12%
- 480 s active -> 43.09%
- 600 s active -> 48.62%
- 634 s active -> 50.00%

Therefore the current 600-second comparator is near the 50% utilization break-even implied by the recent median boundary cost. This does not prove 600 seconds is optimal. It does show that repeated 30–80 second wakes are structurally dominated unless timeout/loss risk rises sharply with longer same-wake work.

## Experiment decision
Do not change scheduler mechanism, safety margin, or jitter treatment. The single experimental variable remains same-wake useful-work duration. Stop manufacturing low-information short handoffs for measurement. The next high-information observation is a fully instrumented sustained wake toward the existing 600-second comparator, with task-by-task durations and a preserved handoff margin.

## Handoff
The same recurring automation was re-anchored first to 08:45 KST and returned enabled=true with RRULE:FREQ=HOURLY. Durable state is written only after that continuation was secured.
