# Cutoff evidence separation after two clean idle pairs

## Question
Does the new 570 sec causal idle observation justify changing Baseline A's 600 sec cutoff?

## Separation
The cutoff controls how long useful work is continued before handoff. The measured idle gap is downstream of both useful-work endpoint placement and the next actual start. Therefore a large idle gap alone does not identify the cutoff as its cause.

Current clean causal idle observations: 91 sec and 570 sec. Current timeout/forced-stop observations in these clean samples: none reported. There is therefore evidence that idle can be large, but no new evidence that 600 sec is unsafe or that a shorter cutoff would reduce idle. Shortening useful work merely to chase the 570 sec gap could reduce utilization, directly violating the objective.

## Admission rule for this run
Keep performing substantive tasks while elapsed time plus estimated next-task duration plus conservative handoff margin remains below the current 600 sec comparator. Record the decision inputs. This is application of Baseline A, not a new policy.

## Next discriminating evidence
A useful comparison requires repeated directly bounded useful-work endpoints and next actual starts, ideally with materially longer same-wake useful work. Only then can observed idle and timeout-loss be compared against useful-work duration without confounding scheduler jitter.
