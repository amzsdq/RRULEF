# Active-duration treatment — clean pair and admission analysis

## Fresh objective check
README.md was read at run start. Objective remains maximum useful-work utilization / minimum real idle gap. Scheduler jitter is diagnostic only.

## Clean causal pair
- previous work_end_time: 2026-09-22T23:40:34+09:00
- actual_next_start_time: 2026-09-22T23:44:55+09:00
- idle_gap_sec: 261
- previous active_work_sec: 105
- paired utilization: 105 / (105 + 261) = 0.2868852459 (28.69%)
- previous scheduled_next_wake: 2026-09-22T23:42:00+09:00
- scheduler_jitter_sec: 175 (diagnostic only)

This is a clean comparable pair because the predecessor endpoint came from state/latest-run.json and the next actual start is directly observed.

## Treatment interpretation
The sole treatment variable remains same-wake useful-work duration. Relative to the prior 20-second active block paired with 319 seconds idle (5.90%), the 105-second block paired with 261 seconds idle yields 28.69%. This is directionally consistent with the hypothesis that short runs waste too much of each handoff cycle, but it is not causal proof because idle gap also changed.

For the currently observed 261-second idle cost, useful work required for target utilization would be:
- 50%: 261 sec active
- 60%: 391.5 sec active
- 70%: 609 sec active
- 75%: 783 sec active
- 80%: 1044 sec active

The practical implication is not to adopt any target percentage as policy. It is to keep extending bounded useful-work blocks while timeout/forced-stop remains false, because 105 seconds is still far below the 10-minute initial baseline and handoff fixed cost dominates utilization.

## Admission decision
At the decision point, continue substantive work if elapsed active time is still materially below the current ~10-minute baseline and the next bounded task plus safety margin fits. Do not spend useful-work budget trying to reduce scheduler jitter. No cutoff change is adopted from this single pair.
