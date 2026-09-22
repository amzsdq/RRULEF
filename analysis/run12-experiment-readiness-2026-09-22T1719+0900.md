# Run 12 — experiment readiness

Question: is there enough evidence to change the 600 sec initial cutoff now?

No.

Evidence currently distinguishes two facts:
- short-run behavior has poor utilization and repeatedly exposes the system to idle boundaries;
- there is not yet an observed forced-stop/lost-work curve at longer same-wake elapsed.

Changing cutoff now would alter the experimental variable before Baseline A has been exercised near its nominal range. That would make it impossible to tell whether any utilization change came from the cutoff value or simply from finally following the baseline.

Therefore the next informative experiment remains execution fidelity: accumulate substantially more same-wake useful work under the unchanged comparator, with exact timing. Only after at least one materially longer sample or a concrete runtime-risk event should cutoff selection be reconsidered.

Decision tuple after this task:
- current elapsed: below comparator
- estimated next task: 60–120 sec
- handoff safety margin: positive
- decision: CONTINUE
