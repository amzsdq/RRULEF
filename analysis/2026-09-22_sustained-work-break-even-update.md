# Sustained-work break-even update

Current experiment changes only same-wake active-work duration; wake lead remains unchanged.

Observed closed pair at 22:47 KST:
- prior active = 180 s
- following idle = 684 s
- utilization = 20.83%

For a fixed 684 s idle cost, active work required for selected utilization levels is:
- 50%: 684 s
- 60%: 1026 s
- 70%: 1596 s
- 75%: 2052 s

These are arithmetic break-even values, not proposed runtime cutoffs. They show why optimizing only the wake lead cannot compensate for very short active windows when actual idle is large.

The next empirical step remains to extend same-wake useful work beyond the directly measured 180 s sample, while watching timeout/forced-stop evidence. Do not simultaneously tighten the wake lead; that would confound attribution.
