# Proposal: Inter-position communication convention (memos/ + x.org.memo_location)

**Status:** Filed (2026-05-01 by orgdef-strategist; awaiting maintainer review and decision artifact)
**Author:** orgdef-strategist (provisional bot identity pending governance ratification)
**Created:** 2026-05-01
**Target version:** canonical-orgs `oagp-family-open-standard` v1.2.0 (additive; recommended_patterns.general entry); orgdef CONTRIBUTING.md prose update
**Origin:** Director-surfaced strategy question 2026-05-01 — Thingalog product-strategist (first non-spec OAGP-derived org) proposed a `handoffs/` directory for intra-org operational handoffs distinct from `memos/`. Director ratified the directional call (hold `memos/` as universal channel) 2026-05-01 and authorized this proposal. memodef v0.2.0 (`body_ref`) shipped same-day in a parallel memodef-strategist session, removing the underlying body-as-JSON-string ergonomic friction that motivated the `handoffs/` proposal.

## Summary

Codify the cross-OAGP-family convention that all inter-position communications — strategist→implementer, strategist→specialist, strategist→peer-strategist, cross-org, cross-spec — use **memodef:Memo artifacts placed in the recipient's working-repo `memos/` directory**. Add an `x.org.memo_location` extension as the per-org escape hatch for adopters whose monorepo or unusual-layout requirements make `memos/` impractical at the canonical path.

This proposal is content-only against the canonical template (one new `recommended_patterns.general` entry) plus prose in CONTRIBUTING.md. No SCHEMA changes. The `x.org.memo_location` extension lives in the existing `x.<domain>.<identifier>` namespace catdef substrate provides; no orgdef schema additions are required to permit it.

## Motivation

Thingalog's product-strategist, deriving the first non-spec OAGP org, proposed a `handoffs/` directory for plain-text-with-`== Section ==`-headers operational handoff prompts (strategist → implementer), distinct from `memos/`. Reasoning: memodef:Memo's body-as-JSON-string envelope is ergonomically painful for hand-authored multi-paragraph operational content; the handoff_prompt_to_implementer artifact category feels different in shape from the cross-spec memos that previously populated `memos/` in catdef-family repos.

The ergonomic friction was real and was independently resolved in memodef v0.2.0, shipped 2026-05-01 (commits `49d4640` proposal, `c7049d8` decision, `9b29931` implementation): `body_ref` OPTIONAL field; co-located sibling `.body.md` files; `body` MUST remain non-empty (1–3-sentence triage summary when `body_ref` is present, preserving AI-legibility primacy). The trigger threshold (`≥2 hand-author cases`) was reached and the spec response shipped the same day. The artifact-category-bifurcation argument, however, is independent of the ergonomic question and would be load-bearing for OAGP family adoption if accepted:

- **Bifurcation propagates to every adopter.** Each new OAGP-derived org would face the question "is this a memo or a handoff?" Mid-line cases (cross-spec coordination memos that are also action-required handoffs; build-directive memos to peer strategists) would get miscategorized inconsistently across orgs. Family-wide tooling (renderer, future indexers, MCP-mediated queries) would have to scan multiple folders with unclear shape contracts.
- **memodef's universal-channel value erodes.** memodef:Memo is content-neutral on whether the comms are cross-org, cross-position, or intra-position; the value of the spec is being THE inter-position channel. Bifurcating it for ergonomic reasons signals to adopters that inventing ad-hoc artifact categories is appropriate whenever memodef:Memo is uncomfortable. The next adopter invents `briefs/`, the one after that invents `prompts/`, and the family-wide channel fragments by accumulation.
- **AI-legibility primacy hierarchy violated.** memodef's load-bearing three-priority ordering is AI-to-AI > auditable > human-readable. A plain-text `handoffs/<file>.md` artifact loses the catdef type-tag, x.memo.* metadata, action_required flag, maildir lifecycle, and structured trail — trading AI-legibility for hand-authoring ergonomics. The trade is the one memodef explicitly says not to make.
- **First-real-org-adopter precedent.** Thingalog is the first real-org adopter of orgdef (post the four spec-org derivations). Whatever pattern lands here will be copied. Accepting `handoffs/` as a separate category sets the pattern; canonizing `memos/` as universal preserves it.

