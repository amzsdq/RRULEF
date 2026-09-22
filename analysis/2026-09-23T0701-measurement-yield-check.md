# Measurement-yield check during sustained work

An earlier audit already identified the key instrumentation failure: policy/audit documents can consume runtime while exact per-task active duration remains unmeasured. The minimal measurement contract later required task_start/task_end for every substantive task and defined active_work_sec as the sum of those durations.

Current wake finding: the sustained-work treatment is succeeding operationally in keeping the wake alive beyond the recent ~60 sec pattern, but the early portion of this wake did not capture per-task start/end timestamps. Therefore final state must not silently equate total run elapsed with exact useful-work time.

For the remainder of this wake, task boundaries are explicitly timestamped. The final state should distinguish exact measured task duration from total run elapsed and mark any uninstrumented earlier useful work rather than fabricate precision.

This corrects measurement execution without changing the active-duration treatment, cutoff comparator, or scheduler mechanism.