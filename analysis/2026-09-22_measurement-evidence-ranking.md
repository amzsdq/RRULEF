# Measurement evidence ranking after first corrected idle sample

Purpose: prevent proxy metrics from contaminating cutoff decisions while keeping Baseline A unchanged.

## Evidence currently usable for optimization
1. `19:43:00 -> 19:44:31`: corrected causal `idle_gap_sec = 91` because the ending boundary was captured before handoff bookkeeping and the next execution start is directly observed.
2. `600 sec` remains only the baseline comparator; there is still no timeout/forced-stop observation that justifies shortening it.

## Evidence retained as diagnostic only
- Earlier requested-wake vs actual-wake lateness samples (including +216.813 sec) describe scheduler behavior, not causal useful-work idle unless paired with an independently observed previous useful-work endpoint.
- The earlier negative `idle_gap_sec` result was a mixed-boundary/overlap artifact and is excluded from utilization estimation.
- Commit completion times and scheduler invocation times are not substituted for useful-work boundaries unless the event itself is the substantive-work endpoint being measured.

## Current inference
One corrected idle sample is enough to validate the boundary-capture method, but not enough to tune the 600-second cutoff. With 91 sec idle, a hypothetical 600 sec of useful work yields 86.83% utilization. The highest-value next evidence is another directly paired useful-work endpoint/start plus a directly bounded active-work interval; further scheduler-jitter tuning is lower value.

No mechanism or threshold is changed by this analysis.
