# 600-second frontier evidence check

Fresh README read performed at this wake.

## Objective
Maximize useful-work utilization / minimize actual idle gap. Scheduler jitter remains diagnostic only.

## Current verified evidence
- Canonical state frontier: 480 s.
- Durable frontier evidence: completed predecessor active_work_sec=480, following idle_gap_sec=251, paired utilization=0.65663475, with no evidence in the frontier record that 600 s completed.
- The frontier-600 record explicitly sets target_active_work_sec=600 and action=continue_to_600s_then_handoff. It is admission/decision evidence, not completion evidence.
- Fresh repository search found no explicit completed `active_work_sec=600` evidence.

## Decision
Do not promote the verified frontier above 480 s. Keep 600 s as the next treatment target. No scheduler mechanism, task estimate, safety margin, or comparator is changed in this experiment.

## Handoff
The same recurring continuation was secured first at the earliest safe near-future time available for this run. The next useful action is to obtain an explicitly completed 600-second same-wake useful-work block with termination status recorded; further threshold/sensitivity analysis without that evidence has low information value.
