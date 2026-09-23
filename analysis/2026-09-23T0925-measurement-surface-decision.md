# Measurement-surface decision — 2026-09-23 09:25 KST

## Fresh-read basis
README defines the invariant objective as maximum utilization / minimum idle time. Baseline A's 600 s budget is an initial comparator, not a rule. Scheduler jitter is diagnostic only.

## What this wake established
The current tool surface exposes repository operations and scheduler updates, but does not expose trustworthy per-tool-call start/end timestamps. Therefore exact `active_work_sec`, `work_end_time`, `run_elapsed_sec`, and handoff overhead cannot be reconstructed from connector latency or scheduled timestamps without fabrication.

This is now treated as a measurement-surface limitation, not as a reason to keep producing recovery-plan documents. The optimization experiment can still make useful progress by preserving the single changed variable (`same-wake useful-work duration`) and doing multiple substantive repository operations per wake while recording only metrics that are directly observable.

## Admission decision
- Do not infer active work from API latency.
- Do not infer work_end from scheduler-update time.
- Do not create more short-duration sensitivity artifacts merely to fill a wake.
- Continue substantive same-wake work until the runtime safety margin, then secure continuation first.
- When a future execution surface exposes trustworthy task boundaries, resume exact interval aggregation immediately.

## Experimental constants
- changed variable: same-wake useful-work duration
- estimated next task: 60 s
- handoff safety margin: 120 s
- comparator: 600 s
- scheduler-jitter optimization: disabled

## Useful-work performed in this wake
1. Fresh-read README.
2. Fresh-read canonical state.
3. Inspected repository layout and accumulated analysis artifacts.
4. Identified that repeated instrumentation-recovery artifacts are now diminishing-return work.
5. Converted the limitation into an admission decision that prevents fabricated metrics while allowing sustained useful work.
6. Secured the same recurring continuation before durable-state write.

## Next high-value work
Stop spending wakes on instrumentation-plan variants. Use repository history to consolidate the accumulated experiment evidence into a compact decision table: observed valid pairs, invalid pairs, timeout outcomes, and the highest directly observed safe active-work duration. That consolidation is useful even before exact boundary instrumentation returns.
