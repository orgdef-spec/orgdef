# Proposal: Charter shape additions (vision / values / red_lines / recommended_patterns) + SSoT rule + position.job_definition

**Status:** Accepted with Modifications (2026-04-26 by orgdef-strategist; see [decisions/proposal-charter-shape-additions.md](../decisions/proposal-charter-shape-additions.md))
**Author:** orgdef-strategist (provisional bot identity pending governance ratification)
**Created:** 2026-04-26
**Target version:** 0.2.0
**Origin:** Empirical dogfood at orgdef-spec, 2026-04-26. Bootstrapped the orgdef-spec org via interactive facilitator roledefs (`org-creation-facilitator`, `job-creation-facilitator`) and surfaced multiple charter-shape additions not in the v0.1 schema. Companion to the just-accepted [`roledef-spec/roledef/proposals/job-placement-and-charter-slots.md`](https://github.com/roledef-spec/roledef/blob/main/proposals/job-placement-and-charter-slots.md); incorporates the SSoT carryover (M3) and `position.job_definition` follow-on (M7 from `proposal-role-vs-job-distinction.md`) per cross-spec coordination obligation.

## Summary

Adds four optional/recommended fields to `orgdef:Organization` (`vision`, `values`, `red_lines`, `recommended_patterns`), one optional field to `orgdef:Position` (`job_definition`), formalizes the **SSoT rule** for the placement-vs-relationships question (orgdef.relationships authoritative; job.metadata.placement a denormalized snapshot), and documents the **org-folder filesystem convention** (`<project>/<orgname>-org/`) in CONTRIBUTING.md.

All additions are grounded in real content from the orgdef-spec dogfood. None breaks existing v0.1 artifacts.

## Motivation

### Empirical evidence from the orgdef-spec dogfood

On 2026-04-26 we bootstrapped the orgdef-spec org through interactive facilitation. The conversation produced an org charter (`orgdef-spec/orgdef-spec-org/orgdef.md`, provisional markdown form) whose substantive content **didn't fit cleanly into the v0.1 fields**. Five distinct content-shapes emerged that wanted homes:

1. **Vision** distinct from mission. orgdef-spec's *mission* is "define org structure/jobs in an open machine-readable way" — concrete and actionable. Its *vision* is "Open Agentic Governance Pattern — the pattern of an AI-first organization, including inter-org-AI exchange" — aspirational framing. Both are load-bearing; collapsing them loses the distinction between *what we ship* and *what we're working toward*.

2. **Values** as named-with-technical-grounding. orgdef-spec articulates two values: openness and completeness. Critically, **completeness is not an aesthetic preference** — it's a hallucination-prevention rule grounded in the technical reality that the primary reader of an orgdef is a machine, and machines confabulate when given null context. Without a structured place to record values *with their rationale*, the technical grounding becomes folk wisdom rather than a defensible MUST.

3. **Red lines**: explicit boundaries the org refuses to cross. orgdef-spec's load-bearing red line is "no NULL-context orgdefs accepted by the spec / validator / facilitator." Distinct from `scope` (what we cover) and `governance_model` (how we decide); a refusal is its own shape.

4. **Recommended patterns** with **recommended_roles** sub-table. The dogfood surfaced a need for a section answering "what we recommend for orgs using this pattern" — distinct from "how this org operates." For canonical orgdefs (templates derived from to bootstrap new orgs), this becomes the **bootstrapping checklist**: minimum role complement, recommended structural patterns, etc. orgdef-spec's recommended_roles entries: `human-director` (MUST), `senior-open-standards-strategist` (MUST), `orgdef-maintainer` (MUST), `canonical-implementor` (SHOULD).

5. **Position.job_definition** — added by the role-vs-job-distinction acceptance (M7). Positions can now reference a Job (specialized) rather than a Role (abstract) directly. orgdef SCHEMA needs the field.

### Why this matters for the canonical-orgdefs library

The orgdef-spec org is the first artifact in what will become a canonical-orgdefs library. The Director's foreshadowing is explicit: orgdef-spec's charter will be lifted into a canonical template for "OAGP-family open standard project," then used to bootstrap orgdefs for the catdef-spec and roledef-spec organizations. The current v0.1 schema doesn't have the slots needed to express the patterns that will compound across the library — vision, values-with-rationale, red lines, and recommended-roles tables are *exactly* what canonical templates will live and die by.

### Cross-spec coordination obligation

Two carryover items from the just-accepted roledef-side decisions land here:

- **SSoT rule articulation** (M3 of [proposal-job-placement-and-charter-slots](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-job-placement-and-charter-slots.md)): the rule is decided on the roledef side; orgdef SCHEMA.md needs to declare it from the orgdef side too so a reader of orgdef alone understands the consistency invariant.
- **`position.job_definition` field** (M7 of [proposal-role-vs-job-distinction](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-role-vs-job-distinction.md)): roledef-side schema landed; orgdef-side schema needs the parallel addition.

## Proposed Change

### `vision` (string or polymorphic) — SHOULD

Single-statement aspirational framing. Distinct from `mission` (concrete deliverable) and `scope` (what's covered/excluded).

```json
"vision": "Open Agentic Governance Pattern — the pattern of an AI-first organization, including inter-org-AI exchange where business owners can share orgdefs as the introduction artifact when engaging lawyers, accountants, marketing firms, etc."
```

Format guidance: 1–2 sentences. Polymorphic translatable per catdef i18n. Articulates *what we're working toward*, not *what we currently ship*.

### `values` (array of objects) — SHOULD

Named values with technical or principled rationale. Each entry:

```json
"values": [
  {
    "name": "openness",
    "description": "orgdef is fundamentally open — a pattern, not a product. No vendor lock-in, no privileged implementer, no proprietary extensions in the core spec.",
    "rationale": "Adoption depends on equal-citizen treatment of all implementers; vendor capture would defeat the standard's purpose."
  },
  {
    "name": "completeness",
    "description": "The orgdef + roledef + job bundle MUST be sufficient that a fresh AI runtime loaded with the bundle becomes the job, with zero context backfill.",
    "rationale": "Hallucination-prevention rule, not aesthetic preference. The primary reader is a machine; null context invites confabulation."
  }
]
```

Sub-fields:
- `name` (string, required) — short identifier, kebab-case
- `description` (string or polymorphic, required) — what the value means in concrete terms
- `rationale` (string or polymorphic, required) — *why* this is a value, ideally with technical or principled grounding

The `rationale` field is the load-bearing innovation. Values without rationale become folk wisdom; values *with* rationale become defensible MUSTs that survive the "but why?" challenge.

### `red_lines` (array of objects) — SHOULD

Explicit refusal boundaries. Each entry:

```json
"red_lines": [
  {
    "rule": "No NULL-context orgdefs accepted by the spec, the validator, or the canonical facilitator.",
    "rationale": "Technical, not aesthetic — null context causes hallucination in the primary (machine) reader. The MUST-have-substantive-charter rule is a hallucination-prevention rule."
  },
  {
    "rule": "No content policing of consumers.",
    "rationale": "What organizations choose to build using the orgdef pattern is their business, not the spec's. orgdef governs the pattern's integrity, not the morality of its applications."
  }
]
```

Sub-fields:
- `rule` (string or polymorphic, required) — the boundary statement
- `rationale` (string or polymorphic, required) — why this red line exists; ideally with grounding (technical, ethical, scope-discipline)

Distinct from `scope` (positive: what we cover) and `governance_model` (process: how we decide). Red lines are *what we refuse, even when asked nicely*.

### `recommended_patterns` (object) — MAY

The "what we recommend for orgs using the pattern" section. Distinct from operational fields (mission, positions, relationships, etc.) which describe *this* org. Structure:

```json
"recommended_patterns": {
  "general": [
    {
      "pattern": "Senior strategist role separation",
      "description": "Orgs SHOULD have a senior strategist role distinct from execution roles, so each position stays in its lane.",
      "rationale": "Same reason developers shouldn't do their own security testing — bounded scope per role enables clean handoffs and prevents authority concentration."
    }
  ],
  "recommended_roles": [
    {
      "role": "human-director",
      "priority": "MUST",
      "why": "Bounded-authority discipline requires a human ratifier."
    },
    {
      "role": {
        "id": "senior-open-standards-strategist",
        "version": "1.0.0",
        "url": "https://roledef.org/roledefs/senior-open-standards-strategist.openthing"
      },
      "priority": "MUST",
      "why": "Library-curation, scope, pattern-promotion calls."
    },
    {
      "role": "orgdef-maintainer",
      "priority": "MUST",
      "why": "Drafts spec text, walks SCHEMA validations."
    },
    {
      "role": "canonical-implementor",
      "priority": "SHOULD",
      "why": "Reference renderers and validators are how the spec gets dogfooded."
    }
  ]
}
```

Sub-fields of `recommended_patterns`:
- `general` (array of objects, optional) — non-role recommended patterns
- `recommended_roles` (array of objects, optional) — minimum role complement

`recommended_roles` entry sub-fields:
- `role` (string OR object) — bare id-string for roles within the family that the consumer can resolve, or full coordinate object (`{id, version, url}`) per `metadata.role_definition` shape for cross-spec references
- `priority` (string, enum: `MUST` | `SHOULD` | `MAY`) — RFC 2119 vocabulary mirroring the rest of the spec family
- `why` (string or polymorphic, required) — brief justification (1 sentence)

For canonical orgdefs (library-template versions), `recommended_roles` becomes the **bootstrapping checklist**: when a new org is derived from the canonical template, the facilitator walks the user through staffing each `MUST` entry as actual jobs.

### `position.job_definition` (object) — OPTIONAL

Per [`proposal-role-vs-job-distinction.md`](https://github.com/roledef-spec/roledef/blob/main/proposals/role-vs-job-distinction.md) M4 and M7. Symmetric with the existing `position.role_definition`:

```json
{
  "type": "orgdef:Position",
  "id": "strategist",
  "name": "Strategist",
  "role_definition": null,
  "job_definition": {
    "id": "orgdef-strategist",
    "version": "1.0.0",
    "url": "https://github.com/orgdef-spec/orgdef/blob/main/orgdef-spec-org/jobs/orgdef-strategist.openthing"
  }
}
```

Validation rules:
- A position MUST have AT LEAST ONE of `role_definition` or `job_definition` (positions without either are informal and signal incomplete authoring; v0.1 tolerates them but v0.2 SHOULD declare at least one)
- A position MAY have BOTH — in which case the job is the operational specialization and the role is the abstract parent (consistent with the role → job → position chain)
- The validator MUST verify that `job_definition.url` resolves to a valid `roledef:Job` (when public)

### SSoT rule (`orgdef.relationships` authoritative; `job.metadata.placement` denormalized)

Per M6 of the just-accepted [`proposal-job-placement-and-charter-slots`](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-job-placement-and-charter-slots.md):

> When both `orgdef.relationships` (Org-side) and `job.metadata.placement` (Job-side) express the same structural facts, **`orgdef.relationships` is authoritative**. `job.metadata.placement` is a **denormalized snapshot for AI cold-start convenience** — populated at job-authoring time and kept in sync going forward.

This proposal adds the orgdef-side declaration of the same rule in SCHEMA.md, plus validator-side enforcement:

- Validator SHOULD verify, for each `position` whose `job_definition` resolves to a public Job, that the Job's `metadata.placement.reports_to` corresponds to an `orgdef.relationships` edge of type `reports_to` from this position
- Validator SHOULD verify the same for `directs` and `coordinates_with` edges
- MAY skip verification with WARN (not FAIL) when the Job lives in a private repo the validator cannot resolve
- When inconsistency is detected, the validator's rendered message MUST cite both sources and identify which is the authoritative one (orgdef.relationships)

### Filesystem convention (CONTRIBUTING.md)

Documented in CONTRIBUTING.md, not enforced by SCHEMA.md (filesystem layout is outside spec scope per separation of concerns):

```
<project>/                       ← project repo root
└── <orgname>-org/               ← org folder
    ├── orgdef.openthing         ← the orgdef artifact
    ├── jobs/                    ← job artifacts directory
    │   └── <job-id>.openthing
    ├── rendered/                ← projected outputs (gitignored)
    └── .gitignore               ← ignores rendered/
```

The `<orgname>-org/` naming convention disambiguates from product/code/asset folders (`src/`, `docs/`, `assets/`); a tool walking the project root can find org folders unambiguously.

For monorepos hosting multiple sub-orgs, the convention generalizes: each sub-org gets its own `<orgname>-org/` directory at the appropriate path.

### Two-section charter discipline (CONTRIBUTING.md)

Documented in CONTRIBUTING.md as a SHOULD-discipline for all orgdefs, MUST for canonical-library-eligible orgdefs:

> Organize orgdef content into two implicit sections:
> 1. **How this org operates** — fields describing this specific org: mission, vision, scope, values, governance_model, positions, relationships, red_lines, metadata
> 2. **What we recommend for orgs using this pattern** — the `recommended_patterns` field, including general patterns and the recommended_roles bootstrapping checklist

The two sections serve different audiences: the first orients a reader (human or AI) joining *this* org; the second guides anyone deriving a *new* org from this one as a template.

## Backward Compatibility

All field additions are OPTIONAL/SHOULD/MAY. Existing v0.1 `orgdef:Organization` artifacts remain valid without any of the new fields. Schema bumps to v0.2.0 (minor: additive only).

`position.job_definition` joins `position.role_definition` as an optional field; v0.1 positions with only `role_definition` continue to validate. v0.2 introduces a SHOULD that positions declare at least one of the two; this is non-breaking (lenient reader, strict writer).

The SSoT rule applies to artifacts using the new fields; v0.1 artifacts that don't yet have `metadata.placement` on their jobs aren't affected.

The filesystem convention and two-section charter discipline land in CONTRIBUTING.md as SHOULDs; existing repos with different layouts continue to work but get nudged toward the convention in submission review.

## Conformance Tests

New conformance fixtures in `orgdef-spec/orgdef/conformance/`:

- `valid_orgs/canonical-aigp-family-spec.openthing` — exemplar orgdef exercising all new fields plus the recommended_roles bootstrapping checklist (the migrated form of `orgdef-spec/orgdef-spec-org/orgdef.md` becomes this fixture)
- `valid_orgs/org-with-job-positions.openthing` — exemplar with positions using `job_definition` references
- `valid_orgs/org-with-mixed-position-references.openthing` — exemplar with some positions referencing role_definition and others referencing job_definition
- `invalid_orgs/values-without-rationale.openthing` — counterexample where a value entry omits the rationale field
- `invalid_orgs/red-lines-as-prose-blob.openthing` — counterexample where red_lines is a string rather than a structured array
- `invalid_orgs/recommended-roles-bad-priority.openthing` — counterexample where a recommended_roles entry uses a non-RFC-2119 priority value
- `invalid_orgs/position-with-neither-role-nor-job.openthing` — counterexample (v0.2 SHOULD violation; warning-not-failure for v0.1 backward compat)
- `invalid_orgs/placement-relationships-mismatch.openthing` — counterexample exercising the SSoT validator rule (job.metadata.placement disagrees with orgdef.relationships)

Validator updates:
- MUST verify `position.job_definition.url` resolves to a valid `roledef:Job` (when public)
- SHOULD verify orgdef.relationships ↔ job.metadata.placement consistency per the SSoT rule
- SHOULD warn on positions declaring neither `role_definition` nor `job_definition`
- MUST validate `values` and `red_lines` entries have all required sub-fields
- MUST validate `recommended_roles` priority values against the RFC 2119 enum

## Alternatives Considered

### Alt 1: Combine `vision` into `scope` or `mission`

Add an "aspiration" sub-field to one of those rather than a top-level field.

**Rejected because:** loses the distinction. The reader of an orgdef benefits from seeing mission (what we ship), scope (what we cover), and vision (what we're working toward) as parallel top-level concepts. Subordinating one collapses the structure unnecessarily.

### Alt 2: Express `values` as free-form prose in `mission` or `metadata`

Don't add a structured field; let authors put values in mission narrative or metadata description.

**Rejected because:** loses the rationale field. The technical grounding for a value is the load-bearing part — it's what makes "completeness" a defensible MUST rather than a vague preference. Free-form prose buries the rationale or omits it entirely.

### Alt 3: Express `red_lines` via guardrail-like fields on positions

Distribute the red lines across position-level guardrails rather than at org level.

**Rejected because:** red lines are *org-level commitments*, not position-level rules. orgdef-spec's "no NULL-context orgdefs" applies to the spec/validator/facilitator collectively, not to any single position's behavior. Org-level red lines also serve as inheritance for derived canonical templates.

### Alt 4: Defer `recommended_patterns` to a separate spec

Bootstrap a `patterndef-spec` or similar to hold canonical patterns; orgdef stays minimal.

**Rejected because:** orgdefs ARE templates for derivation; recommended_patterns IS the natural home. Pulling pattern recommendations into a sibling spec adds coordination overhead without clear payoff. If pattern catalogs grow rich enough to warrant their own spec down the road, that's a v0.x consideration.

### Alt 5: Make `vision`, `values`, `red_lines`, `recommended_patterns` MUST instead of SHOULD

Force adoption.

**Rejected because:** raises the friction floor for bootstrap-stage and bespoke private orgdefs. SHOULD-with-strong-encouragement (and MUST for canonical-library-eligible) is the right balance — encourages substantive authorship without blocking adoption.

### Alt 6: Inline filesystem convention into SCHEMA.md instead of CONTRIBUTING.md

Make the org-folder layout a schema rule.

**Rejected because:** filesystem layout is outside the schema's purview. Schema describes artifact content; CONTRIBUTING describes how artifacts are organized in a repo. The separation matters because some adopters (e.g., monorepo hosts, alternative VCS users) may have different layouts that still produce valid artifacts.

## Open Questions

1. **Field naming**: `red_lines` vs `non_negotiables` vs `prohibitions` vs `refusals`. Bikeshed-with-real-content welcome. Author's weak preference: `red_lines` (matches the catdef-family conversational convention used in role stewardship and Director-level memos).

2. **`recommended_roles` priority vocabulary**: RFC 2119 (MUST/SHOULD/MAY) vs alternatives (`required`/`recommended`/`optional`). Author's weak preference: RFC 2119 for family consistency. Open to alternatives if consumer ergonomics suffer.

3. **`recommended_patterns.general` shape**: currently proposed as array of `{pattern, description, rationale}` objects. Could also be array of strings (just the pattern statement). Object form preferred for the rationale parallel with values/red_lines but adds verbosity.

4. **Two-section charter discipline strength**: SHOULD for all orgdefs vs MUST for canonical-library-eligible only vs MUST for all. Author's weak preference: SHOULD universal, MUST for canonical (validator enforces only for canonical-library entries).

5. **`vision` vs separate `aspiration` field**: should the aspirational framing be one field (`vision`) or split into `vision` (where we want to be) and `mission` (already exists, what we ship)? Author's weak preference: keep it as a single `vision` field; the existing `mission` already covers the concrete deliverable.

6. **Migration of dogfood artifact** ordering: this proposal references `orgdef-spec/orgdef-spec-org/orgdef.md` as the empirical exemplar. After acceptance, that artifact migrates to `.openthing` form using the new fields and becomes the conformance fixture `valid_orgs/canonical-aigp-family-spec.openthing`. Should the conformance fixture be a *copy* of the operational orgdef or a *reference* to it (via CONTRIBUTING-documented mirroring pattern)? Author's weak preference: copy, with metadata.history noting the mirror relationship.

7. **`position.job_definition` resolution requirement**: the proposed validator rule says "MUST verify the URL resolves to a valid `roledef:Job` when public." Should the resolution happen at validation time (network fetch) or only structural-shape verification? Author's weak preference: structural-only at write-time; URL resolution at read-time / runtime (consistent with how `metadata.role_definition` URL resolution works on the roledef side).

## Acceptance Criteria

If accepted:

1. **orgdef SCHEMA.md update** — define `vision`, `values`, `red_lines`, `recommended_patterns` as top-level fields on `orgdef:Organization`; define `position.job_definition` as optional field on `orgdef:Position`; document the SSoT rule alongside the position fields.

2. **orgdef CONTRIBUTING.md update** — document the org-folder filesystem convention; document the two-section charter discipline; document the `recommended_roles` bootstrapping checklist pattern.

3. **Conformance fixtures** — `valid_orgs/` and `invalid_orgs/` additions per Conformance Tests section above.

4. **Validator updates** — per the validator-rules section: `job_definition` URL resolution; SSoT consistency check; values/red_lines/recommended_roles structural validation.

5. **Migration of dogfood artifact** — `orgdef-spec/orgdef-spec-org/orgdef.md` migrated to formal `.openthing` JSON using the new fields. The migrated artifact becomes the reference exemplar fixture (per Open Question 6).

6. **Cross-spec coordination already complete** — the SSoT rule and `position.job_definition` field were coordinated with roledef-strategist via the just-accepted `proposal-role-vs-job-distinction` and `proposal-job-placement-and-charter-slots` decisions. This proposal articulates the orgdef-side of the same coordination.

7. **Foreshadowing: canonical template extraction** — once accepted and migrated, the orgdef-spec org's orgdef artifact will be lifted into a canonical-library entry (working title: `canonical-orgs/oagp-family-open-standard.openthing`), serving as the bootstrap template for catdef-spec, roledef-spec, and future OAGP-family member specs. That extraction is its own follow-on proposal in the canonical-orgdefs library work item; this proposal merely creates the substrate for it.

## References

- `orgdef-spec/orgdef-spec-org/orgdef.md` — empirical exemplar (provisional markdown form pending this proposal's acceptance and subsequent migration)
- `orgdef-spec/orgdef-spec-org/jobs/orgdef-strategist.openthing` — companion job artifact (already migrated to roledef v0.2 formal form per the just-accepted job-placement-and-charter-slots decision)
- [`roledef-spec/roledef/decisions/proposal-role-vs-job-distinction.md`](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-role-vs-job-distinction.md) — the parent decision that established the Job type and the `position.job_definition` follow-on
- [`roledef-spec/roledef/decisions/proposal-job-placement-and-charter-slots.md`](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-job-placement-and-charter-slots.md) — the sibling decision that established the SSoT rule articulated here
- `roledef-spec/roledef/proposed-roledefs/org-creation-facilitator.openthing` — the facilitator that produces orgdef artifacts using the proposed shape
- `roledef-spec/roledef/proposed-roledefs/job-creation-facilitator.openthing` — the facilitator that produces job artifacts referenced from orgdef positions
- Originating conversation: Director (Scott) + orgdef-strategist, 2026-04-26 (orgdef-spec org bootstrap dogfood and post-decision-landing follow-on session)
