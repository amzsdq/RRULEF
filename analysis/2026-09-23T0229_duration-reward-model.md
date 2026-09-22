# Active-duration reward model — 02:29 KST

Sole treatment variable remains same-wake useful-work duration. Observed predecessor boundary idle = 1291 s.

If boundary idle repeated unchanged, utilization sensitivity is:
- 210 s active: 13.99% (observed predecessor)
- 300 s active: 18.86%
- 450 s active: 25.84%
- 600 s active: 31.73%
- 900 s active: 41.08%
- 1291 s active: 50.00%

Interpretation: with boundary costs of this magnitude, premature same-wake handoff has a large utilization penalty. These values are sensitivity diagnostics, not fixed targets. The experiment should first establish the safe runtime frontier near the existing ~600 s Baseline-A region before considering a higher adaptive cutoff.

No scheduler-jitter optimization is inferred from this model.