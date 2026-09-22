# Next-run execution card — 2026-09-22 16:42 KST

This card is a compact substantive queue to prevent the next wake from stopping after status bookkeeping. Baseline A remains unchanged.

## Execute in order while safe
1. Fresh-read README and latest run only; avoid re-reading all history.
2. Instantiate the same-wake measurement template with exact actual start and prior exact/bounded work_end anchor.
3. Perform one substantive evidence task and append its observed start/end timestamps.
4. Record elapsed / next-task estimate / safety margin. If safely below budget, immediately perform the next evidence task.
5. Continue until approaching runtime risk, a real blocker occurs, or useful queue is exhausted.
6. On handoff, secure the same recurring wake first, confirm enabled, then persist final work_end and handoff metrics.

## Useful evidence tasks
- Reconcile the newest run against the bounded evidence ledger.
- Update aggregate utilization using only compatible exact/bounded observations.
- Test whether a near-budget literal Baseline A sample now exists; if not, continue collecting rather than tuning.
- If sufficient near-budget samples eventually exist, prepare—but do not silently launch—the one-variable cutoff experiment.

## Measurement priority
Exact final work_end_time is especially valuable because it converts the following wake's idle_gap from a bound into an exact observation.

## Decision tuple after this task
- elapsed: below current initial budget
- estimated next useful task: 60–120 sec
- handoff safety margin: still positive
- decision: CONTINUE if runtime permits; otherwise secure handoff before final state write