The right structural answer is that operational handoffs ARE memodef:Memos with `action_required: true`. The body-as-JSON-string ergonomics was a memodef-spec problem, scoped to memodef v0.2 (`body_ref` field, now shipped). orgdef-spec's role is declaring WHERE such memos live in an org's filesystem; this proposal does that.

## Proposed Change

### P1. Add `recommended_patterns.general` entry to canonical template

Add to `proposed-orgs/oagp-family-open-standard.openthing` `recommended_patterns.general` array:

```json
{
  "pattern": "memos/ as the universal inter-position communication channel",
  "description": "Inter-position communications — strategist→implementer, strategist→specialist, strategist→peer-strategist (intra-org), cross-org, cross-spec — SHOULD use memodef:Memo artifacts placed in the recipient's working-repo `memos/` directory. memodef:Memo with `action_required: true` covers the operational-handoff case; with `action_required: false` covers FYI / institutional-memory comms. Adopters whose layout makes `memos/` impractical at the canonical path MAY declare an alternative via the `x.org.memo_location` extension on their orgdef artifact.",
  "rationale": "Bifurcating inter-position comms across multiple directory categories propagates artifact-category ambiguity to every adopter, miscategorizes mid-line cases (cross-spec coordination + action-required + build-directive memos), and trades AI-legibility for hand-authoring ergonomics. memodef:Memo is content-neutral on intra-vs-cross-position scope; memos/ is the family channel. Hand-authoring ergonomic friction (body-as-JSON-string for multi-paragraph operational content) is resolved by the memodef v0.2.0 `body_ref` OPTIONAL field (sibling `.body.md` files, co-located, with `body` carrying a triage summary); resolving the friction inside memodef preserves the universal-channel value of memos/."
}
```

Bump canonical template version `1.1.0 → 1.2.0` (additive minor; no breaking changes).

### P2. Document `x.org.memo_location` extension in CONTRIBUTING.md

Add to `CONTRIBUTING.md` under a new "Inter-position communication conventions" section:

> Per the canonical recommended_patterns.general entry "memos/ as the universal inter-position communication channel," operational orgdefs SHOULD use `memos/` at the working-repo root for inter-position memos. Adopters whose layout makes this impractical (monorepos, vendor-imposed directory conventions, unusual deployment shapes) MAY declare an alternative path via the `x.org.memo_location` extension on the orgdef:Organization artifact:
>
> ```json
> {
>   "x.org.memo_location": "communications/inter-position/"
> }
> ```
>
> Validators SHOULD treat the path as relative to the artifact's working repo. The default convention when `x.org.memo_location` is absent is `memos/`. Sub-directory conventions within the location (e.g., maildir-style `inbox/`, `read/`, `archive/`) are governed by memodef-spec, not orgdef.

### P3. Document migration path for existing handoffs/ directories

Add to `CONTRIBUTING.md` (same section):

> Adopters who previously created an alternative directory category for intra-org operational handoffs (e.g., `handoffs/`) SHOULD migrate those artifacts to `memos/` as memodef:Memo artifacts with `action_required: true`. The body content of the prior plain-text artifact carries forward as the memo's body string; metadata (from / to / subject / sent / action_required) wraps the existing content. Deletion of the prior directory completes the migration; intermediate states where both directories exist for the same artifact category SHOULD be avoided.

## Backward Compatibility

Strictly additive. No existing operational orgdef artifact becomes invalid:

