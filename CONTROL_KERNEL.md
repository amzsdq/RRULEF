# RRULEF Integrated Relay Kernel v1

## Authority
- Writable workspace: `amzsdq/RRULEF` only.
- External evidence sources: `amzsdq/tEST`, `amzsdq/workwork` are READ_ONLY.
- Dynamic experiment state lives in `state/controller.json`; do not hard-code changing frontier/target values into the automation prompt.
- The sole invariant objective is maximum useful-work utilization / minimum real idle gap, subject to continuation correctness and recoverability.

## Stable scheduler invariants
1. Reuse the same canonical automation only.
2. Keep `is_enabled=true`, `timing_mode=exact_schedule`.
3. Every schedule mutation writes a complete recurring VEVENT containing both DTSTART and `RRULE:FREQ=HOURLY`.
4. Never use DTSTART-only one-shot, `dtstart_offset_json`, replacement automation, or new automation for normal continuation.
5. A scheduler update call and a later observed wake are different evidence:
   - WRITE_OK: mutation call returned success.
   - STATE_OK: returned/live state has intended same ID + DTSTART + RRULE + enabled state.
   - WAKE_OK: the intended later invocation actually occurred.
6. Never report continuation success without the evidence level actually observed.
7. Scheduler jitter is diagnostic. Do not sacrifice useful work merely to optimize jitter.

## Wake protocol
1. Record actual START.
2. Fresh-read `README.md`, `state/controller.json`, and current live automation state.
3. Close the previous physical pair when direct timestamps exist:
   `idle_gap_sec = actual_start - previous_work_end_time`.
4. Read tEST/workwork only when:
   - their observed head/evidence is newer than the stored watermark,
   - the active experiment needs external comparison,
   - an anomaly needs precedent.
   Never write to those repositories.
5. Apply exactly one active experimental variable from `state/controller.json`.
6. For H1_DUAL_ARM only:
   - pre-arm crash insurance immediately after bootstrap:
     `PREARM_NEXT = START + target_runtime_sec + prearm_gap_sec`;
   - mutate same recurring automation and verify WRITE_OK/STATE_OK before substantive work.
7. Perform continuous useful work. Finishing one unit is not a reason to stop while a safe useful unit fits the admission rule.
8. No sleeping, padding, no-op work, or policy ceremony merely to consume runtime.
9. At each task boundary record current elapsed, estimated next-task time, close reserve, and safety margin. Admit another unit only if the active controller rule permits it.
10. On normal handoff, finish the smallest in-flight unit and record actual work_end_time.
11. For H1_DUAL_ARM, compute `FINAL_NEXT = actual handoff time + final_lead_sec`, then write the same complete recurring VEVENT and verify live state. This final verified write is authoritative. If it fails, retain the verified pre-arm fallback and classify DEGRADED_CONTINUATION; never pretend final rearm succeeded.
12. Only after final live verification, persist the final scheduler projection and run evidence to RRULEF durable state.
13. On the next invocation, retrospectively classify WAKE_OK and compute actual idle gap/utilization.

## Experimental discipline
- One experiment changes one primary variable.
- Current H1 changes only: add start-of-turn crash-insurance pre-arm.
- Runtime target, final lead, measurement guard, and useful-work definition stay fixed during H1.
- Compare H1 against final-only behavior on:
  continuation success, stale/missed final rearm, actual idle gap, useful-work utilization, scheduler-write overhead, overlap/concurrency, forced stop.
- If pre-arm adds overhead/overlap without measurable recovery value, remove it.
- External evidence may nominate a candidate but cannot promote RRULEF's own runtime frontier without RRULEF direct evidence.

## Failure classification
- STALE_DUE: intended DTSTART is not future-dated at mutation time.
- WRITE_FAIL: scheduler mutation failed.
- STATE_MISMATCH: returned/live DTSTART/RRULE/enabled state differs from intent.
- FINAL_REARM_MISSED: normal final rearm was omitted or not reached.
- WAKE_MISSED: intended next invocation was not observed.
- OVERLAP: concurrent/duplicate invocation evidence.
- DURATION_FAIL: forced stop/close loss plausibly caused by runtime duration.
- NON_DURATION_FAIL: provider/tool/network/GitHub failure independent of duration.

## External-research assimilation
Treat tEST as the stronger source for scheduler semantics/lead-time behavior and workwork as the stronger source for runtime-boundary/pre-arm behavior. When they conflict, do not average. Reproduce the disputed mechanism inside RRULEF with one changed variable and use RRULEF's own direct evidence for promotion.
