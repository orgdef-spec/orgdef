> **WITHDRAWN 2026-05-23** — This artifact was drafted in orgdef-strategist scope before the data-vs-pattern sharpening landed (see [memos/2026-05-23-1100--thingalog-strategist--orgdef-strategist--handoff-addendum-data-vs-pattern.body.md](../memos/2026-05-23-1100--thingalog-strategist--orgdef-strategist--handoff-addendum-data-vs-pattern.body.md)). The transcript-tagging convention is OAGP-pattern-shape work, not orgdef-format-shape; the proper venue is [oagp-org](https://github.com/scottconfusedgorilla/oagp-org). Substantive analysis (alternatives considered, OQs, naming rationale) is preserved as input material for oagp-strategist's eventual canonical decision; referenced from `oagp-org/memos/2026-05-23-1200--orgdef-strategist--oagp-strategist--inbox-pointers-withdrawn-orgdef-strategist-artifacts.body.md`. **DO NOT cite this file as a ratified orgdef-strategist decision.**

---

# Proposal: Bootstrap-session transcript position-tag convention (`<orgname>-bootstrap-helper`)

**Status:** WITHDRAWN 2026-05-23 (originally Filed 2026-05-23 by orgdef-strategist; withdrawn same day after data-vs-pattern sharpening)
**Author:** orgdef-strategist
**Created:** 2026-05-23
**Target version:** OAGP-canonical convention (transcriptdef-adjacent; orgdef-spec hosts the convention pending transcriptdef-spec seat staffing); canonical CONTRIBUTING.md prose update
**Origin:** Surfaced by thingalog-strategist 2026-05-22 in [memos/2026-05-22-1530--thingalog-strategist--orgdef-strategist--oagp-bootstrap-empirical-validation-complete.body.md §5](../memos/2026-05-22-1530--thingalog-strategist--orgdef-strategist--oagp-bootstrap-empirical-validation-complete.body.md). Empirical occasion: during `/oagp-bootstrap` validation against `dangerstorm-oagp-test` (2026-05-22), ccc-ninja tagged the bootstrap-session transcript as `dangerstorm-oagp-strategist` — a position that does not exist in the new org's roster.

## Summary

Codify the cross-OAGP-family convention that **transcripts of `/oagp-bootstrap` sessions are position-tagged as `<orgname>-bootstrap-helper`** rather than against any of the org-being-bootstrapped's permanent staffed positions. The bootstrap-helper is a transient cross-functional role that exists only during the adoption arc and retires at the Phase 5 hand-off.

This proposal is content-only: a CONTRIBUTING.md prose entry plus a sentence in the canonical `/oagp-bootstrap` skill content. No SCHEMA changes. No new orgdef:Position type; bootstrap-helper is explicitly NOT a position (positions are persistent seats; bootstrap-helper is a session-scoped designation).

## Motivation

`/oagp-bootstrap` sessions create an AI role whose shape shifts within the session arc:

- **Phase 1 (Survey):** read-only orientation — observer-shaped
- **Phase 2 (Propose):** drafting org charter + red lines — strategist-shaped
- **Phase 3 (Ratify):** waiting on PO input — facilitator-shaped
- **Phase 4 (Instantiate):** writing files, staging, committing — implementer-shaped
- **Phase 5 (Hand-off):** producing onboarding summary — strategist-shaped

The role's defining property is that **it does not map to any of the org-being-bootstrapped's permanent positions.** The org doesn't exist yet during Phases 1–3; even after Phase 4 instantiation, the bootstrap-helper has performed work across multiple seat-shapes without occupying any one of them.

When transcript-capture tooling (ccc-ninja, future equivalents) auto-tags the session, the natural default is to grab a familiar position name — `<orgname>-strategist` — which has three failure modes:

1. **Confuses the seat's institutional history.** A transcript tagged `<orgname>-strategist` belongs to that seat's history per the seat-vs-incumbent convention. If the bootstrap-session transcript lands there, future readers of the strategist seat's history will infer institutional acts that the seat did not actually perform (it didn't even exist during much of the session).
2. **Misleads about authority.** "Strategist" implies institutional standing; the bootstrap-helper has none. Its calls are subject to full PO ratification at every phase boundary; it's structurally less authoritative than any staffed seat.
3. **Creates name collision when the strategist seat staffs.** The first real strategist's transcripts then have to share lineage with the bootstrap-helper's session, which is a category confusion (the strategist inherits the seat from PO ratification + onboarding, not from the bootstrap arc).

