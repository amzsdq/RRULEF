# Observed cost decomposition

For the predecessor cycle now closed:
- completed useful work: 63 sec
- recorded handoff_overhead_sec: 17 sec
- following real idle gap: 624 sec

Descriptively, recorded handoff overhead is only 2.72% of the following idle gap, while the idle gap is 9.90x the useful-work duration. This does not prove handoff overhead can never matter, but it shows that optimizing a few seconds of handoff bookkeeping is not the highest-value intervention in this sample.

The active experiment therefore remains unchanged: amortize boundary exposure with longer completed same-wake useful work, while recording timeout/forced-stop. No scheduler or handoff mechanism is modified in this experiment.