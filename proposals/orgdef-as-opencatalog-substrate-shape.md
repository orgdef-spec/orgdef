# Proposal: orgdef as `.opencatalog` (atomic-transportable substrate shape, SCHEMA v1.0.0)

**Status:** Filed (2026-05-10 by orgdef-strategist; awaiting maintainer review and decision artifact)
**Author:** orgdef-strategist (provisional bot identity pending governance ratification)
**Created:** 2026-05-10
**Target version:** orgdef SCHEMA v1.0.0 (major bump from 0.3.0; substrate-shape change); canonical-template `oagp-family-open-standard.opencatalog` v2.0.0 (filename + shape change); operational orgdef artifacts in 6 working repos migrated; CONTRIBUTING.md substantive rewrite
**Origin:** Director-driven strategic conversation 2026-05-10 — recovering the original-intent substrate shape for orgdef artifacts. Path B chosen over Path A (export-layer multi-file bundle) per Director's "An orgdef should be an atomic thing" framing. Surfaced by openbraid Phase E E2's discovery that current `.openthing`-per-org + separate `.openthing`-per-job artifacts don't atomically transport. Director acknowledged the gap as their oversight: "This is my failure, I did not notice that we had not done this."

## Summary

Switch orgdef artifacts from `.openthing` (single org artifact + separate job artifact files) to `.opencatalog` (atomic bundle with positions and job specializations as items). This is a substrate-shape correction recovering the Director's original-intent vision that didn't quite land during the 0.x experimental phase. Single file = atomic transportability = the substrate shape the family always needed.

Substantial migration: orgdef SCHEMA v0.3.0 → v1.0.0 (major bump; this is the 1.0 landing point because the substrate shape is finally aligned). Canonical-template v1.3.0 → v2.0.0 (filename + shape both change). Six operational org artifacts migrated across five spec repos + thingalog. Canonical-orgs library entry migrated. CONTRIBUTING.md substantive rewrite. openbraid Phase E pauses pending this proposal landing, then refactors against the new target shape (which turns out to be SIMPLER for openbraid to implement, not harder).

## Motivation

### The transportability gap is the symptom; the substrate-shape miss is the cause

openbraid Phase E E2 (job artifact ingestion) surfaced that ingesting an org as one logical unit requires bundling multiple `.openthing` files: the orgdef artifact PLUS each job artifact under `<project>/org/jobs/`. The current convention treats these as separate transportable units; ingesting them as a coherent org requires either a multi-file upload UX, a zip-or-envelope wrapper at the export layer (Path A), or a substrate-shape correction (Path B).

Path A solves the symptom (export bundles multiple files). Path B addresses the underlying substrate-shape miss: an organization IS atomically one thing (a charter + its positions + their specializations). Splitting it into the orgdef-openthing + N job-openthings was a 0.x experimental shape that didn't match the substrate's catalog primitive.

### Director's framing — atomic-transportable was the original intent

Director's exact framing 2026-05-10: "I thought orgdefs were `.opencatalog`, not `.openthing`? So that they were transportable?" Followed by: "An orgdef should be an atomic thing." The substrate-shape correction is recovering documented-but-not-implemented original intent, not a new design direction. The 0.x evolution (charter-shape-additions, role-vs-job-distinction, canonical-template v1.0/1.1/1.2/1.3, placement convention, naming convention) refined orgdef internals while leaving the substrate-shape choice unexamined. This proposal closes that gap before the family grows further.

### The 1.0 landing point

orgdef SCHEMA has been pre-1.0 (currently v0.3.0) signaling "still experimentally evolving." With the substrate-shape correction landing, the spec stabilizes at its intended foundation. SCHEMA v1.0.0 is the correct version-bump: this is the original-intent substrate shape landing as the foundation for everything downstream. Future evolution (`forward_work_items[]`, structured cross-org references, `x.position.lifecycle` promotion, sub-org linking per the deferred memory note) becomes post-1.0 minor additions.

### Window of opportunity — only six artifacts to migrate

