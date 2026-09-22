# Utilization leverage audit — 2026-09-22

## Inputs
- Baseline A comparator: 600 sec (unchanged).
- Direct paired sample: active_work_sec=85, idle_gap_sec=496, utilization=14.63%.
- Scheduler jitter remains diagnostic/exogenous, not an optimization target.

## Useful-work leverage with idle held fixed
Using U = W/(W+I), with I=496 sec:
- W=85 sec -> 14.63%
- W=300 sec -> 37.69%
- W=600 sec -> 54.74%
- W=900 sec -> 64.47%

Required useful work for target utilization if idle remains 496 sec:
- 50% -> W=496 sec
- 60% -> W=744 sec
- 70% -> W=1157.3 sec
- 80% -> W=1984 sec

## Decision consequence
The direct sample provides no evidence for reducing the 600-sec comparator. With a large inter-run idle gap, reducing useful work mechanically lowers utilization unless the shorter run causally reduces idle or timeout loss. No such causal evidence exists in the current clean sample set.

The next high-value evidence is therefore not another policy document or a scheduler-jitter optimization. It is another directly paired run containing:
1. per-task measured active_work_sec,
2. a directly captured final useful-work endpoint,
3. the next actual start,
4. timeout/forced-stop outcome.

Only after multiple paired samples should cutoff adaptation be evaluated. The experimental variable remains per-task duration instrumentation; cutoff and scheduler mechanism remain unchanged.