- **Operational orgdefs without an `x.org.memo_location` extension** continue to work; default convention is `memos/` (which is what every catdef-family operational orgdef already uses, per the placement-convention migration that landed 2026-04-30).
- **Operational orgdefs that adopt `x.org.memo_location`** are forward-compatible with the catdef-substrate's lenient-reader rule (unknown `x.<domain>.<identifier>` extensions are preserved on round-trip, never rejected).
- **Adopters who previously created bespoke inter-position directories** (e.g., Thingalog's `handoffs/`) require a one-time migration; see P3. The migration is mechanical and bounded (one directory per affected adopter; no cross-adopter coordination).

No orgdef SCHEMA changes; no canonical artifact required-field changes; no validator-behavior changes beyond the SHOULD-pattern guidance.

## Conformance Tests

No new conformance fixtures are strictly required (this is a SHOULD-pattern, not a MUST-validation). However, the canonical-orgs library SHOULD demonstrate the pattern by example:

- The post-promotion `canonical-orgs/oagp-family-open-standard.openthing` (once the canonical-orgs library proposal lands fully) will include the new recommended_patterns.general entry verbatim.
- The four spec-org operational orgdefs (`orgdef-spec/org/orgdef-spec.openthing`, `memodef-spec/memodef/org/memodef-spec.openthing`, `roledef-spec/roledef/org/roledef-spec.openthing`, `catdef-spec/catdef-spec/org/catdef-spec.openthing`) all use the default `memos/` convention; no migration required for them.
- A future canonical-orgs entry that uses `x.org.memo_location` as a non-default value would serve as the reference fixture for the extension's use; deferred until an adopter (operational or canonical) genuinely needs it.

## Alternatives Considered

### Alternative 1: Accept the `handoffs/` proposal

Codify a `handoffs/` directory category alongside `memos/`, with content-shape and naming conventions specific to operational handoffs.

**Why rejected.** Bifurcation propagates to every adopter; mid-line cases miscategorized inconsistently; memodef's universal-channel value erodes; trades AI-legibility for ergonomics in violation of memodef's three-priority hierarchy; sets the "invent a folder" precedent for the next adopter that hits memodef friction. See Motivation.

### Alternative 2: Defer the call until memodef v0.2 (`body_ref`) ships

Wait for memodef v0.2 to ship `body_ref`, which removes the underlying ergonomic friction; revisit the placement convention only after the friction is gone.

**Why rejected, and why moot in retrospect.** Thingalog was committing the precedent today; deferral would have meant accepting `handoffs/` in practice while waiting for memodef. Independent of timing, the orgdef-side placement convention is structurally separate from the memodef-side ergonomic fix; both ship in parallel without blocking each other. memodef v0.2.0 in fact shipped same-day (2026-05-01) in a parallel session, making the deferral question moot — but the parallel-shipping outcome confirms rather than contradicts the rationale: placement and ergonomics belong in different specs and should ship independently.

### Alternative 3: Mandate `memos/` (MUST, not SHOULD) with no escape hatch

Make `memos/` REQUIRED for every orgdef artifact, no `x.org.memo_location` extension permitted.

**Why rejected.** Forecloses on monorepo and vendor-imposed-layout adopters legitimately. SHOULD with documented escape hatch preserves discipline (default is universal; deviation requires explicit declaration that's machine-discoverable) without forcing adopters out of the family.

### Alternative 4: Document the convention only in CONTRIBUTING.md without canonical template patch

Add the prose in CONTRIBUTING.md but don't update the canonical template's recommended_patterns.

**Why rejected.** The canonical template is what every new orgdef derivation reads; deriving from a canonical that doesn't carry the pattern means each deriver has to re-discover the convention via CONTRIBUTING.md. The canonical-template's recommended_patterns.general slot exists exactly for guidance like this; using it is internally consistent with how the canonical already carries patterns like "Senior strategist role separation" and "Two-section charter discipline."

## Open Questions

### OQ1. Should `x.org.memo_location` accept a list of paths (multi-location) or only a single string?

**Working position: single string.** Multi-location implies inbox-routing rules ("memos to position X go here, memos to position Y go there") that approach memodef-side concerns. orgdef declares the org-level default; finer routing is per-recipient within the recipient's working tree (which memodef already governs via maildir or flat conventions).

**Resolution invited from:** maintainer review.

### OQ2. Should validators warn (or note) on operational orgdefs that have an `x.org.memo_location` extension declaring a non-default path?

**Working position: no warning by default; validators MAY surface as informational note.** The extension is a legitimate escape hatch; firing a warning treats deviation as suspect, which contradicts the SHOULD-with-escape-hatch shape. Informational note for human-readable validator output is acceptable; structured warnings are not.

**Resolution invited from:** maintainer review.

### OQ3. Is there an OAGP-family parallel concern for `proposals/` placement?

`proposals/` (orgdef and roledef) and `decisions/` (orgdef, roledef, catdef) follow the same per-spec convention as `memos/` did pre-migration. If a future adopter raises an analogous "where do proposals live" question, the answer should compose with this proposal's `x.org.memo_location` shape (`x.org.proposals_location`?).

**Working position: do not preempt the parallel.** This proposal scopes to `memos/`; other directory placement questions get raised when an adopter actually asks. Avoid the architecture-astronaut tax of solving theoretical adopters' problems.

**Resolution invited from:** maintainer review; flagged for future-proposal triage.

## References

- Director ratification: 2026-05-01 conversation in orgdef-strategist chair
- Thingalog-strategist's directional proposal (the precipitating case): inferred from Director's surfaced quote 2026-05-01
- Memo to thingalog-strategist: [`s:/projects/thingalog/memos/2026-05-01-1430--orgdef-strategist--thingalog-strategist--inter-position-communication-convention.openthing`](s:/projects/thingalog/memos/2026-05-01-1430--orgdef-strategist--thingalog-strategist--inter-position-communication-convention.openthing)
- Cross-spec memo to memodef-strategist (body_ref case-2 trigger): [`s:/projects/memodef-spec/memodef/memos/inbox/2026-05-01-1430--orgdef-strategist--memodef-strategist--body-ref-case-2-trigger.openthing`](s:/projects/memodef-spec/memodef/memos/inbox/2026-05-01-1430--orgdef-strategist--memodef-strategist--body-ref-case-2-trigger.openthing)
- memodef AI-legibility primacy hierarchy: `s:/projects/memodef-spec/memodef/CLAUDE.md` (or charter — the three-priority ordering AI-to-AI > auditable > human-readable)
- memodef body_ref shipped: memodef-spec commits `49d4640` (proposal), `c7049d8` (decision), `9b29931` (implementation, version bump 0.1.0 → 0.2.0); FYI memo from memodef-strategist confirming no orgdef-side patch needed at [`s:/projects/orgdef-spec/orgdef/memos/2026-05-01-2000--memodef-strategist--orgdef-strategist--body-ref-v0.2-shipped-no-patch-needed.openthing`](s:/projects/orgdef-spec/orgdef/memos/2026-05-01-2000--memodef-strategist--orgdef-strategist--body-ref-v0.2-shipped-no-patch-needed.openthing)
- Thingalog's product-strategist roledef: [`s:/projects/thingalog/org/jobs/product-strategist.openthing`](s:/projects/thingalog/org/jobs/product-strategist.openthing) (the `handoff_prompt_to_implementer` output_contract entry — destination clause should be additively amended per the migration ask in the thingalog memo)
- Canonical template current state (pre-this-proposal, v1.1.0): `s:/projects/orgdef-spec/orgdef/proposed-orgs/oagp-family-open-standard.openthing`
- catdef-family placement-convention precedent (placement of org folder): `s:/projects/orgdef-spec/orgdef/decisions/proposal-canonical-template-v1.1-and-placement-convention.md`
