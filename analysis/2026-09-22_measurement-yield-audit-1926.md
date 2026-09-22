# Measurement-yield audit — 2026-09-22 19:26 KST

## Question
Are recent wakes producing evidence that can actually discriminate between continuation/handoff policies, or mostly producing measurement-policy prose?

## Evidence inspected
Recent commits show repeated clean-boundary definitions and audits, while the latest preceding pair still lacks the one datum required to close cross-run idle: a directly captured useful_work_end_time.

## Finding
The bottleneck is no longer definition quality. It is endpoint capture. Additional policy prose without a captured endpoint has near-zero marginal value for the objective.

## Operational consequence
For the current single-variable experiment, useful work should prioritize producing a valid causal measurement pair over adding further policy layers. A valid pair has exactly two critical observed boundary values:
1. useful_work_end_time from the ending wake;
2. actual_start_time from the following wake.

Everything else is secondary metadata unless needed to interpret timeout loss or handoff cost.

## Baseline implication
No evidence from this audit supports shortening the 600-sec comparator. There remains no observed timeout/forced-stop loss in the inspected latest state. The next decision should therefore continue useful bounded work while safely below the comparator, then capture the endpoint directly before handoff bookkeeping.
