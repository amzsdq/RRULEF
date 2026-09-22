# Boundary-elimination test plan

## Purpose
Turn the invariant objective into a falsifiable next experiment without changing the current cutoff.

## Single variable
Whether a safe next useful task is executed in the current wake instead of voluntarily handing off while elapsed time remains materially below 600 sec.

Everything else remains unchanged: same scheduler class, same recurring automation, same 600 sec initial comparator, same measurement definitions.

## Measurement
For each task in the target wake record:
- task_start_time
- task_end_time
- task_duration_sec
- cumulative_active_work_sec
- run_elapsed_sec at decision
- estimated_next_task_sec
- handoff_safety_margin assessment
- continue/handoff decision

At the next actual wake record previous work_end_time -> actual_next_start_time as idle_gap_sec. Do not credit scheduler jitter reduction as causal benefit.

## Success criterion
Evidence favors continuing bounded work when it produces more completed useful work per active+idle wall interval without increasing forced-stop/lost-work cost. One long run is evidence, not final proof.

## Stop condition inside a wake
Handoff only when the 600 sec comparator is reached/exceeded, a concrete runtime-risk signal appears, or the estimated next bounded task would consume the remaining safety margin. Mere completion of an artifact is not a stop condition.

## Decision tuple
- current elapsed: below comparator
- estimated next useful task: 60-180 sec
- safety margin: positive on currently observed evidence
- decision: CONTINUE
