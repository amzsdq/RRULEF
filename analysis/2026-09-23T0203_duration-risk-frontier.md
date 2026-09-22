# Duration-risk frontier update

Experiment variable remains same-wake useful-work duration only.

Observed safe points relevant to the current treatment:
- 270s useful work: no timeout/forced stop
- 300s useful work: no timeout/forced stop

No observed failure frontier has yet been reached. Therefore:
1. 300s is a demonstrated-safe lower bound for the useful-work envelope, not an optimum.
2. The README's ~600s Baseline A remains a valid next discriminating target.
3. A 150s handoff is dominated as an experimental choice when useful work remains available and no risk signal exists, because it creates another boundary while leaving most of the baseline budget unused.
4. Do not change scheduler mechanism during this treatment; doing so would confound duration with wake behavior.

Admission fields for next task boundary:
- elapsed_sec_at_decision: continue accumulating toward ~600s
- estimated_next_task_sec: prefer bounded tasks <=150s
- handoff_safety_margin_sec: 120s initial comparison value
- admission condition: start next bounded useful task only if elapsed + estimated_next_task + margin remains inside the current runtime-risk envelope.

The 120s margin is recorded as a comparison value, not promoted to a permanent policy.
