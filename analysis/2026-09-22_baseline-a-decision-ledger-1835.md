# Baseline A decision ledger — 2026-09-22 18:35 KST

Objective: maximize useful-work utilization / minimize actual idle gap. Baseline A 600-sec comparator unchanged.

## Fresh evidence
- README fresh-read at wake start.
- Previous durable run: actual start 18:23:20 KST; no exact final useful-work endpoint; no forced stop.
- Current actual start: 18:35:39 KST.
- Scheduled wake was 18:34:00 KST, so scheduler_jitter_sec = +99. This is diagnostic only and is not an optimization target.

## Decision ledger
1. elapsed ~= 0 sec. Task: fresh README + prior durable-state read. Expected task <= 90 sec. Comparator margin >= 510 sec. Decision: CONTINUE.
2. elapsed < 180 sec. Task: close the previous scheduled-vs-actual pair and persist a clean decision ledger. Expected task <= 120 sec. Comparator margin > 300 sec. No timeout/forced-stop signal. Decision: CONTINUE.
3. Next useful task: preserve a directly observed current work_end_time so the next wake can compute an exact idle_gap_sec. Expected <= 120 sec. Handoff safety margin remains positive. Decision: perform then HANDOFF; do not alter cutoff in this experiment.

## Result
This wake closes one diagnostic pair exactly: scheduled 18:34:00 -> actual 18:35:39 = +99 sec jitter. It still does not close an exact useful-work idle-gap pair because the prior run did not publish an exact work_end_time. Therefore no idle-gap point estimate is fabricated.

The useful controlled action in this wake is to publish an explicit current work_end_time after substantive work, enabling the next wake to compute an exact previous-work-end -> actual-start idle gap. No new policy and no cutoff change.