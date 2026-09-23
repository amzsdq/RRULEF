# H1 dual-arm failure envelope

## Question
What failure class does H1 actually improve, and what does it cost, while changing only the start-of-turn pre-arm variable?

## Fixed H1 constants
- target runtime: 600s
- pre-arm gap: 180s
- final lead: 180s
- pre-arm due: START+780s
- final due on clean close: CLOSE+180s
- same canonical recurring RRULE

## Failure envelope
Let `t` be seconds after START when the current invocation ceases before the verified final rearm.

Under H1, the verified pre-arm remains authoritative fallback. Its due is START+780s. The upper-bound continuation delay from a crash at `t` to the pre-armed due is therefore `780-t` seconds, for `0 <= t < final_rearm`.

Examples:
- crash at START+60s -> fallback delay 720s
- crash at START+300s -> fallback delay 480s
- crash at START+480s -> fallback delay 300s
- crash at START+600s immediately before final rearm -> fallback delay 180s

This is not the normal idle gap. It is the bounded recovery delay only when the final rearm path is not completed.

For a clean close at approximately START+600s, final rearm replaces the fallback with CLOSE+180s. Thus the pre-arm should not increase the normal intended handoff gap if the final writer succeeds.

## What H1 does not prove
- It does not prove +3m is globally optimal.
- It does not prove a 600s RRULEF runtime is safe; RRULEF still needs direct completion evidence.
- It does not prove two scheduler writes are worth their control overhead.
- It does not make WRITE_OK or STATE_OK equivalent to the future WAKE_OK.
- It does not inherit workwork's 16m safe lower bound as RRULEF's frontier.

## Measurable H1 value
H1 is valuable only for the failure class `FINAL_REARM_MISSED` / forced termination before final scheduler write. Its benefit is a bounded recovery due that already exists before substantive work. Its cost is one extra scheduler mutation + one live-state verification per turn.

Therefore the experiment should not be judged merely by clean-turn success. Required comparison dimensions are:
1. extra pre-arm control overhead;
2. normal clean-close idle gap after final rearm;
3. whether any pre-arm remains unintentionally authoritative after a clean close;
4. overlap/duplicate evidence;
5. recovery delay on a real or deliberately bounded final-rearm-missed event;
6. long-run useful-work utilization.

## Decision rule
- KEEP/continue H1 if pre-arm measurably bounds a real final-rearm failure with no material overlap and tolerable overhead.
- REJECT H1 if clean turns dominate, final rearm is sufficiently reliable, and the extra mutation/verification reduces utilization without demonstrated recovery value.
- Do not manufacture destructive failure merely to make H1 look useful. A later bounded fault-injection experiment may be registered separately after baseline H1 samples; that would be a different primary variable/experiment.

## External evidence assimilated this wake
workwork produced a new start record for an 18m W2 write/checkpoint-heavy probe at 16:34:54 KST. It pre-armed START+21m and reports WRITE_OK/STATE_OK with a 16m safe lower bound at probe start. Because it is only an in-progress start record, it supports the mechanics of pre-arm but provides no new clean 18m completion evidence yet.
