# Controller consistency audit — H1

## Finding
The current H1 controller intentionally freezes:
- target_runtime_sec = 600
- fixed_estimated_next_task_sec = 120
- fixed_close_reserve_sec = 60
- fixed_safety_margin_sec = 120
- admission condition: elapsed + estimated_next_task + close_reserve + safety_margin < target

With those fixed values, a new nominal 120s unit is admissible only while:

`elapsed + 120 + 60 + 120 < 600`

therefore:

`elapsed < 300s`.

This means the admission rule is a **new-work cutoff**, not a requirement to voluntarily close at 300s. A task admitted just before the cutoff may continue to its safe boundary after 300s. However, the controller as written does not itself guarantee 600s of useful work because no new nominal 120s unit may be started at/after 300s.

## Consequence
Do not misclassify an H1 scheduler sample that closes below 600s as a 600s runtime PASS. H1's primary variable is pre-arm enabled, so its scheduler/recovery evidence can still be valid below 600s, but RRULEF frontier promotion from 480s to 600s remains a separate direct-evidence obligation.

## No mutation this wake
Changing the admission constants/rule now would violate H1's one-variable guard. Therefore this audit records the ambiguity without modifying H1. A later registered experiment should resolve whether the target means:
1. desired minimum useful-work duration, with a soft new-work cutoff near target minus close reserve; or
2. hard envelope only, where shorter closes are allowed after the admission cutoff.

The distinction matters because otherwise `target_runtime_sec=600` can be mistaken for a tested 600s workload when the admission controller structurally permits earlier normal close.
