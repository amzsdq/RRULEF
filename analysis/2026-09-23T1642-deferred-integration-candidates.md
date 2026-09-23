# Deferred integration candidates discovered during H1

These are potentially useful findings from the two external researchers, but applying them now would contaminate H1. They are queued, not adopted.

## Candidate D1 — adaptive minimal restore
`tEST` has evidence for a one-authoritative-record-first bootstrap on routine clean paths, with semantic expansion on boundary/promotion/anomaly/rollback/reconciliation/prompt-change/ambiguity. This could reduce RRULEF bootstrap read overhead.

Defer reason: changing restore/read policy during H1 would add another optimization variable and make control-overhead comparison harder.

## Candidate D2 — pre-arm-only continuation
`workwork` uses start-of-turn pre-arm as the only scheduler mutation during strict duration probes. This removes final scheduler mutation overhead.

Defer reason: H1 specifically tests pre-arm + final verified rearm because RRULEF has historical final-rearm omission/stale-DTSTART failures. Removing final rearm now would change the treatment architecture, not merely observe H1.

## Candidate D3 — authority fencing for overlap
workwork's historical overlap evidence and authority-generation research suggest fencing can make concurrent wakes safer.

Defer reason: RRULEF currently treats overlap as H1 failure evidence. Adding fencing would mask whether dual-arm itself causes harmful overlap and would add substantial mechanism complexity.

## Candidate D4 — runtime target above 600s
workwork directly supports a 16m strict clean pass and is probing 18m.

Defer reason: runtime safety is environment/workload dependent. RRULEF remains directly verified only to 480s and its 600s duration experiment is frozen during H1.

## Rule
After H1 resolves, rank deferred candidates by expected improvement in long-run useful-work utilization per added control complexity. Test one at a time; do not import them merely because another repository promoted them.
