# Evidence-ranking refresh

Current directly usable evidence ranks as follows:

1. Non-overlapping observed predecessor endpoint -> successor actual start pairs are valid for idle-gap measurement.
2. Completed active duration is valid for utilization only when directly instrumented or explicitly recorded as completed work.
3. Timeout_or_forced_stop is the failure constraint for extending duration.
4. Scheduler jitter remains diagnostic and must not substitute for causal idle gap.
5. Sensitivity calculations are useful for leverage, but cannot promote a cutoff without completed-duration and timeout evidence.

The current 63 sec / 624 sec pair satisfies items 1 and 2 for the predecessor. The current wake is extending duration, but because its early task boundaries were not individually timestamped, its final active-work accounting must preserve that limitation rather than infer exact useful time from wall-clock elapsed.

No treatment change.