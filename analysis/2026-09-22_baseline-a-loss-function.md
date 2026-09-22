# Baseline A loss-function check — 2026-09-22 18:23 KST

Objective: maximize useful-work utilization / minimize actual idle gap. Baseline A remains unchanged at the 600-sec initial comparator.

## Empirical question

What evidence would justify voluntarily ending a wake before the 600-sec comparator?

## Current evidence

- Existing qualified/partially-qualified runs report no timeout_or_forced_stop event.
- The 18:13 sample had a first decision at <=17 sec with estimated next task 60 sec and >=523 sec comparator margin, so CONTINUE was the correct Baseline-A decision.
- Prior short wakes therefore provide evidence about avoidable boundary exposure, not evidence that the runtime becomes unsafe early.

## Loss model for the next decisions

For a candidate next task, compare:

- continue benefit: additional useful task time retained in the current wake and one handoff boundary avoided/delayed;
- continue risk: probability-weighted loss if runtime termination discards unfinished work;
- handoff cost: measured handoff overhead plus the subsequent actual idle gap.

Until a concrete timeout signal or failed-work observation raises continue risk materially, an early voluntary handoff with a large positive safety margin has no empirical advantage under the repository objective.

## Controlled variable

No mechanism changed. The only tested behavior remains Baseline-A execution fidelity: continue safe useful work while elapsed + estimated_next_task + safety margin fits below the current comparator.

## Next measurement

Collect a same-wake sample substantially longer than the historical tens-of-seconds runs, recording decision-point elapsed time, estimated next-task duration, safety margin, and any forced-stop/lost-work event. Do not optimize scheduler jitter.
