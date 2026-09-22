# Run 12 — measurement priority

The highest-value missing observation is no longer another argument that premature handoff is costly. It is a same-wake sample with materially longer useful work and exact task timing.

Next measurement should prioritize, in order:
1. exact actual start timestamp;
2. per-task start/end or duration for substantive tasks;
3. cumulative active work;
4. decision tuple after each task;
5. exact final work_end_time before handoff;
6. next actual start, to close idle_gap_sec.

Avoid spending the work budget producing additional policy prose unless it resolves a concrete decision. Existing evidence is sufficient to keep Baseline A unchanged; new value comes from exercising it.

Decision tuple after this task:
- current elapsed: below comparator
- estimated next task: 60–120 sec
- handoff safety margin: positive
- decision: CONTINUE
