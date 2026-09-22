# Run 12 — utilization target table

Using the indexed 10-run aggregate only as a descriptive starting point:
- active = 323 sec
- idle = 1470 sec
- utilization = 323 / (323 + 1470) = 18.02%

Holding the already-observed 1470 sec idle fixed purely for arithmetic, the total active time required to reach utilization targets is:
- 25% utilization: active = 490 sec, +167 sec versus observed
- 33.3% utilization: active ≈ 735 sec, +412 sec
- 40% utilization: active = 980 sec, +657 sec
- 50% utilization: active = 1470 sec, +1147 sec

This table is not a forecast because longer same-wake work should also change the number of handoff boundaries and therefore future idle exposure. Its value is scale: adding only tens of seconds per wake is unlikely to close the utilization deficit quickly. The experiment needs materially longer useful-work intervals, which is consistent with literal Baseline A execution.

Decision tuple after this task:
- current elapsed: below comparator
- estimated next task: 90–180 sec
- handoff safety margin: positive
- decision: CONTINUE
