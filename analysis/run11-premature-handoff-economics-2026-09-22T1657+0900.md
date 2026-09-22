# Run 11 — premature handoff economics

## Inputs
Use only the durable 10-run comparable sample:
- useful active work = 323 sec
- observed idle gap = 1470 sec
- runs = 10
- active work/run = 8–72 sec
- forced stops/timeouts = 0

## Derived quantities
- aggregate utilization = 323 / (323 + 1470) = 18.0156%
- mean active work per sampled run = 32.3 sec
- mean observed idle gap per sampled transition = 147.0 sec
- observed idle:active ratio = 1470 / 323 = 4.551:1

This means each second of useful work in that sample was accompanied by about 4.55 sec of observed inter-run idle. The sample does **not** establish that the scheduler would improve if re-anchored; it establishes that exposing the workflow to many handoff boundaries is expensive under the observed environment.

## Counterfactual boundary reduction (diagnostic, not causal claim)
If the same 323 sec of useful work had been packed into fewer same-wake chunks, each eliminated boundary would avoid exposure to one future idle-gap draw. We cannot claim the exact seconds saved because scheduler delay is exogenous and variable. But the direction is robust: fewer unnecessary boundaries cannot add an inter-run gap that never occurs.

The strongest currently justified intervention is therefore execution fidelity: continue useful work within the wake while the current 10-minute comparator and safety margin permit it. Do not tune jitter and do not change cutoff yet.

## Decision tuple after this task
- current elapsed: still well below 10-minute initial budget
- estimated next task: 120–240 sec
- handoff safety margin: high
- decision: CONTINUE
