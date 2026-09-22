# Run 12 — timeout evidence threshold

Purpose: keep the single-variable experiment interpretable while deciding when an early handoff is evidence-based.

Current indexed evidence reports zero observed forced stops in the 10 comparable short runs. Recent runs also report timeout_or_forced_stop=false. Therefore an early handoff below the current 600 sec comparator should be justified by an observable runtime-risk signal, not merely elapsed anxiety.

Useful observable evidence includes: an actual forced stop/lost durable work; a platform/runtime warning that materially reduces remaining execution margin; or a next task whose estimated duration plus durable-save/handoff margin would cross the current comparator or a known runtime bound.

Absent such evidence, bounded useful work should continue while elapsed remains materially below 600 sec. This is not a new policy; it is an evidence interpretation for Baseline A and does not change its cutoff.

Decision tuple after this task:
- current elapsed: below comparator
- estimated next task: 60–150 sec
- handoff safety margin: positive
- decision: CONTINUE
