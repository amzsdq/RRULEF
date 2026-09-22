# Active-duration treatment admission — 2026-09-23 01:09 KST

## Fresh objective check
README fresh-read confirms the sole invariant is maximum utilization / minimum real idle. Scheduler jitter remains diagnostic only.

## Closed predecessor
Canonical predecessor:
- previous active_work_sec: 167
- previous work_end_time: 2026-09-23T01:05:44+09:00
- current actual start: 2026-09-23T01:06:31+09:00
- causal idle_gap_sec: 47
- paired utilization: 167 / (167 + 47) = 0.7803738318 (78.04%)
- pair_valid: true

## Single-variable decision
Keep the experiment variable unchanged: same-wake useful-work duration. Do not change the wake/jitter mechanism.

The next useful treatment should extend sustained useful work beyond the recent 167-second run rather than spending the wake on scheduler tuning. Target useful-work envelope: approximately 240-300 seconds if runtime safety remains healthy. This is an experimental target, not a new policy or fixed cutoff.

Admission fields for adaptive-cutoff comparison:
- elapsed_sec_at_decision: ~120
- estimated_next_task_sec: 120-180
- handoff_safety_margin_sec: 120
- decision: continue useful work while safe; handoff before timeout risk dominates

## Interpretation
This pair materially improves on the five-pair aggregate previously recorded (33.42%), but a single 47-second idle observation is not enough to infer a mechanism change. Continue collecting clean causal pairs while increasing useful work only within the same experiment variable.