Canonicalizing the `<orgname>-bootstrap-helper` tag resolves all three.

## Proposed Change

### P1. CONTRIBUTING.md prose entry

Add to `CONTRIBUTING.md` under a new "Bootstrap-session transcript position-tagging" section:

> Transcripts captured during `/oagp-bootstrap` sessions SHOULD be tagged with the position designation `<orgname>-bootstrap-helper` — for example, `dangerstorm-bootstrap-helper`, `thingalog-bootstrap-helper`. The bootstrap-helper is a **session-scoped** designation, NOT an orgdef:Position. It exists for the duration of the bootstrap arc and retires at Phase 5 hand-off.
>
> The bootstrap-helper designation captures the structural reality that:
>
> 1. During Phases 1–3, the org-being-bootstrapped does not yet exist; no permanent position can own the work.
> 2. The AI's role shape shifts within the session (observer → strategist → facilitator → implementer → strategist again); a single permanent position would mis-represent any single phase.
> 3. The bootstrap-helper has no institutional authority — every phase boundary requires explicit PO ratification.
>
> When the same wall-clock session continues past Phase 5 hand-off into ongoing staffed-seat work (e.g., the AI continues as the Implementer of the newly bootstrapped org), subsequent transcript entries SHOULD be re-tagged against the actual staffed position. Hand-off is the role-switch boundary.

### P2. Canonical `/oagp-bootstrap` skill content addition

Add a sentence near the top of the canonical `/oagp-bootstrap` skill body:

> Transcript-capture tooling SHOULD tag this session as `<orgname>-bootstrap-helper` per the canonical OAGP convention. See CONTRIBUTING.md "Bootstrap-session transcript position-tagging."

This is informational to the AI peer running the bootstrap; the actual tagging is performed by the transcript-capture tool (ccc-ninja or equivalent), not by the AI itself.

## Backward Compatibility

