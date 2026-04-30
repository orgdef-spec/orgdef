# Proposal: Canonical orgdefs library (canonical-orgs/ directory + metadata.kind + derivation conventions)

**Status:** Accepted with Modifications (2026-04-26 by orgdef-strategist; see [decisions/proposal-canonical-orgs-library.md](../decisions/proposal-canonical-orgs-library.md))
**Author:** orgdef-strategist (provisional bot identity pending governance ratification)
**Created:** 2026-04-26
**Target version:** 0.3.0
**Origin:** Recursive completion of the orgdef-spec dogfood. Director (Scott) foreshadowed this work: "the last recursive piece is going to be to draft our first model orgdef, based on your/our orgdef organization. Which I will then use to create orgdefs for the roledef and catdef organizations." This proposal creates the substrate for that work and includes the first canonical template (`aigp-family-open-standard`) as the exemplar submission.

## Summary

Adds a `canonical-orgs/` directory to the orgdef-spec repo for **canonical templates** — orgdef artifacts that exist to be *derived from*, not to describe a real org. Adds `metadata.kind` field on `orgdef:Organization` to discriminate `operational` (default) from `canonical-template`. Adds derivation conventions (parallel to roledef's `metadata.derived_from` rules) for orgdefs derived from canonical templates. Includes the first canonical template, `aigp-family-open-standard`, generalized from the just-migrated orgdef-spec orgdef.

## Motivation

### The catdef-family bootstrap needs templates, not just samples

The catdef-family currently has one orgdef in formal `.openthing` form (`orgdef-spec/orgdef-spec-org/orgdef.openthing`, just migrated). Three more are imminent:

- `catdef-spec/catdef-spec-org/orgdef.openthing` (the catdef-spec org's orgdef)
- `roledef-spec/roledef-spec-org/orgdef.openthing` (the roledef-spec org's orgdef)
- `memodef-spec/memodef-spec-org/orgdef.openthing` (the memodef-spec org's orgdef, when memodef bootstraps further)

All four orgs share substantial structural commonalities — same governance model (bounded AI + human Director), same load-bearing values (openness, completeness), same red lines (no NULL-context, no content policing), same recommended-roles complement (director/strategist/maintainer/implementor). Authoring each from scratch would duplicate this work three times and invite drift; cross-spec inconsistencies would erode the family-coherence story.

The clean answer: **extract the common structure into a canonical template**, derive each spec's orgdef from it. That's exactly what the Director foreshadowed.

### Sample vs canonical: a distinction worth making explicit

There's a real difference between:
- **Operational orgdefs** — describe a real org (e.g., orgdef-spec, an actual project with actual roles staffed)
- **Canonical templates** — exist to be derived from (e.g., "AIGP-family open standard", a pattern other orgs instantiate)

These have different lifecycles, different audiences, different curation criteria. Conflating them in a single `orgs/` directory loses the distinction (renderers can't differentiate; validators can't apply different rules; library curation can't track which entries are templates vs operational).

Brother-roledef's just-accepted [`role-vs-job-distinction`](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-role-vs-job-distinction.md) (M3) introduced `sample-jobs/` as a sibling of `roledefs/` for the parallel distinction. orgdef should follow the same pattern with `canonical-orgs/` as a sibling of `orgs/`.

### Derivation needs explicit conventions

Roledef has [explicit derivation conventions](https://github.com/roledef-spec/roledef/blob/main/SCHEMA.md#derivation-rules) for safe `derived_from` chains: additive-only for guardrails, voice/identity refinable but not contradictable, output_contract additive-or-tightenable, etc. Without parallel conventions for orgdef derivation, derivers don't know what's safe to change and what's load-bearing for the canonical pattern.

Empirically (from drafting the AIGP-family canonical template included with this proposal): the conventions are obvious in some cases (mission/scope are replaced; values are inherited verbatim) and subtle in others (vision is inheritable-but-refinable; governance_model can be customized within bounds). Articulating them prevents future bikeshed-by-implementer.

## Proposed Change

### `canonical-orgs/` directory

Add `canonical-orgs/` as a sibling of `orgs/` in the orgdef-spec repo:

```
orgdef-spec/orgdef/
├── orgs/                    ← operational orgdefs (real orgs)
│   ├── orgdef-spec.openthing
│   ├── catdef-spec.openthing
│   └── ...
├── canonical-orgs/          ← canonical templates (derive from these)
│   ├── aigp-family-open-standard.openthing
│   ├── canadian-non-profit.openthing (future)
│   ├── early-stage-saas.openthing (future)
│   └── ...
├── proposed-orgs/           ← submissions in flight (either type)
│   └── ...
└── ...
```

Submissions to either `orgs/` or `canonical-orgs/` flow through `proposed-orgs/` first per the existing two-stage workflow. The `metadata.kind` field (below) determines the destination at promotion time.

### `metadata.kind` field

Add an optional `metadata.kind` field on `orgdef:Organization`:

```json
"metadata": {
  "kind": "operational"  // or "canonical-template"
}
```

Cardinality: OPTIONAL. Default: `operational` (when absent). Enum: `operational` | `canonical-template`.

`operational` = describes a real org. `canonical-template` = exists to be derived from. Validators apply different rules to each (per below).

### Derivation conventions for orgdefs

Mirror roledef's `metadata.derived_from` discipline. A derived orgdef:

- MUST declare `metadata.derived_from` pointing at the canonical template (id + version + url)
- Inherits the canonical's content as its starting point (git-fork-style; no runtime merge)
- May modify per the additive-only conventions below

**Additive-only conventions (SHOULD discipline):**

| Field | Convention | Rationale |
|---|---|---|
| `mission` | REPLACE | Each org has its own concrete deliverable |
| `vision` | REFINE (specialize, don't contradict) | Vision is family-level; derivations specialize the framing |
| `scope` | REPLACE | Each org has its own scope |
| `governance_model` | INHERIT or REFINE | The bounded-AI-plus-Director pattern is family-level; derivations may add detail |
| `values` | ADDITIVE ONLY | Canonical values (openness, completeness) are family invariants; derivers MAY add new values; SHOULD NOT remove canonical ones |
| `red_lines` | ADDITIVE ONLY | Canonical red lines (no NULL-context, no content policing) are family invariants; same rule as values |
| `recommended_patterns` | ADDITIVE ONLY | Canonical patterns are family invariants; same rule |
| `v1_success_criterion` | REFINE or REPLACE | Each org has its own v1 milestone; the recursive self-describing form is canonical-recommended but not mandatory |
| `positions` | REPLACE | Each org has its own positions; canonical's positions are SLOT-shaped placeholders |
| `relationships` | REPLACE | Each org has its own relationships |
| `metadata.kind` | MUST be `operational` | Derived orgs are operational; deriving FROM a derived org isn't supported in v0.3 (single-tier derivation only) |

**Validator behavior:**

- For `metadata.kind: canonical-template` artifacts:
  - SHOULD permit `[SLOT: ...]` placeholder strings in any field (signaling derivation slots)
  - SHOULD NOT require that `positions` or `relationships` resolve to operational entities
  - MUST NOT enforce required-field MUSTs that don't make sense for a template (e.g., a template's `mission` may be a slot rather than a concrete statement)

- For `metadata.kind: operational` artifacts with `metadata.derived_from`:
  - MUST verify `derived_from.url` resolves to a `canonical-template`-kinded artifact
  - SHOULD verify additive-only invariant against the parent (no removed values, red_lines, recommended_patterns entries)
  - MAY verify content of REFINE-discipline fields (vision, governance_model) hasn't structurally contradicted the parent — this is a soft check, since "contradicted" is judgmental

### First canonical template: `aigp-family-open-standard`

Submitted alongside this proposal at `proposed-orgs/aigp-family-open-standard.openthing`. Generalized from `orgdef-spec/orgdef-spec-org/orgdef.openthing` (just migrated). Slot-shaped fields use `[SLOT: description]` placeholders for content derivers must fill.

The template's intended derivers (initial):
- `catdef-spec/catdef-spec-org/orgdef.openthing` (the catdef-spec organization)
- `roledef-spec/roledef-spec-org/orgdef.openthing` (the roledef-spec organization)
- `memodef-spec/memodef-spec-org/orgdef.openthing` (when memodef bootstraps further)
- Future AIGP-family member specs

## Backward Compatibility

All additions are purely additive. Existing v0.2 orgdef artifacts (none of which yet declare `metadata.kind`) continue to validate as `operational` (the default). The `canonical-orgs/` directory is new; no existing artifacts move into or out of it. Derivation conventions are SHOULDs; existing artifacts without `metadata.derived_from` are unaffected.

Schema bumps to v0.3.0 (additive minor).

## Conformance Tests

New conformance fixtures in `orgdef-spec/orgdef/conformance/`:

- `valid_orgs/canonical-template-with-slots.openthing` — exemplar canonical-template artifact with `[SLOT: ...]` placeholders in mission/scope/positions
- `valid_orgs/operational-derived-from-canonical.openthing` — exemplar operational artifact with `metadata.derived_from` pointing at a canonical template, demonstrating the additive-only invariant (canonical values preserved + new value added)
- `invalid_orgs/operational-removed-canonical-value.openthing` — counterexample where a derived operational artifact removed a canonical value entry (violates additive-only)
- `invalid_orgs/canonical-template-with-operational-positions.openthing` — counterexample: a canonical-kinded artifact whose positions reference real job_definitions (canonical templates' positions should be SLOT-shaped, not point at operational jobs)
- `invalid_orgs/derived-from-non-canonical.openthing` — counterexample: an operational artifact whose `derived_from` points at another operational artifact (single-tier derivation: only canonical-templates are derivable parents in v0.3)

## Alternatives Considered

### Alt 1: No separate directory; use `metadata.kind` only

Put canonical templates and operational orgdefs in the same `orgs/` directory; differentiate only by `metadata.kind`.

**Rejected because:** loses the discoverability the directory split provides. A library browser ("show me the canonical templates I can derive from") needs to enumerate them efficiently; a metadata filter is possible but slower and less obvious. Brother-roledef's `sample-jobs/` precedent argues for the directory split.

### Alt 2: Use roledef's `sample-jobs/` naming (`sample-orgs/`)

Match the sibling-spec convention exactly: `sample-orgs/` instead of `canonical-orgs/`.

**Considered but rejected:** the orgdef use case is stronger than "sample." Templates are *intentionally* meant to be derived from; they're the canonical reference for a class of orgs. "Sample" understates the role; "canonical" matches the actual function. Modest cross-family inconsistency in naming is acceptable when the underlying use is meaningfully different.

(Note for future cross-spec coordination: roledef's `sample-jobs/` may want to evolve into `canonical-jobs/` if its use case shifts toward canonical reference rather than just demonstration. Not blocking either spec now.)

### Alt 3: Inline the canonical template content into the proposal

Author the template in the proposal text itself (no separate artifact); make it instantiate directly from spec text.

**Rejected because:** the template is itself an `.openthing` artifact and benefits from being a real, validatable, fetchable file. Derivers should be able to `git clone` it, fork it, modify it. A proposal-text-only template can't be cleanly derived from.

### Alt 4: Multi-tier derivation (canonical-template can derive from canonical-template)

Allow chains: a specialized canonical template (e.g., "Canadian non-profit AIGP-family open standard") could derive from the general AIGP-family canonical.

**Considered but deferred to v0.4+:** v0.3 establishes single-tier derivation (operational derives from canonical-template). Multi-tier is appealing for richer template hierarchies but adds complexity (chain validation, additive-only across multiple tiers, version-skew issues across the chain). Defer until concrete use cases motivate it. v0.3's single tier covers the catdef-family's immediate needs.

### Alt 5: Don't add `metadata.kind`; differentiate by location only

Use `canonical-orgs/` directory presence as the sole signal; no `metadata.kind` field.

**Rejected because:** validators and renderers benefit from a content-level signal that survives file movement. A canonical artifact moved out of `canonical-orgs/` (e.g., into a derived org's working repo as a reference) should still be recognizable as a canonical template. Location is convention; metadata is content.

## Open Questions

1. **Naming bikeshed: `canonical-orgs` vs alternatives** (`templates`, `canonical-templates`, `org-templates`, `sample-orgs` for cross-family parity). Author's weak preference: `canonical-orgs` per Alt 2 reasoning.

2. **`metadata.kind` enum extensibility**: should the enum be exactly `{operational, canonical-template}` or allow extensions (`anonymized-sample`, `historical-record`, etc.)? Author's weak preference: closed enum for v0.3, extension via `x.<domain>.kind` if domains need other distinctions.

3. **`[SLOT: ...]` placeholder convention**: this is currently informal — slot-shaped fields use string content like `[SLOT: 1-2 sentence statement of...]`. Should the placeholder convention be formalized (e.g., a structured `__slot__` object), or stay informal? Author's weak preference: stay informal for v0.3; formalize if patterns surface.

4. **Required-field treatment for canonical templates**: this proposal says validators MUST NOT enforce required-field MUSTs that don't make sense for templates. But which MUSTs? `id`, `name`, `version`, `type`, `catdef`, `orgdef` are clearly still required. `mission`, `positions`, `relationships` arguably aren't (they're slot-shaped in templates). Should the spec list which MUSTs are template-relaxed vs strict? Author's weak preference: yes, list explicitly in SCHEMA.md.

5. **Inheritance semantics for `recommended_patterns.recommended_roles`**: the canonical's `recommended_roles` table includes `[SLOT: spec-name]-maintainer` and `canonical-implementor` entries. Derivers fill in the slot-name. Is this inheritance (the entry stays, slot gets filled) or replacement (the entry is rewritten)? Author's weak preference: inheritance with slot-fill (preserves the canonical's role-complement reasoning).

6. **Cross-spec coordination follow-ons**: roledef's `sample-jobs/` will want similar derivation conventions for jobs (an operational job derived from a sample-job). Not in scope of this proposal but flagged as parallel work brother-roledef may want to take up. Currently roledef's `metadata.derived_from` is generic (works for role-from-role and job-from-job); explicit job-specific derivation conventions could parallel this proposal's orgdef-specific ones.

## Acceptance Criteria

If accepted:

1. **orgdef SCHEMA.md update** — add `metadata.kind` field; document derivation conventions (additive-only invariant, REPLACE/REFINE/INHERIT discipline per field); list which MUSTs are template-relaxed (Open Question 4); document `[SLOT: ...]` placeholder convention.

2. **orgdef CONTRIBUTING.md update** — document `canonical-orgs/` directory; explain operational-vs-canonical-template distinction; document the canonical-template submission workflow (same two-stage as operational, but promotes to `canonical-orgs/` instead of `orgs/`); document derivation submission expectations (PR description includes which canonical was derived from).

3. **Conformance fixtures** — per the Conformance Tests section above.

4. **Validator updates** — per the validator-behavior section above.

5. **Promote first canonical template** — `proposed-orgs/aigp-family-open-standard.openthing` (submitted alongside this proposal) gets promoted to `canonical-orgs/aigp-family-open-standard.openthing` upon acceptance, becoming the first entry in the canonical library.

6. **Foreshadowed downstream work** (separate proposals):
   - Derive `catdef-spec/catdef-spec-org/orgdef.openthing` from the AIGP-family canonical
   - Derive `roledef-spec/roledef-spec-org/orgdef.openthing` from the AIGP-family canonical
   - Eventually: derive memodef and other AIGP-family member specs

## References

- Empirical exemplar (the source for generalization): [orgdef-spec-org/orgdef.openthing](../orgdef-spec-org/orgdef.openthing)
- First canonical template (submitted alongside this proposal): [proposed-orgs/aigp-family-open-standard.openthing](../proposed-orgs/aigp-family-open-standard.openthing)
- Sibling-spec precedent for the directory-split pattern: [`roledef-spec/roledef/decisions/proposal-role-vs-job-distinction.md`](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-role-vs-job-distinction.md) (M3 added `sample-jobs/`)
- Sibling-spec precedent for derivation conventions: [`roledef-spec/roledef/SCHEMA.md`](https://github.com/roledef-spec/roledef/blob/main/SCHEMA.md) — `metadata.derived_from` rules
- Originating Director foreshadowing: 2026-04-26 conversation, "the last recursive piece is going to be to draft our first model orgdef, based on your/our orgdef organization. Which I will then use to create orgdefs for the roledef and catdef organizations."
