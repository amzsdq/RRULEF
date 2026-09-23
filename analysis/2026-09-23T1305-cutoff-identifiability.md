# Cutoff identifiability check — 2026-09-23 13:05 KST

Objective remains maximum useful-work utilization / minimum actual idle gap. No scheduler-jitter optimization and no cutoff change in this check.

## Evidence used
Exact paired rows currently accepted by the measurement contract:

| active sec | following idle sec | utilization |
|---:|---:|---:|
| 20 | 319 | 5.90% |
| 105 | 261 | 28.69% |
| 32 | 304 | 9.52% |
| 480 | 251 | 65.66% |

Approximate ~90/468/16.13% remains qualitative-only and is excluded from exact fitting.

## What is identifiable now
The exact rows strongly support the coarse direction that, when a wake boundary costs hundreds of idle seconds, tiny useful-work blocks are inefficient. The 480-second completed block has the best observed utilization among the exact rows and had no forced-stop evidence.

## What is not identifiable now
A precise adaptive cutoff is not identified. Active duration and following idle cost both vary, samples are sparse and non-random, and there is no directly completed 600-second treatment. Fitting a numeric optimum from these rows would confound active-duration effect with boundary-idle variation.

## Operational decision
Do not lower the verified frontier below 480 seconds. Do not promote 600 seconds without direct completion evidence. Keep one changed variable: same-wake useful-work duration. The next informative experiment remains a directly instrumented 600-second useful-work completion followed by its actual next-start boundary.

## Admission rule for that experiment
Record task-boundary durations directly. At each decision point retain current elapsed, estimated next-task duration, and handoff safety margin. Only continue if the next task fits the runtime-risk envelope; otherwise secure continuation first and persist the completed boundary. Targets, commit timestamps, connector latency, and whole-turn wall time are not completion evidence.