Strictly additive. No existing OAGP-canonical convention is contradicted because no canonical convention existed before this proposal — the dangerstorm-oagp-test transcript at `dangerstorm-oagp-strategist/` is a one-off pre-canonization artifact that does NOT require migration (no other transcripts share the directory; the seat doesn't actually exist on the dangerstorm-oagp-test side either, so the tag is structurally orphaned and harmless).

Future bootstrap-session transcripts captured before tooling updates to the new convention can be retroactively re-tagged via simple directory rename. This is the same migration shape as any operational convention change; not a substrate-level concern.

## Conformance Tests

No new conformance fixtures required. The convention governs transcript-capture tooling behavior, not orgdef artifact validity. Conformance verification is:

- Manual: future `/oagp-bootstrap` invocations should produce transcripts at `transcripts/<orgname>-bootstrap-helper/` rather than at `transcripts/<orgname>-strategist/` or similar.
- Tooling-side: transcript-capture tools (ccc-ninja, equivalents) SHOULD recognize `/oagp-bootstrap` invocations and apply the bootstrap-helper tag automatically.

## Alternatives Considered

### Alt 1: `<orgname>-bootstrap-session` (event-flavored)

Rejected. Transcripts in the transcriptdef substrate are tagged by **position** (the seat that produced the reasoning record), not by **event** (the wall-clock interval). Event-flavored naming would violate the seat-vs-incumbent framing and create a category split in how transcripts are addressed across the family.

### Alt 2: `<orgname>-bootstrap-strategist` (role-flavored, strategist-leaning)

Rejected. The bootstrap-helper's work spans strategist-shape AND implementer-shape phases; tagging only "strategist" misleads about Phase 4 implementer work. Also creates name confusion with the actual `<orgname>-strategist` seat that may staff post-bootstrap.

### Alt 3: Sub-divide the session into per-phase position tags

Rejected. Creates multiple transcripts for one wall-clock session, multiplying tracking overhead without clear payoff. The bootstrap arc is more coherent as one transcript than as five sub-transcripts. The phase boundaries are PO-ratification gates, not seat changes.

### Alt 4: Leave the convention to tooling vendors (ccc-ninja, etc.)

Rejected. Tooling vendors solving the problem independently will converge on different names (some will pick `bootstrap-strategist`, some `bootstrap-session`, some `<orgname>-setup`). Family-wide tooling that traverses bootstrapped orgs (analyzers, indexers, future audit tools) would face inconsistent naming. Canonical convention preempts the fragmentation.

### Alt 5: Defer to transcriptdef-spec when that seat staffs

Considered. **Working position: file the convention here now; flag for transcriptdef-coordination when that seat staffs.** Rationale: the empirical need is current (dangerstorm-oagp-test transcript already filed under a wrong tag; future bootstraps will compound the inconsistency without canonical guidance). The convention is content-only (no transcriptdef schema implication); transcriptdef-strategist can re-home or refine it after staffing. The cost of waiting is higher than the cost of forward-coordination.

## Open Questions

### OQ1. Tooling vendor adoption mechanism

How does the canonical convention propagate to ccc-ninja and future transcript-capture tools? Recommended hosting: the canonical `/oagp-bootstrap` skill content carries the convention as instruction; tool vendors that auto-tag based on skill invocation read the canonical content and apply the tag.

**Working position:** the convention lives in canonical `/oagp-bootstrap` skill content (per P2 above) AND in canonical CONTRIBUTING.md prose (per P1). Tool vendors are expected to honor it; non-compliant tools produce inconsistent transcripts that human/AI readers can manually re-tag.

### OQ2. Post-handoff re-tagging mechanism

When the same wall-clock session continues past Phase 5 into staffed-seat work, who performs the re-tag? The AI itself? The tooling? The PO?

**Working position:** the AI peer SHOULD signal the role transition explicitly (e.g., "Bootstrap complete; continuing as `<orgname>-implementer` per PO direction") and request the tooling re-tag. Tool implementations vary; if the tool can't re-tag mid-session, the convention is for the AI to surface the transition in the transcript so post-hoc re-tagging is possible.

### OQ3. Multi-org bootstrap-helper sessions

If a single bootstrap-helper session bootstraps multiple orgs (e.g., a meta-bootstrap creating a parent org + several child orgs), does the tag become `<parent>-bootstrap-helper` or split across multiple?

**Working position:** noted, no action this cycle. The empirical case has not surfaced; defer until an adopter genuinely runs a multi-org bootstrap and surfaces the routing question. The `<orgname>-bootstrap-helper` convention is sufficient for single-org bootstrap (the empirically observed case).

## Cross-spec coordination

- **transcriptdef-spec:** the convention IS transcriptdef-adjacent (it governs how transcripts are position-tagged). transcriptdef-spec is mentioned in the substrate stack but I have not observed a dedicated transcriptdef-strategist seat. **Action:** file this proposal in orgdef-spec/proposals/ as the holding venue; when transcriptdef-strategist seat staffs (or transcriptdef-spec acquires a `/canonical-conventions` location), coordinate re-homing or referenceing this proposal from there. Cross-spec citation rather than re-drafting.
- **ccc-ninja (and equivalent tooling vendors):** informational coordination only. Tooling vendors are not OAGP-spec stakeholders per the equal-citizen-runtime discipline; the canonical convention is the authority and tools honor it as they choose.
- **No catdef / roledef / memodef coordination required.** The convention is content-only; no substrate fields involved.
