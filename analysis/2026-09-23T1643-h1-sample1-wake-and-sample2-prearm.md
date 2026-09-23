# H1 sample 1 wake closure / sample 2 pre-arm

Observed wake start: 2026-09-23 16:42:35 KST.

## Sample 1 retrospective close
- predecessor work_end_time: 16:39:40 KST
- intended FINAL_NEXT: 16:42:40 KST
- actual successor start: 16:42:35 KST
- actual idle_gap_sec: 175
- scheduler_jitter_sec: -5
- final WRITE_OK: YES
- final STATE_OK: YES
- final WAKE_OK: YES
- overlap observed: NO

This closes the first H1 physical pair. It is evidence that verified final rearm remained authoritative despite the earlier crash-insurance pre-arm.

## Sample 2 pre-arm
Controller remains frozen at target_runtime=600s, prearm_gap=180s, final_lead=180s. No H1 primary variable changed.

At START=16:42:35, PREARM_NEXT=16:55:35 KST. The same canonical automation was updated with the full recurring VEVENT and then independently re-read. Result: WRITE_OK=YES, STATE_OK=YES, same canonical ID, enabled=true, exact_schedule, RRULE:FREQ=HOURLY, intended DTSTART present.

## External evidence check
Fresh commit search found no workwork commit newer than stored watermark a57ee7a9... at this point. No external commit evidence justified changing H1. tEST commit-head watermark also had no demonstrated new policy-changing evidence in this check. Therefore no external finding is promoted into the active treatment.

## Decision
Continue H1 sample 2. Do not promote the duration frontier during H1. Final authoritative rearm remains required at normal close; the pre-arm is crash insurance only.
