# Clean pair + admission decision — 2026-09-22 23:39 KST

Fresh README invariant: maximize useful-work utilization / minimize actual end-to-next-start idle; scheduler jitter is diagnostic only.

## Closed causal pair
- previous durable work_end_time: 2026-09-22T23:33:30+09:00
- actual_next_start_time: 2026-09-22T23:38:49+09:00
- idle_gap_sec: 319
- previous active_work_sec: 20
- paired utilization: 20 / (20 + 319) = 5.90%
- previous scheduled_next_wake: 2026-09-22T23:36:00+09:00
- scheduler_jitter_sec: 169 (diagnostic; not an optimization target)

This is the first pair closed directly from the canonical state/latest-run.json pointer without repository-wide endpoint discovery.

## Single-variable experiment status
Primary variable remains same-wake useful-work duration. Do not change wake-lead mechanism in this treatment.

For an idle cost of 319 s, utilization sensitivity is:
- active 20 s => 5.90%
- active 180 s => 36.07%
- active 300 s => 48.47%
- active 480 s => 60.08%
- active 600 s => 65.29%

These are sensitivity values, not claims that idle will remain constant.

## Admission decision record
At this checkpoint, elapsed useful-work is still far below the 10-minute baseline budget. The next bounded task is to preserve this clean pair and canonicalize the current endpoint. Estimated next bounded task <= 90 s; handoff safety margin 120 s. Continue useful work rather than voluntarily closing solely because one measurement unit completed.

## Finding
The canonical latest-run pointer removed endpoint-discovery ambiguity successfully. The dominant measurable loss in this pair is still boundary idle relative to a very short 20 s active block. This supports continuing the active-duration treatment rather than spending useful-work budget tuning scheduler jitter.
