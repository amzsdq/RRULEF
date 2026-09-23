# H1 evidence classification matrix

The integration layer must not collapse evidence classes from RRULEF, tEST, and workwork.

| Evidence | Can validate H1 mechanism? | Can promote RRULEF runtime frontier? | Notes |
|---|---:|---:|---|
| RRULEF pre-arm WRITE_OK only | no | no | mutation accepted, future wake unknown |
| RRULEF pre-arm STATE_OK | partial | no | intended recurring state verified, future wake unknown |
| RRULEF clean final rearm STATE_OK | partial | no | normal handoff state verified |
| following RRULEF actual wake | yes for prior WAKE_OK | no by itself | closes continuation pair |
| RRULEF direct 600s useful-work completion + clean close | yes | candidate yes | still needs following wake for full handoff evidence |
| tEST lead-time/wake result | mechanistic support | no | scheduler semantics source |
| workwork strict 16m CLEAN_PASS_WAKE_OK | mechanistic/runtime support | no | different workload/repo; cannot inherit frontier |
| workwork 18m start record | pre-arm mechanics only | no | in progress; not duration PASS |
| target/filename/commit latency | no | no | never substitute for direct duration |

## Current direct status
- RRULEF verified active frontier remains 480s.
- H1 sample 1 pre-arm WRITE_OK=YES, STATE_OK=YES, WAKE_OK=PENDING.
- bootstrap reanchor wake occurred and is retrospectively WAKE_OK=YES.
- no direct predecessor work_end_time exists in `state/latest-run.json`, so ACTUAL_IDLE_GAP for this wake remains unavailable rather than inferred.
- workwork 16m strict clean pass is external supporting evidence only.

## Guard
Every future integration decision must state which row/class its evidence belongs to. This prevents the two common false promotions: treating scheduler state as actual wake, and treating another repository's duration success as RRULEF's own runtime proof.
