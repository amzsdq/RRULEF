# Active-duration evidence consolidation — 2026-09-23 09:35 KST

## Objective
Fresh README read. Optimize useful-work utilization / real work-end-to-next-start idle. Scheduler jitter remains diagnostic only.

## Directly observed clean pairs
| active_work_sec | idle_gap_sec | utilization | forced stop | evidence |
|---:|---:|---:|---|---|
| 20 | 319 | 5.90% | false | 2026-09-22T2339_clean-pair-and-admission.md |
| 105 | 261 | 28.69% | false | 2026-09-22T2345_active-duration-admission.md |
| 32 | 304 | 9.52% | false | 2026-09-22T2350_active-duration-treatment.md |

Earlier retained anchoring evidence reports 13 direct post-change idle samples with mean 178.15 s and median 176 s, plus a ~30 s active / 176 s idle pair yielding 14.56%. It also records historical 10-run aggregate active 323 s / idle 1470 s = 18.02%.

## What the evidence does and does not prove
The clean pairs are not a randomized causal comparison because idle changed between runs. They do establish that bookkeeping-sized active blocks pay a large boundary cost. The 105 s clean pair is the highest directly verified active-work duration located in the currently consolidated evidence set; it completed without forced stop. Do not claim a higher directly observed safe duration until a source is located.

At the retained post-anchor mean idle of 178.15 s, 180 s active is approximately the 50% utilization break-even. This is leverage analysis, not a cutoff rule. The nominal 600 s Baseline-A comparator remains an experimental reference, not doctrine.

## Decision
The current evidence is sufficient to reject further 20–105 s bookkeeping-sized handoffs as the main experiment. Preserve the single changed variable: same-wake useful-work duration. Scheduler mechanism, estimated next task (60 s), safety margin (120 s), and 600 s comparator remain fixed.

Next high-value treatment is a directly measured same-wake active block materially above the verified 105 s point, preferably crossing 180 s if runtime safety permits. Continue bounded substantive tasks inside the same wake; do not hand off merely because one analysis artifact completed. If direct task-boundary timing is unavailable, do not fabricate active time; continue useful repository work and leave unavailable timing fields null.

## Admission checkpoint
At this decision point the known directly verified active-duration frontier is 105 s, well below the nominal 600 s comparator. Estimated next bounded task: 60 s. Handoff safety margin: 120 s. In the absence of a concrete runtime-risk signal, another bounded useful task is admissible before handoff.
