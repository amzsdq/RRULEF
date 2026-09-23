# Adaptive-cutoff evidence check — corrected 2026-09-23 12:26 KST

## Question
Do currently valid samples justify changing Baseline A's initial ~600-second comparator or introducing an adaptive cutoff now?

## Corrected evidence
Exact paired active/idle/utilization samples passing the current evidence gate: n=4.
- 20 s active -> 319 s idle -> 5.90%
- 105 s active -> 261 s idle -> 28.69%
- 32 s active -> 304 s idle -> 9.52%
- 480 s active -> 251 s idle -> 65.66%

Additional clean idle-only boundaries exist, but they cannot be used for exact active-duration fitting. No directly completed 600-second active-work sample is available.

## Hypothesis check
The corrected evidence materially strengthens the qualitative active-duration hypothesis: bookkeeping-sized runs are dominated by boundary idle, while the longest directly completed block has much higher paired utilization. This is consistent with extending useful work while timeout/forced-stop remains false.

It still does not identify a precise adaptive decision boundary based on `current_elapsed + estimated_next_task + safety_margin`: idle varies across samples, active durations are sparse/non-random, and there is no observed timeout-risk curve beyond the verified 480-second frontier.

The 480-second sample completed without forced stop, so there is no direct evidence to reduce the cutoff below 480 seconds. Absence of a completed 600-second sample means the frontier must not be promoted to 600 seconds.

## Decision
- Keep Baseline A comparator unchanged for now.
- Do not introduce wake-lead tuning while active-duration extension remains the experiment variable.
- Do not fit a precise adaptive cutoff from these four sparse pairs.
- Highest-information next evidence remains a directly instrumented completed active interval beyond 480 seconds, with its following end-to-start idle gap captured on the next wake.

This correction changes the evidence count and confidence in the qualitative duration hypothesis, not the experimental mechanism.