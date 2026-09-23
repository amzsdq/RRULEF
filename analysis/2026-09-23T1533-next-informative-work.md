# Next informative work — 2026-09-23 15:33 KST

README fresh-read. Objective remains maximum useful-work utilization / minimum actual idle gap. Scheduler jitter remains diagnostic only.

## Current constraint
This execution surface still does not expose a direct task timer, so it cannot honestly promote the 600-second active-work frontier. The verified frontier remains 480 seconds with a following observed idle gap of 251 seconds.

## Substantive decision
Repeated 480→600 sensitivity arithmetic and repeated promotion-gate restatement have zero marginal information gain. While direct timing is unavailable, repository work should be selected by whether it can change a future decision or remove measurement ambiguity.

Priority order for bounded same-wake work:
1. close a real predecessor→successor boundary when both timestamps are directly available;
2. audit new run records for DIRECT/DERIVED_VALID evidence capable of changing the frontier;
3. remove contradictory or duplicate state that could cause a later worker to misclassify target/admission values as completed durations;
4. only then perform new modeling, and only if it changes an admission or handoff decision.

## Admission decision
- current_elapsed_sec: unobserved
- estimated_next_task_sec: 120
- handoff_safety_margin_sec: 120
- comparator_sec: 600
- changed experimental variable: none; same-wake useful-work duration remains the sole treatment variable
- action: continue bounded substantive repository work rather than terminate after bookkeeping

No duration is inferred from commit, connector, scheduler, or whole-turn timestamps.