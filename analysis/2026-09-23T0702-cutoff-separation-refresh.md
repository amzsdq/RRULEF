# Cutoff-evidence separation refresh

The newly observed 624 sec idle gap still does not identify the 600 sec active-work comparator as unsafe. Idle is downstream of the previous work endpoint and next actual start; shortening active work in response to a large idle gap would generally increase boundary frequency and can reduce utilization.

Current failure evidence remains the decisive missing variable for shortening the comparator: no timeout_or_forced_stop has been observed in the inspected ~180 sec sustained sample, and recent shorter samples also report false.

Current run admission remains governed by elapsed + estimated next bounded task + handoff margin relative to the nominal comparator. This is application of Baseline A, not a threshold change. Scheduler jitter is not a treatment.