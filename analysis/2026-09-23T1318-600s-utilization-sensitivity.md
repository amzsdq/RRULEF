# 600-second utilization sensitivity — 2026-09-23 13:18 KST

Objective: maximize useful-work utilization / minimize actual idle gap. Scheduler jitter is not optimized here. This analysis does not promote 600 seconds; it quantifies the expected utilization effect of extending the verified 480-second block to 600 seconds while holding boundary idle fixed.

## Inputs
Exact historical following-idle values: 319, 261, 304, 251 seconds. Verified frontier: 480 seconds active with 251 seconds following idle, utilization 65.663475%.

## Controlled sensitivity
For each observed idle cost `I`, compare `U480 = 480/(480+I)` with `U600 = 600/(600+I)`.

| held-fixed idle sec | U480 | U600 | gain from +120s active |
|---:|---:|---:|---:|
| 251 | 65.66% | 70.51% | +4.84 pp |
| 261 | 64.78% | 69.69% | +4.91 pp |
| 304 | 61.22% | 66.37% | +5.15 pp |
| 319 | 60.08% | 65.29% | +5.21 pp |

Across the exact observed idle range, a safe completed 600-second block would raise utilization by roughly 4.84–5.21 percentage points relative to a 480-second block **if boundary idle were held fixed**. This is arithmetic sensitivity, not causal evidence that the next observed idle will be unchanged.

## Decision implication
The evidence gives a concrete reason to keep 600 seconds as the next single-variable treatment: the potential utilization gain is material, while no exact 480-second run shows forced-stop evidence. However, 600 seconds remains unverified until direct task-boundary instrumentation records an actual completed 600-second useful-work block. No adaptive cutoff is promoted from this calculation.
