# 194s active-duration treatment — closed successor pair

Fresh README objective: maximize useful-work utilization / minimize actual idle gap. Scheduler jitter remains diagnostic only.

## Predecessor treatment
- previous active_work_sec: 194
- previous work_end_time: 2026-09-23T00:32:42+09:00
- timeout_or_forced_stop: false
- treatment variable: same-wake useful-work duration only

## Successor observation
- actual_next_start_time: 2026-09-23T00:34:13+09:00
- idle_gap_sec: 91
- paired_utilization = 194 / (194 + 91) = 0.68070 = 68.07%
- pair_valid: true

## Interpretation
The >=180s useful-work treatment now has a clean successor pair. Relative to the immediately preceding 84s/217s pair (27.91%), this observation is substantially higher utilization, but it is one sample and the idle environment also changed, so it is not sufficient by itself to claim a causal improvement. Continue the same active-duration variable and collect another >=180s clean pair before changing cutoff or wake mechanics.

No scheduler-jitter optimization and no new policy introduced.
