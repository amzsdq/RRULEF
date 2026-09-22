# Idle-gap data-quality audit — 2026-09-22 18:23 KST

## Finding

The recent runs correctly stopped fabricating exact idle gaps when the preceding work_end_time was only a lower bound. This matters because the optimization target is actual idle_gap_sec, not scheduler jitter.

## Consequence

A run pair is eligible for exact utilization comparison only when:
1. preceding work_end_time is directly observed or tightly bounded at the end of useful work;
2. next actual_start_time is observed;
3. active_work_sec is directly measured or represented explicitly as a bound;
4. timeout/lost-work outcome is recorded.

This is measurement hygiene, not a new execution policy. Baseline A and its 600-sec initial comparator are unchanged.

## Immediate implication

Do not use <=549 sec or similar conservative upper bounds as if they were exact idle gaps. They are useful for safety/accounting but cannot rank nearby cutoff variants. The next useful empirical gain is a clean consecutive run pair with a directly observed work_end_time and next actual start.
