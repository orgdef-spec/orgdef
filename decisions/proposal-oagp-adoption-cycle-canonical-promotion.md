> **WITHDRAWN 2026-05-23** — This decision artifact was drafted in orgdef-strategist scope before the data-vs-pattern sharpening landed (see [memos/2026-05-23-1100--thingalog-strategist--orgdef-strategist--handoff-addendum-data-vs-pattern.body.md](../memos/2026-05-23-1100--thingalog-strategist--orgdef-strategist--handoff-addendum-data-vs-pattern.body.md)). The canonical-promotion call is OAGP-pattern-shape work, not orgdef-format-shape; the proper venue is [oagp-org](https://github.com/scottconfusedgorilla/oagp-org), and the proper decider is oagp-strategist (vacant; interim authority Director). The holding-venue framing this decision invokes was a strategist-seat overreach — the right move would have been to surface "OAGP-spec needs its own home" rather than absorb pattern-shape work into orgdef-spec scope. PO scaffolded oagp-org 2026-05-23 as the proper venue. Substantive analysis (4 OQ resolutions, build directive, design choices, forward-references) is preserved as input material; referenced from `oagp-org/memos/2026-05-23-1200--orgdef-strategist--oagp-strategist--inbox-pointers-withdrawn-orgdef-strategist-artifacts.body.md`. **DO NOT treat this as a ratified decision.** The companion proposal at [proposals/oagp-adoption-cycle-canonical-promotion.md](../proposals/oagp-adoption-cycle-canonical-promotion.md) is also withdrawn.

---

# Proposal Decision: Canonical promotion of the OAGP adoption-cycle pair (`/oagp-bootstrap` + `/oagp-onboard`)

**Disposition:** WITHDRAWN 2026-05-23 (originally drafted as Accept; withdrawn same day after data-vs-pattern sharpening — wrong-venue authorship rather than substantive revision)
**Origin:** [proposals/oagp-adoption-cycle-canonical-promotion.md](../proposals/oagp-adoption-cycle-canonical-promotion.md), originating from a chain of three thingalog-strategist memos:
- [memos/2026-05-22-1430--thingalog-strategist--orgdef-strategist--oagp-adoption-cycle-pattern-promotion.body.md](../memos/2026-05-22-1430--thingalog-strategist--orgdef-strategist--oagp-adoption-cycle-pattern-promotion.body.md) (pattern_promotion_memo establishing the gate)
- [memos/2026-05-22-1530--thingalog-strategist--orgdef-strategist--oagp-bootstrap-empirical-validation-complete.body.md](../memos/2026-05-22-1530--thingalog-strategist--orgdef-strategist--oagp-bootstrap-empirical-validation-complete.body.md) (validation closeout, gate closed)
- [memos/2026-05-23-0900--thingalog-strategist--orgdef-strategist--oagp-canonical-work-handoff.body.md](../memos/2026-05-23-0900--thingalog-strategist--orgdef-strategist--oagp-canonical-work-handoff.body.md) (hand-off authorizing orgdef-strategist takeover)

**Decided:** 2026-05-23 by orgdef-strategist
**Authorization:** Director (Product Owner) explicitly authorized this directional call 2026-05-23 in the strategist-seat-staffing session: hand-off acceptance + "let's do those two first" directive paired this decision with the bootstrap-helper transcript-tagging decision as the strategist's first work-product from the chair.

**Bootstrap caveat:** OAGP-spec-level governance venue does not yet exist. This decision is filed in orgdef-spec as the holding venue, structurally analogous to the parallel transcript-tagging decision filed same session. Re-home or cross-reference from OAGP-spec / oagp.org once those governance venues mature. The decision's substantive content (canonical designation of the pair) persists across any future re-homing; the holding venue is a citation convenience, not a scope claim.

## Disposition

Accepted as drafted; no modifications. The gate condition established in the 2026-05-22-1430 pattern_promotion_memo (empirical validation of the bootstrap side) was closed in the 2026-05-22-1530 validation closeout (`dangerstorm-oagp-test` end-to-end run, 11/11 discipline checks passed, 5 SKILL.md iterations surfaced and merged). The onboard side was independently validated earlier same day. Both sides are empirically grounded; the canonical-promotion call has empirical foundation, not just architectural draft status.

All four Open Questions resolve to their working positions; rationale below.

## Rationale

### Why Accept

Three independent arguments converge on canonical promotion (proposal §Motivation/"Why canonicalize now"):

1. **Adoption-barrier collapse.** The pair reduces OAGP adoption cost from "days of spec-reading + manual orgdef drafting" to "one skill invocation per side + PO ratification cycle." Without canonical designation, this property remains accessible only via Thingalog's repo — limiting reach to adopters who already know to look there.
2. **Reference-implementation drift risk.** The longer the canonical-vs-Thingalog-local distinction goes un-declared, the harder it becomes to draw later. Empirical evidence: the Caliper org (hand-off §3.C) already diverges from Thingalog in three load-bearing conventions (position-naming style, memo routing, proposals/decisions separation) — and the divergences are valid OAGP-shape implementations. Without canonical designation, adopters cannot easily distinguish "Thingalog-local choice" from "OAGP-canonical requirement."
3. **Compositional readiness.** The companion canonical convention (transcript-tagging in [proposal-bootstrap-session-transcript-position-tag.md](proposal-bootstrap-session-transcript-position-tag.md)) and the implicit cross-runtime delivery matrix all reach maturity at the same point. Canonicalizing the pair now gives them a designated parent to attach to.

Each alone would justify designation; together they overdetermine the call.

### Why no modifications

The proposal stays within strategist scope: no SCHEMA changes, no catdef/roledef/memodef coordination required for the substantive call, no library-promotion stretch. Build directive items are well-bounded (decision artifact, README index entry, thingalog-strategist coordination memo, FYI memos to sibling-spec strategists). All five rejected alternatives have defensible refusals stated inline.

The holding-venue framing (orgdef-spec hosts the canonical-promotion decision pending OAGP-spec / oagp.org governance maturation) honestly represents the current bootstrap-state and parallels the transcript-tagging decision's framing. The canonical-by-reference citation approach (P2) preserves operational clarity without over-claiming residence authority over content thingalog-strategist drafted.

### On the hand-off-memo-as-de-facto-input pattern

The substantive canonical-promotion analysis lives across three memos from thingalog-strategist (pattern promotion, validation closeout, hand-off), not in a single proposal artifact filed in orgdef-spec/proposals/. The proposal artifact filed today ([proposals/oagp-adoption-cycle-canonical-promotion.md](../proposals/oagp-adoption-cycle-canonical-promotion.md)) is orgdef-strategist's articulation of the canonical-promotion call for Director ratification; it cites the three memos as foundational input.

This is structurally clean (substantive analysis from sibling strategist arrives as memos; orgdef-strategist evaluates and either drafts the proposal or refuses to promote) but worth flagging as a workflow precedent for future cross-spec-originating canonical promotions. The hand-off memo §6 explicitly disclaims silent inheritance of decision-shaped recommendations made during seat vacancy; this decision artifact ratifies the substance of those recommendations after orgdef-strategist's own evaluation.

## Resolutions to Open Questions

### OQ1 → out of scope this cycle; cross-runtime packaging is canonical-implementor or PO-directed work

**Strategist call: working position accepted.** Cross-runtime delivery packaging is execution work, properly held by the canonical-implementor seat (currently vacant) or by PO-directed coordination. orgdef-strategist's role is canonical designation + open-question surfacing; packaging is a separate scope.

If packaging work needs to start before the canonical-implementor seat staffs, the natural sequence is: PO direction → thingalog-strategist coordination (since canonical-draft content lives there) → packaging-and-distribution under whichever execution authority the PO designates. orgdef-strategist supplies coordination support, not execution.

### OQ2 → defer to PO; provisional recommendation: package iff framing is cross-vendor-explicit

**Strategist call: working position accepted.** PO is deliberating the Claude plugin packaging question per hand-off §3.D. Provisional orgdef-strategist recommendation: packaging is fine **iff** framing makes the cross-vendor-neutrality structural — README + plugin.json description explicitly point at oagp.org canonical hosting (when ready) and list other delivery mechanisms. The plugin is one transport, not the canonical.

Cross-vendor neutrality is OAGP's structural advantage; packaging decisions that obscure this advantage compromise the strategic positioning. orgdef-strategist will weigh in explicitly when PO surfaces the call.

### OQ3 → forward work item; canonical-by-reference framing handles the migration

**Strategist call: working position accepted.** oagp.org canonical hosting timeline is PO-directed; no orgdef-strategist commitment required this cycle. When the venue is ready, the canonical-by-reference framing in P2 specifies the migration mechanism: skill header URLs, README index entry, third-party adopters' citations all citation-update. Substantive canonical status persists.

### OQ4 → FYI memos to sibling-spec strategists; not coordination-required

**Strategist call: working position accepted.** Substrate stack references in the skills are descriptive (the skills reference what already exists in catdef / roledef / orgdef / memodef / transcriptdef); canonicalizing the skill content does not change the substrate. FYI memos are the right shape, not coordination memos requiring sibling-spec response.

Build directive includes drafting these FYI memos (one each to catdef-strategist, roledef-strategist, memodef-strategist) post-decision-ratification.

## Build directive (for orgdef-maintainer when scaffolding work begins)

Execute in this order:

1. **README.md OAGP-canonical-skills section (P3)** — add a brief section to `README.md` listing the canonical adoption-cycle pair with citation links to the canonical-by-reference skill URLs at Thingalog repo. Frame as "OAGP-canonical content; currently hosted at Thingalog pending oagp.org canonical venue."
2. **Coordination memo to thingalog-strategist (P4)** — draft and file at `s:/projects/thingalog/memos/2026-05-23-...--orgdef-strategist--thingalog-strategist--canonical-promotion-ratified.openthing` (+ body_ref) per the canonical inter-position-communication convention. Content: acknowledge canonical designation; request SKILL.md header updates per proposal P2 framing; request Thingalog-internal citation updates ("Thingalog draft" → "OAGP-canonical"); note bootstrap-helper transcript-tagging convention's P2 patch ships under this coordination.
3. **FYI memos to sibling-spec strategists (per OQ4 resolution)** — draft and file:
   - `catdef-spec/.../memos/2026-05-23-...--orgdef-strategist--catdef-strategist--oagp-canonical-skill-promotion-fyi.openthing`
   - `roledef-spec/.../memos/2026-05-23-...--orgdef-strategist--roledef-strategist--oagp-canonical-skill-promotion-fyi.openthing`
   - `memodef-spec/.../memos/2026-05-23-...--orgdef-strategist--memodef-strategist--oagp-canonical-skill-promotion-fyi.openthing`
   - (transcriptdef-spec FYI deferred until that governance venue exists)
4. **No SCHEMA.md changes** — this proposal is content-only at the skill-canonical-designation level; no orgdef SCHEMA additions.
5. **No version bump on orgdef SCHEMA** — same reasoning as item 4. Canonical-orgs library does not gain a new entry from this decision; the pair is a skill, not an orgdef:Organization.
6. **Conformance fixtures (deferred)** — no orgdef-artifact conformance fixture required. Skill-level conformance is operational (adoption attempts succeed; canonical URLs remain valid); no automated test fixture applies at orgdef-spec scope.

## Cross-spec coordination

- **OAGP-spec governance maturation:** this decision is filed at orgdef-spec as holding venue per Bootstrap caveat above. When OAGP-spec governance venue exists, re-home or cross-reference; citation update only.
- **thingalog-strategist:** post-decision coordination memo per build directive item 2. thingalog-strategist's hand-off memo §5 commits to staying available for coordination memos as needed; the canonical-promotion-ratified memo invokes that commitment.
- **catdef-strategist / roledef-strategist / memodef-strategist:** FYI memos per build directive item 3. No substantive response required; the FYIs ensure sibling strategists can field adopter questions referencing the substrate stack with awareness of the canonical designation.
- **transcriptdef-spec:** the parallel transcript-tagging decision applies; its P2 patch (canonical skill content addition) ships as part of this decision's build directive item 2 (the coordination memo to thingalog-strategist). The two decisions ship as a coherent canonical-adoption-arc package.

## Notable design choices

1. **Holding-venue framing made explicit.** OAGP-spec / oagp.org governance does not yet exist; rather than wait for it (deferring the canonical-promotion value indefinitely), file in orgdef-spec with explicit forward-reference. Same shape as the parallel transcript-tagging decision; pair forms a precedent for OAGP-spec-level work during the OAGP-bootstrap interval.
2. **Canonical-by-reference, not canonical-by-residence.** The Thingalog repo hosts the content; this decision designates it canonical. Header framing in the skill files cites this decision as their authority. Decoupling residence from canonicity preserves operational flexibility (Thingalog repo could re-host or re-license; the canonical status persists via this decision's authority).
3. **Build directive coordination memos, not silent assumption.** Per the hand-off memo §6's explicit framing (work done during seat vacancy is captured for inheritance, not assumed adopted), the canonical-promotion's downstream coordination (with thingalog-strategist for skill-header updates, with sibling-spec strategists for FYI) flows through proper memo channels — not informal cross-session assumption. Preserves audit trail.
4. **Companion-decision shipping.** This decision and the transcript-tagging decision ship same session as a coherent package. The transcript-tagging convention's P2 build directive (skill content patch) is shipped under THIS decision's build directive item 2 (coordination memo with thingalog-strategist), preventing the conventions from arriving at the canonical-draft content via independent uncoordinated patches.
5. **Deferring cross-runtime packaging without rejecting it.** OQ1's working position (packaging is canonical-implementor or PO-directed) refuses to commit orgdef-strategist to execution work while preserving the question's open status. Empirical experience may reveal that the packaging IS strategist-scope-adjacent enough to warrant later re-evaluation; the working position holds without foreclosing future revision.

## Items not incorporated

None. The proposal's Open Questions resolve to working positions; no proposal text required modification.

## Workflow validation

- **Strategist scope check:** Canonical designation of skill-level content using existing substrate primitives, with build directive items confined to README updates + coordination memos. No catdef/roledef/memodef substrate changes; no orgdef SCHEMA changes; no library-promotion stretch. Within strategist scope per the orgdef-strategist roledef output_contract.strategist_deliverables (drafted proposal artifacts; design calls; pattern-promotion calls).
- **Cross-spec discipline:** OAGP-spec governance venue absence handled via Bootstrap caveat + holding-venue framing (same pattern as transcript-tagging decision). Sibling-spec coordination handled via FYI memos per OQ4 resolution. transcriptdef-spec absence noted; deferred.
- **Director ratification:** Directional call authorized 2026-05-23 by Director's hand-off acceptance + "let's do those two first" directive. This decision artifact drafted for Director acceptance per standard pattern.
- **Same-session companion-decision check:** This decision and [proposal-bootstrap-session-transcript-position-tag.md](proposal-bootstrap-session-transcript-position-tag.md) ship same session; build directives are coordinated (transcript-tagging P2 patch ships under this decision's build directive item 2). No conflict; no double-counting.

## Forward-reference resolution

- **OAGP-spec / oagp.org governance maturation:** when OAGP-spec governance venue exists, re-home or cross-reference this decision (citation update). When oagp.org canonical hosting exists, migrate the canonical-by-reference URLs in the README index entry and in the skill file headers (additional citation updates). Substantive canonical status persists across both migrations.
- **canonical-implementor seat staffing:** when the orgdef-spec canonical-implementor seat staffs (currently vacant), cross-runtime delivery packaging coordination per OQ1 may shift from "PO-directed" to "canonical-implementor-scoped." Re-evaluate working position at that point.
- **OAGP plugin packaging decision (OQ2):** when PO surfaces the call, orgdef-strategist files a position memo per the provisional recommendation in OQ2 resolution. Cross-vendor framing requirement is load-bearing.
- **Caliper local-convention canonical decisions** (per hand-off §3.C): the Caliper org's three convention divergences (position-naming style, memo routing, proposals/decisions separation) are flagged as next-priority strategist work in the queue. Each divergence is a candidate for proposal artifact in subsequent sessions; the canonical-promotion of the adoption-cycle pair makes those calls more urgent (canonical-content divergences need canonical resolution).
- **Org-state-fork-for-time-travel cross-spec promotion** (per hand-off §3.A): currently Thingalog-internal; candidate for separate canonical-promotion arc following the same shape as this one. Not coupled to this decision; queued for orgdef-strategist's later session.
- **Async-organization positioning** (per hand-off §3.B): orgdef-strategist's position TBD; recommend coordination with PO before drafting (the framing has book-positioning vs spec-positioning dimensions that benefit from PO input before strategist commitment).

## Notes

- This is the second OAGP-canonical decision filed by orgdef-strategist after seat-staffing on 2026-05-23 (paired with the transcript-tagging decision). The pattern (substantive analysis filed as proposal; strategist call ratified via decision; build directive carefully bounded; cross-spec coordination via FYI/coordination memos; holding-venue framing where OAGP-spec governance is immature) is now established as a precedent for OAGP-canonical-scoped work originating from orgdef-strategist's chair during the bootstrap interval.
- The canonical-promotion designation is reversible in principle (if empirical experience surfaces a load-bearing problem, the designation can be revised or rescinded via subsequent decision). In practice, the empirical evidence base (two clean end-to-end validations + the SKILL.md iteration discipline) gives the designation high confidence; revision is unlikely but not foreclosed.
- The hand-off memo's §6 explicit framing ("work done by adjacent seats during a vacancy is captured for inheritance, not assumed adopted") may itself be worth canonizing as a small OAGP-canonical convention. Flag for future-proposal triage; not in scope this cycle.

## References

- Originating proposal: [proposals/oagp-adoption-cycle-canonical-promotion.md](../proposals/oagp-adoption-cycle-canonical-promotion.md)
- Pattern_promotion_memo (gate established): [memos/2026-05-22-1430--thingalog-strategist--orgdef-strategist--oagp-adoption-cycle-pattern-promotion.body.md](../memos/2026-05-22-1430--thingalog-strategist--orgdef-strategist--oagp-adoption-cycle-pattern-promotion.body.md)
- Validation closeout (gate closed): [memos/2026-05-22-1530--thingalog-strategist--orgdef-strategist--oagp-bootstrap-empirical-validation-complete.body.md](../memos/2026-05-22-1530--thingalog-strategist--orgdef-strategist--oagp-bootstrap-empirical-validation-complete.body.md)
- Hand-off memo (orgdef-strategist takeover): [memos/2026-05-23-0900--thingalog-strategist--orgdef-strategist--oagp-canonical-work-handoff.body.md](../memos/2026-05-23-0900--thingalog-strategist--orgdef-strategist--oagp-canonical-work-handoff.body.md)
- Companion decision (paired ship): [proposal-bootstrap-session-transcript-position-tag.md](proposal-bootstrap-session-transcript-position-tag.md)
- Canonical-draft skill content: `s:/projects/thingalog/skills/oagp-bootstrap/SKILL.md` and `s:/projects/thingalog/skills/oagp-onboard/SKILL.md`
- Empirical-validation evidence: `s:/projects/dangerstorm-oagp-test/` (commits `6df43fd` bootstrap + `fa24371` transcript)
- Thingalog-side institutional commitment: `s:/projects/thingalog/memos/2026-05-22-1430--thingalog-strategist--thingalog-strategist--oagp-adoption-cycle-bootstrap-and-onboard-pair.openthing`
- Sibling-precedent decision artifacts (for shape comparison): [proposal-inter-position-communication-convention.md](proposal-inter-position-communication-convention.md), [proposal-canonical-orgs-library.md](proposal-canonical-orgs-library.md)
