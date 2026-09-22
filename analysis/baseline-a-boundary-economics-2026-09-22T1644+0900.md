# Baseline A boundary economics — 2026-09-22 16:44 KST

## Question
Given scheduler jitter is exogenous, what controllable mechanism most directly improves useful-work utilization?

## Derivation
Each voluntary handoff creates a new boundary across which the system is exposed to an actual idle gap before useful work resumes. The realized gap may be short or long and its scheduler component is exogenous, but the decision to create the boundary is controllable.

For two safe useful tasks A and B that fit in the same wake:
- premature handoff path: work(A) -> handoff overhead -> actual idle gap -> work(B)
- continue path: work(A) -> work(B) -> later handoff

The continue path removes one handoff overhead and one exposure to an actual idle gap without requiring scheduler jitter to improve. Therefore, while runtime safety remains positive, avoiding premature handoff is structurally favorable to utilization.

## Constraint
This does not justify blindly maximizing wake duration. Timeout/forced-stop loss is a failure cost. The decision boundary must still compare current elapsed, estimated next-task duration, and handoff safety margin.

## Current experiment implication
Do not tune the 10-minute cutoff yet. First obtain literal same-wake samples that actually approach the budget. Otherwise a cutoff comparison is confounded by execution-fidelity failure.

## Decision tuple after task 2
- current elapsed: still materially below initial 10-minute budget
- estimated next task: 60–120 sec
- handoff safety margin: high
- decision: CONTINUE

No experimental variable changed.
