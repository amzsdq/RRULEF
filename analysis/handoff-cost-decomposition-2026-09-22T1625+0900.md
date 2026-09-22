# Handoff-cost decomposition — 2026-09-22 16:25 KST

## Observed recent transitions
Using three recent runs with explicit handoff overhead:

| run | active work | handoff overhead | following idle gap |
|---|---:|---:|---:|
| 16:10 | 31 s | 7 s | 238 s |
| 16:14 | 24 s | 10 s | 252 s |
| 16:17 | 26 s | 13 s | 163 s |
| total | 81 s | 30 s | 653 s |

Observed active/(active+idle) utilization across these transitions is 81/(81+653) = 11.0%.

## Counterfactual that does not assume better scheduler jitter
If those three short active segments had been safely performed inside one continuous wake rather than separated by two intermediate handoffs, the 81 seconds of useful work itself does not change. The avoidable component is the need to incur intermediate post-handoff gaps at all. We cannot claim all 653 seconds would disappear because the final wake transition still exists and scheduler delay is exogenous.

A conservative framing is therefore:
- handoff bookkeeping itself: only 30 sec observed across the three runs;
- post-handoff idle exposure: 653 sec observed;
- optimization target: reduce the *number of exposures* to post-handoff idle by doing more safe useful work before handoff, not by assuming each exposure's scheduler jitter becomes smaller.

## Why longer same-wake work is the dominant candidate
The 10-sample audit found 323 sec active and 1470 sec idle. Even if handoff bookkeeping were reduced to zero, that would not address the dominant idle mass. Conversely, combining several short safe tasks into one wake removes intermediate opportunities for large idle gaps while leaving scheduler behavior untouched.

## Experimental implication
The next valid comparison should hold the 10-minute cutoff constant and change no scheduler mechanism. The only correction is execution fidelity: actually continue safe useful tasks in the same wake. Compare resulting active-work duration and number of handoff exposures against the short-run sample set.