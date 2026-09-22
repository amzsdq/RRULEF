# Clean-pair recovery after overlap anomaly

## Fresh inputs
- actual start: 2026-09-22T23:54:30+09:00
- finalized predecessor work_end_time: 2026-09-22T23:52:29+09:00
- predecessor active_work_sec: 47
- predecessor requested next wake: 2026-09-22T23:57:00+09:00

## Causal pair
The predecessor endpoint is earlier than this actual start, so this pair is valid.

- idle_gap_sec = 121
- paired utilization = 47 / (47 + 121) = 0.2797619 = 27.98%
- scheduler_jitter_sec = -150 relative to the predecessor's recorded requested wake. This is diagnostic only and is not a treatment target.

## Interpretation
The immediately preceding overlap anomaly did not persist into this pair. Therefore the canonical endpoint can continue to be used, provided each successor rejects rather than clamps any non-positive/overlapping causal interval.

The clean-pair set now contains 20/319 (5.90%), 105/261 (28.69%), 32/304 (9.52%), and 47/121 (27.98%). The idle denominator varies materially, so these samples do not identify a causal slope for active duration. They do continue to show that short bookkeeping-sized runs can be dominated by inter-run idle cost.

## Experiment decision
Do not change cutoff, wake mechanism, or jitter handling in this run. Preserve the single treatment variable: same-wake useful-work duration. The next informative active-duration target remains >=180 seconds with timeout_or_forced_stop recorded, followed by a clean successor pair. The 600-second Baseline A comparator remains unchanged.