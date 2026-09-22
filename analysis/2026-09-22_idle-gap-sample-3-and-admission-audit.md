# Third causal idle sample + admission audit — 2026-09-22 20:45 KST

README was fresh-read before this analysis. Baseline A remains the comparator; no cutoff or scheduler mechanism is changed in this experiment.

## Causal idle sample 3
- previous directly captured work_end_time: 2026-09-22T20:34:42+09:00
- actual_next_start_time: 2026-09-22T20:45:05+09:00
- idle_gap_sec: 623
- requested scheduled_next_wake: 2026-09-22T20:45:00+09:00
- scheduler_jitter_sec: +5 (diagnostic only)

This is the third corrected direct idle-gap sample after 91 sec and 570 sec. The dispersion remains large, so scheduler jitter is not a useful optimization target by itself.

## Admission-rule audit
The previous run recorded run_elapsed_sec≈620 sec while its final substantive work endpoint was only 22 sec after actual_start_time (20:34:20 -> 20:34:42). That combination is internally inconsistent if run_elapsed_sec is intended to mean elapsed wall time for that wake. More importantly, it caused handoff despite very little directly attributable useful work in that wake.

This exposes a measurement/admission defect: a stale or miscomputed elapsed value can terminate useful work early. Baseline A is defined around accumulated useful work near 600 sec, not merely an unreliable elapsed field. Therefore future admission decisions should use directly accumulated per-task active_work_sec plus estimated_next_task_sec and handoff safety margin, while run_elapsed_sec remains a timeout-risk guard. This is an interpretation/correction of measurement use, not a cutoff change.

## Decision
- Do not shorten the 600-sec comparator.
- Continue direct per-task duration instrumentation.
- Treat directly accumulated active_work_sec as the primary progress quantity for the 600-sec comparator.
- Treat wall-clock run_elapsed_sec only as a safety guard against runtime timeout.
- No scheduler-mechanism change in this experiment.
