# Sustained-work decision-boundary evidence

Current experiment changes one variable only: same-wake active-work duration is allowed to grow instead of handing off early for measurement density.

## Boundary observations
1. Wake start: elapsed ~0 s; next task = fresh objective/state read (~30-60 s); handoff reserve very large -> CONTINUE.
2. After direct-state validation: elapsed still far below nominal 600 s comparator; next task = derive milestone from observed idle (~60-90 s); no forced-stop evidence in prior 180 s sample -> CONTINUE.
3. After milestone derivation: next task = preserve experiment rationale durably (~30-60 s); reserve remains large -> CONTINUE.
4. Next target boundary for subsequent sustained sample: when elapsed approaches ~300 s, compare estimated next bounded task duration plus handoff reserve against remaining nominal budget. Do not convert 300 s into a fixed cutoff; it is an evidence milestone.

## Adaptive-cutoff implication
The useful decision variable is not `elapsed >= constant` alone. A future adaptive rule should estimate:
remaining_safe_time = inferred_safe_runtime - elapsed - handoff_reserve.
Continue only when estimated_next_task_time fits inside remaining_safe_time. Current evidence is insufficient to set inferred_safe_runtime above the nominal 600 s comparator, so no policy change is made here.
