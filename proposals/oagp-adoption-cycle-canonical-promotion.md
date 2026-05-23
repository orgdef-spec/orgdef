> **WITHDRAWN 2026-05-23** — This artifact was drafted in orgdef-strategist scope before the data-vs-pattern sharpening landed (see [memos/2026-05-23-1100--thingalog-strategist--orgdef-strategist--handoff-addendum-data-vs-pattern.body.md](../memos/2026-05-23-1100--thingalog-strategist--orgdef-strategist--handoff-addendum-data-vs-pattern.body.md)). The canonical-promotion call is OAGP-pattern-shape work, not orgdef-format-shape; the proper venue is [oagp-org](https://github.com/scottconfusedgorilla/oagp-org). The "holding venue" framing this proposal invokes (`orgdef-spec hosts pending OAGP-spec governance maturation`) **correctly identified the missing piece (OAGP-spec needs a home) but chose the wrong response (absorb pattern-shape work into orgdef-spec scope rather than surface that OAGP-spec needed to exist)**. PO scaffolded oagp-org 2026-05-23 as the proper venue. Substantive analysis (alternatives considered, OQs, build directive structure) is preserved as input material; referenced from `oagp-org/memos/2026-05-23-1200--orgdef-strategist--oagp-strategist--inbox-pointers-withdrawn-orgdef-strategist-artifacts.body.md`. **DO NOT cite this file as a ratified orgdef-strategist decision.**

---

# Proposal: Canonical promotion of the OAGP adoption-cycle pair (`/oagp-bootstrap` + `/oagp-onboard`)

**Status:** WITHDRAWN 2026-05-23 (originally Filed 2026-05-23 by orgdef-strategist; withdrawn same day after data-vs-pattern sharpening)
**Author:** orgdef-strategist
**Created:** 2026-05-23
**Target version:** OAGP-canonical designation (skill-level, not spec-schema); orgdef-spec serves as holding venue pending OAGP-spec governance maturation
**Origin:** Pattern_promotion_memo from thingalog-strategist 2026-05-22 ([memos/2026-05-22-1430--thingalog-strategist--orgdef-strategist--oagp-adoption-cycle-pattern-promotion.body.md](../memos/2026-05-22-1430--thingalog-strategist--orgdef-strategist--oagp-adoption-cycle-pattern-promotion.body.md)) followed by empirical-validation closeout 2026-05-22 ([memos/2026-05-22-1530--thingalog-strategist--orgdef-strategist--oagp-bootstrap-empirical-validation-complete.body.md](../memos/2026-05-22-1530--thingalog-strategist--orgdef-strategist--oagp-bootstrap-empirical-validation-complete.body.md)) closing the empirical-validation gate. Hand-off confirmed 2026-05-23 ([memos/2026-05-23-0900--thingalog-strategist--orgdef-strategist--oagp-canonical-work-handoff.body.md](../memos/2026-05-23-0900--thingalog-strategist--orgdef-strategist--oagp-canonical-work-handoff.body.md)).

## Summary

Designate the adoption-cycle pair — `/oagp-bootstrap` (founding-side skill) + `/oagp-onboard-<orgname>` (joining-side skill) — as **OAGP-canonical content**. Cite the canonical-draft skill content currently hosted at the Thingalog repo as canonical-by-reference pending OAGP-spec governance venue and future oagp.org canonical hosting. Pair this designation with the bootstrap-helper transcript-tagging convention (parallel decision filed same session).

This proposal is **content-only at the OAGP-canonical-skill level**. No orgdef SCHEMA changes; no catdef / roledef / memodef coordination required for the substantive call (the pair already uses existing substrate primitives). The build directive items concern (a) the canonical designation statement, (b) coordination with thingalog-strategist for skill-header updates citing this decision, and (c) forward-reference resolution for the eventual oagp.org canonical hosting transition.

## Motivation

### The empirical case

`/oagp-bootstrap` and `/oagp-onboard` have been independently validated end-to-end across two real adoption arcs:

| Side | When | How | Result |
|---|---|---|---|
| **Onboard** | 2026-05-22 ~13:00 EDT | `/oagp-onboard-thingalog` C4C shortcut, fresh-AI test | 27 internal steps, 1 turn to summarize, full discipline preserved (no auto-staffing) |
| **Bootstrap** | 2026-05-22 ~14:00–15:00 EDT | `/oagp-bootstrap` against `dangerstorm-oagp-test` fork | All 5 phases executed cleanly, 5 SKILL.md iterations surfaced and merged, discipline preserved (preserve-don't-overwrite respected, bounded-authority on commit, no auto-staffing) |

The validation closeout's discipline-check table (validation memo §2.B) enumerates 11 discipline properties all of which held. The bootstrap test additionally surfaced a pre-canonization OAGP-precursor in the test project (DangerStorm's `memory/` folder) which the bootstrap-helper correctly **respected as a complementary pattern** rather than subsuming — empirical evidence that the preserve-don't-overwrite discipline is load-bearing under real-project conditions.

### Why canonicalize now

Three independent reasons converge on "now":

1. **Adoption-barrier collapse.** The pair reduces OAGP adoption cost from "days of spec-reading + manual orgdef drafting" to "one skill invocation per side + PO ratification cycle." This is the load-bearing property for cross-vendor cross-runtime adoption; deferring canonical designation defers the property's accessibility.
2. **Reference-implementation drift risk.** Until OAGP-canonical designation lands, the pair lives as Thingalog-internal artifacts. Each additional adopter encountering the skills via Thingalog's repo absorbs Thingalog-specific conventions as if they were canonical (because there is no canonical to disambiguate from). The longer this persists, the harder it becomes to draw the line later between "OAGP-canonical" and "Thingalog-local."
3. **Compositional readiness.** The companion canonical conventions (transcript-tagging in [decisions/proposal-bootstrap-session-transcript-position-tag.md](../decisions/proposal-bootstrap-session-transcript-position-tag.md); the implicit cross-runtime delivery matrix; the bootstrap-helper authority discipline) are all reaching maturity at the same point. Canonicalizing the pair now gives them a designated parent to attach to; deferring forces them to float ungrounded.

### Why orgdef-spec is the holding venue

OAGP-spec-level governance venue does not yet exist. There is no `oagp-spec/` repo with a designated maintainer; no `oagp.org` canonical hosting yet; no OAGP-strategist seat distinct from the spec-org strategists. During this bootstrap interval, OAGP-canonical decisions structurally fall to whichever spec-org strategist is appropriately positioned — for the adoption-cycle pair, that is orgdef-strategist (the pair operates on orgdef artifacts as primary substrate; orgdef-strategist holds delegated authority for orgdef-shaped concerns).

This is the same holding-venue pattern as the parallel transcript-tagging convention: file here, with explicit forward-reference to OAGP-spec / oagp.org once those governance venues mature. Re-homing later is a citation update, not substantive re-litigation.

## Proposed Change

### P1. Designate the pair OAGP-canonical (decision-artifact statement)

The companion decision artifact ([decisions/proposal-oagp-adoption-cycle-canonical-promotion.md](../decisions/proposal-oagp-adoption-cycle-canonical-promotion.md)) records the canonical designation. The decision is the authority; this proposal carries the substantive analysis behind it.

### P2. Canonical-content citation

Until oagp.org canonical hosting lands, the canonical-by-reference skill content lives at:

- **`/oagp-bootstrap` canonical-draft:** `https://github.com/scottconfusedgorilla/thingalog/blob/master/skills/oagp-bootstrap/SKILL.md`
- **`/oagp-onboard` canonical-draft:** `https://github.com/scottconfusedgorilla/thingalog/blob/master/skills/oagp-onboard/SKILL.md`

These URLs are **canonical-by-reference**, not canonical-by-residence. The Thingalog repo currently hosts the content as a matter of operational expediency (thingalog-strategist drafted them; the empirical validation happened there). After OAGP-canonical designation, the content's authority derives from this designation, not from the URL.

**Header framing for the canonical-draft files:** thingalog-strategist (per build directive coordination) updates the SKILL.md headers to cite this decision as their canonical authority — e.g., a frontmatter or top-of-file note: *"This skill is OAGP-canonical per [orgdef-spec decision 2026-05-23](https://github.com/orgdef-spec/orgdef/blob/main/decisions/proposal-oagp-adoption-cycle-canonical-promotion.md). Hosted here pending oagp.org canonical venue."*

### P3. Index entry in orgdef-spec README

Add a brief OAGP-canonical-skills section to the orgdef-spec README listing the canonical adoption-cycle pair with citation links. This is the discoverability surface for the canonical designation until oagp.org canonical content lands.

### P4. Build directive coordination with thingalog-strategist

After this decision is ratified, file a coordination memo to thingalog-strategist:

- Acknowledge canonical designation
- Request SKILL.md header updates per P2 framing
- Request that any Thingalog-internal memos referencing the pair update their citations from "Thingalog draft" to "OAGP-canonical"
- Note: the bootstrap-helper transcript-tagging convention from the parallel decision applies; the canonical `/oagp-bootstrap` skill content should incorporate the one-sentence reference per that decision's P2

## Backward Compatibility

Strictly additive. No existing OAGP-canonical designation contradicts this one (none existed prior). No existing orgdef:Organization artifact becomes invalid; no validator behavior changes; no SCHEMA changes.

Existing adoption attempts that found and used the Thingalog-hosted skills become retroactively canonical-compliant the moment this designation lands (they were using the canonical-by-reference content all along; designation just makes that explicit).

## Conformance Tests

No new conformance fixtures required at the orgdef-spec level. The canonical-promotion concerns skill-level canonicity, not orgdef artifact validity.

Conformance verification is operational:

- **Adoption attempts using the canonical-by-reference skills SHOULD succeed cleanly** (per the two empirical instances; future bootstraps and onboards extend the evidence base).
- **The canonical-content URLs SHOULD remain valid** until oagp.org hosting transitions; thingalog-strategist coordinates URL stability as part of the post-decision build directive.

## Alternatives Considered

### Alt 1: Defer canonical designation until oagp.org canonical hosting exists

Rejected. The adoption-barrier-collapse value, reference-implementation-drift risk, and compositional-readiness arguments above all advise against deferral. The cost of waiting for oagp.org (which has no current ETA) compounds with every additional un-canonized adoption. Designating now and citation-updating later is cheaper than the alternative.

### Alt 2: Promote the pair to orgdef-spec's `proposed-orgs/` or `orgs/` library

Rejected. The pair is a skill, not an orgdef:Organization artifact. orgdef-spec's `orgs/` library is for canonical organizational charters, not for tooling/adoption skills. Categorical mismatch; would force a stretch of the library's scope.

### Alt 3: File the canonical designation as a top-level OAGP-spec artifact

Rejected (currently impractical). No OAGP-spec governance venue exists; filing there would mean either creating that venue first (substantial scope expansion outside this turn's authorization) or filing at a non-existent URL. orgdef-spec as holding venue is the next-best option until OAGP-spec governance matures.

### Alt 4: Designate the pair OAGP-canonical without specifying hosting

Rejected as too thin. Without a citation surface, "OAGP-canonical" becomes a designation without referent — adopters cannot find the canonical content without word-of-mouth. The canonical-by-reference framing (P2) preserves operational clarity while honestly representing the current bootstrap-state.

### Alt 5: Package and host the canonical content directly in orgdef-spec/skills/

Considered. Would put the canonical content under orgdef-spec's direct authority and remove the canonical-by-reference indirection. **Working position: rejected this cycle; revisit if Thingalog repo hosting becomes problematic.** Rationale: copying the content here would create a second canonical surface (orgdef-spec/skills/ AND the Thingalog repo), each at risk of drifting from the other. The canonical-by-reference approach is cleaner during the holding-venue interval; copy-into-orgdef-spec/ is an option if hosting expediency changes.

## Open Questions

### OQ1. Cross-runtime delivery package coordination

The pair's cross-runtime delivery matrix (per validation closeout §6 and hand-off §3.E) lists Claude Code skill, C4C shortcut, claude.ai project, ChatGPT custom GPT, Gemini Gem, Perplexity Space, and generic first-message-primer. Some are packaged; most are not. **Who packages?**

**Working position:** out of scope this cycle. Cross-runtime delivery packaging is execution work, properly held by the canonical-implementor seat (currently vacant in orgdef-spec) or by PO-directed coordination with thingalog-strategist or external collaborators. orgdef-strategist's role is to designate canonical status and surface the open packaging question; the packaging itself is a separate scope.

### OQ2. OAGP plugin packaging for Claude marketplace

Per hand-off memo §3.D: the question of whether to package the pair as a Claude plugin for Anthropic's marketplace is in PO deliberation. The packaging is mechanically straightforward; the strategic tension is positioning (cross-vendor neutrality vs. Anthropic-ecosystem distribution).

**Working position:** orgdef-strategist will weigh in when PO surfaces the call. Recommendation (provisional): packaging is fine **iff** the framing is explicit that the plugin is a Claude-Code-specific delivery of an open cross-vendor spec, with README/manifest pointing at oagp.org canonical hosting (when ready) and explicitly listing other delivery mechanisms. The plugin is one transport, not the canonical.

### OQ3. oagp.org canonical hosting timeline

Eventually the canonical-by-reference framing should resolve to oagp.org canonical hosting (e.g., `oagp.org/skills/oagp-bootstrap` and `oagp.org/skills/oagp-onboard`, optionally with runnable endpoints at `oagp.org/bootstrap?repo=<url>` per validation closeout §6.5). **When does this happen?**

**Working position:** noted as forward work item; PO and orgdef-strategist coordinate timing. The canonical-by-reference framing in P2 specifies the migration is a citation update (skill header URLs, README index entry, any third-party adopters' citations); the substantive canonical status persists across the migration.

### OQ4. Cross-spec coordination for the substrate stack references

The skills reference catdef → roledef → orgdef → memodef → transcriptdef. Canonicalizing the skills implicitly canonicalizes the substrate-stack framing as part of OAGP's public-facing surface. **Do the sibling-spec strategists (catdef, roledef, memodef) need to coordinate-acknowledge?**

**Working position:** informational FYI memos to sibling-spec strategists, not coordination-required. The substrate stack is descriptive (the skills reference what already exists); canonicalizing the skill content does not change the substrate. FYI memos are the right shape: "the adoption-cycle pair has been OAGP-canonically designated; you may receive adopter questions referring to the substrate stack; here is the canonical content for reference."

## Cross-spec coordination

- **OAGP-spec governance maturation:** the canonical designation filed here is a holding-venue artifact pending OAGP-spec / oagp.org maturation. Forward-reference: re-home or cross-reference from OAGP-spec when that venue exists; citation update only.
- **thingalog-strategist:** post-decision coordination memo for SKILL.md header updates + Thingalog-internal citation updates per P4.
- **Sibling-spec strategists (catdef, roledef, memodef):** FYI memos per OQ4 working position. No substantive coordination required.
- **transcriptdef-spec:** the parallel transcript-tagging decision applies; the canonical `/oagp-bootstrap` skill content's P2 patch (one-sentence reference to the bootstrap-helper convention) ships under that decision's build directive.
