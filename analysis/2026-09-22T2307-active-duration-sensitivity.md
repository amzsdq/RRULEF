# Active-duration sensitivity at 468-sec observed idle

Single-variable experiment: active useful-work duration only. Scheduler/wake mechanism held constant.

Observed clean idle cost from the latest pair: 468 sec.

Utilization sensitivity, assuming the same idle cost:

| active_work_sec | utilization |
|---:|---:|
| 90 | 16.13% |
| 180 | 27.78% |
| 240 | 33.90% |
| 300 | 39.06% |
| 360 | 43.48% |
| 420 | 47.30% |
| 468 | 50.00% |
| 480 | 50.63% |
| 540 | 53.57% |
| 600 | 56.18% |

Marginal interpretation:
- 90 -> 180 sec: +11.65 percentage points
- 180 -> 300 sec: +11.28 pp
- 300 -> 480 sec: +11.57 pp
- 480 -> 600 sec: +5.55 pp

The current evidence therefore does not justify early handoff at ~90-180 sec merely for measurement. A longer same-wake work interval has materially larger expected utilization impact than shaving a few seconds from scheduler lead, provided timeout/forced-stop risk remains low.

No new cutoff is adopted here. Continue collecting directly measured active duration and timeout outcomes before promoting a threshold.