Director's relevant framing: "Fortunately since we are still in the development phase, I am the only user." The family currently has six operational orgdef artifacts:

1. `orgdef-spec/org/orgdef-spec-organization.openthing` (orgdef-strategist seat home)
2. `memodef-spec/org/memodef-spec-organization.openthing`
3. `roledef-spec/org/roledef-spec-organization.openthing`
4. `catdef-spec/org/catdef-spec-organization.openthing`
5. `thingalog/org/thingalog-organization.openthing` (first non-spec adopter)
6. `openbraid-org/org/openbraid-org.openthing` (precipitating product; itself an OAGP-family-shaped org)

Plus the canonical-orgs library entry `orgs/catdef-org.openthing` (Tier 2 of the prior naming-convention decision; this proposal folds it in).

Plus the canonical-template at `proposed-orgs/oagp-family-open-standard.openthing` (the source template all five spec orgs derive from).

Migrating eight artifacts before broader adoption is dramatically cheaper than migrating eighty. The window is now.

## Proposed Change

### P1. orgdef artifact shape is `.opencatalog` not `.openthing`

The substrate shape for an `orgdef:Organization` artifact is the catdef substrate's `.opencatalog` format, not `.openthing`. An orgdef IS a catalog of items (positions, role-specialization jobs) bound by catalog-level metadata (the org's charter — mission, vision, scope, governance, values, red lines, recommended patterns, relationships).

### P2. Catalog-level fields vs items (Director-ratified design)

**Catalog-level (org-charter fields, present in EVERY orgdef.opencatalog):**

- `catdef`, `orgdef`, `type: "orgdef:Organization"`, `id`, `name`, `version` — substrate envelope + identification
- `mission`, `vision`, `scope`, `governance_model` — narrative org-level fields
- `values[]`, `red_lines[]`, `recommended_patterns{}` — structured org-level guidance
- `relationships[]` — typed edges between positions (catalog-level array; positions referenced by id)
- `metadata{}` — license, authors, history, derived_from, repository, homepage, extracted_from, etc.

**Items (each carries a catdef substrate type tag):**

- `{ "type": "orgdef:Position", "id": "<pos-id>", ... }` — one item per position in the org
- `{ "type": "roledef:Job", "id": "<job-id>", "version": "<v>", ... }` — one item per job specialization; referenced from positions via `position.job_definition: { id, version }`

Position items reference role definitions and job definitions:

```json
{
  "type": "orgdef:Position",
  "id": "implementer",
  "name": "Implementer",
  "status": "staffed",
  "role_definition": { "id": "senior-project-oriented-software-engineer", "version": "1.0.0", "url": "https://roledef.org/roledefs/senior-project-oriented-software-engineer.openthing" },
  "job_definition": { "id": "implementer", "version": "1.0.0" },
  "description": "...",
  "incumbent": { ... }
}
```

`role_definition` keeps the URL (roledefs are external; resolved via roledef.org).
`job_definition` becomes `{ id, version }` only — no URL needed because the job is an item in the SAME opencatalog. URL is optional fallback for cross-org reference cases.

Job items contain the full job artifact content:

```json
{
  "type": "roledef:Job",
  "id": "implementer",
  "version": "1.0.0",
  "charter": "...",
  "identity": "...",
  "voice": "...",
  "output_contract": [...],
  "guardrails": [...],
  "metadata": { "role_definition": {...}, "org_definition": {...}, "placement": {...}, "license": "MIT", ... }
}
```

This is the EXISTING `roledef:Job` shape verbatim, just embedded as an item rather than authored as a separate file.

### P3. Filename convention: `<id>-organization.opencatalog`

Same `-organization` suffix discipline shipped 2026-05-01 in the operational-org-artifact-naming-convention decision, just new extension. Examples:

- `orgdef-spec/org/orgdef-spec-organization.opencatalog`
- `thingalog/org/thingalog-organization.opencatalog`
- `openbraid-org/org/openbraid-org-organization.opencatalog`

