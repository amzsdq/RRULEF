# Duration frontier synthesis — 2026-09-23 01:54 +09:00

This continues the same single-variable experiment: same-wake useful-work duration.

Observed clean predecessor pair this wake:
- predecessor useful work: 300 s
- real boundary idle: 932 s
- utilization: 24.35%
- predecessor forced stop/timeout: false

Sensitivity at the same observed 932 s boundary cost (not a prediction of scheduler behavior):
- 300 s active => 24.35%
- 450 s active => 32.56%
- 600 s active => 39.16%
- 720 s active => 43.58%

Marginal gain from 300 -> 600 s is +14.81 percentage points under the same boundary cost. Because the prior 300 s run completed without timeout/forced-stop, current evidence does not justify reducing the initial 600 s Baseline-A budget. It also does not yet justify raising the cutoff above 600 s: the runtime safety frontier has not been measured there.

Decision record for adaptive-cutoff comparison:
- current elapsed at synthesis: ~60–90 s
- estimated next task block: 120–180 s
- handoff safety margin: 120 s
- decision: continue useful work while elapsed + estimated task + margin remains inside the current 600 s experimental envelope; secure continuation before final handoff.
- changed variable: none beyond useful-work duration.
- deliberately unchanged: scheduler/wake mechanism, jitter handling, safety margin semantics.

Practical inference: the strongest current lever is boundary amortization by sustained useful work, not chasing scheduler jitter. The next discriminating evidence is a clean run approaching the 600 s envelope with timeout_or_forced_stop=false/true recorded.
