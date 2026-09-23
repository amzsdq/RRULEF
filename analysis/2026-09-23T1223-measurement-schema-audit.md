# Measurement-schema audit — 2026-09-23 12:23 KST

## Scope
Work-queue item 1: audit measurement-schema consistency. Objective remains maximum useful-work utilization / minimum actual idle gap. No experimental variable is changed here.

## Findings

### 1. Canonical metric definitions are coherent
README and `analysis/2026-09-22_measurement-contract-minimal.md` agree on the useful chain:
- directly observe substantive task boundaries;
- `active_work_sec = sum(task durations)`;
- persist `work_end_time` at the last substantive boundary;
- next wake computes `idle_gap_sec = actual_next_start_time - previous work_end_time`;
- scheduler jitter is diagnostic only.

### 2. Historical run records are heterogeneous
Older Markdown run records can contain directly asserted wall-clock boundaries (for example `runs/2026-09-22T1523+0900.md` and `...T1527+0900.md`), while current `state/latest-run.json` correctly leaves unavailable duration/boundary fields null. Therefore field presence alone is not evidence quality.

Classification for reuse:
- **DIRECT**: timestamp/duration explicitly captured at the substantive boundary in the run record.
- **DERIVED_VALID**: arithmetic from DIRECT boundaries, with the source boundaries preserved.
- **TARGET_OR_ADMISSION**: planned duration, cutoff, filename, decision checkpoint, or requested wake; never completion evidence.
- **UNOBSERVED**: null / explicitly not claimed.

### 3. Frontier record mixes predecessor evidence with current-treatment admission
`runs/2026-09-23T030454+0900-frontier-600.json` directly carries the predecessor pair (`previous_active_work_sec=480`, `idle_gap_sec=251`) but its `target_active_work_sec=600` and `continue_to_600s_then_handoff` are TARGET_OR_ADMISSION. It does not contain `active_work_sec=600` plus a completed substantive boundary. Therefore `state/frontier-evidence.json` is correct to keep 480 seconds verified and 600 seconds pending.

### 4. Current blocker is instrumentation continuity, not a reason to fabricate duration
`state/latest-run.json` has `active_work_sec`, `work_end_time`, `run_elapsed_sec`, and handoff overhead null because this runtime surface has not supplied trustworthy per-task boundary timestamps. Those nulls are measurement-integrity preserving. Connector latency, commit timestamps, filenames, scheduler timestamps, and whole-turn elapsed time must not fill them.

## Minimal normalization rule
For future evidence-table construction, accept a sample only when every metric used by the row is DIRECT or DERIVED_VALID. Preserve null otherwise. Do not rewrite historical records merely to make schemas uniform.

## Next useful-work item
Build the compact paired-run evidence table using only rows that pass the rule above. This advances work-queue item 2 without changing cutoff, handoff mechanism, or scheduler-jitter treatment.