Job artifact files DELETE after migration. The `<project>/org/jobs/<job-id>.openthing` files no longer exist as standalone — their content lives as items in the parent org's opencatalog.

### P4. orgdef SCHEMA v1.0.0 rewrite

SCHEMA.md substantively rewrites to:

- Define orgdef:Organization as opencatalog-shape (not openthing-shape)
- Define orgdef:Position item shape (the MUST/SHOULD fields per position)
- Reference roledef:Job item shape (the existing roledef spec's Job type embeds naturally; cross-spec coordination with roledef-strategist captured below)
- Define catalog-level field requirements (MUST/SHOULD per the prior pre-1.0 evolution, now codified)
- Define inheritance via `metadata.derived_from` (existing pattern; carries forward unchanged)
- Define `metadata.kind: "operational" | "canonical-template"` enforcement per kind

Major-version bump: 0.3.0 → 1.0.0. Pre-1.0 readers MUST NOT silently accept v1.0.0+ artifacts (substrate shape differs); v1.0.0+ readers MAY provide a v0.x → v1.0.0 migration assist for archived artifacts but the migration is the adopter's responsibility.

### P5. Canonical-template migration

`proposed-orgs/oagp-family-open-standard.openthing` → `proposed-orgs/oagp-family-open-standard.opencatalog`. Version 1.3.0 → 2.0.0 (major bump; substrate-shape change). instantiation_notes (11) and (13) update to reference the new shape; recommended_patterns.general entries inherited verbatim; values/red_lines/recommended_patterns inheritance shape unchanged.

The canonical template demonstrates the opencatalog shape as the reference for derivers.

### P6. Operational org migrations (6 artifacts + 1 canonical-library entry + 1 canonical-template)

| Repo | Source artifacts | Target |
|---|---|---|
| `orgdef-spec/orgdef/` | `org/orgdef-spec-organization.openthing` + `org/jobs/orgdef-strategist.openthing` | `org/orgdef-spec-organization.opencatalog` |
| `memodef-spec/memodef/` | `org/memodef-spec-organization.openthing` + `org/jobs/` (currently empty placeholder) | `org/memodef-spec-organization.opencatalog` |
| `roledef-spec/roledef/` | `org/roledef-spec-organization.openthing` + `org/jobs/` (currently empty placeholder) | `org/roledef-spec-organization.opencatalog` |
| `catdef-spec/` | `org/catdef-spec-organization.openthing` + `org/jobs/` (currently empty placeholder) | `org/catdef-spec-organization.opencatalog` |
| `thingalog/` | `org/thingalog-organization.openthing` + `org/jobs/implementer.openthing` + `org/jobs/product-strategist.openthing` | `org/thingalog-organization.opencatalog` |
| `openbraid-org/openbraid/` | `org/openbraid-org.openthing` + `org/jobs/openbraid-director.openthing` + `org/jobs/openbraid-engineer.openthing` + `org/jobs/openbraid-strategist.openthing` | `org/openbraid-org-organization.opencatalog` |

Plus:
- Canonical-orgs library: `orgs/catdef-org.openthing` → `orgs/catdef-org.opencatalog` (also resolves the Tier-2 deferral from the prior naming-convention decision; folded in)
- Canonical-template: `proposed-orgs/oagp-family-open-standard.openthing` → `proposed-orgs/oagp-family-open-standard.opencatalog`

For each migration: read the existing `.openthing` orgdef artifact, read the N job artifacts, compose into a single `.opencatalog` with positions + jobs as items, preserve all org-level metadata, append a `metadata.history` entry recording the substrate-shape migration, bump the artifact's `version` field (major bump). Delete the old `.openthing` files + `org/jobs/` directories. Commit per repo with `orgdef-strategist@orgdef.org` author identity.

### P7. CONTRIBUTING.md substantive rewrite

The placement convention, filename convention, derivation discipline all update to reflect the opencatalog shape. The previously-shipped sections (Inter-position communication conventions, Operational org-artifact filename conventions, Canonical OAGP position addressing) carry forward with shape-updated examples. New section: "Job artifacts as items, not files" explaining that `<project>/org/jobs/` directory is RETIRED — job content lives as items inside the parent orgdef.opencatalog.

### P8. openbraid Phase E refactor (cross-spec coordination)

openbraid Phase E is paused per the URGENT memo to openbraid-engineer (2026-05-10 11:00). When this proposal's decision lands:

- E1 ingest path: target `.opencatalog`, not `.openthing`-bundle. Simpler.
- E2: disappears as a separate path. Jobs are local items inside the orgdef.opencatalog; ingested as part of E1.
- E3 unchanged: roledefs still external.
- E4 unchanged: three-level URL semantics still apply.
- E5: simpler. Export = serve the stored opencatalog.

Net effect for openbraid: Phase E gets **simpler**, not harder.

## Backward Compatibility

**Substantial break.** v0.x orgdef.openthing artifacts are NOT readable by v1.0.0 readers. v1.0.0+ readers MAY provide migration tooling but the migration is the adopter's responsibility. Pre-1.0 artifacts in the wild (currently: the 6 operational artifacts in OAGP-family repos + 1 canonical-library entry + 1 canonical-template — all listed in P6) get migrated as part of this proposal.

**Why a clean break is acceptable here:** Director's "I am the only user" framing during development phase. Six artifacts to migrate; one human; no external adopter constraints. The cost of a clean break now is dramatically lower than the cost of carrying v0.x compatibility shims forward indefinitely. The window for breaking changes closes when external adopters land; we are still inside that window.

Strict-writer / lenient-reader (catdef family precedent): v1.0.0+ writers MUST emit v1.0.0+ shape; v1.0.0+ readers MAY accept v0.x artifacts via a documented migration helper, but MUST NOT silently treat v0.x artifacts as v1.0.0 (the shapes are different; silent acceptance would mask real bugs).

## Conformance Tests

Conformance fixtures in `orgdef-spec/orgdef/conformance/`:

- **`valid_orgs/`** — exemplar v1.0.0 opencatalog orgdef artifacts demonstrating the new shape. Each of the 6 migrated operational artifacts can serve as a conformance fixture.
- **`invalid_orgs/`** — counterexamples (e.g., orgdef.opencatalog missing required catalog-level fields; position items with missing id; job items with `type: roledef:Job` but missing `charter` field).
- **`runtime_evidence/`** — per-runtime conformance evidence (openbraid Phase E ingestion success + boot payload composition + export round-trip serves as the first runtime evidence file).

## Alternatives Considered

### Alt 1: Path A (export-layer multi-file bundle)

Solve transportability at the export layer: openbraid (and any tooling) bundles the orgdef.openthing + N job.openthing files as a zip-or-envelope payload at export/transport time. The on-disk shape stays `.openthing` per artifact; the over-the-wire shape is bundled.

Rejected by Director 2026-05-10 ("Path B, all the way"). Path A solves the symptom but leaves the substrate-shape miss in place; the family's "an org is one atomic thing" intent gets buried in export-layer wrapper code rather than landing in the substrate where it belongs.

### Alt 2: Defer to a future v0.4 → v1.0 migration window

Continue 0.x evolution; defer the opencatalog shape correction until 1.0 ships for other reasons.

Rejected: the window of "one user, six artifacts to migrate" closes as external adopters arrive. Deferring makes the eventual migration more expensive. Director's "we are still in development phase" framing is the right time-sensitivity read.

### Alt 3: Keep `.openthing`, add `inherits_from` and other catalog-shape features inline

Stay with `.openthing` substrate; add fields normally found in `.opencatalog` (items array, inherits_from, etc.) directly to the orgdef:Organization openthing shape.

Rejected: this is `.opencatalog` shape with a `.openthing` filename. Either the family adopts the substrate's catalog primitive cleanly, or it doesn't. Half-measure increases confusion, not clarity.

### Alt 4: Major version 0.4.0 instead of 1.0.0

Bump minor for the substrate-shape change.

Rejected: substrate-shape change is not a minor concern. v1.0.0 is the right framing because this IS the foundation landing — pre-1.0 was experimental; 1.0.0 is the substrate-aligned foundation. Future evolution (forward_work_items, sub-org linking, etc.) becomes post-1.0 minor additions.

## Open Questions

Director ratified the four key design decisions inline 2026-05-10:

- **OQ1 — Jobs as items with type tag vs inline objects:** Director ratified items-with-type-tag (each thing has substrate identity; inline would be more compact but less substrate-aligned).
- **OQ2 — SCHEMA major-version 1.0.0 or 0.4.0:** Director ratified 1.0.0 (original-intent landing).
- **OQ3 — Relationships catalog-level array vs items:** Director ratified catalog-level array (lightweight; promote to items only if relationships gain richer structure).
- **OQ4 — Operational org version bumps:** each org bumps major (e.g., thingalog 1.3.3 → 2.0.0) reflecting substrate-shape change. Per-artifact history entry records the migration.

No further OQs invited; the proposal is decision-ready. orgdef-maintainer review remaining for schema-conformance checks and any drafted text refinement.

## Cross-spec coordination

- **catdef-strategist:** orgdef-as-opencatalog is consistent with catdef substrate (opencatalog IS a substrate primitive); no catdef changes needed. Informational notification once decision lands.
- **roledef-strategist:** the `roledef:Job` type is now embedded as items in orgdef.opencatalog rather than authored as standalone `.openthing` files. roledef SCHEMA stays unchanged (Job type definition is the same; just embedding context differs). Informational notification once decision lands; if roledef-strategist wants to add commentary in roledef CONTRIBUTING.md about jobs-as-items vs jobs-as-files, that's their call.
- **memodef-strategist:** no direct impact on memodef-spec. memo addressing (deferred OQ3 from the prior addressing proposal) still scopes to memodef-side companion when ready.
- **openbraid-engineer:** URGENT pause memo sent 2026-05-10 11:00 (`memos/inbox/2026-05-10-1100-...`). Will follow with a Phase E refactor-target memo once this proposal's decision lands.
- **render.catdef.org team:** rendering target shifts from .openthing to .opencatalog for orgdefs. Should be a small renderer change since opencatalog rendering is already supported; just need to ensure orgdef:Organization opencatalog type renders cleanly with position+job items.

## References

- Director-driven strategic conversation 2026-05-10 in orgdef-strategist chair
- Originating problem (openbraid Phase E E2 transportability gap discovery): the 10:00 + 10:30 memos to openbraid-strategist + the 11:00 pause memo to openbraid-engineer in openbraid-org/openbraid/memos/inbox/
- Path A vs Path B framing: prior conversation captured Director's "An orgdef should be an atomic thing" and "This is my failure, I did not notice that we had not done this" + "we are still in development phase, I am the only user"
- Prior placement-convention decision (filename convention this proposal extends to .opencatalog): [`decisions/proposal-operational-org-artifact-naming-convention.md`](../decisions/proposal-operational-org-artifact-naming-convention.md)
- Prior canonical-orgs-library decision (Tier-2 rename folded in): [`decisions/proposal-canonical-orgs-library.md`](../decisions/proposal-canonical-orgs-library.md)
- Prior canonical OAGP addressing decision (URL semantics unaffected by substrate-shape change; URLs still resolve to position items): [`decisions/proposal-canonical-oagp-position-addressing.md`](../decisions/proposal-canonical-oagp-position-addressing.md)
- catdef substrate spec (opencatalog primitive this proposal adopts): [`https://github.com/catdef/catdef-spec/blob/main/CATIO_SPEC.md`](https://github.com/catdef/catdef-spec/blob/main/CATIO_SPEC.md)
- Operational org artifacts to migrate (6 + canonical-library + canonical-template; all enumerated in P6)
