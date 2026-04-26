# orgdef Schema — v0.1.0

This document defines the structure and validation rules for **orgdef artifacts**: portable, machine-readable specifications of organizational structure, expressed as catdef-compliant `.openthing` files.

An orgdef artifact describes an organization completely enough that:

- A reader (human or AI) can reconstruct the organization's structure: who has what authority, who reports to whom, what relationships exist between roles
- The relationships between positions can be machine-traversed (graph queries, visualization, validation)
- Position role-definitions are interoperable with the [roledef](https://github.com/roledef-spec/roledef) library (positions reference roledefs by id+url)
- The org chart can be rendered, validated, and forked independently

This schema is the **load-bearing artifact** for orgdef. Everything else (this README, CONTRIBUTING, CLAUDE) is built around it.

---

## Conformance language

This document uses RFC 2119 keywords:

- **MUST** / **MUST NOT** — required for conformance; absence or violation makes the artifact invalid
- **SHOULD** / **SHOULD NOT** — recommended; well-designed orgdefs follow these but they are not required for validity
- **MAY** — permitted; an author's choice with no recommendation either way

The schema also uses catdef's `x.` extension namespace pattern. Fields prefixed with `x.<domain>.<identifier>` are extensions — defined by adopters, not by the orgdef spec, and ignored by runtimes that don't recognize them.

---

## Substrate: catdef

An orgdef artifact is a catdef `.openthing` document. catdef provides the structural format; orgdef defines the semantic shape inside that format. Every orgdef artifact MUST:

- Be a valid catdef document (parseable as JSON conforming to catdef structural rules)
- Declare the catdef version it stamps under (`catdef` field)
- Declare the orgdef schema version it conforms to (`orgdef` field)
- Have its `type` set to one of the orgdef-namespaced types (`orgdef:Organization` for a single org; `orgdef:Library` for a catalog of orgs)

Beyond these constraints, orgdef inherits catdef's full semantic toolkit (field types, polymorphic translatable fields, subcat enrichment, extension namespace, forward-compatibility rules, policy compliance).

---

## File extensions

orgdef artifacts use the catdef substrate's universal formats:

```
catdef-org.openthing                ← single organization
catdef-family.opencatalog           ← catalog of organizations
```

---

## Top-level structure: `orgdef:Organization`

```json
{
  "catdef": "1.4",
  "orgdef": "0.1.0",
  "type": "orgdef:Organization",
  "id": "<short-identifier>",
  "name": "<human-readable name>",
  "version": "<semver>",

  "mission": "...",
  "scope": "...",
  "governance_model": "...",

  "positions": [...],
  "relationships": [...],

  "metadata": {...},

  "x.<domain>.<identifier>": ...
}
```

---

## Required fields (MUST) — `orgdef:Organization`

Every `orgdef:Organization` artifact MUST have all of the following fields, with non-empty values.

### `catdef` (string, semver)

The catdef version the artifact stamps under. Per catdef's writer-strict stamping rule (CA-002), the writer MUST declare the minimum catdef version that defines every feature used.

```json
"catdef": "1.4"
```

### `orgdef` (string, semver)

The orgdef schema version this artifact conforms to. Used by validators to apply the correct schema rules.

```json
"orgdef": "0.1.0"
```

### `type` (string, fixed value)

MUST be exactly the string `"orgdef:Organization"` for a single-org artifact, or `"orgdef:Library"` for a catalog of orgs.

```json
"type": "orgdef:Organization"
```

### `id` (string)

Short, kebab-case identifier for the organization. Used in filenames, URLs, and cross-references. MUST be unique within its publishing namespace (e.g., within `github.com/orgdef-spec/orgs/`).

```json
"id": "catdef-org"
```

### `name` (string or polymorphic)

Human-readable name of the organization. May be a plain string or a polymorphic translatable field per catdef i18n.

```json
"name": "catdef + roledef ecosystem"
```

### `version` (string, semver)

The artifact's own version (separate from the schema version).

```json
"version": "1.0.0"
```

### `positions` (array of `orgdef:Position` objects)

The roles/seats in the organization. Every orgdef MUST declare at least one position. See **Position structure** below.

```json
"positions": [
  { "id": "strategist", "name": "Strategist", ... },
  { "id": "maintainer", "name": "Maintainer", ... },
  ...
]
```

### `relationships` (array of `orgdef:Relationship` objects)

Typed edges between positions. Every orgdef MUST declare at least one relationship (otherwise the org is just a list of disconnected roles, which is rarely useful and signals incomplete authoring). See **Relationship structure** below.

```json
"relationships": [
  { "type": "reports_to", "from": "strategist", "to": "human-steward" },
  { "type": "validates_for", "from": "validator", "to": "contributor" },
  ...
]
```

---

## Recommended fields (SHOULD) — `orgdef:Organization`

### `mission` (string)

One- or two-sentence statement of what the organization exists to do. Used for org-level orientation.

```json
"mission": "Steward the catdef substrate spec and the catdef-family consumer specs as open standards."
```

### `scope` (string)

What the organization covers and explicitly excludes. Distinguishes this org from adjacent orgs.

```json
"scope": "catdef substrate + roledef + future catdef-family consumer specs (orgdef, openmemo, openorg, aigp). Out of scope: AWS Thinkbox OpenJD, Oracle Open Agent Specification, chrisbarry/openagent — adjacent specs in different technical domains."
```

### `governance_model` (string)

How decisions get made in this org. Brief; details belong in CONTRIBUTING.md / CLAUDE.md per spec.

```json
"governance_model": "Bounded AI authority + human-maintainer ratification. AI sessions draft, validate, decide, sign off; human maintainers merge. Vendors do not own the spec."
```

### `metadata` (object)

Authorship, licensing, attribution, version history, related orgs.

```json
"metadata": {
  "authors": ["..."],
  "license": "MIT",
  "created": "2026-04-26",
  "extracted_from": "...",
  "related": ["..."],
  "homepage": "https://orgdef.org/orgs/<id>",
  "repository": "https://github.com/orgdef-spec/orgdef/blob/main/orgs/<id>.openthing",
  "history": [...]
}
```

---

## Position structure (`orgdef:Position`)

Each entry in the `positions` array is a position object.

### Required fields (MUST)

#### `id` (string)

Short, kebab-case identifier for the position. Used in `relationships` to reference this position. Unique within the org.

```json
"id": "catdef-strategist"
```

#### `name` (string)

Human-readable name of the position.

```json
"name": "catdef Strategist"
```

#### `status` (enumerated string)

The current operational status of the position. One of:

- `staffed` — currently occupied by an incumbent (human, AI session arc, or other agent)
- `vacant` — defined but not currently occupied
- `shared` — occupied by multiple incumbents simultaneously
- `informal` — operationally active but not yet formalized (no incumbent declared)

```json
"status": "staffed"
```

### Recommended fields (SHOULD)

#### `role_definition` (object)

Reference to the roledef that defines what this position IS. Object with `id` + `version` + `url`. The url SHOULD point at a canonical roledef library URL.

```json
"role_definition": {
  "id": "catdef-strategist",
  "version": "2.0.0",
  "url": "https://roledef.org/roledefs/catdef-strategist.openthing"
}
```

When a position has no `role_definition` reference, the position's behavior is informal — the position exists but its role hasn't been roledef-extracted. This is acceptable for v0.1 bootstrapping; orgdefs SHOULD migrate informal positions to roledef-referenced positions over time.

#### `incumbent` (string or object)

Who currently occupies the position. May be a string (free-form name or session arc identifier) or an object with structured fields (name, kind: human/ai/group, contact, etc.). v0.1 leaves this loosely typed; future spec versions may tighten.

```json
"incumbent": "scott (human steward)"
```

```json
"incumbent": {
  "kind": "ai",
  "session_arc": "session that bootstrapped catdef + roledef + orgdef across 2026-04-25 to 2026-04-26",
  "portable": true,
  "portable_via": "https://roledef.org/roledefs/catdef-strategist.openthing"
}
```

#### `description` (string)

Brief description of what this position does within this organization specifically (organization-specific framing, complementary to but distinct from the roledef's role-level description).

#### `notes` (string or array)

Free-form notes about the position — informal context, history, transitional state.

---

## Relationship structure (`orgdef:Relationship`)

Each entry in the `relationships` array is a relationship object.

### Required fields (MUST)

#### `type` (enumerated string)

The kind of relationship. orgdef v0.1 defines these standard types:

- `reports_to` — hierarchical authority. `from` is subordinate; `to` is authority.
- `peer_of` — collaborative co-equal. Symmetric; both `from` and `to` are at the same level.
- `derives_from` — derivation lineage. `from` is the derived role; `to` is the parent. Mirrors roledef's `metadata.derived_from` at the org level.
- `validates_for` — validator → contributor pattern. `from` validates submissions from `to`.
- `implements_for` — implementor → spec pattern. `from` implements work that `to` strategically directs.
- `coordinates_with` — cross-spec or cross-org coordination. Symmetric; both `from` and `to` are coordinating equals.
- `drafts_for` — drafter → ratifier pattern. `from` produces drafts; `to` ratifies / merges.

Custom relationship types MAY be expressed via the `x.` extension namespace (e.g., `x.healthcare.consults_for`). Standard types SHOULD be preferred when applicable.

```json
"type": "reports_to"
```

#### `from` (string)

The position id at the source of the relationship.

```json
"from": "catdef-strategist"
```

#### `to` (string)

The position id at the target of the relationship.

```json
"to": "human-steward"
```

### Recommended fields (SHOULD)

#### `description` (string)

Brief description of the specific relationship in this org's context. Distinguishes orgs that share the same relationship type but apply it differently.

```json
"description": "Strategist drafts decisions and signs off; human steward merges. No autonomous merge authority."
```

#### `bidirectional` (boolean, default false)

For inherently symmetric relationship types (`peer_of`, `coordinates_with`), `bidirectional: true` declares the relationship explicitly so renderers know to draw it as undirected. Asymmetric types (`reports_to`, `validates_for`, etc.) leave this unset (defaults to false / directed).

---

## Top-level structure: `orgdef:Library`

A catalog of orgdef artifacts, used to index multiple orgs published by the same publisher. Same shape as catdef catalogs.

```json
{
  "catdef": "1.4",
  "orgdef": "0.1.0",
  "type": "orgdef:Library",
  "id": "<library-id>",
  "name": "<human-readable name>",
  "description": "...",
  "version": "<semver>",
  "data": {
    "items": [
      {
        "id": "<org-id>",
        "name": "...",
        "version": "...",
        "description": "...",
        "file": "orgs/<org-id>.openthing",
        ...
      }
    ]
  },
  "metadata": {...}
}
```

---

## Extension fields (`x.` namespace)

orgdef artifacts MAY include any number of extension fields under the `x.<domain>.<identifier>` namespace. Per the catdef-family self-description SHOULD-rule, each extension SHOULD carry a `description` field for naive-agent handling.

Plausible extensions (illustrative, not normative):

```
"x.legal.jurisdiction": "..."
"x.governance.charter_url": "..."
"x.org.fiscal_year": "..."
"x.org.compensation_band": {...}
"x.healthcare.licensing_required": [...]
```

---

## Reserved namespaces

The following namespaces are reserved by the orgdef spec and MUST NOT be used as adopter extensions:

- `orgdef:*` — reserved for orgdef spec types and fields
- `catdef:*` — reserved by catdef substrate
- `x.orgdef.*` — reserved for orgdef-spec-coordinated extensions

Adopters use their own `x.<domain>.<identifier>` namespaces.

---

## Internal consistency rules

A valid orgdef artifact MUST:

1. Have at least one `position` and at least one `relationship`
2. Have every `relationship.from` and `relationship.to` resolving to a position id within the same artifact
3. Stamp a `catdef` version that defines every catdef feature used (writer-strict)
4. Have unique position ids within the artifact

A valid orgdef artifact SHOULD:

1. Have at least one position with a `role_definition` reference (otherwise the artifact is a structure-only org with no role-behavior context — sometimes legitimate, often a sign of incomplete authoring)
2. Have positions and relationships that together form a connected graph (disconnected sub-graphs may indicate authoring errors; intentional sub-graphs SHOULD be split into separate orgdef artifacts)
3. Use standard relationship types when the relationship matches one; reserve `x.<domain>.<identifier>` extensions for genuinely domain-specific relationships

---

## Future considerations (not in v0.1)

These have come up in design discussion but are deferred to v0.2+:

- **Authority boundaries.** Per-position `does_what` / `does_not_do_what` arrays mirroring roledef's `x.governance.boundary`. Worth promoting once 2-3 orgdefs have authored these informally.
- **Time-bounded relationships.** `valid_from` / `valid_to` on relationships and positions for orgs that change over time.
- **Cross-org references.** When this org coordinates with another org (e.g., catdef-org coordinates with the broader open-standards-org community), reference by id+url with declared relationship.
- **Visualization hints.** `x.orgdef.layout_hints` for renderers that want author-suggested positioning.
- **Conformance levels.** Multi-level conformance (L1: structural; L2: relationship-graph traversable; L3: full role-definition resolution).

These belong to v0.2+ and will be triaged as orgdef matures.

---

## Versioning

orgdef follows semver:

- **Patch** (0.1.X): clarifications, editorial fixes, no behavior changes
- **Minor** (0.X.0): new optional fields, new standard relationship types, backward-compatible additions
- **Major** (X.0.0): breaking changes (removed required fields, changed semantics)

The schema version is independent from any individual artifact's `version` field.

---

## Examples

### Minimal `orgdef:Organization`

```json
{
  "catdef": "1.4",
  "orgdef": "0.1.0",
  "type": "orgdef:Organization",
  "id": "minimal-org",
  "name": "Minimal Example",
  "version": "1.0.0",
  "positions": [
    { "id": "leader", "name": "Leader", "status": "staffed" },
    { "id": "member", "name": "Member", "status": "staffed" }
  ],
  "relationships": [
    { "type": "reports_to", "from": "member", "to": "leader" }
  ]
}
```

### Position with full role_definition reference

```json
{
  "id": "catdef-strategist",
  "name": "catdef Strategist",
  "status": "staffed",
  "role_definition": {
    "id": "catdef-strategist",
    "version": "2.0.0",
    "url": "https://roledef.org/roledefs/catdef-strategist.openthing"
  },
  "incumbent": {
    "kind": "ai",
    "session_arc": "bootstrapping session 2026-04-25 to 2026-04-26",
    "portable": true,
    "portable_via": "https://roledef.org/roledefs/catdef-strategist.openthing"
  },
  "description": "Stewards the catdef substrate spec and coordinates catdef-family ecosystem decisions."
}
```

### Standard relationship types in use

```json
{ "type": "reports_to", "from": "catdef-strategist", "to": "human-steward", "description": "Drafts and signs off; steward merges." }
{ "type": "peer_of", "from": "catdef-strategist", "to": "roledef-strategist", "description": "Sister strategist roles; both derived from senior-open-standards-strategist.", "bidirectional": true }
{ "type": "derives_from", "from": "catdef-strategist", "to": "senior-open-standards-strategist", "description": "Derived per roledef metadata.derived_from declaration (catdef-strategist v2.0.0)." }
{ "type": "validates_for", "from": "roledef-validator", "to": "roledef-contributor", "description": "Validates schema-conformance of submitted roledefs." }
{ "type": "implements_for", "from": "catdef-canonical-implementor", "to": "catdef-strategist", "description": "Implements catdef.org Worker code per strategist build directives." }
{ "type": "coordinates_with", "from": "catdef-org", "to": "roledef-org-related-artifacts", "description": "Cross-spec coordination for substrate-vs-consumer decisions.", "bidirectional": true }
{ "type": "drafts_for", "from": "catdef-maintainer", "to": "human-steward", "description": "Drafts spec text (CATDEF_SPEC.md, etc.); steward merges." }
```

---

## Status

**v0.1.0 — bootstrap.** This schema is being authored alongside the first orgdef artifact (catdef-org). Both are likely to iterate as we discover what the schema actually needs to support. Stable shape expected by v0.1.x; substantive changes go through the proposal workflow per CONTRIBUTING.md.
