# External evidence watermark correction

## Problem
Using only repository commit HEAD as the freshness watermark is insufficient for `amzsdq/tEST` because routine clean-success evidence is append-only in Issue #1 and can advance without a repository commit.

At this wake:
- tEST repository HEAD remained `c52fda...`.
- Issue #1 had advanced through comment id `5790898592` at 16:33:51 KST.
- Therefore a commit-only freshness check would incorrectly classify tEST as unchanged.

## Correction
Track source-specific durable surfaces:
- tEST: repository HEAD **and** latest authoritative Issue #1 comment id/timestamp.
- workwork: repository HEAD is currently sufficient for the observed runtime evidence because its probe records are committed files; add another watermark only if workwork begins using a non-commit durable surface for authoritative runtime results.

This is an observation-layer correction, not a change to H1's scheduler treatment variable.

## Latest tEST relevance
The newest observed tEST record concerns deterministic recovery identity elision and marks its jitter sample SKIP because the invocation preceded stored DTSTART. It does not provide new evidence for H1 pre-arm/final-rearm policy, so no H1 mechanism is changed from that record.
