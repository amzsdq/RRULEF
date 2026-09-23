# Next treatment contract — active-duration frontier

This is an execution aid, not a new policy.

## Fixed controls
- experiment variable: same-wake useful-work duration only
- estimated next bounded task: 60 s
- handoff safety margin: 120 s
- nominal comparator: 600 s
- scheduler jitter: diagnostic only
- wake mechanism: unchanged during this treatment

## Verified frontier entering treatment
- highest directly verified active block in consolidated clean-pair evidence: 105 s
- that block: timeout_or_forced_stop=false
- retained post-anchor idle mean: 178.15 s; 180 s active is approximately 50% utilization under that idle assumption

## Treatment
Seek a directly measured active block >105 s; crossing 180 s is the next informative milestone if runtime safety permits. Perform multiple bounded substantive repository tasks in the same wake rather than creating a handoff after each artifact.

At every observable task boundary, retain current elapsed, next-task estimate, and safety margin. If the next bounded task plus margin no longer fits safely, secure the same recurring continuation first and then persist state. If exact task timing is not observable, timing remains null rather than inferred from connector latency.

## Success / failure interpretation
Success: directly observed >105 s same-wake useful work with no forced stop; >180 s is stronger evidence.
Failure: timeout/forced stop or lost incomplete work; record the loss rather than hiding it.
Non-result: another short bookkeeping-only handoff without concrete runtime-risk evidence.
