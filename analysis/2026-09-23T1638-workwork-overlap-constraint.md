# External overlap constraint applied to H1

Fresh READ_ONLY workwork state provides two relevant facts:

1. strict 16m probe is recorded as `CLEAN_PASS_WAKE_OK`, target reached, elapsed lower bound 996s, WRITE_OK/STATE_OK true, retrospective WAKE_OK true. This supports pre-arm as a functioning continuation primitive in that environment but does not promote RRULEF's runtime frontier.

2. workwork also records overlap probe `OVERLAP-15M-WAKE12M-01` as `CONCURRENT` with 198s observed overlap. This is directly relevant to H1's rollback condition: a pre-armed successor can become concurrent if its due arrives before the active invocation has actually closed.

## H1 implication
H1 pre-arm is START+780s while the nominal runtime target is 600s, leaving a nominal 180s separation. Therefore H1 must treat `active invocation still running near START+780s` as a hard close/recovery hazard, not merely scheduler jitter.

The current experiment constants are unchanged. The external overlap result strengthens the measurement requirement:
- record actual close before pre-arm due;
- never intentionally run through the pre-arm due just to satisfy a duration target;
- if active work approaches the pre-arm due without successful final close/rearm, classify overlap risk explicitly;
- any observed concurrent successor is evidence against H1 unless a future fenced authority design is separately registered and tested.

This does not change H1's primary variable; it sharpens an already-declared rollback condition using new external evidence.
