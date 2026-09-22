# Sustained-work frontier risk model — 2026-09-23 01:34 KST

Experiment variable remains same-wake useful-work duration only.

## Current evidence
- Latest completed useful-work interval: 270s.
- No timeout or forced stop at 270s.
- Baseline initial cutoff: ~600s, explicitly not a fixed rule.
- Current run started 01:32:25 KST.
- Predecessor pair: 270s active / 147s idle = 64.75% utilization.

## Why extend rather than hand off early
At fixed boundary idle D, utilization U=A/(A+D) rises monotonically with active interval A. With the observed predecessor D=147s:
- A=270s => 64.75%
- A=420s => 74.07%
- A=480s => 76.56%
- A=600s => 80.32%

This does not prove those durations are runtime-safe. It quantifies the reward for measuring the frontier instead of repeatedly stopping near 2–4 minutes.

## Admission guard
Continue only while a next useful task can finish with a handoff reserve. For the current experiment use the existing initial 600s envelope as comparison, not as a promoted policy. At each task boundary record elapsed, estimated task duration, and reserve. Do not alter scheduler behavior during this sample.
