# Active-duration treatment plan — 2026-09-23 00:03 KST

## Fresh-read invariant
README objective remains maximum useful-work utilization / minimum real idle gap. Scheduler jitter remains diagnostic only.

## Current durable predecessor
- previous actual_start_time: 2026-09-23T00:00:43+09:00
- previous active_work_sec: 132
- previous work_end_time: 2026-09-23T00:02:55+09:00
- previous idle_gap_sec: 353
- previous paired_utilization: 0.0536193
- timeout_or_forced_stop: false

## Single treatment variable
Continue changing only same-wake useful active-work duration. Do not change cutoff logic, jitter handling, or handoff mechanism in this experiment.

## Next informative treatment
Target a directly measured useful-work block >=180 seconds before handoff, provided the runtime safety margin remains adequate. Record the actual duration rather than assigning a nominal value.

Admission check before each next task:
- elapsed_sec_at_decision: measure at decision time
- estimated_next_task_sec: estimate from the concrete task
- handoff_safety_margin_sec: retain 120 seconds for comparability until evidence supports changing it
- admit only if the estimated task plus safety margin fits the remaining safe runtime budget

## Interpretation guard
Do not infer a causal active-duration slope from utilization alone because idle_gap_sec varies exogenously between pairs. The >=180-second block is useful primarily to test whether longer same-wake useful work can be completed without timeout/forced-stop and whether amortized utilization improves across subsequent clean pairs.
