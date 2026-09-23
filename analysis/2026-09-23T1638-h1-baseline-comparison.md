# H1 baseline comparison frame

## Direct RRULEF baseline evidence
Two prior direct pairs illustrate why handoff reliability matters more than second-perfect jitter:

1. 2026-09-22 23:33:30 -> 23:38:49
   - active_work_sec: 20
   - idle_gap_sec: 319
   - paired utilization: 5.90%
   - scheduled wake was 23:36:00; observed scheduler jitter 169s was diagnostic.

2. 2026-09-23 01:55:27 -> 02:03:24
   - active_work_sec: 150
   - idle_gap_sec: 477
   - paired utilization: 23.92%
   - root cause included a stale requested DTSTART at scheduler-write time, a handoff correctness failure rather than evidence that provider jitter itself should be optimized.

## Why H1 is a valid next experiment
The previous RRULEF treatment extended useful-work duration but still left a catastrophic correctness mode: if final rearm is omitted, stale, or never reached, the recurring hourly fallback can dominate the next idle boundary. H1 changes only one variable—pre-arm enabled at wake start—to bound that failure mode before substantive work.

## H1 measurements required
For each H1 sample preserve:
- scheduled_for and actual_start;
- predecessor work_end_time and direct idle_gap_sec when available;
- pre-arm intended due, WRITE_OK, STATE_OK;
- useful-work duration and task count;
- final-rearm intended due, WRITE_OK, STATE_OK;
- whether final rearm superseded pre-arm;
- next actual invocation and retrospective WAKE_OK;
- overlap/duplicate evidence;
- scheduler mutations count and observable handoff/control overhead.

## Comparison rule
Do not compare H1 against a theoretical zero-idle system. Compare against RRULEF's own final-only historical behavior and, later, a registered final-only control under the same 600s target if necessary. External tEST/workwork evidence is mechanistic support only.

## Current sample-1 admission
At this checkpoint H1 sample 1 has completed bootstrap, live pre-arm verification, external-head reconciliation, and failure-envelope analysis. These are substantive control/research units but do not constitute a 600s completion. Continue useful work while the admission inequality remains satisfied; do not promote 600s until a direct normal-close sample reaches the target and a later invocation supplies WAKE_OK.
