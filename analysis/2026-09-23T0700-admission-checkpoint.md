# Adaptive admission checkpoint

This is a measurement checkpoint inside the existing active-duration treatment, not a new cutoff policy.

At this checkpoint:
- run elapsed is approximately 244 sec from observed start;
- completed useful-work accounting is slightly lower because deliberate non-work wait is excluded;
- estimated next bounded substantive task: <=60 sec;
- handoff safety margin: 120 sec;
- nominal Baseline-A comparator: ~600 sec;
- timeout/forced-stop observed so far: false.

244 + 60 + 120 = 424 sec, materially inside the nominal 600 sec comparator. Therefore the next bounded task is admitted and handoff is not yet justified. The recurring continuation is already secured, so extending useful work does not require changing the scheduler mechanism.

This checkpoint is retained so later adaptive-cutoff work can compare elapsed time, task estimate, safety margin, and realized outcome.