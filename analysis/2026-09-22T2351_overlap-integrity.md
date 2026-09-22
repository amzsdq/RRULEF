# Overlap / measurement-integrity finding

- actual_start_time: 2026-09-22T23:51:42+09:00
- canonical previous work_end_time: 2026-09-22T23:52:36+09:00
- implied idle_gap_sec: -54 (invalid as an idle measurement)
- previous active_work_sec: 125
- previous scheduled_next_wake: 2026-09-22T23:54:00+09:00

## Finding
The canonical predecessor ends 54 seconds after this run actually started. Therefore this pair cannot be used as a normal `work_end_time -> actual_next_start_time` idle sample. Treating it as zero idle would also be wrong because it would hide overlap / timestamp inconsistency.

This is useful evidence for utilization work: the current state model assumes serial non-overlapping runs, but the observed runtime can start while the canonical predecessor claims to still be active. Until a clean predecessor is available, exclude this pair from cutoff-effect estimates rather than contaminating the experiment.

## Experiment discipline
No cutoff or scheduler-jitter treatment was changed on the basis of this invalid pair. The sole active treatment remains same-wake useful-work duration. Continuation was secured before durable-state write.
