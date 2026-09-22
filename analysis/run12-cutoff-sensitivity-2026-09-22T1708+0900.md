# Run 12 cutoff sensitivity without changing cutoff — 2026-09-22 17:08 KST

## Question
What magnitude of utilization gain is available merely by reducing premature handoff boundaries, without assuming any improvement in scheduler jitter?

## Fixed empirical baseline
Earlier comparable set: active A=323 sec, observed idle I=1470 sec, utilization U=A/(A+I)=18.0156%.

## Boundary-exposure sensitivity
This is a counterfactual sensitivity calculation, not a new policy. Hold useful work A=323 sec fixed and suppose same-wake continuation avoids a fraction f of the observed idle boundary exposure while scheduler behavior itself is unchanged.

- f=10%: effective idle 1323 sec; U=323/(323+1323)=19.62%
- f=25%: effective idle 1102.5 sec; U=323/(323+1102.5)=22.66%
- f=50%: effective idle 735 sec; U=323/(323+735)=30.53%
- f=75%: effective idle 367.5 sec; U=323/(323+367.5)=46.78%

These are not forecasts because individual idle gaps are not proven iid and continuation may also change the amount of useful work. They quantify the size of the known lever only.

## Interpretation
The potential gain from eliminating unnecessary wake boundaries is large enough that execution fidelity should be measured before tuning the 600-sec comparator. Even a 25% reduction in exposure to the already-observed idle pool would move the arithmetic utilization from 18.0% to 22.7% under the deliberately conservative assumption of no extra useful work.

## Decision tuple after this task
- current elapsed: below initial comparator
- estimated next useful task: 90–180 sec
- handoff safety margin: high
- decision: CONTINUE

No cutoff, scheduler, or policy variable changed.
