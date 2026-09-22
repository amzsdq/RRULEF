# Duration-efficiency checkpoint — 2026-09-23 01:27 KST

## Purpose
Continue the sole treatment variable: same-wake useful-work duration. Do not optimize scheduler jitter and do not introduce another mechanism.

## Current causal evidence
The latest clean pair is 151s useful work followed by 188s real idle, utilization 44.54%. The immediately preceding clean pair was 34s useful work followed by 442s idle, utilization 7.14%.

This is not a controlled proof that duration alone caused the utilization difference because idle is exogenous and varied substantially. It is, however, sufficient to reject bookkeeping-sized early termination as an efficient default under the observed boundary costs.

## Useful-work leverage under observed idle
For a fixed idle cost I, paired utilization is W/(W+I). With I=188s:
- W=151s -> 44.54%
- W=240s -> 56.07%
- W=300s -> 61.48%
- W=480s -> 71.86%
- W=600s -> 76.14%

These are sensitivity calculations only. They do not establish a new cutoff.

## Admission decision 2
Current run remains well below the initial 10-minute baseline envelope. Estimated next useful task is ~150s; retained handoff safety margin is 120s. Continue useful work. The recurring continuation is already secured as failure protection. Stop only when the next task plus safety margin makes timeout risk material; otherwise early handoff would directly increase boundary frequency and expected idle exposure.
