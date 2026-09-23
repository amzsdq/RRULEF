# H1 stale-DTSTART safety check

Historical RRULEF failure: a final handoff selected an absolute due that was already stale by the time the scheduler write occurred.

H1 uses two different time bases deliberately:

## Pre-arm
`PREARM_NEXT = observed START + 600s target + 180s gap = START+780s`.

The pre-arm happens immediately after bootstrap, so its eligibility margin at write time is approximately the full 780s minus bootstrap overhead. STATE_OK must still verify the intended future DTSTART.

## Final rearm
`FINAL_NEXT = actual handoff time + 180s`.

The final due is not copied from the pre-arm and is not computed from an old target clock. It is recomputed from actual close/handoff time immediately before the final scheduler write. Therefore ordinary work-duration variance cannot by itself make FINAL_NEXT stale.

## Required write-time guard
Immediately before each scheduler mutation:
- intended DTSTART must be strictly future-dated relative to the current observed clock;
- after mutation, live state must equal intended DTSTART + RRULE + enabled state.

If tool/control latency is so large that the intended due is no longer future at write time, recomputing a new due would be a scheduler recovery action and must be recorded; silently accepting stale state is forbidden.

## H1 implication
The dual-arm design addresses two different failure modes:
- pre-arm bounds loss when final rearm is never reached;
- close-relative final rearm prevents the historical stale-absolute-due failure on normal close.

These properties are separable and must be measured separately; a successful pre-arm cannot excuse a stale final write.
