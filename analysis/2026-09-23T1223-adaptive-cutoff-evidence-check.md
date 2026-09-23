# Adaptive-cutoff evidence check — 2026-09-23 12:23 KST

## Question
Do currently valid samples justify changing Baseline A's initial ~600-second comparator or introducing an adaptive cutoff now?

## Evidence actually available
- Exact paired active/idle/utilization samples passing the current evidence gate: n=1 (`480 s active -> 251 s idle`, utilization 65.66%, no forced stop).
- Additional clean idle-only boundaries exist (for example 61 s and 91 s), but their predecessor active duration is not directly bounded in the same evidence artifact.
- A 468 s idle boundary exists with predecessor active duration recorded only approximately (`~90 s`), so it is unsuitable for exact cutoff fitting.
- No directly completed 600-second active-work sample is currently available.

## Hypothesis check
A generic mathematical statement is supported: for a fixed positive idle cost `I`, utilization `A/(A+I)` increases as active useful work `A` increases. This explains why very short runs are structurally expensive when handoff idle is material.

A runtime policy claim is **not** yet supported: the data cannot identify a superior adaptive decision boundary based on `current_elapsed + estimated_next_task + safety_margin`, because there is only one exact active-duration/idle pair and no observed timeout-risk curve across longer durations.

The 480-second sample also completed without forced stop, so there is no direct evidence that the cutoff should be reduced below 480 seconds. Conversely, absence of a completed 600-second sample means the frontier should not be promoted to 600 seconds.

## Decision
- Keep Baseline A comparator unchanged for now.
- Do not introduce a second variable such as wake-lead tuning while active-duration extension remains the experiment variable.
- Do not fit an adaptive cutoff from idle-only or approximate-duration records.
- Highest-information next evidence remains a directly instrumented completed active interval beyond the verified 480-second frontier, with its following end-to-start idle gap captured on the next wake.

This is an evidence decision, not a new policy layer.
