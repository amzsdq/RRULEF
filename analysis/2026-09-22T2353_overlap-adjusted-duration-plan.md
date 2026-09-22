# Overlap-adjusted active-duration plan

## Evidence retained
- The sustained-work test requires directly measured active duration, timeout outcome, a following clean idle pair, and no concurrent mechanism change.
- Existing comparable clean pairs are 20/319 (5.90%), 105/261 (28.69%), and 32/304 (9.52%).
- Earlier sensitivity analysis shows that, for multi-minute idle costs, extending active useful work has much larger expected utilization leverage than shaving scheduler jitter.

## New integrity constraint from this wake
The canonical predecessor claimed `work_end_time=23:52:36`, while this wake actually began at `23:51:42`. The -54 sec implied gap is not a valid idle sample. It indicates overlap or timestamp/state-finalization inconsistency. This pair is excluded, not clamped to zero.

## Consequence for the active-duration experiment
This does not justify changing the treatment variable. Continue the same treatment: materially longer same-wake useful work, while recording timeout/forced-stop. However, only non-overlapping finalized predecessor -> successor pairs may enter paired-utilization comparisons. This is a measurement-validity rule, not a scheduler optimization.

The next informative duration target remains >=180 sec because prior criteria identified that as materially beyond the 30–60 sec bookkeeping windows. It is an evidence target, not a new cutoff. The 600 sec Baseline-A comparator remains unchanged until enough clean longer samples exist.
