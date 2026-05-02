# Proposal: Add `ai-pair-built-saas` to the canonical-orgs library

**Status:** Filed (2026-05-01 by orgdef-strategist; awaiting maintainer review and decision artifact)
**Author:** orgdef-strategist (provisional bot identity pending governance ratification)
**Created:** 2026-05-01
**Target version:** New canonical-template artifact `proposed-orgs/ai-pair-built-saas.openthing` v1.0.0; canonical-orgs library expansion (the second canonical, after `oagp-family-open-standard`)
**Origin:** thingalog-strategist memo 2026-05-01-0208 (canonical-derivation experience for Thingalog) — the first non-spec OAGP-derived org. Memo surfaced a recurring shape (one human Product Owner + AI Product Strategist + AI Implementer + auxiliary vacant positions) that did not fit the existing `oagp-family-open-standard` canonical and offered Thingalog v1.1.0+ as a worked example for a new canonical. Director authorized filing 2026-05-01.

## Summary

Add a second canonical-template to the canonical-orgs library: `ai-pair-built-saas`, capturing the recurrent shape of SaaS products built by a small core (one human Product Owner + AI Product Strategist + AI Implementer) with auxiliary vacant positions for specialist work (Mobile Developer, Security Tester, Revenue/Marketing Officer) staffed as the project matures. Thingalog v1.1.0+ is the empirical anchor (the orgdef-derivation that surfaced the shape).

The companion canonical-template artifact (`proposed-orgs/ai-pair-built-saas.openthing`) is to be drafted by thingalog-strategist as a follow-on submission per the originating-org-strategist-drafts-the-canonical discipline; this proposal makes the strategist call (scope, naming, slot structure) and clears the canonical for promotion when the artifact lands.

## Motivation

### The shape is recurrent and well-grounded

Thingalog's orgdef artifact captures a coherent SaaS-org shape that is unlikely to be unique to Thingalog:

- **Triad core**: human Product Owner (final authority, product direction, ratifier) + AI Product Strategist (artifact-producing: memos, design docs, decision records) + AI Implementer (code-producing: commits, deploys, audit-logged admin operations). Seat separation is structural; matters more than headcount.
- **Auxiliary vacant positions**: Mobile Developer, Security Tester, Revenue/Marketing Officer — defined-but-unstaffed seats that come online as the project matures (or remain vacant if the project's scope doesn't require them). Pattern serves projects that don't have these capabilities at v0/v1 but need to declare structurally where the work *would* land if/when staffed.
- **AI-Implementer with audit trail**: The substantive innovation that makes "one human + one AI ships SaaS" credible rather than fanciful. Implementer holds delegated implementation authority gated by an audit-logged admin tier (e.g., platform_admin) for cross-domain operations; pushes only with explicit go-ahead; every admin-tier action audit-logged. Generalizes across the portfolio.
- **Bidirectional coordinates_with on Strategist↔Implementer**: Recognizes that strategy and implementation collaborate symmetrically (Strategist may consult Implementer on architectural feasibility before drafting; Implementer may surface architectural concerns mid-build for Strategist consideration). Distinct from a hierarchical reports_to.

These properties are observed in Thingalog and credibly imminent in adjacent Scott-portfolio products (PXMemo, DangerStorm, Atomic Maple, Conversii, ToolVault — share design DNA, separate codebases). They also generalize beyond the Scott portfolio: any small-team AI-pair-built SaaS that takes bounded AI authority seriously and wants to declare its structure machine-readably will face the same shape.

### `oagp-family-open-standard` doesn't fit

The existing canonical-template is spec-shaped: mission about "defining X in an open machine-readable way that bootstraps any AI worker into Y," recommended_patterns about senior strategist role separation and recursive self-describing v1 milestone, recommended_roles oriented around standards work (senior-open-standards-strategist, maintainer, canonical-implementor). Product-shaped orgs need a different canonical: mission about a product or service the org delivers; recommended_patterns about Product Owner + AI seats triad and audit-trail discipline; recommended_roles oriented around product, implementation, and revenue.

