# Active-duration utilization envelope — 2026-09-23 01:04 KST

## Objective
Keep the sole experiment variable as same-wake useful-work duration. Scheduler jitter is diagnostic only.

## Clean paired samples observed in the current treatment sequence
| predecessor active_work_sec | successor idle_gap_sec | paired utilization |
|---:|---:|---:|
| 84 | 217 | 27.91% |
| 194 | 91 | 68.07% |
| 72 | 211 | 25.44% |
| 142 | 467 | 23.32% |
| 130 | 253 | 33.94% |

Overlap-invalid pairs are excluded rather than clamped to zero idle.

## Derived envelope
Across these five clean pairs:
- total predecessor useful work = 622 sec
- total observed idle = 1,239 sec
- aggregate useful-work utilization = 622 / (622 + 1,239) = 33.42%
- mean idle gap = 247.8 sec
- median idle gap = 217 sec

For a fixed external idle gap I, utilization is A/(A+I), where A is same-wake active work. Using the observed median idle 217 sec:
- A=96 sec -> 30.67%
- A=180 sec -> 45.34%
- A=300 sec -> 58.03%
- A=600 sec -> 73.44%

Using the observed mean idle 247.8 sec:
- A=96 sec -> 27.92%
- A=180 sec -> 42.08%
- A=300 sec -> 54.76%
- A=600 sec -> 70.77%

## Decision implication
The present evidence does not justify changing wake/jitter mechanics inside this experiment. It does justify continuing to push the one allowed variable — useful-work duration — upward while timeout/forced-stop remains false. The strongest completed treatment so far (194 sec) finished without forced stop, so the next useful evidence is another >=180 sec clean treatment and successor pair, then progressively longer durations if safety remains intact.

No new policy is introduced; this is measurement evidence for adaptive cutoff later.