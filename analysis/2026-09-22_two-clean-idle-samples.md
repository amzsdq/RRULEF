# Two corrected causal idle samples

Baseline A remains unchanged at the 600 sec initial comparator. This note changes no mechanism; it closes the next measurement pair only.

## Clean samples

1. Prior clean pair: useful_work_end_time 19:43:00 -> actual_next_start_time 19:44:31 = 91 sec idle.
2. Current pair: useful_work_end_time 19:45:25 -> actual_next_start_time 19:54:55 = 570 sec idle.

The second value is causal idle by the README definition. It is not scheduler jitter and should not be relabeled as such.

## Immediate implication

For a hypothetical 600 sec useful-work block followed by the observed idle:
- 91 sec idle => utilization = 600/(600+91) = 86.83%.
- 570 sec idle => utilization = 600/(600+570) = 51.28%.
- Two-sample mean idle = 330.5 sec; paired with 600 sec useful work, illustrative utilization = 64.48%.

These are sensitivity calculations, not a cutoff estimate. Two samples are still too few and the 570 sec observation may reflect wake timing / handoff placement rather than the 600 sec cutoff itself.

## Decision

Do not change the 600 sec comparator yet. The highest-value next evidence is to continue useful work in the current wake rather than hand off early, then record a direct useful_work_end_time so another causal pair can be closed. No scheduler-jitter optimization is introduced.
