# Experiment collision guard

## Conflict found
`state/frontier-evidence.json` still describes an active-duration experiment whose single changed variable is `same-wake useful-work duration`, with next direct target 600s.

H1's single changed variable is different: `start_of_turn_crash_insurance_prearm_enabled`.

Treating a single H1 turn as simultaneously advancing both experiments would violate one-variable-at-a-time discipline because scheduler mechanism and duration treatment would both differ from the historical control.

## Resolution without changing H1
During H1:
- keep the verified 480s frontier as historical fact;
- keep 600s as the next future duration-treatment target;
- **freeze runtime-frontier promotion** while H1 is active;
- H1 may record actual useful-work duration descriptively, but it cannot promote the active-duration frontier;
- after H1 is accepted/rejected, resume a separately registered duration treatment at 600s with scheduler mechanism held fixed.

This prevents external workwork duration results and H1 scheduler samples from accidentally becoming mixed evidence for RRULEF's runtime frontier.
