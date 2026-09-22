# Measurement-integrity audit — 2026-09-22 16:25 KST

## Scope
Fresh-read README plus recent durable Baseline A records. Cutoff remains unchanged.

## Findings

### 1. Decision text contradicted the action
Recent runs explicitly recorded all three of these facts together:
- elapsed only 24–31 sec,
- estimated next useful task 45–90 sec,
- handoff safety margin high / far below 10-minute budget.

Yet the wake ended and handed off. That is an execution-integrity defect, not evidence against the 10-minute cutoff.

Examples:
- 16:10 run: elapsed 31 sec, next task 45–90 sec, safety margin high.
- 16:14 run: elapsed 24 sec, next task 45–90 sec, safety margin high.
- 16:17 run: elapsed 26 sec, next task 45–90 sec, safety margin high.

### 2. `active_work_sec` has mixed precision semantics
Some records report exact-looking active_work_sec values derived from start/end timestamps, while the 16:21 audit correctly switched to a conservative `>=16` lower bound because connector-backed useful work could not be cleanly separated from tool latency/bookkeeping. Future records should preserve observed precision rather than invent exactness. This is measurement hygiene; it does not alter the experiment.

### 3. `tasks_completed` overstates substantive throughput when bookkeeping is counted
Several short runs report five completed tasks, but the listed tasks are mainly README read, previous-run read, metric calculation, unchanged-cutoff confirmation, and wake securing. These are necessary control-plane operations, but counting each as equivalent to substantive optimization work can make throughput look healthier than it is.

Recommendation: retain `tasks_completed` for compatibility, but in prose distinguish control/measurement tasks from substantive optimization artifacts. Do not add a mandatory schema field unless it proves useful.

### 4. Observed handoff overhead is small relative to post-handoff idle
Recent examples:
- 16:10: handoff_overhead 7 sec vs idle_gap 238 sec.
- 16:14: handoff_overhead 10 sec vs idle_gap 252 sec.
- 16:17: handoff_overhead 13 sec vs idle_gap 163 sec.

Therefore reducing a few seconds of handoff bookkeeping is not the primary lever. The much larger lever is avoiding unnecessary handoffs by continuing useful work within a wake.

## Actionable conclusion
Do not change scheduler jitter handling or the 10-minute cutoff yet. First obtain literal continuous Baseline A samples where multiple substantive tasks are performed sequentially and the wake continues while elapsed time plus estimated next task remains safely inside the runtime margin.