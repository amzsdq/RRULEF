# H1 integration decision — 2026-09-23 16:30 KST

## Sources reviewed
READ_ONLY:
- amzsdq/tEST: same-automation recurring RRULE experiments, +3m practical lead evidence, WRITE_OK/STATE_OK/WAKE_OK separation, P2 rejection of unnecessary extra mutation.
- amzsdq/workwork: pre-arm-at-start runtime research, long-turn boundary search, start+target+gap crash-insurance pattern.
- amzsdq/RRULEF: verified own frontier 480s; 600s direct completion evidence still pending; prior stale-DTSTART failure exists.

## Synthesis
Do not copy either source wholesale.

tEST optimizes a final-write continuation path and found extra provisional mutation unnecessary in its tested context. workwork removes end mutation and pre-arms at turn start, which protects long-turn continuation but can leave a longer idle gap if a turn closes early.

RRULEF has a concrete failure class that neither should be ignored: final rearm can be omitted/stale, causing fallback to the hourly recurrence. Therefore H1 tests a bounded hybrid:
- start pre-arm = crash insurance;
- final verified rearm = authoritative fast continuation;
- pre-arm survives only when final close/rearm is missed.

## Single changed variable
Compared with final-only continuation, H1 changes only `start_of_turn_crash_insurance_prearm_enabled=false -> true`.

Frozen during H1:
- target runtime = 600s
- prearm/final nominal gap = 180s
- scheduler jitter remains diagnostic only
- same automation + recurring hourly RRULE
- exact live verification for the experimental scheduler writes
- RRULEF direct evidence required for frontier promotion

## Success criteria
H1 is useful only if it reduces or bounds catastrophic handoff gaps from final-rearm omission/stale-due failures without causing material overlap or enough write/control overhead to reduce long-run useful-work utilization.

## Rejection criteria
Reject H1 and return to final-only if:
- overlap/concurrency appears,
- start pre-arm routinely becomes the actual handoff despite successful close,
- extra mutation creates measurable control bottleneck,
- no final-rearm failure is observed across enough runs and utilization is lower.

## Immediate bootstrap
The currently live RRULEF schedule was still anchored to 16:00 hourly recurrence after the 15:59:57 run. That state is not counted as H1 evidence. Operator bootstrap will re-anchor the same recurring automation to a near-future wake; the first scheduled run under the new kernel begins H1 evidence collection.
