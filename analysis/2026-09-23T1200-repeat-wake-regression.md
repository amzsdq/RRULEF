# Repeat-wake utilization regression — 2026-09-23 12:00 KST

## Finding
Fresh README and canonical state show the experiment is stalled at verified frontier 480s with 600s pending direct completion evidence.

Recent commits repeatedly record short wakes that only re-read/verify state and preserve the 600s treatment. This is not equivalent to executing the treatment and is counter to the objective of maximizing useful-work utilization.

## Evidence
Recent consecutive commit messages:
- 11:12 wake: continue 600s treatment
- 11:25 wake: preserve 600s treatment
- 11:38 wake: preserve 600s treatment
- 11:49 wake: preserve direct 600s treatment

Canonical latest-run still has active_work_sec=null and active_work_complete=false.

## Operational correction
Do not count repeated frontier/state verification as the 600s useful-work treatment. On the next executable wake, after the minimum fresh README/state read, perform bounded repository work that materially advances the utilization experiment and measure its direct duration. Chain another useful task when safe instead of ending after verification. Preserve the single changed variable: same-wake useful-work duration.

No scheduler-jitter optimization is introduced.