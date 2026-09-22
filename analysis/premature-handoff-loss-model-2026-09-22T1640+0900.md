# Premature-handoff loss model — 2026-09-22 16:40 KST

## Question
Without assuming scheduler jitter improves, what does reducing avoidable handoff count buy us?

## Observed basis
The existing 10-sample check recorded 323 sec useful work and 1470 sec idle, for 18.0% aggregate utilization. Individual wakes used only 8–72 sec useful work, so most wakes did not exercise the 10-minute budget.

## Mechanism
Every avoidable early handoff creates another exposure to the external wake delay distribution. Keeping useful work inside the current wake does not need scheduler jitter to improve; it simply removes an entire boundary at which idle can occur.

A conservative counterfactual should therefore not subtract an assumed jitter value. It should compare:
- observed: useful task A -> handoff -> idle gap -> useful task B
- same-wake: useful task A -> useful task B, provided B fits safely before runtime risk

The removable quantity is the boundary's actual future idle gap, whatever it turns out to be. This is why premature handoff count is actionable even when jitter itself is exogenous.

## Experimental implication
Do not introduce a new cutoff yet. First execute enough sequential useful tasks in one wake to approach the existing budget and record exact task timestamps. That isolates execution fidelity from scheduler behavior and supplies the evidence needed for the next one-variable experiment.

## Decision tuple after this task
- current elapsed: below current 10-minute initial budget
- estimated next useful task: 60–120 sec
- handoff safety margin: high
- decision: CONTINUE
