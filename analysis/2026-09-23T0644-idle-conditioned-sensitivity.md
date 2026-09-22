# Active-duration sensitivity at 594-sec observed idle

This is analysis under the same treatment variable: completed same-wake useful-work duration. It does not change the scheduler/wake mechanism.

Using the newly observed valid idle boundary of 594 sec as a conditioning value:

| active_work_sec | utilization if idle=594s |
|---:|---:|
| 61 | 9.31% |
| 120 | 16.81% |
| 180 | 23.26% |
| 300 | 33.56% |
| 420 | 41.42% |
| 480 | 44.69% |
| 540 | 47.62% |
| 594 | 50.00% |
| 600 | 50.25% |

Interpretation:
- With a boundary cost on the order of this observed 594s sample, sub-minute/roughly-one-minute voluntary handoff is strongly dominated by continuing safe useful work.
- Reaching 50% utilization would require active work approximately equal to the idle boundary, absent a reduction in the boundary itself.
- This is sensitivity analysis, not evidence that 594s or 600s is the optimal cutoff. Timeout/forced-stop risk determines the upper safe frontier.
- Therefore the next evidence priority is a genuinely longer completed same-wake sample, not further scheduler-jitter tuning.