# Sustained-work break-even — 2026-09-22 22:27 KST

## Objective
README fresh-read. Optimize useful-work utilization / actual idle gap; scheduler jitter remains diagnostic only.

## Fixed mechanism
Near-future anchoring is retained unchanged. The prior experiment closed with 13 direct post-change idle samples averaging 178.15 s and median 176 s, versus prior comparison mean 634 s.

## Single-variable experiment now active
Only change: eliminate measurement-driven premature handoff and execute Baseline A literally toward the nominal 600 s comparator, subject to timeout safety margin.

## Quantitative admission rule for this experiment
This is analysis, not a new permanent policy.

For a cycle with active work A and subsequent idle I, utilization is A/(A+I). Using the retained anchoring experiment's observed mean idle I=178.15 s:
- A=30 s -> 14.41%
- A=60 s -> 25.19%
- A=120 s -> 40.25%
- A=180 s -> 50.26%
- A=300 s -> 62.74%
- A=480 s -> 72.92%
- A=600 s -> 77.11%

Useful implication: with idle exposure near the observed post-change mean, a 180 s active interval is approximately the break-even point for 50% utilization. Repeated 30–60 s measurement-only wakes are therefore structurally incapable of high duty cycle even when wake anchoring works well.

## Decision boundary
At each task boundary record:
- current run elapsed
- estimated next useful task duration
- handoff safety margin

Continue substantive work when the next task fits materially inside the remaining 600 s comparator and no concrete forced-stop risk is observed. Do not hand off solely for cleaner measurement. Handoff remains mandatory before runtime-risk becomes material.

## Evidence linkage
The prior run measured a ~30 s active interval followed by 176 s idle, yielding 14.56% paired utilization. The historical 10-run aggregate had 323 s active / 1470 s idle = 18.02%, and prior analysis already showed that adding only tens of seconds per wake is insufficient. This break-even calculation converts that qualitative conclusion into explicit active-window targets without changing the experimental variable.

## Status
CONTINUE sustained-work experiment. Next useful work should seek an actual same-wake active interval materially above 180 s if runtime safety permits; 600 s remains comparator, not doctrine.
