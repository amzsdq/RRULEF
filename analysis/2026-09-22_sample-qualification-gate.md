# Empirical sample qualification gate — 2026-09-22

This is an analysis result, not an operating policy change.

A run can inform adaptive-cutoff selection only when it has enough direct timing evidence to distinguish useful work, handoff cost, and next-wake idle gap. Minimum evidence:

1. Direct task start/end timestamps for substantive tasks.
2. Direct `handoff_decision_time` and `handoff_complete_time` if a handoff occurs.
3. The following wake records its actual start, allowing the previous run's idle gap to be closed.
4. Any timeout/forced stop or lost incomplete work is recorded rather than discarded.

Existing samples without these boundaries remain useful for qualitative evidence (for example, demonstrating that >100 sec same-wake work can complete without forced stop) but should not be used to numerically optimize the 600-sec comparator.

Reason: changing the cutoff from mixed or lower-bound intervals would optimize measurement artifacts rather than utilization.
