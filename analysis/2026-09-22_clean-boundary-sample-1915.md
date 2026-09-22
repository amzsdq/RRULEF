# Clean boundary sample — 2026-09-22 19:15 KST

Baseline A comparator remains 600 sec. No cutoff or scheduler-mechanism change in this sample.

## Direct observations
- actual_start_time: 2026-09-22T19:14:59+09:00
- README fresh-read at run start.
- Previous run has no valid useful_work_end_time, so cross-run idle_gap_sec is intentionally not asserted.

## Substantive work performed
1. Fresh-read canonical README and revalidated objective/measurement definitions.
2. Fresh-read the immediately preceding run state and reconciled the required next action.
3. Audited the latest commit sequence to ensure no intervening state invalidated the clean-boundary experiment.
4. Created this clean sample artifact with explicit causal timestamps rather than reusing durable-tail timestamps as useful-work boundaries.

## Decision ledger
At the first continuation decision, elapsed runtime was far below the 600-sec comparator and there was no timeout/forced-stop evidence. The next useful task (commit/run-history reconciliation plus durable sample write) was bounded and safe, so work continued rather than handing off early.

Experimental variable remains only useful-work boundary placement. Scheduler jitter is diagnostic only.

## Measurement discipline
- Do not infer active_work_sec from wall-clock runtime.
- Do not use durable save completion as useful_work_end_time.
- The final useful_work_end_time for this run must be captured immediately before handoff bookkeeping begins.
- The following run should use that timestamp plus its actual_start_time to close a causally ordered idle-gap sample.
