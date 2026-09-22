# Duration-treatment admission — 2026-09-23 00:00 KST

## Fresh inputs
- README fresh-read: objective remains maximum utilization / minimum actual idle gap; scheduler jitter is diagnostic only.
- Canonical predecessor: work_end_time=2026-09-22T23:54:50+09:00, active_work_sec=20, timeout_or_forced_stop=false.
- Actual current start=2026-09-23T00:00:43+09:00.

## Closed causal pair
- idle_gap_sec=353.
- paired_utilization=20/(20+353)=0.0536193 (5.36%).
- Previous requested wake=2026-09-23T00:01:00+09:00; scheduler_jitter_sec=-17. Diagnostic only; no attempt is made to optimize it.

## Treatment decision
The clean pair reinforces that bookkeeping-sized 20-second active blocks are dominated by inter-run idle cost. Keep the single experimental variable unchanged: same-wake useful-work duration. Do not change cutoff, jitter handling, or handoff mechanism in this sample.

Admission record before the next useful task:
- elapsed_sec_at_decision: 10
- estimated_next_task_sec: 180
- handoff_safety_margin_sec: 120
- action: continue
- rationale: the intended >=180-second treatment plus safety margin remains far below the current ~10-minute baseline budget, and the previous run had no timeout/forced stop.

The recurring continuation was secured before this durable write.