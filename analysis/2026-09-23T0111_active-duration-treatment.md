# Active-duration treatment — 2026-09-23 01:11 KST

## Fresh objective check
README.md was freshly read at this wake. Objective remains maximum useful-work utilization / minimum actual idle gap. Scheduler jitter is diagnostic only.

## Closed causal pair
Predecessor canonical state:
- previous active_work_sec: 138
- previous work_end_time: 2026-09-23T01:08:49+09:00
- actual next start: 2026-09-23T01:11:53+09:00
- idle_gap_sec: 184
- pair_valid: true
- paired utilization: 138 / (138 + 184) = 0.428571 (42.86%)

This closes the prior 138-second treatment without timeout/forced stop. It is materially below the immediately prior 167s/47s pair (78.04%), reinforcing that individual pair utilization is dominated by variable idle gaps and should not be used alone to infer a duration effect.

## Sole experimental variable
Keep same-wake useful-work duration as the only treatment variable. Do not change wake/jitter mechanism in this treatment.

The prior admission target was 240–300 seconds useful work. This wake should therefore continue useful repo analysis/work toward that envelope if runtime safety permits. The target is experimental, not a new policy.

## Admission decision evidence
At start, predecessor had no timeout/forced stop. A 240–300s useful-work treatment remains admissible with a conservative handoff margin, provided the run does not approach runtime-risk territory. Record elapsed time, estimated next-task duration, and safety margin before handoff.
