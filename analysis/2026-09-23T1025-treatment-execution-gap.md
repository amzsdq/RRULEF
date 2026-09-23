# 10:25 KST — 600s treatment execution gap

## Fresh inputs
- README objective: maximize useful-work utilization / minimize actual idle gap; 600s is an initial comparator, not a fixed rule.
- Canonical state at wake: verified frontier=480s, next informative milestone=600s.
- Recent commits repeatedly admit/check the 600s treatment but do not contain a completed 600s sample.

## Finding
The current bottleneck is not threshold selection. It is treatment execution. The last several wakes have spent their useful work on evidence checks, admission records, and state reconciliation, then handed off before producing the one observation that would advance the experiment: a completed same-wake useful-work block beyond 480s, preferably 600s.

This is a utilization defect because each voluntary short handoff creates another idle boundary while the experiment variable is supposed to be same-wake useful-work duration.

## Single-variable discipline
Changed variable remains only: same-wake useful-work duration.
Keep fixed for the next treatment:
- comparator: 600s
- estimated next task: 120s
- handoff safety margin: 120s
- scheduler mechanism: same recurring automation
- jitter: diagnostic only

## Execution rule for next treatment
Do not spend another wake producing a threshold/admission/evidence-check document unless new contradictory evidence appears. After fresh README/state restore and continuation safety, immediately perform chained safe repository work. A bounded unit completing before 600s is not a handoff trigger; select the next safe useful unit. Stop voluntarily only after reaching the treatment target or when remaining runtime margin cannot safely cover the next bounded unit plus handoff margin.

## Measurement integrity
A 600s PASS requires durable evidence that explicitly supports completed active work at that duration and normal termination. Filenames, target fields, commit messages, scheduler timestamps, connector latency, and whole-turn wall time are not substitutes for active-work evidence.

## Outcome of this wake
This wake identifies and removes a repeated analytical loop but does not claim the 600s treatment PASS. Frontier remains 480s pending an actual completed treatment sample.
