# Adaptive-cutoff evidence checkpoint — 2026-09-23 02:43 KST

Treatment remains same-wake useful-work duration only.

## Decision model
The current ~600 s envelope is an experimental timeout-avoidance envelope, not a policy invariant. For each next useful unit, record:
- current elapsed useful-work budget consumed
- estimated next useful unit duration
- handoff safety margin

Admission condition under the current experiment: admit another useful unit only when its expected completion plus safety margin remains inside the experimental envelope. This is being recorded for later comparison against fixed-cutoff Baseline A; it is not yet promoted as the new baseline.

## Current sample
- actual wake start: 02:39:45 KST
- predecessor pair: 240 s active / 440 s idle / 35.29% utilization
- planned sample duration: 360 s useful work
- checkpoint planned at ~240 s
- estimated next useful unit: 120 s
- safety margin: 120 s
- timeout/forced-stop signal so far: none observed in predecessor sample

## Why continue
With 440 s observed boundary cost, increasing active duration has high potential leverage on utilization. The experiment therefore spends this wake on useful analysis/state work rather than scheduler-jitter tuning. The clean frontier is still below the initial ~600 s envelope, so extending the clean sample is higher information value than inventing a new mechanism.
