# Sustained-work execution gap — 2026-09-23 08:52 KST

## Fresh-read invariant
README objective remains maximum utilization / minimum idle. Scheduler jitter is diagnostic, not an optimization target. Baseline A's 600 s is an initial comparator, not doctrine.

## Newly closed boundary
Previous state records previous work end at 2026-09-23T08:34:27+09:00 and current predecessor wake start at 08:42:06, with directly observed idle_gap_sec=459. That predecessor active duration is incomplete, so paired utilization remains invalid rather than fabricating precision.

For this wake, actual execution began at approximately 2026-09-23T08:51:58+09:00 from runtime context. The predecessor state has no work_end_time, so the new idle boundary cannot be computed cleanly. Preserve null.

## Operational finding
The experiment has repeatedly produced analysis saying a sustained same-wake sample is the highest-value next observation, while the implementation keeps handing off after short analysis bursts. That is now the dominant experiment defect: evidence production is substituting for the treatment itself.

No scheduler mechanism is changed. The single treatment variable remains same-wake useful-work duration. This wake therefore spends its available work on concrete repository/state inspection and experiment correction, rather than another short-duration sensitivity model.

## Admission state
- comparator_sec: 600
- estimated_next_task_sec: 60
- handoff_safety_margin_sec: 120
- changed variable: same-wake useful-work duration only
- scheduler_jitter optimization: false
- timeout_or_forced_stop: false at checkpoint

## Next action
Continue concrete useful work within the same wake while safe. At handoff, secure the same recurring wake first, then persist state. Do not promote incomplete active-work timing to a clean utilization sample.
