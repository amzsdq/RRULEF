# Boundary-amortization evidence summary

Using only directly recorded pairs already present in repository analysis:

- 20 active / 319 idle -> 5.90%
- 32 active / 304 idle -> 9.52%
- 105 active / 261 idle -> 28.69%
- 61 active / 594 idle -> 9.31%
- 63 active / 624 idle -> 9.17%

Pooled descriptively (not as a causal estimator): 281 sec active and 2102 sec following idle, or 11.79% aggregate paired utilization across these five boundaries.

The pooled number is not suitable for selecting a cutoff because boundary idle changed between samples. It is useful for one operational conclusion: the observed system is paying substantially more boundary idle than completed useful work in this short-duration regime. Another short voluntary handoff has low information value and predictably adds another boundary exposure.

The current experiment should therefore spend its next available runtime on extending completed useful work toward the first >=180 sec frontier sample while preserving timeout/forced-stop measurement. No scheduler variable is changed.