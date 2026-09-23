# Valid paired-run evidence table — corrected 2026-09-23 12:56 KST

Acceptance rule: every value used for an **exact** paired-utilization row must be DIRECT or DERIVED_VALID under `analysis/2026-09-23T1223-measurement-schema-audit.md`. Approximate active durations remain useful as a separate lower-confidence stratum; they must not be mixed into exact cutoff fitting.

## Exact paired evidence

| predecessor active_work_sec | following idle_gap_sec | paired utilization | source | status |
|---:|---:|---:|---|---|
| 20 | 319 | 0.05899705 (5.90%) | `analysis/2026-09-22T2339_clean-pair-and-admission.md` | VALID_EXACT |
| 105 | 261 | 0.28688525 (28.69%) | `analysis/2026-09-22T2345_active-duration-admission.md` | VALID_EXACT |
| 32 | 304 | 0.09523810 (9.52%) | `analysis/2026-09-22T2350_active-duration-treatment.md` | VALID_EXACT |
| 480 | 251 | 0.65663475 (65.66%) | `runs/2026-09-23T030454+0900-frontier-600.json` + `state/frontier-evidence.json` | VALID_EXACT |

Exact-pair count: 4.

## Approximate paired evidence — separate stratum

| predecessor active_work_sec | following idle_gap_sec | paired utilization | source | status |
|---:|---:|---:|---|---|
| ~90 | 468 | 0.1613 (16.13%) | `analysis/2026-09-22T2306-closed-pair-and-utilization.md` | VALID_APPROXIMATE_ONLY |

This row is a real historical pair, but the predecessor active duration is approximate. It therefore increases qualitative evidence that boundary idle dominates short blocks, while **not** increasing the exact-pair count and **not** entering precise adaptive-cutoff fitting.

## Other excluded/useful evidence
- `analysis/2026-09-22_first-corrected-idle-sample.md`: clean idle gap but no directly bounded predecessor active duration in that artifact; idle-only evidence.
- `runs/2026-09-22T1523+0900.md`: 61 s clean end/start gap, but active duration is explicitly not claimed; idle-only evidence.
- `runs/2026-09-23T030454+0900-frontier-600.json`: `target_active_work_sec=600` is admission/target evidence only; it cannot create a 600-second completed row.

## Result
The repository contains **four exact pairs plus at least one approximate pair**. The earlier canonical phrase `known-at-least-5-clean-or-exact-pairs` conflated confidence classes and is retired. Exact evidence still supports the qualitative active-duration hypothesis: very short useful-work blocks have poor utilization when boundary idle is hundreds of seconds, while the 480-second completed block reached 65.66%. Idle cost varies materially across samples, so these sparse/non-random pairs still do not identify a precise adaptive cutoff.

Operational implication remains unchanged: keep the verified 480-second frontier, preserve 600 seconds as the next direct-completion milestone, and prioritize direct instrumentation rather than changing another mechanism.