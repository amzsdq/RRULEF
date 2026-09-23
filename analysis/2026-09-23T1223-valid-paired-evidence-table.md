# Valid paired-run evidence table — 2026-09-23 12:23 KST

Acceptance rule: every value used for a paired utilization row must be DIRECT or DERIVED_VALID under `analysis/2026-09-23T1223-measurement-schema-audit.md`. Approximate active durations, targets/admissions, and idle-only samples are excluded from the paired table.

| predecessor active_work_sec | following idle_gap_sec | paired utilization | timeout / forced stop | source | status |
|---:|---:|---:|---|---|---|
| 480 | 251 | 0.65663475 (65.66%) | false | `runs/2026-09-23T030454+0900-frontier-600.json` + canonical `state/frontier-evidence.json` | VALID |

## Excluded but still useful evidence
- `analysis/2026-09-22T2306-closed-pair-and-utilization.md`: idle gap 468 s is directly bounded, but predecessor active work is only `~90`; exclude from exact paired-utilization comparison.
- `analysis/2026-09-22_first-corrected-idle-sample.md`: 91 s clean idle gap, but no directly bounded predecessor active duration in that artifact; use as idle-only evidence, not a paired-utilization row.
- `runs/2026-09-22T1523+0900.md`: 61 s clean end/start gap, but active duration is explicitly not claimed; idle-only evidence.
- `runs/2026-09-23T030454+0900-frontier-600.json`: `target_active_work_sec=600` is admission/target evidence only; it cannot create a 600-second paired row.

## Result
There is currently only one exact paired sample strong enough for direct active-duration/utilization comparison. It supports the verified 480-second frontier but is insufficient to fit or promote an adaptive cutoff. The next experiment should not change cutoff from this table alone.

## Next useful-work item
Work-queue item 3 should test only hypotheses that can be evaluated without pretending the excluded rows are exact active-duration pairs. If no such hypothesis has adequate support, retain Baseline A and prioritize new directly instrumented samples.
