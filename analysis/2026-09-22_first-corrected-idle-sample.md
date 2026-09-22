# First corrected causal idle-gap sample

Fresh README read performed before this analysis.

## Direct boundary pair
- previous directly observed useful-work end: `2026-09-22T19:43:00+09:00`
- current actual execution start: `2026-09-22T19:44:31+09:00`
- corrected `idle_gap_sec = 91`

This is the first boundary pair in the recent sequence where the previous endpoint was explicitly captured before handoff bookkeeping and the next start is directly observed. It therefore supersedes the earlier negative/mixed-boundary sample for optimization evidence.

## What the sample says
The 91-second idle gap is an outcome metric. Scheduler jitter is not treated as the optimization target and no scheduler mechanism or cutoff is changed in this sample.

For a run with active useful work `A` seconds followed by a 91-second causal idle gap, utilization is:

`U = A / (A + 91)`

Useful-work requirements implied by this observed gap:
- 80% utilization requires `A >= 364 sec`
- 85% utilization requires `A >= 516 sec`
- 90% utilization requires `A >= 819 sec`

At exactly 600 seconds of useful work, the corresponding utilization would be `600 / 691 = 86.83%` if the next causal idle gap were again 91 seconds.

These are sensitivity calculations, not a recommendation to change the 600-second comparator. One clean idle sample is insufficient to change cutoff. The next evidence priority is to obtain additional corrected causal idle gaps plus directly bounded active useful-work time, while keeping Baseline A unchanged.

## Experiment discipline
Changed variable: none. This run closes a previously missing measurement boundary. Baseline A remains the comparator.
