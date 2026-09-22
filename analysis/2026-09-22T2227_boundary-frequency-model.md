# Boundary-frequency model — 2026-09-22 22:27 KST

## Purpose
Continue useful work under the same sustained-work experiment. No mechanism change.

A handoff boundary exposes the system to an actual idle interval. If active windows are unnecessarily short, the same amount of useful work pays that idle cost repeatedly.

Using retained post-anchor mean idle = 178.15 s only as a descriptive exposure estimate:

For 600 s of total useful work split into equal active windows:
- 20 windows x 30 s -> 20 idle exposures ~= 3563 s idle; descriptive utilization ~= 14.4%
- 10 windows x 60 s -> ~=1782 s idle; ~=25.2%
- 5 windows x 120 s -> ~=891 s idle; ~=40.2%
- 3.33 windows x 180 s -> ~=594 s idle; ~=50.3%
- 2 windows x 300 s -> ~=356 s idle; ~=62.7%
- 1.25 windows x 480 s -> ~=223 s idle; ~=72.9%
- 1 window x 600 s -> ~=178 s idle; ~=77.1%

These are not forecasts: actual idle is stochastic and scheduler jitter is not being optimized. The calculation isolates the cost of boundary count while holding observed idle exposure constant.

## Operational inference
The next major utilization gain is expected from reducing avoidable handoff-boundary count, not from further sampling of the already-retained anchoring mechanism. Therefore useful tasks that can safely be chained in the same wake should be chained. Measurement should occur at natural task boundaries without manufacturing extra handoffs.

## Current experiment integrity
Changed variable remains exactly one: premature measurement-driven handoff -> sustained useful work. Near-future anchoring, nominal 600 s comparator, and jitter treatment remain unchanged.
