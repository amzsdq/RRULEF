# Duration admission at the 06:55 boundary

Single treatment variable: completed same-wake useful-work duration.

Observed boundary cost for the newly closed pair is 624 sec. Holding that observed boundary only as a sensitivity condition (not as a controlled causal constant):

- 63 sec active -> 9.17% utilization (observed predecessor)
- 120 sec active -> 16.13%
- 300 sec active -> 32.47%
- 480 sec active -> 43.48%
- 600 sec active -> 49.02%
- 720 sec active -> 53.57%

These are sensitivity values, not predictions of scheduler behavior and not evidence that 600 or 720 sec is safe. The experiment still lacks completed-work samples near the initial 600 sec baseline.

Admission consequence: while timeout_or_forced_stop remains false and elapsed useful work is materially below the initial ~600 sec comparator, a bounded next task should normally be admitted when estimated task time plus handoff safety margin fits. Voluntary handoff around ~60 sec should not be treated as a candidate optimum merely because a continuation is already secured.

No scheduler-jitter optimization is introduced.