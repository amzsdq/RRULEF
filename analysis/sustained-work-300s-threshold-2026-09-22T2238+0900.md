# Sustained-work experiment — 300 s threshold rationale

README fresh-read at this wake. Single changed variable remains: suppress measurement-driven premature handoff and extend same-wake useful work; near-future anchoring, scheduler-jitter treatment, and nominal 600 s comparator remain unchanged.

## Direct evidence entering this wake
Previous run endpoint: 2026-09-22 22:36:19 +09:00.
Previous active-work sample: ~180 s, timeout_or_forced_stop=false.
Previous observed idle gap before that run: 296 s.

For utilization U=A/(A+I), holding I=296 s only as the latest observed reference:
- A=180 -> U=37.82%
- A=240 -> U=44.78%
- A=296 -> U=50.00%
- A=300 -> U=50.34%
- A=360 -> U=54.88%
- A=480 -> U=61.86%
- A=600 -> U=66.96%

Thus 300 s is not a new policy cutoff. It is the next empirical milestone because it crosses the latest observed idle cost and therefore crosses 50% paired utilization if idle remains near 296 s. A clean >=300 s sample without forced stop is more decision-useful than collecting another short idle sample.

## Decision rule for this experiment only
At each useful-task boundary record elapsed time, estimated next-task duration, and safety margin. Continue while a bounded useful task fits with a conservative handoff reserve; do not spend active time trying to reduce scheduler jitter. Preserve a clean endpoint before timeout risk becomes material.
