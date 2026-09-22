# Safe-envelope inference — 2026-09-23 01:29 KST

## Question
How far can same-wake useful-work duration be extended before timeout risk dominates the utilization benefit?

## Evidence available
Recent canonical state history contains completed runs with active_work_sec values including 167, 138, 34, and 151 seconds, all recorded without timeout/forced stop. Earlier sensitivity analysis already showed that at a 468-second observed idle cost, increasing active duration from 90 to 600 seconds monotonically raises paired utilization from 16.13% to 56.18% if idle is held constant for leverage analysis.

The latest clean boundary has 188 seconds idle. At that boundary cost, 300 seconds useful work would imply 61.48% paired utilization and 600 seconds 76.14%, absent timeout loss.

## Inference
The data do not yet identify the runtime failure frontier because recent executions have generally handed off far before the initial 600-second budget. Therefore reducing the cutoff below 600 seconds is unsupported by timeout evidence. Conversely, raising it beyond 600 seconds is also unsupported because the current sample has not safely exercised that region.

## Experiment implication
Keep the current single variable: useful-work duration. The highest-value next evidence is a genuinely sustained run approaching the existing ~600-second baseline envelope while retaining a 120-second handoff safety margin and recording task-by-task duration. Do not add scheduler changes. Do not promote 240–300 seconds to a cutoff; it is only an intermediate treatment band.
