# 600s treatment runtime-observability blocker

Fresh-read basis: README objective is maximum useful-work utilization / minimum actual idle gap; 600s is a treatment comparator, not a policy.

## Direct observation
Recent commit history shows repeated wake checkpoints from ~10:25 through 12:00, but no directly measured completed 600s same-wake active-work sample. `state/latest-run.json` therefore correctly leaves `active_work_sec`, `work_end_time`, and `run_elapsed_sec` null.

## Root cause
The current execution surface exposes repository/API operations and scheduler updates, but it does not expose a monotonic per-turn runtime clock or a trustworthy callback that marks the end of each useful task. Whole-turn wall time, connector latency, commit timestamps, filenames, or scheduled timestamps are not valid substitutes for active useful-work duration.

Consequently, repeatedly writing `600s pending` checkpoints cannot produce the missing measurement. That loop consumes useful-work budget without increasing experimental information.

## Actionable correction
Do not promote the frontier above 480s without direct evidence. Do not spend future wakes re-proving that 600s is pending. Use each wake for concrete repository work and record task count/results. A 600s frontier experiment becomes valid only when the runtime surface provides directly observed start/end boundaries (or an equivalent trusted timer). Until then, duration fields remain null rather than fabricated.

Single changed variable remains same-wake useful-work duration; no jitter optimization is introduced.
