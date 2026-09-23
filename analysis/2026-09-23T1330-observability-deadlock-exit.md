# Observability deadlock exit

## Fresh objective
README was fresh-read this wake. Optimize useful-work utilization and actual work_end -> next actual_start idle gap; scheduler jitter remains diagnostic only.

## Finding
The current loop says the next informative milestone is direct 600s completion, while the current execution surface has repeatedly stored `active_work_sec=null`, `work_end_time=null`, and `run_elapsed_sec=null`. Repeating arithmetic sensitivity or provenance review cannot produce the missing direct 600s observation. That is an observability deadlock, not evidence that 600s is unsafe.

## Useful action
Stop spending future wakes on additional 480-vs-600 arithmetic unless new measured timing evidence arrives. Until a wake has a trustworthy task-duration boundary, use it for substantive repository work and preserve the verified 480s frontier without fabricating timing fields.

## Next experiment
Single changed variable remains same-wake useful-work duration. On the first execution surface that exposes trustworthy elapsed/task-boundary timing, attempt a 600s useful-work block while holding the existing 120s estimated-next-task and 120s handoff safety-margin comparators fixed. Record direct active_work_sec/work_end_time, then close its next-start idle pair on the following wake.

## Admission decision
current_elapsed_sec: unobserved
estimated_next_task_sec: 120
handoff_safety_margin_sec: 120
comparator_sec: 600
decision: do not claim 600s completion; continue useful work and wait for directly observable timing rather than manufacturing a duration from wall/commit/scheduler timestamps.
