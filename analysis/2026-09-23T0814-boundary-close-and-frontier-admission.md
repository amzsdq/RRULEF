# 08:14 boundary close and frontier admission

- Fresh README read: objective remains maximum useful-work utilization / minimum real idle gap; scheduler jitter is diagnostic only.
- Experiment held fixed: `baseline-a-active-work-duration`; only same-wake useful-work duration is the experimental variable.
- Previous completed active work: 67 sec, ending 08:07:07 +09:00.
- Actual next start: 08:14:28 +09:00.
- Real idle gap: 441 sec.
- Paired utilization: 67 / (67 + 441) = 0.1318897638 = 13.189%.
- This is another valid short-run boundary sample; it is not an optimal-cutoff estimate.
- Short-run evidence is already saturated. The next informative evidence remains a fully instrumented sustained wake toward the 600 sec comparator, with task-by-task timing from task 1.
- Admission inputs held fixed: estimated next task 60 sec; handoff safety margin 120 sec; comparator 600 sec.
- Continuation was secured first as the same enabled recurring automation, near-future wake 08:25 +09:00, before durable-state write.
- Do not spend useful-work budget optimizing scheduler jitter.
