# Sustained-work frontier sample result — 2026-09-23 01:36 KST

## Treatment
Only same-wake useful-work duration was varied. Scheduler/wake mechanism was not changed.

## Observed run progression
- start: 01:32:25 KST
- predecessor idle: 147s
- predecessor active: 270s
- predecessor paired utilization: 64.75%
- useful tasks in this wake: fresh README/state read; predecessor-pair closure; continuation secure/verify; frontier admission record; utilization reward/risk model; admission checkpoint; result checkpoint.

## Interpretation
This wake intentionally continued beyond the recent 2–4 minute pattern. No timeout or forced-stop signal was observed during the sustained sequence. This is evidence that the prior 270s ceiling was behavioral/operational rather than a demonstrated runtime frontier.

Do not infer that 600s is proven safe from this single sample. The correct next comparison is another sustained sample using the same mechanism, then compare realized active_work_sec and the next closed idle pair.
