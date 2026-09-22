# Boundary closure and cutoff evidence — 2026-09-23 07:41 KST

README fresh-read. Objective remains maximum useful-work utilization / minimum actual idle gap; scheduler jitter is diagnostic only.

## Boundary closure
Predecessor canonical state is fully measured:
- previous active_work_sec: 30 sec
- previous work_end_time: 2026-09-23T07:31:05+09:00
- actual next start: 2026-09-23T07:41:39+09:00
- observed idle_gap_sec: 634 sec
- paired utilization: 30 / (30 + 634) = 4.518%

This is another valid short-run sample. It strengthens the evidence that voluntary handoff after only tens of seconds is dominated by boundary idle cost. It does not identify an optimal long-run cutoff.

## Single-variable experiment
Keep scheduler mechanism unchanged. The only treatment remains same-wake useful-work duration. Comparator remains 600 sec, estimated next task 60 sec, handoff safety margin 120 sec. These remain experimental values, not policy.

## Evidence synthesis
Valid short-run pairs now repeatedly show low utilization under large observed boundary costs. The next information gain is not another 20–60 second wake; it is a fully instrumented sustained-work wake that approaches the current admission frontier without timeout. The measurement guard remains mandatory: active_work_sec is the sum of completed timed substantive intervals, never run_elapsed_sec.

## Decision
Continue substantive same-wake work while current_elapsed + estimated_next_task + handoff_safety_margin remains below the comparator. Do not spend useful-work budget optimizing scheduler jitter. Handoff only near the frontier, after securing recurring continuation first.