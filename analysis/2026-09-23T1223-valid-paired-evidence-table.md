# Valid paired-run evidence table — corrected 2026-09-23 12:26 KST

Acceptance rule: every value used for a paired utilization row must be DIRECT or DERIVED_VALID under `analysis/2026-09-23T1223-measurement-schema-audit.md`. Approximate active durations, targets/admissions, and idle-only samples are excluded.

| predecessor active_work_sec | following idle_gap_sec | paired utilization | source | status |
|---:|---:|---:|---|---|
| 20 | 319 | 0.05899705 (5.90%) | `analysis/2026-09-22T2339_clean-pair-and-admission.md` | VALID |
| 105 | 261 | 0.28688525 (28.69%) | `analysis/2026-09-22T2345_active-duration-admission.md` | VALID |
| 32 | 304 | 0.09523810 (9.52%) | `analysis/2026-09-22T2350_active-duration-treatment.md` | VALID |
| 480 | 251 | 0.65663475 (65.66%) | `runs/2026-09-23T030454+0900-frontier-600.json` + canonical `state/frontier-evidence.json` | VALID |

## Excluded but still useful evidence
- `analysis/2026-09-22T2306-closed-pair-and-utilization.md`: predecessor active work is only `~90`; exclude from exact comparison.
- `analysis/2026-09-22_first-corrected-idle-sample.md`: clean idle gap but no directly bounded predecessor active duration in that artifact; idle-only evidence.
- `runs/2026-09-22T1523+0900.md`: 61 s clean end/start gap, but active duration is explicitly not claimed; idle-only evidence.
- `runs/2026-09-23T030454+0900-frontier-600.json`: `target_active_work_sec=600` is admission/target evidence only; it cannot create a 600-second completed row.

## Result
There are four exact paired samples, not one. They support the qualitative active-duration hypothesis: very short useful-work blocks have poor utilization when boundary idle is hundreds of seconds, while the 480-second completed block reached 65.66%. They are still insufficient for a precise adaptive cutoff because idle varies and durations are sparse/non-random. Keep the verified 480-second frontier and prioritize directly instrumented longer samples rather than changing another mechanism.

## Correction note
The prior version incorrectly omitted three historical artifacts that explicitly asserted exact predecessor active duration and following idle gap. See `analysis/2026-09-23T1226-evidence-table-correction.md`.