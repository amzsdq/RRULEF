# Sustained-work test criteria — 2026-09-22 22:28 KST

## Experiment question
With near-future anchoring fixed, does materially extending same-wake useful work improve utilization without introducing timeout/forced-stop loss?

## Evidence before sample
- retained anchor mean idle: 178.15 s across 13 direct post-change samples
- latest short-cycle pair: ~30 s active + 176 s idle = 14.56% utilization
- historical indexed comparator: 323 s active + 1470 s idle = 18.02% utilization
- indexed timeout evidence: zero observed forced stops in the referenced 10-run comparator; this is absence of evidence, not proof of 600 s safety

## What counts as a useful sample
A sustained-work sample is informative if:
1. active_work_sec is directly recorded rather than inferred from commit timestamps;
2. it materially exceeds the recent 30–60 s measurement-driven windows; >=180 s is especially useful because, at the retained mean idle, it crosses the descriptive 50% utilization break-even;
3. timeout_or_forced_stop is recorded;
4. the following actual_next_start closes the causal pair and yields idle_gap_sec;
5. no other mechanism changes during the sample.

## Evaluation
Primary: paired utilization = active_work_sec / (active_work_sec + following idle_gap_sec).
Secondary: timeout/forced-stop loss and tasks_completed.
Diagnostic only: scheduler_jitter_sec.

A single clean >=180 s sample is not enough to set a permanent cutoff. It is enough to test whether the previous measurement-driven 30–60 s behavior was grossly underutilizing the wake. Multiple clean samples near progressively longer active windows are required before changing the 600 s comparator.

## Decision tuple after this task
- current elapsed: still far below 600 s comparator
- estimated next useful task: bounded analysis/state write, <120 s
- handoff safety margin: strongly positive
- decision: CONTINUE