Forcing product-shaped orgs to derive from `oagp-family-open-standard` would cause derivation friction comparable to (or greater than) the friction memodef and roledef hit deriving from v1.0.0 — but for a different reason: spec-shaped slots simply don't fit product-shaped contexts. A second canonical solves this.

### Library expansion is the foreshadowed downstream work

The canonical-orgs-library decision (2026-04-26) explicitly foreshadowed downstream library expansion: "Derive [other OAGP-family member specs] as they bootstrap further" — and beyond that, the Director-surfaced framing in CREATE_NEW_ORG.md that "organizations that produce bespoke orgdefs MAY be invited to submit them as canonical templates." Thingalog produced the first bespoke orgdef under that framework; the proposal-and-promote pattern starts here.

## Proposed Change

### Strategist calls in this proposal

#### C1. Naming: `ai-pair-built-saas`

Two names were offered by thingalog-strategist's memo: `oagp-substrate-consumer-saas` (more precise) and `ai-pair-built-saas` (broader). **Strategist call: `ai-pair-built-saas`.**

Rationale:
- The truly-generalizing pattern is the AI-pair structure (Owner + Strategist + Implementer triad; AI-Implementer with audit trail). Substrate-consumer concerns (catdef-as-substrate, schema-as-data, MCP-mediated access) are a SEPARATE dimension that some AI-pair-built SaaS will adopt and others won't.
- Naming the canonical after the broader pattern preserves applicability to non-OAGP-substrate adopters who still want the AI-pair shape.
- Substrate-consumer concerns can layer atop `ai-pair-built-saas` as either (a) a separate canonical `oagp-substrate-consumer` that adopters compose via `metadata.derived_from` chains, or (b) recommended_patterns.general entries inside `ai-pair-built-saas` for adopters who happen to consume OAGP substrates. Decision deferred per OQ2 below.
- Counter-argument: `oagp-substrate-consumer-saas` is more precise, doesn't overpromise generality. The right way to handle that risk is to keep the name broad and let actual adoption demonstrate the generality — if no non-OAGP-substrate AI-pair SaaS adopts, the name was aspirational; that's recoverable. If we name it narrowly and a broader audience surfaces, renaming is harder than narrowing scope at the recommended_patterns level.

#### C2. Scope: AI-pair structural concerns only; substrate-consumer concerns are separable

The canonical's slot structure should capture:
- **Triad core** (positions: product-owner, product-strategist, implementer)
- **Auxiliary vacant positions** (positions: mobile-developer, security-tester, revenue-officer — slot-shaped, deriver decides which to keep)
- **Standard relationships**: reports_to chains to product-owner; bidirectional coordinates_with on strategist↔implementer; validates_for from security-tester to implementer (when staffed)
- **Recommended patterns**: AI-Implementer-with-audit-trail; Product Owner + AI Strategist + AI Implementer triad; Seat-separation discipline
- **Recommended roles**: human-director (MUST), product-strategist roledef (MUST when staffed; gap — see roledef-spec coordination memo), senior-project-oriented-software-engineer (MUST; canonical roledef exists), blackhat-tester (SHOULD; canonical roledef exists), mobile-developer (MAY; gap), revenue-marketing-officer (MAY; gap)

The canonical does NOT include:
- Substrate-specific values (e.g., schema-as-data, no-vendor-lock-in to a specific runtime, substrate-version-stamping discipline) — these belong in a separate substrate-consumer canonical or in adopter-side derivation
- Multi-tenant-specific values (e.g., tenant-isolation-as-primitive) — multi-tenancy is a deployment shape; AI-pair SaaS may be single-tenant SaaS, on-prem-deployable, etc. These belong in adopter-side derivation
- Domain-specific red lines (e.g., content moderation requirements) — these are adopter-domain concerns

