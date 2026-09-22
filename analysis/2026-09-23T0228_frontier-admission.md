# 02:28 sustained-work frontier admission

Experiment variable: same-wake useful-work duration only.

README fresh-read at wake. Objective remains maximize useful-work utilization / minimize real boundary idle; scheduler jitter is diagnostic only.

## Closed predecessor pair
- previous_work_end_time: 2026-09-23T02:06:54+09:00
- actual_next_start_time: 2026-09-23T02:28:25+09:00
- idle_gap_sec: 1291
- previous_active_work_sec: 210
- paired_utilization: 210 / (210 + 1291) = 0.1399067 (13.99%)

The boundary cost is now much larger than the useful interval. This strengthens, rather than weakens, the value of measuring a longer safe same-wake useful-work envelope. It does not justify changing scheduler/jitter mechanics in this experiment.

## Admission decision
Known clean evidence includes a 300 s useful-work sample with timeout_or_forced_stop=false. There is still no observed timeout frontier near the README's initial ~600 s budget. The next discriminating treatment therefore remains extending useful work toward ~600 s while holding the wake mechanism constant.

At this decision point:
- elapsed_sec_at_decision: ~35
- estimated_next_task_sec: 240-300
- handoff_safety_margin_sec: 120
- action: CONTINUE useful work; do not lower cutoff from lack of timeout evidence.

Continuation was secured first as the same enabled recurring reservation before durable evidence was written.