# Baseline A decision record — 2026-09-22 16:44 KST

## Decision
Keep Baseline A unchanged for this experiment window.

## Evidence basis
The available corrected samples demonstrate that premature handoff was a dominant execution-fidelity problem, but they do not yet exercise the 10-minute cutoff closely enough to estimate a better cutoff. Changing the threshold now would change a variable before its baseline was actually tested.

## What would justify change
A later one-variable experiment becomes justified only after literal same-wake samples approach the current budget with usable work remaining and no forced-stop loss, or show runtime-risk/failure cost before that point. At that time, change only the cutoff mechanism/value and compare actual idle-gap/utilization outcomes.

## What is explicitly not optimized
- scheduler jitter itself
- number of artifacts
- policy completeness

Artifacts are useful only insofar as they create evidence or implementation that improves maximum useful-work utilization / minimum actual idle gap.

## Decision tuple after task 5
- current elapsed: below initial budget
- estimated next task: 60–120 sec
- handoff safety margin: positive
- decision: CONTINUE while safe