The deriver's job is to take `ai-pair-built-saas` v1.0.0 and ADD their substrate / multi-tenancy / domain concerns via REPLACE-mission/vision and ADDITIVE-ONLY values/red_lines/recommended_patterns. Thingalog v1.1.0+ is the worked example demonstrating exactly this layering.

#### C3. Worked example: Thingalog v1.1.0+

Thingalog's orgdef at version 1.1.0 (the post-Director-restructure state captured in the 2026-05-01-0208 derivation memo) is the empirical anchor. The canonical-template is a generalization of Thingalog: positions, relationships, and AI-pair recommended_patterns are lifted; substrate-consumer + multi-tenant + domain-specific values/red_lines/recommended_patterns are dropped (left for derivers to add).

The canonical-template artifact shape (specific slot-vs-fixed content) is to be drafted by thingalog-strategist as the originating-org's strategist, per the lift-from-source-strategist discipline that paralleled how orgdef-strategist authored `oagp-family-open-standard` from orgdef-spec. The companion artifact lands at `proposed-orgs/ai-pair-built-saas.openthing` and is strategist-cleared for promotion to `canonical-orgs/` upon (a) this proposal's acceptance + (b) the canonical-orgs library directory existing on disk (currently pending the canonical-orgs-library SCHEMA v0.3 work per that decision's build directive).

#### C4. Slot convention: `[SLOT: ...]` strings at v1.0.0

Per the canonical-orgs-library decision's M1, the structured `__slot__` object convention is the long-term goal but the interim `[SLOT: ...]` string convention is acceptable for new canonical-templates pending the migration patch. `ai-pair-built-saas.openthing` v1.0.0 uses `[SLOT: ...]` strings; migration to `__slot__` objects happens at the same patch cycle as `oagp-family-open-standard`'s migration.

### Build directive (companion artifact authoring)

To be executed by **thingalog-strategist** (originating-org strategist, per the lift-from-source-strategist discipline):

1. **Author `proposed-orgs/ai-pair-built-saas.openthing`** in the orgdef-spec repo (PR or branch), generalized from `s:/projects/thingalog/org/thingalog.openthing` v1.1.0+. Use `[SLOT: ...]` string conventions for v1.0.0; `metadata.kind: canonical-template`. Slot the mission, vision, scope, position descriptions; preserve verbatim the AI-pair-specific recommended_patterns (Product Owner + AI Strategist + AI Implementer triad; AI-Implementer with audit trail; Seat-separation discipline) with rationales; drop substrate-consumer + multi-tenant + Thingalog-domain content (those are adopter-side derivations).
2. **Submit via standard two-stage workflow**: PR adding `proposed-orgs/ai-pair-built-saas.openthing`; orgdef-maintainer validates schema-conformance and library-fit; orgdef-strategist signs off on the substantive shape.
3. **Promotion to `canonical-orgs/`** awaits the canonical-orgs library directory existing on disk (gated on canonical-orgs-library SCHEMA v0.3 work landing per that decision's build directive). Acceptable for the artifact to live in `proposed-orgs/` indefinitely until the directory lands; this matches `oagp-family-open-standard`'s current state.

orgdef-strategist (this seat) does NOT draft the artifact in this proposal; the strategist call captured here scopes and approves the shape. orgdef-maintainer reviews the eventual artifact for schema-conformance and library-fit.

## Backward Compatibility

Strictly additive. No SCHEMA changes; no existing canonical-template modifications; no validator-behavior changes.

`ai-pair-built-saas` derivation conventions inherit the additive-only discipline established by `oagp-family-open-standard`: REPLACE on mission/vision/scope, ADDITIVE-ONLY on values/red_lines/recommended_patterns/positions/relationships. Adopters who derive from `ai-pair-built-saas` declare `metadata.derived_from = {id: "ai-pair-built-saas", version: "1.0.0", url: "..."}` and follow the same conventions documented in CONTRIBUTING.md for the existing canonical.

Adopters who choose to derive from `oagp-family-open-standard` instead are unaffected.

## Conformance Tests

The canonical-template artifact itself, once authored, is the conformance fixture for the AI-pair-built SaaS shape. Validators that recognize `metadata.kind: canonical-template` (per the canonical-orgs-library decision's M1/M2) treat it identically to `oagp-family-open-standard`.

A future operational orgdef artifact derived from `ai-pair-built-saas` (Thingalog at v1.2.0+ when it adopts the canonical formally; or another adopter's first-derivation) serves as a conformance fixture for the derivation discipline.

No new validator behavior is required.

## Alternatives Considered

### Alt 1: Name `oagp-substrate-consumer-saas` instead

Narrower, more precise scope. Rejected per C1: substrate-consumer concerns are separable from AI-pair structural concerns; naming the canonical after the broader pattern preserves applicability to non-OAGP-substrate adopters.

### Alt 2: Defer until 2+ adopters surface the same shape

Wait until at least one more Scott-portfolio product (PXMemo, DangerStorm, Atomic Maple, Conversii, ToolVault) or external adopter explicitly produces an orgdef with the AI-pair triad shape; only then promote to canonical.

Rejected: precedent for canonical-template authoring is single-empirical-anchor sufficient when the shape is well-grounded. `oagp-family-open-standard` was authored from a single source (orgdef-spec orgdef itself), generalized at authoring time, and proven by three subsequent derivations (memodef, roledef, catdef). Deferring `ai-pair-built-saas` until 2+ derivations exist would block thingalog-strategist's offered worked example AND postpone the AI-pair shape's availability for the imminent next adopters.

### Alt 3: Derive `ai-pair-built-saas` from `oagp-family-open-standard` via metadata.derived_from

Treat `oagp-family-open-standard` as the parent canonical and `ai-pair-built-saas` as a specialization.

Rejected: the two are different shapes (spec-shaped vs product-shaped), not parent-and-child. Forcing a derivation chain would carry spec-shaped slots into a product-shaped canonical (e.g., recommended_roles for senior-open-standards-strategist, recursive-self-describing-v1 milestone) that don't fit. They are sibling canonicals — both v1.0.0; neither inherits from the other.

### Alt 4: Make `ai-pair-built-saas` a recommended_patterns entry on `oagp-family-open-standard` instead of a separate canonical

Add a recommended_patterns.general entry to `oagp-family-open-standard` describing the AI-pair triad shape, instead of authoring a separate canonical.

Rejected: recommended_patterns are guidance for adopters of a specific canonical shape; they don't carry positions or relationships. A canonical-template's value is delivering the entire org shape (positions + relationships + recommended_patterns + recommended_roles) in a single inheritable artifact. AI-pair-built SaaS adopters need positions and relationships as much as they need the patterns; recommended_patterns alone is insufficient.

## Open Questions

### OQ1. Should `ai-pair-built-saas` declare `metadata.derived_from` pointing at `oagp-family-open-standard`?

**Working position: no, sibling canonicals.** Per Alt 3 rejection above. Both canonicals are at v1.0.0; neither parents the other. A future hypothetical "OAGP-canonical-meta" might parent both, but that's premature.

**Resolution invited from:** maintainer review.

### OQ2. Should there be a separate `oagp-substrate-consumer` canonical that composes with `ai-pair-built-saas` via `metadata.derived_from`?

The substrate-consumer concerns dropped from `ai-pair-built-saas` (substrate compliance, schema-as-data, MCP-mediated access, no-vendor-lock-in red line) are themselves a recurring pattern across catdef-substrate consumers. Could be canonicalized separately and composed with `ai-pair-built-saas` by adopters who want both layers (e.g., Thingalog itself).

**Working position: defer until empirical adoption surfaces the need.** A single `oagp-substrate-consumer` canonical could absorb the substrate concerns; or the concerns could live at the substrate spec's adoption-guidance level (catdef-spec README or adopter-onboarding docs). Defer the call until a non-Thingalog substrate-consumer org surfaces; if 2+ substrate-consumer orgs surface the same shape with substantive overlap, file a follow-up proposal for a `oagp-substrate-consumer` canonical.

**Resolution invited from:** future strategist-triage when more adopters surface.

### OQ3. Should the canonical-template's recommended_roles include the three roledef-library gaps (`senior-product-strategist`, `senior-mobile-developer`, `revenue-marketing-officer`) as currently-unauthored?

The Thingalog-strategist memo surfaced these three gaps. The canonical-template's recommended_roles slot would naturally list them at appropriate priority levels, but with no canonical roledef URL to point at (since they're gaps in the roledef library).

**Working position: yes, list them — with bare-string entries (no URL coordinate object) and priority levels (`senior-product-strategist` MUST; `senior-mobile-developer` MAY; `revenue-marketing-officer` MAY) plus a `why` field naming the gap explicitly.** This pattern is the family precedent — orgdef-spec.openthing's recommended_roles uses bare strings for in-org-or-TBD-canonical roles. Once the roledef-library gaps are filled (per the cross-spec memo to roledef-strategist filed alongside this proposal), the canonical-template can be patched to upgrade the bare-string entries to full coordinate objects.

**Resolution invited from:** maintainer review.

### OQ4. Authorship coordination: does the orgdef-strategist seat author the canonical artifact, or does thingalog-strategist?

**Working position: thingalog-strategist authors.** The lift-from-source-strategist discipline that paralleled `oagp-family-open-standard`'s authoring (orgdef-strategist authored the canonical from orgdef-spec, the seat that owns the source orgdef) applies. thingalog-strategist owns Thingalog's orgdef; thingalog-strategist drafts the canonical lift. orgdef-strategist (this seat) holds the strategist call (this proposal) and reviews the drafted artifact for schema-conformance + library-fit + faithfulness to the strategist call.

**Resolution invited from:** thingalog-strategist via cross-spec memo (filed alongside this proposal accepting their offer); maintainer review.

## References

- Originating memo: [`memos/2026-05-01-0208--thingalog-strategist--orgdef-strategist--canonical-derivation-experience.openthing`](../memos/2026-05-01-0208--thingalog-strategist--orgdef-strategist--canonical-derivation-experience.openthing) (the bespoke-derivation experience memo that surfaced the shape)
- Cross-spec memo accepting thingalog-strategist's authorship offer: [`s:/projects/thingalog/memos/2026-05-01-2300--orgdef-strategist--thingalog-strategist--canonical-ai-pair-built-saas-authorship.openthing`](s:/projects/thingalog/memos/2026-05-01-2300--orgdef-strategist--thingalog-strategist--canonical-ai-pair-built-saas-authorship.openthing) (filed alongside this proposal)
- Cross-spec memo to roledef-strategist about three roledef-library gaps: [`s:/projects/roledef-spec/roledef/memos/2026-05-01-2300--orgdef-strategist--roledef-strategist--three-roledef-library-gaps.openthing`](s:/projects/roledef-spec/roledef/memos/2026-05-01-2300--orgdef-strategist--roledef-strategist--three-roledef-library-gaps.openthing) (filed alongside this proposal)
- Director ratification: 2026-05-01 conversation in orgdef-strategist chair, instructing "File both" (referring to this proposal + the roledef-strategist memo as the two held-but-not-yet-filed thingalog-thread follow-ups)
- Source artifact (the worked example): [`s:/projects/thingalog/org/thingalog.openthing`](s:/projects/thingalog/org/thingalog.openthing) v1.1.0+
- Sibling canonical (the existing first canonical-template): [`proposed-orgs/oagp-family-open-standard.openthing`](../proposed-orgs/oagp-family-open-standard.openthing) v1.1.0
- Canonical-orgs-library decision (foreshadowed library expansion): [`decisions/proposal-canonical-orgs-library.md`](../decisions/proposal-canonical-orgs-library.md)
- Inter-position-communication-convention decision (the prior 2026-05-01 thingalog-thread artifact): [`decisions/proposal-inter-position-communication-convention.md`](../decisions/proposal-inter-position-communication-convention.md)
