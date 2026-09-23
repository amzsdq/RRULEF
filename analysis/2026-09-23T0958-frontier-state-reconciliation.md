# Active-duration frontier reconciliation — 2026-09-23 09:58 KST

Fresh README and canonical state were read before this reconciliation.

## Finding
The current canonical state says `verified_active_frontier_sec=105` and `next_informative_milestone_sec=180`. That is stale relative to durable run evidence.

Durable evidence `runs/2026-09-23T030454+0900-frontier-600.json` records a valid predecessor pair with `previous_active_work_sec=480`, `idle_gap_sec=251`, `paired_utilization=0.65663475`, and `pair_valid=true`. Its decision checkpoint explicitly says the 480-second predecessor completed without timeout/forced stop and the next treatment is extension toward 600 seconds.

Therefore:
- verified completed clean frontier = at least 480 s, not 105 s;
- 180 s is already dominated as an informative milestone;
- 600 s remains the next treatment target/comparator, but is NOT itself proven completed by this artifact. The filename/commit wording `frontier-600` is admission/target evidence, not proof that 600 s was achieved.

## Experimental integrity
No scheduler mechanism, estimated-next-task rule, or safety-margin treatment is changed here. This is a state/evidence reconciliation, not a new experimental variable.

## Next treatment
Run the same-wake useful-work-duration treatment beyond the verified 480 s frontier, targeting 600 s if bounded work plus handoff safety margin still fits. Record 600 s as verified only after a directly supported completed active block exists. Do not regress to 105/180 s planning and do not infer completion from target labels or commit messages.
