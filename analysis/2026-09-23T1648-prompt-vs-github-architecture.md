# Prompt vs GitHub control-plane architecture — 2026-09-23

## Research question
What belongs in the ChatGPT Automation prompt, what belongs in GitHub durable state, and what repository structure minimizes bootstrap/control overhead while preserving recovery and correctness?

## Evidence considered
- Current RRULEF prompt and repository layout.
- tEST convergence: progressively removed redundant scheduler reads, metadata fields, and routine ledger rewrites while preserving reconstructability.
- workwork runtime research: compact `state/current.json` as dynamic source of truth plus stable methodology documents.
- Historical R protocol-storage A/B already recorded a judge whose recommendation space explicitly included `HYBRID_STABLE_CORE_WITH_DURABLE_DYNAMIC_STATE`; this is strong prior evidence that the architecture question has already been recognized experimentally.
- Kubernetes object model separates desired `spec` from observed `status`; generation/observed-generation patterns prevent confusing stale observed state with the latest desired state.

## Finding 1 — Current RRULEF prompt is over-embedded
The live RRULEF prompt duplicates stable execution semantics already present in CONTROL_KERNEL.md and repeats dynamic experiment semantics that are also present in state/controller.json. This creates three risks:
1. stale duplicated policy after GitHub changes;
2. larger cold-start parsing/context cost;
3. ambiguity when prompt and repository disagree.

A pointer-only prompt is also too weak for this runtime because failure to read GitHub must not silently remove scheduler identity/safety fences.

## Recommended boundary: HYBRID_STABLE_CORE_WITH_DURABLE_DYNAMIC_STATE

### Embed in automation prompt only
- ROLE / repository / canonical automation identity.
- Source-of-truth rule and one bootstrap entrypoint.
- Minimum fail-safe scheduler invariants that must survive GitHub read failure: same canonical only; no create/replacement; preserve recurring RRULE; enabled/exact schedule; never stale DTSTART.
- Required bootstrap order: read active pointer -> desired spec -> observed status.
- Fail-closed behavior when the entrypoint cannot be read/validated.
- Minimal user-report contract if required.

### Keep in GitHub
Everything expected to evolve or be experimentally tuned:
- objective details and experiment hypothesis;
- runtime target, lead, gap, cutoff, reserve, margin;
- admission algorithm;
- active experiment and primary variable;
- external-source watermarks;
- frontier/promotion/rollback criteria;
- evidence schema and measurements;
- detailed failure taxonomy;
- historical decisions, analyses, trials and raw evidence;
- current/next task and checkpoints.

## Finding 2 — Separate desired and observed state
Do not keep desired treatment and accumulated samples in one controller blob. Split them.

- `spec/experiment.json`: desired current experiment/policy.
- `status/current.json`: observed current/last-run state only.
- `status/observed.json`: generation/hash of spec actually consumed by the last run.

Every spec mutation increments `generation` (or changes an immutable content hash). Status records `observed_generation`. A run must never claim it executed a new spec when its observed_generation is older.

## Finding 3 — Use a single bootstrap pointer
Normal wake should not scan README + kernel + controller + latest evidence. Use one small entrypoint:

`control/active.json`

It names exact current kernel/spec/status/schema paths and their generation/version. Normal wake reads active.json, then only the referenced objects. Broader history is progressive-disclosure recovery/debug input, not routine bootstrap input.

## Recommended clean repository layout
```
README.md                       # human orientation only
control/
  active.json                   # only routine bootstrap pointer
  kernel.md                     # stable executable semantics
  schemas/
spec/
  experiment.json               # desired state, generation N
  runtime-policy.json           # desired runtime tunables if separated
status/
  current.json                  # observed state, observed_generation
  handoff.json                  # compact continuation checkpoint
evidence/
  runs/<run-id>.json            # immutable-ish raw run evidence
  trials/<trial-id>.json        # trial aggregation / acceptance evidence
events/
  YYYY-MM-DD.jsonl              # optional compact append-only material transitions only
derived/
  frontier.json                 # rebuildable materialized view
  utilization.json              # rebuildable statistics
decisions/
  ADR-xxxx.md                   # only promotion/rejection/architecture decisions
archive/                        # superseded bulky material
```

## Write/read rules
1. `control/active.json` is tiny and changes only when routing/version changes.
2. `spec/*` is operator/controller desired state; do not mix measurements into it.
3. `status/*` is controller-owned observed state; it may not redefine desired policy.
4. `evidence/*` is append/new-file evidence; never rewrite history to make a result cleaner.
5. `derived/*` is disposable/rebuildable from evidence and may be compactly updated.
6. `decisions/*` is sparse. Routine reasoning does not get a Markdown file.
7. README is not machine authority.

## Repository decision
A new clean repository is recommended for the architecture experiment rather than restructuring RRULEF in place during H1. RRULEF/tEST/workwork should remain read-only evidence sources for this experiment. Reason: RRULEF already contains large historical analysis/run surfaces and is simultaneously the subject of active relay experiments; changing storage topology there would confound runtime and architecture variables.

The new repository should not become another permanent layer by default. Its lifecycle is laboratory -> validated template -> either (A) promoted as canonical template/runtime repository or (B) archived after the proven structure is migrated into the production repository.

## Experiment plan
Compare three variants with identical task/runtime/scheduler policy:
A. PROMPT_HEAVY — stable + dynamic policy embedded.
B. HYBRID — minimal immutable safety/bootstrap kernel embedded, dynamic desired/observed state in GitHub.
C. POINTER_ONLY — prompt contains identity + active pointer only.

Primary measurements:
- bootstrap GitHub reads/tool calls;
- time to first substantive work when observable;
- prompt size;
- stale-policy incidence after a GitHub-only policy mutation;
- recovery behavior when GitHub read is unavailable/malformed;
- reconstructability after interruption;
- control-plane overhead / useful-work utilization;
- unsafe scheduler mutation or ambiguity count.

Adverse tests are mandatory: GitHub read failure, stale status with newer spec generation, malformed active pointer, policy update between wakes, and interrupted close.

## Prediction / promotion rule
Current leading hypothesis is HYBRID. Promote it only if it preserves the prompt-heavy variant's scheduler/recovery safety while materially reducing duplicated policy/staleness/bootstrap overhead, and it must outperform pointer-only under at least one recovery/fail-safe test. If pointer-only is equally safe and cheaper, prefer pointer-only. If prompt-heavy materially improves recoverability, retain the minimum additional embedded invariants demonstrated necessary by the failure.

## Immediate implication for RRULEF
Do not restructure RRULEF during active H1. After H1 or in a separate architecture laboratory, test the three variants. If HYBRID wins, RRULEF's current long prompt should be reduced to identity + active pointer + irreducible scheduler safety kernel, and `state/controller.json` should be split into desired spec and observed status.