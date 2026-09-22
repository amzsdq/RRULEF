# Run 12 — boundary exposure value

Baseline A remains unchanged. This note asks what useful-work gain is required for continuing inside the current wake to dominate an immediate handoff, without assuming scheduler jitter improves.

Indexed comparable evidence: 323 sec active and 1470 sec observed idle across 10 runs, so observed idle exposure per boundary averages 147 sec. This is descriptive, not a scheduler forecast.

If a safe next task consumes t seconds of useful work now, continuing avoids creating one handoff boundary before that task. The relevant comparison is therefore not 'can jitter be reduced?' but whether the expected timeout/lost-work cost of t exceeds the value of useful work plus one avoided boundary exposure.

For bounded next tasks of 60, 120, and 180 sec, an immediate handoff exposes the system to another idle boundary before receiving that useful work. With no positive forced-stop observation in indexed evidence and current elapsed well below the 600 sec comparator, there is presently no empirical reason to prefer immediate handoff over executing such bounded tasks now.

This does not prove 600 sec is optimal. It supports literal execution of Baseline A until either elapsed approaches the comparator or a concrete runtime-risk signal appears.

Decision tuple after this task:
- current elapsed: below 600 sec comparator
- estimated next task: 60–150 sec
- handoff safety margin: positive
- decision: CONTINUE
