# Corrected causal idle series — four samples

## Evidence
Corrected causal idle gaps now closed from directly recorded prior substantive endpoints to actual next starts:

- sample 1: 91 sec
- sample 2: 570 sec
- sample 3: 623 sec
- sample 4: 664 sec

Descriptive values only (n=4):
- min: 91 sec
- max: 664 sec
- mean: 487.0 sec
- median: 596.5 sec

## Interpretation
The series is too small and heterogeneous for a cutoff change. Three of four observed gaps are roughly 9.5–11.1 minutes. The latest sample had scheduler jitter of only +32 sec, while the causal idle gap was 664 sec, so scheduler jitter is clearly not interchangeable with actual idle gap.

No corrected sample provides evidence that reducing the 600-sec useful-work comparator reduces the subsequent causal idle gap. With a large exogenous/inter-run gap, shortening useful work without reducing that gap mechanically worsens utilization.

## Decision
- Keep Baseline A comparator at 600 sec.
- Do not optimize scheduler jitter.
- Continue direct per-task active-work instrumentation so the numerator of utilization is measured rather than assumed.
- Do not add a new policy layer from four samples.
