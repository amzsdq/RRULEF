# Observed completed-duration frontier

Repository evidence inspected in this wake contains completed useful-work durations in the short regime (20, 32, ~60, 61, 63, ~90, 105 sec) plus a historical sustained sample of approximately 180 sec with timeout_or_forced_stop=false.

Important distinction:
- Short-pair utilization varies widely because following idle varies widely; these samples cannot identify a causal duration-response curve.
- Runtime-safety evidence is monotonic only in a weak sense: the repository has direct evidence that ~180 sec completed without forced stop, but not yet equivalent direct evidence at 300/480/600 sec.

Therefore the current information frontier is >180 sec. A completed sample around 300 sec is the next useful runtime-safety observation. If it completes without forced stop, later runs can probe farther toward 480/600 while retaining the same single treatment variable.

This is a frontier description, not a permanent cutoff rule.