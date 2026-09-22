# Sustained-work sample execution — 2026-09-22 22:33 KST

## Experiment integrity
README fresh-read. The only changed operational variable remains measurement-driven premature handoff -> sustained same-wake useful work. Near-future anchoring, nominal 600 s comparator, and jitter treatment remain fixed.

## Closed prior causal pair
- previous direct work_end_time: 2026-09-22 22:28:23 +09:00
- actual_next_start_time: 2026-09-22 22:33:19 +09:00
- idle_gap_sec: 296
- prior scheduled_next_wake: 2026-09-22 22:31:00 +09:00
- scheduler_jitter_sec: +139 (diagnostic only)
- previous active_work_sec: ~60
- paired utilization: 60 / (60 + 296) = 16.85%

This reinforces the boundary-frequency result: a ~60 s useful window still pays a large boundary exposure and is structurally poor utilization.

## Current wake execution target
Do not hand off for measurement density. Chain bounded useful tasks until at least 180 s direct same-wake active span is obtained, then continue farther if the next bounded task plus handoff margin still fits safely under the nominal 600 s comparator.

Decision tuple at sample start:
- current elapsed: ~0 s
- estimated next useful task: 60-120 s
- handoff safety margin: strongly positive
- decision: CONTINUE

No cutoff change is authorized by this sample; 180 s is a measurement milestone, not a policy threshold.
