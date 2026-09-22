# Boundary-cost reconciliation — 2026-09-23 08:43 KST

Same experiment; no mechanism change.

Two observed regimes exist in the durable analysis:
1. retained post-anchor experiment: 13 samples, mean idle 178.15 s, median 176 s;
2. recent clean boundaries from later short wakes: 393, 441, 555, 634, 749, 807, 643 s, median 634 s.

These should not be blended into a single scheduler-jitter target. Jitter remains exogenous. The robust conclusion shared by both regimes is about boundary frequency: short active windows repeatedly expose the system to a non-trivial idle boundary cost.

Utilization sensitivity:
- with I=178.15 s: A=180 -> 50.26%, A=300 -> 62.74%, A=480 -> 72.92%, A=600 -> 77.11%
- with I=634 s: A=180 -> 22.11%, A=300 -> 32.12%, A=480 -> 43.09%, A=600 -> 48.62%

Therefore the direction of the current experiment is robust to the regime difference: increasing safe same-wake useful work is preferable to manufacturing extra short handoffs. The exact optimal cutoff is still unknown and 600 s remains a comparator, not a rule.

The next decisive evidence is a fully instrumented sustained sample, not another tens-of-seconds sample. Keep estimated-next-task=60 s and safety-margin=120 s fixed while changing only same-wake useful-work duration.
