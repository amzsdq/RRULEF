# Cutoff sensitivity analysis — 2026-09-23 00:00 KST

This is useful work under the existing active-duration treatment; it does not change the treatment variable.

Using the newly closed clean idle cost of 353 seconds as a scenario input only (not as a claim that future idle is fixed), active work required for target paired utilization is:
- 25% utilization: 117.7 sec
- 33.3% utilization: 176.5 sec
- 40% utilization: 235.3 sec
- 50% utilization: 353 sec
- 60% utilization: 529.5 sec

Implication: the planned >=180-second block is a meaningful next treatment point because, at this idle-cost scenario, it crosses roughly one-third utilization while staying materially below the 10-minute baseline budget. A 180-second successful sample does not by itself justify a cutoff change; timeout outcome and the following clean causal pair are required.