> **WITHDRAWN 2026-05-23** — This decision artifact was drafted in orgdef-strategist scope before the data-vs-pattern sharpening landed (see [memos/2026-05-23-1100--thingalog-strategist--orgdef-strategist--handoff-addendum-data-vs-pattern.body.md](../memos/2026-05-23-1100--thingalog-strategist--orgdef-strategist--handoff-addendum-data-vs-pattern.body.md)). The transcript-tagging convention is OAGP-pattern-shape work, not orgdef-format-shape; the proper venue is [oagp-org](https://github.com/scottconfusedgorilla/oagp-org), and the proper decider is oagp-strategist (vacant; interim authority Director). Substantive strategist-call content (the `<orgname>-bootstrap-helper` recommendation, OQ resolutions, build directive) is preserved as input material; referenced from `oagp-org/memos/2026-05-23-1200--orgdef-strategist--oagp-strategist--inbox-pointers-withdrawn-orgdef-strategist-artifacts.body.md`. **DO NOT treat this as a ratified decision.** The companion proposal at [proposals/bootstrap-session-transcript-position-tag.md](../proposals/bootstrap-session-transcript-position-tag.md) is also withdrawn.

---

# Proposal Decision: Bootstrap-session transcript position-tag convention (`<orgname>-bootstrap-helper`)

**Disposition:** WITHDRAWN 2026-05-23 (originally drafted as Accept; withdrawn same day after data-vs-pattern sharpening — wrong-venue authorship rather than substantive revision)
**Origin:** [proposals/bootstrap-session-transcript-position-tag.md](../proposals/bootstrap-session-transcript-position-tag.md)
**Decided:** 2026-05-23 by orgdef-strategist
**Authorization:** Director (Product Owner) explicitly authorized this directional call 2026-05-23 in the strategist-seat-staffing session, in response to thingalog-strategist's hand-off memo (see [memos/2026-05-23-0900--thingalog-strategist--orgdef-strategist--oagp-canonical-work-handoff.body.md](../memos/2026-05-23-0900--thingalog-strategist--orgdef-strategist--oagp-canonical-work-handoff.body.md) §3 and §4). Director directive: "let's do those two first," authorizing this decision and the parallel canonical-promotion decision in the same session.

**Bootstrap caveat:** This decision is filed in orgdef-spec because the transcriptdef-spec governance venue does not yet exist. Re-home or cross-reference from transcriptdef-spec once that seat staffs. The convention is content-only (no schema implication for either spec); re-homing is a citation update, not substantive re-litigation.

## Disposition

Accepted as drafted; no modifications. The proposal's argument that the bootstrap-helper is **structurally not a position** (and therefore should not borrow a position name) is load-bearing. The `<orgname>-bootstrap-helper` tag honestly captures the transient cross-functional nature without misleading future readers about the seat's institutional history.

All three Open Questions resolve to their working positions; rationale below.

## Rationale

### Why Accept

The empirical case from `dangerstorm-oagp-test` (transcript tagged `dangerstorm-oagp-strategist` against a position that doesn't exist in the new org's roster) is the canonical motivating instance. Without a canonical tag, transcript-capture tooling will default to whatever name pattern its heuristics produce — different tools converge differently, the family-wide transcript namespace fragments by accumulation, and seat-history queries return false positives forever.

The three failure modes the proposal articulates (confused seat history, misleading authority signal, name collision at staffing) are independent of each other; each alone would justify canonization, and together they overdetermine the call.

The proposal's preferred name (`bootstrap-helper`) is honest about three properties that competitor names obscure:

1. **Role-flavored, not event-flavored** — `bootstrap-helper` reads as a thing that did work, which matches what transcripts capture. `bootstrap-session` reads as an interval, which would invite event-keyed transcript organization across the family (a structural divergence from the existing position-keyed convention).
2. **`helper`, not `strategist`** — the bootstrap-helper has no institutional authority; every phase boundary is PO-gated. "Helper" matches the actual authority shape; "strategist" would inflate it.
3. **Implicit transience** — `helper` reads as task-shaped rather than seat-shaped. Future readers reading `transcripts/<orgname>-bootstrap-helper/` immediately understand they are not reading a staffed seat's history.

### Why no modifications

The proposal stays within scope (no SCHEMA changes; CONTRIBUTING.md prose + one sentence in canonical skill content; no new orgdef:Position type). All five rejected alternatives have defensible refusals stated inline; no proposal text required revision to address them.

The deferral to transcriptdef-spec (Alt 5 / OQ in cross-spec coordination) is the right discipline: file the convention here as the current holding venue, with explicit forward-reference to transcriptdef-spec once that seat exists. The cost of waiting until transcriptdef-spec staffs is higher than the cost of forward-coordination — every additional un-canonized bootstrap accumulates inconsistent transcript tags that future cleanup must address.

## Resolutions to Open Questions

### OQ1 → tooling vendors honor canonical-skill-and-CONTRIBUTING.md guidance; non-compliant tools produce inconsistent transcripts subject to manual re-tag

**Strategist call: working position accepted.** Author's framing is correct. The OAGP-canonical convention does not (and cannot) compel third-party tooling behavior — equal-citizen-runtime discipline applies to tooling vendors equivalently to AI runtime vendors. The canonical convention is the authority; non-compliant tools produce non-canonical outputs that can be re-tagged post-hoc.

This is the same structural shape as canonical orgdef SCHEMA versus validator implementations: the spec is the authority, validators implement it, non-compliant validators produce non-canonical outputs.

### OQ2 → AI peer signals role-transition in transcript; tooling re-tags if possible, otherwise manual post-hoc re-tag

**Strategist call: working position accepted.** Author's framing is correct. The role-transition (bootstrap-helper → staffed seat) is a wall-clock-session-internal event that requires AI legibility (so the AI knows which discipline applies to which work) and transcript legibility (so future readers can locate the transition).

The convention: AI peer says something like "Bootstrap complete; continuing as `<orgname>-implementer` per PO direction." Transcript-capture tooling MAY re-tag from that signal; if it cannot, the post-hoc re-tag is a substrate operation (directory rename) that human or AI peer can perform.

### OQ3 → defer; no empirical case yet

**Strategist call: noted, no action this cycle.** Multi-org bootstrap (one helper, multiple orgs in one session) has not been empirically observed. The single-org bootstrap case (which IS empirically observed) is sufficiently covered by `<orgname>-bootstrap-helper`. Filing a routing convention for the hypothetical multi-org case would be premature canonization; flag for future-proposal triage if/when surfaced.

## Build directive (for orgdef-maintainer when scaffolding work begins)

Execute in this order:

1. **CONTRIBUTING.md update (P1)** — add the new "Bootstrap-session transcript position-tagging" section per the proposal's P1 prose, verbatim.
2. **Canonical `/oagp-bootstrap` skill content patch (P2)** — coordinate with thingalog-strategist (current holder of the canonical-draft skill content at `s:/projects/thingalog/skills/oagp-bootstrap/SKILL.md`) to add the one-sentence reference per P2, verbatim. This patch ships as part of the canonical-promotion arc (see [decisions/proposal-oagp-adoption-cycle-canonical-promotion.md](proposal-oagp-adoption-cycle-canonical-promotion.md)).
3. **No SCHEMA.md changes** — this proposal is content-only; no orgdef SCHEMA additions.
4. **No version bump on orgdef SCHEMA** — same reasoning as item 3.
5. **Conformance fixtures (deferred)** — the convention governs tooling behavior, not artifact validity; no conformance fixture required. A future canonical-orgs entry exercising the convention would serve as a reference example; queue when an adopter genuinely needs it.

## Cross-spec coordination

- **transcriptdef-spec:** the convention is transcriptdef-adjacent (it governs how transcripts are position-tagged). transcriptdef-spec is referenced in the substrate stack (catdef → roledef → orgdef → memodef → transcriptdef) but the strategist seat does not yet appear to be staffed in a dedicated spec org. **Action:** filed here as holding venue per Bootstrap caveat above; coordinate re-homing or referencing from transcriptdef-spec once that seat staffs. Cross-spec citation expected, not substantive re-litigation.
- **canonical-promotion arc:** this decision composes with [decisions/proposal-oagp-adoption-cycle-canonical-promotion.md](proposal-oagp-adoption-cycle-canonical-promotion.md). The P2 patch (canonical skill content) ships as part of that arc's build directive.
- **No catdef / roledef / memodef coordination required.** Content-only convention; no substrate fields involved.

## Notable design choices

1. **Position-vs-non-position distinction made explicit.** The proposal AND the decision explicitly call out that bootstrap-helper is NOT an orgdef:Position. This is load-bearing: positions are persistent seats with institutional standing; bootstrap-helper is a session-scoped designation with no standing. The naming convention BORROWS the position-tag-shape (`<orgname>-<designation>`) for transcript-organization purposes only; it does not create a position. Future readers must not infer the bootstrap-helper into orgdef:Position lists or seat-history queries.
2. **`helper` over `strategist` is the load-bearing word choice.** Alt 2 (`bootstrap-strategist`) is the most plausible competitor and would have worked structurally; rejecting it is a deliberate authority-signal call. The bootstrap-helper has zero institutional authority by construction; the name should match.
3. **Single transcript per session, not per-phase sub-transcripts.** The phase boundaries are PO-ratification gates, not seat changes. Operationally, one transcript per session matches how the work coheres for the AI peer and for future readers tracing the arc.
4. **Forward-coordination posture for transcriptdef-spec.** Rather than wait for transcriptdef-strategist to staff before canonizing, file here with explicit forward-reference. Empirical need is current; waiting is more expensive than re-homing later.

## Items not incorporated

None. The proposal's Open Questions resolve to working positions; no proposal text required modification.

## Workflow validation

- **Strategist scope check:** This is a SHOULD-pattern addition to CONTRIBUTING.md prose + one sentence in canonical skill content. Both fall within strategist scope per the orgdef-strategist roledef output_contract.strategist_deliverables. No catdef substrate changes; no orgdef SCHEMA changes. Cross-spec coordination (transcriptdef-spec) is forward-flagged per Bootstrap caveat.
- **Cross-spec discipline:** transcriptdef-spec governance venue does not yet exist; filing here with explicit forward-reference is the correct discipline (compare: orgdef-strategist initially held same-head with catdef/roledef/memodef during bootstrap; transcript-tagging temporarily holds same-venue with orgdef pending transcriptdef-spec governance maturation).
- **Director ratification:** Directional call authorized 2026-05-23 by Director "let's do those two first" directive. This decision artifact drafted for Director acceptance per standard pattern.

## Forward-reference resolution

- **transcriptdef-spec governance maturation:** once transcriptdef-spec acquires its own strategist seat + proposals/decisions venues, this decision SHOULD be cross-referenced or re-homed (citation update, not re-litigation). The current orgdef-spec placement is a holding venue per Bootstrap caveat.
- **Canonical-promotion arc:** the P2 build directive item (canonical skill content patch) ships as part of [decisions/proposal-oagp-adoption-cycle-canonical-promotion.md](proposal-oagp-adoption-cycle-canonical-promotion.md) build directive.
- **Tooling-vendor adoption:** as ccc-ninja (and future transcript-capture tooling) update to honor the convention, any prior-tagged bootstrap-session transcripts SHOULD be re-tagged retroactively. The dangerstorm-oagp-test transcript at `transcripts/dangerstorm-oagp-strategist/` is the known pre-canonization case; thingalog-strategist coordination recommended for the re-tag (one directory rename).

## Notes

- This is the first OAGP-canonical convention filed by orgdef-strategist after seat-staffing on 2026-05-23. The pattern (small focused convention, content-only, no schema implication, forward-coordinated with adjacent spec) is the strategist seat's natural shape; future canonical conventions in this scope should aim for similar economy.
- The `bootstrap-helper` convention pairs naturally with the canonical-promotion of `/oagp-bootstrap` itself; the two decisions ship in the same session as a coherent canonical-adoption-arc package.

## References

- Originating proposal: [proposals/bootstrap-session-transcript-position-tag.md](../proposals/bootstrap-session-transcript-position-tag.md)
- Surfacing memo (the OAGP-spec-level question that triggered this proposal): [memos/2026-05-22-1530--thingalog-strategist--orgdef-strategist--oagp-bootstrap-empirical-validation-complete.body.md §5](../memos/2026-05-22-1530--thingalog-strategist--orgdef-strategist--oagp-bootstrap-empirical-validation-complete.body.md)
- Hand-off memo authorizing the orgdef-strategist seat's response: [memos/2026-05-23-0900--thingalog-strategist--orgdef-strategist--oagp-canonical-work-handoff.body.md](../memos/2026-05-23-0900--thingalog-strategist--orgdef-strategist--oagp-canonical-work-handoff.body.md)
- Empirical motivating instance: dangerstorm-oagp-test transcript at `s:/projects/dangerstorm-oagp-test/transcripts/dangerstorm-oagp-strategist/2026-05-22-1342--...` (the wrong-tag case; subject to retroactive re-tag per Forward-reference resolution)
- Canonical-promotion arc (parallel decision filed same session): [decisions/proposal-oagp-adoption-cycle-canonical-promotion.md](proposal-oagp-adoption-cycle-canonical-promotion.md)
- Canonical-draft skill content (where the P2 patch applies): `s:/projects/thingalog/skills/oagp-bootstrap/SKILL.md`
