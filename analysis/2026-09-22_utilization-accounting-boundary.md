# Utilization accounting boundary

This is a measurement clarification, not a new policy.

The objective metric is `active_work / (active_work + actual idle gap)`. To keep it empirically valid:

- `active_work_sec` counts only bounded substantive work intervals.
- Connector waits and durable bookkeeping are not silently promoted to useful work.
- `work_end_time` is the endpoint of the last bounded substantive interval.
- `actual_next_start_time` is observed at the next wake.
- `idle_gap_sec` is computed only after both endpoints exist.
- scheduler jitter remains diagnostic only.

For the 17:49 sample, the valid bounded useful-work evidence is `>=145 sec`. The later mixed interval cannot be allocated between active work and overhead from existing timestamps, so it must remain unclassified rather than being forced into either bucket.

This preserves comparability and prevents false utilization improvements caused by accounting changes.