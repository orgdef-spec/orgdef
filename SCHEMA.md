# orgdef Schema — v1.0.0

This document defines the structure and validation rules for **orgdef artifacts**: portable, machine-readable specifications of organizational structure, expressed as catdef-compliant `.opencatalog` files.

An orgdef artifact describes an organization atomically — charter + position roster + role specializations bundled in one transportable file — so that:

- A reader (human or AI) can reconstruct the organization's structure: positions, relationships, governance, recommended patterns, values, red lines
- A fresh AI runtime can boot into a position with full context (org + role + job specialization + inbox state) from one file
- The org chart can be rendered, validated, exported, and migrated between hosting protocols (git ↔ openbraid ↔ future) without information loss
- Position role-definitions are interoperable with the [roledef](https://github.com/roledef-spec/roledef) library (positions reference roledefs by id+url) and job specializations live as items inside the same opencatalog

This schema is the **load-bearing artifact** for orgdef. The README, CONTRIBUTING, CLAUDE, and canonical template are built around it.

## Version 1.0.0 — substrate-shape landing

orgdef v0.x was experimental; the substrate-shape (`.openthing` per org + separate `.openthing` per job) didn't atomically transport. v1.0.0 corrects this by adopting the catdef substrate's `.opencatalog` primitive: one file carries the entire org. Pre-1.0 artifacts must be migrated; v1.0.0+ readers MUST NOT silently accept v0.x artifacts (substrate shape differs). Migration tooling is the adopter's responsibility.

---

## Conformance language

This document uses RFC 2119 keywords:

- **MUST** / **MUST NOT** — required for conformance; absence or violation makes the artifact invalid
- **SHOULD** / **SHOULD NOT** — recommended; well-designed orgdefs follow these but they are not required for validity
- **MAY** — permitted; an author's choice with no recommendation either way

The schema uses catdef's `x.` extension namespace pattern. Fields prefixed with `x.<domain>.<identifier>` are extensions — defined by adopters, not by the orgdef spec, and ignored by runtimes that don't recognize them.

---

## Substrate: catdef opencatalog

An orgdef artifact is a catdef `.opencatalog` document of type `orgdef:Organization`. catdef provides the structural format (catalog with items); orgdef defines the semantic shape (which items appear, what catalog-level fields the charter carries). Every orgdef artifact MUST:

- Be a valid catdef opencatalog document (parseable as JSON conforming to catdef structural rules)
- Declare the catdef version it stamps under (`catdef` field)
- Declare the orgdef schema version it conforms to (`orgdef` field; MUST be `"1.0.0"` or higher for v1.0.0+ shape)
- Have its `type` set to `"orgdef:Organization"` (or `"orgdef:Library"` for a catalog OF orgdefs — see Library section)

Beyond these constraints, orgdef inherits catdef's full semantic toolkit (field types, polymorphic translatable fields, extension namespace, forward-compatibility rules, policy compliance).

---

## File extensions

orgdef artifacts use catdef substrate's catalog format:

- `<id>-organization.opencatalog` — single organization (one orgdef:Organization per file)
- `<id>.opencatalog` — library/catalog of orgdefs (one orgdef:Library per file)

The `-organization` filename suffix (operational orgs) is per the 2026-05-01 operational-org-artifact-naming-convention decision. Canonical-library entries in `orgs/` use `<id>.opencatalog` without the suffix because their library context disambiguates.

---

## Top-level structure: `orgdef:Organization`

```json
{
  "catdef": "1.4",
  "orgdef": "1.0.0",
  "type": "orgdef:Organization",
  "id": "<short-identifier>",
  "name": "<human-readable name>",
  "version": "<semver>",

  "mission": "...",
  "vision": "...",
  "scope": "...",
  "governance_model": "...",

  "values": [...],
  "red_lines": [...],
  "recommended_patterns": {...},
  "relationships": [...],

  "items": [
    { "type": "orgdef:Position", ... },
    { "type": "orgdef:Position", ... },
    { "type": "roledef:Job", ... },
    ...
  ],

  "metadata": {...},

  "x.<domain>.<identifier>": ...
}
```

**Catalog-level fields** (mission, vision, scope, governance_model, values, red_lines, recommended_patterns, relationships, metadata) describe the org as a whole.

**Items** are the typed things that compose the org: positions (the roster) and jobs (the specializations).

---

## Required catalog-level fields (MUST)

Every `orgdef:Organization` artifact MUST have these catalog-level fields with non-empty values.

### `catdef` (string, semver)

The catdef version the artifact stamps under. Per catdef's writer-strict stamping rule (CA-002), the writer MUST declare the minimum catdef version that defines every feature used.

```json
"catdef": "1.4"
```

### `orgdef` (string, semver)

The orgdef schema version this artifact conforms to. For v1.0.0+ shape, MUST be `"1.0.0"` or higher.

```json
"orgdef": "1.0.0"
```

### `type` (string, fixed value)

MUST be exactly `"orgdef:Organization"` for a single-org artifact, or `"orgdef:Library"` for a library of orgs.

### `id` (string)

Short, kebab-case identifier for the organization. Used in filenames, URLs, and cross-references. MUST be unique within its publishing namespace.

### `name` (string or polymorphic)

Human-readable name. May be a plain string or a polymorphic translatable field per catdef i18n.

### `version` (string, semver)

The artifact's own version (separate from the schema version). Bumps on substantive content change per [versioning rules](#versioning).

### `mission` (string)

What the organization does. Single-paragraph statement, machine-readable.

### `governance_model` (string)

How decisions get made: who has what authority, who ratifies, who escalates. Substantive content (the catdef-family pattern: bounded AI authority + human Director ratification, but each org adapts).

### `items` (array of typed objects)

The roster + specializations that compose the org. Every orgdef MUST declare at least one item of type `orgdef:Position`. See **Items** section.

### `metadata` (object)

Provenance + history per catdef metadata convention. See **Metadata** section.

---

## Recommended catalog-level fields (SHOULD)

### `vision` (string)

Why the org exists; what world it's working toward. Often the OAGP-family-style two-clause structure (noun-phrase first clause + primary-reader-is-AI invariant clause).

### `scope` (string)

What the org covers and explicitly does NOT cover. Negative-scope-as-definition often clarifies positive scope.

### `values` (array of objects)

What the org cares about; load-bearing for tie-breaking decisions. Each value: `{ name, description, rationale }`.

### `red_lines` (array of objects)

What the org WILL NOT do, regardless of pressure. Each red_line: `{ rule, rationale }`.

### `recommended_patterns` (object)

Patterns the org recommends for adopters deriving from this orgdef. Two sub-arrays:
- `general`: structural patterns, each `{ pattern, description, rationale }`
- `recommended_roles`: roles the org recommends, each `{ role, priority, why }` where `role` is either a bare-string id or a coordinate object `{ id, version, url }`

### `relationships` (array of `orgdef:Relationship` objects)

Typed edges between positions. Lightweight; catalog-level array (not items). Each relationship: `{ type, from, to, description }` where `type` ∈ {`reports_to`, `peer_of`, `derives_from`, `validates_for`, `implements_for`, `coordinates_with`, `directs`}.

---

## Items: positions and jobs

Items are the typed things in the orgdef catalog. Each item MUST have a `type` field carrying a catdef-family substrate type tag.

### `orgdef:Position` item

A role/seat in the organization.

```json
{
  "type": "orgdef:Position",
  "id": "<position-id>",
  "name": "<human-readable>",
  "status": "staffed" | "vacant" | "shared",
  "role_definition": { "id": "...", "version": "...", "url": "..." } | null,
  "job_definition": { "id": "...", "version": "..." } | null,
  "description": "...",
  "incumbent": { ... } | null,
  "x.<domain>.<identifier>": ...
}
```

**Required position fields (MUST):**
- `type` — exactly `"orgdef:Position"`
- `id` — kebab-case, unique within the org's items
- `status` — one of `"staffed"`, `"vacant"`, `"shared"`

**Recommended position fields (SHOULD):**
- `name` — display name
- `description` — what the position does
- `role_definition` — reference to a canonical roledef (id + version + url). Roledefs are external (typically at roledef.org); resolved by fetch.
- `job_definition` — reference to an `orgdef:Job` item in the same opencatalog by `{ id, version }`. URL is optional fallback for cross-org reference cases. When the job is local (same opencatalog), URL MAY be omitted.
- `incumbent` — who currently occupies the position: `{ kind: "human" | "ai", identifier | session_arc, portable?, portable_via?, notes? }`

### `roledef:Job` item

A job specialization that binds an org-specific responsibility set to a position. Embedded in the orgdef.opencatalog rather than authored as a standalone file. Full `roledef:Job` shape per the roledef SCHEMA — including `charter`, `identity`, `voice`, `output_contract`, `guardrails`, `metadata.role_definition`, `metadata.org_definition`, `metadata.placement`.

```json
{
  "type": "roledef:Job",
  "id": "<job-id>",
  "version": "<semver>",
  "charter": "...",
  "identity": "...",
  "voice": "...",
  "output_contract": [...],
  "guardrails": [...],
  "metadata": {
    "role_definition": { "id": "...", "version": "...", "url": "..." },
    "org_definition": { "id": "...", "version": "...", "url": "..." },
    "placement": { "reports_to": "...", "directs": [...], "coordinates_with": [...] },
    ...
  }
}
```

The Job item's `id` MUST match the `job_definition.id` of the position it specializes. The Job item's `version` SHOULD match the position's `job_definition.version`.

For complete `roledef:Job` field definitions, see the [roledef SCHEMA](https://github.com/roledef-spec/roledef/blob/main/SCHEMA.md). The orgdef spec defers to roledef on Job item content; orgdef only specifies that Job items embed in the orgdef.opencatalog rather than living as separate files.

---

## Internal consistency (validators MUST check)

- Every `relationships[].from` and `relationships[].to` MUST resolve to a Position item's `id` in the same opencatalog.
- Every Position item's `job_definition.id` (when present) MUST resolve to a Job item's `id` in the same opencatalog (unless `job_definition.url` declares an external job).
- Position item `id`s MUST be unique within the opencatalog.
- Job item `id`s MUST be unique within the opencatalog.
- Position and Job ids MAY share names (a Position with id `implementer` and a Job item with id `implementer` is a common pattern — the position is specialized by the job of the same id).

---

## Metadata (catalog-level)

```json
"metadata": {
  "authors": ["..."],
  "license": "MIT",
  "created": "YYYY-MM-DD",
  "extracted_from": "...",
  "homepage": "...",
  "repository": "https://github.com/.../<id>-organization.opencatalog",
  "history": [
    { "version": "x.y.z", "date": "YYYY-MM-DD", "change": "..." }
  ],
  "derived_from": { "id": "...", "version": "...", "url": "..." },
  "kind": "operational" | "canonical-template",
  "v1_success_criterion": "..."
}
```

**Required (MUST):**
- `license` — SPDX-shaped license string

**Recommended (SHOULD):**
- `authors` — declared authorship
- `created` — original creation date
- `repository` — canonical URL where the artifact lives
- `history` — substantive evolution record
- `kind` — `"operational"` for adopted orgs; `"canonical-template"` for slot-shaped templates

`derived_from` (when present) declares lineage from a canonical-template or another orgdef. Carries `{ id, version, url }`.

---

## Versioning

orgdef SCHEMA semver:
- **Major** — breaking shape changes (e.g., v0.x → v1.0 substrate-shape correction; future v1.x → v2.0 would be a similarly breaking move)
- **Minor** — additive features (new optional fields, new item types, new relationship types)
- **Patch** — clarifications, editorial improvements, validator-behavior refinements

Per-artifact semver (the `version` field on each orgdef):
- **Major** — substantive shape change in the artifact (substrate-shape migration, position-roster restructure, governance-model overhaul)
- **Minor** — additive content (new position, new value, new pattern)
- **Patch** — editorial fixes, metadata.history updates, non-substantive refinement

---

## `orgdef:Library` (catalog of orgdefs)

A library aggregates multiple orgdefs by reference. Used for canonical-orgs collections.

```json
{
  "catdef": "1.4",
  "orgdef": "1.0.0",
  "type": "orgdef:Library",
  "id": "<library-id>",
  "name": "<human-readable>",
  "version": "<semver>",
  "description": "...",
  "items": [
    { "type": "orgdef:Reference", "id": "...", "version": "...", "url": "..." },
    ...
  ],
  "metadata": {...}
}
```

Library items are references, not embedded orgdefs (orgdefs at scale are large; libraries reference them by URL).

---

## Extension namespace

orgdef inherits catdef's `x.<domain>.<identifier>` extension pattern. Established extensions in the family:

- `x.org.org_location` — canonical hosting location with protocol discriminator + optional mirror list
- `x.org.memo_location` — per-org override for memo placement (default: `<project>/memos/`)
- `x.position.lifecycle` — position lifecycle marker (`"forward-looking"` | `"operational"` | `"transitional-shared"`)
- `x.position.linked_orgs` — sub-org linking at position nodes (deferred; future proposal)

Custom adopter extensions: any `x.<adopter-domain>.<identifier>`.

---

## Migration from v0.x

v0.x orgdef.openthing artifacts migrate to v1.0.0 orgdef.opencatalog as follows:

1. Open the v0.x orgdef.openthing artifact
2. Promote its top-level fields (mission, vision, scope, etc.) to catalog-level fields
3. Each entry in the old `positions[]` array becomes a `{ "type": "orgdef:Position", ... }` item in the new `items[]` array
4. For each Position with a `job_definition.url` pointing at a separate `<project>/org/jobs/<job-id>.openthing` file: open that job artifact, embed its content as a `{ "type": "roledef:Job", ... }` item in the same `items[]` array; replace the position's `job_definition` with `{ id, version }` (drop the URL since the job is local)
5. Bump the artifact's `version` major (substrate-shape change)
6. Bump the artifact's `orgdef` field to `"1.0.0"`
7. Rename the file from `<id>-organization.openthing` to `<id>-organization.opencatalog`
8. Append a `metadata.history` entry recording the substrate migration
9. Delete the old `<project>/org/jobs/` directory (its content now lives in items)

The five spec-org operational orgs + thingalog + openbraid-org + canonical-orgs library entry + canonical-template all migrated as part of the orgdef SCHEMA v1.0.0 ship (2026-05-10).
