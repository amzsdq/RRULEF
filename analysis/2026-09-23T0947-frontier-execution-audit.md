# Active-duration frontier execution audit — 2026-09-23 09:47 KST

## Objective
Maximize useful-work utilization and minimize actual idle gap. Scheduler jitter remains diagnostic only.

## Fresh-state finding
The prior state already selected one treatment variable: same-wake useful-work duration, with a verified clean frontier of 105 s and a next informative milestone of 180 s. Fixed controls remain estimated_next_task_sec=60, handoff_safety_margin_sec=120, comparator_sec=600.

## Execution audit
Recent durable history shows repeated analysis/state commits, but the selected treatment has not yet produced a new directly measured >105 s active-work sample. That means more threshold analysis is not useful work for this experiment. The bottleneck is treatment execution/observability, not model selection.

## Decision
1. Do not change scheduler mechanism, task estimate, safety margin, or comparator.
2. Do not create another sensitivity/threshold analysis after this audit unless new measured evidence arrives.
3. Continue substantive repository work within the same wake; a handoff before the treatment is attempted counts as premature unless runtime-risk evidence requires it.
4. Admit a frontier result only when active_work_sec is directly observable. Do not substitute connector latency, commit timestamps, scheduler timestamps, or whole-turn wall time.
5. If timing remains unobservable, keep timing fields null but continue useful work; do not spend the wake repeatedly documenting the same limitation.

## Current evidence
Clean historical pairs remain:
- 20 s active / 319 s idle = 5.90%
- 32 s active / 304 s idle = 9.52%
- 105 s active / 261 s idle = 28.69%

The next information gain therefore requires a directly observed active block >105 s, preferably >=180 s, under the unchanged controls.
