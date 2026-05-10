# Contributing to orgdef

orgdef is an open standard plus a community-curated reference library of organization-chart definitions. This document describes how to contribute — both new orgdef artifacts to the library and proposed changes to the spec.

## Governance

orgdef is stewarded independently of any single AI vendor or implementation. The standard exists to enable interoperability between AI runtimes and human organizations — not to codify any one vendor's organizational format.

**Vendors do not own the spec.** Anthropic, xAI, OpenAI, Google, Meta, and any future AI provider are equal citizens from orgdef's perspective. Each may propose changes; no one gets unilateral authorship.

**The library is curated; the spec is open.** The canonical library at `github.com/orgdef-spec/orgdef` (and its mirror at `orgdef.org`, once provisioned) is curated for quality, fit, and breadth. The orgdef schema itself is content-neutral and freely usable — anyone can publish their own orgdef library at any URL using the same format. Forks are welcome.

### AI-assisted maintenance

orgdef is maintained with AI-assisted review, following the pattern established by [catdef](https://github.com/catdef/catdef-spec) and [roledef](https://github.com/roledef-spec/roledef). Routine work — drafting validation reports, reviewing submissions, applying patch-level fixes — is drafted by Claude sessions operating under roles defined in [CLAUDE.md](CLAUDE.md). Merges to `main`, schema version bumps, and governance decisions are made only by human maintainers through the normal pull-request review process.

## Two kinds of contribution

Contributions to orgdef fall into two categories:

1. **Org submissions** — adding a new orgdef artifact to the library
2. **Spec proposals** — proposing changes to the orgdef schema, the contribution process, or governance rules

## 1. orgdef submissions

### The two-stage workflow

orgdef artifacts follow a two-stage process via the `proposed-orgs/` and `orgs/` directories:

- `proposed-orgs/` — submissions in flight; publicly visible but not yet promoted to canonical
- `orgs/` — the canonical library; all entries here have passed validation and review

**Submission steps:**

1. **Fork** the repo
2. **Author your orgdef artifact** following the schema in [SCHEMA.md](SCHEMA.md) and the procedure in this document
3. **Add the file** to `proposed-orgs/<your-org-id>.openthing` in your fork
4. **Open a PR** against `main`
5. **Validation runs** — produces a validation report posted on the PR
6. **Maintainer review** — checks scope, quality, library fit, attribution
7. **Strategist sign-off** — required for borderline cases (scope-edge, library-fit calls)
8. **Promotion at merge** — the maintainer atomically:
   - Moves the file from `proposed-orgs/` to `orgs/`
   - Adds the entry to `catalog.opencatalog`
   - Adds a decision artifact to `decisions/<id>.md`
9. **Merge**

Once merged, the orgdef artifact is part of the canonical library and is available via `github.com/orgdef-spec/orgdef/blob/main/orgs/<id>.openthing`.

### Validation expectations

A submission MUST pass:

- **Schema validation** — all MUST fields present per [SCHEMA.md](SCHEMA.md), correct catdef wrapping, valid versioning, no reserved namespace misuse, internal consistency rules satisfied (every `relationship.from` and `relationship.to` resolves to a position id in the same artifact, etc.)
- **Roledef-reference resolution** — every `position.role_definition` reference (id + version + url) MUST resolve to an actual published roledef at the cited URL. Broken references are a FAIL condition.

A submission SHOULD pass:

- **Roledef-coverage on key positions** — at least the structurally-load-bearing positions in the org SHOULD have `role_definition` references. Informal positions (no role_definition) are acceptable in v0.1 bootstrap but signal incomplete authoring.
- **Connected graph** — positions and relationships SHOULD form a connected graph; disconnected sub-graphs may indicate authoring errors

### Quality bar

The library is curated. Even valid submissions may be rejected for:

- **Redundancy** — the library already has good coverage of this org class
- **Scope** — the org is too narrow (only useful for one specific user) or too broad ("a generic organization") or outside orgdef's intended scope
- **Quality** — the artifact authoritatively describes the org but the org structure itself is incoherent (vague relationships, undefined authority, etc.)

If your orgdef is rejected for the canonical library, you can still publish it at any URL using the same format. Curation is not censorship.

### What goes in `proposed-orgs/`

- Files MUST be valid `.openthing` files conforming to [SCHEMA.md](SCHEMA.md)
- Filenames MUST match the org's `id` field exactly: `<id>.openthing`
- IDs MUST be unique across `proposed-orgs/` AND `orgs/`
- Each submission SHOULD include (in the PR description):
  - The org's source — extracted from a real organization? Authored from documented practice? Designed from scratch?
  - Roledef-reference accounting — which positions have `role_definition` references; for those that don't, why not (intentional informality vs forward work)
  - Validation plan — schema check + roledef-reference resolution

## 2. Spec proposals

Changes to the orgdef schema, the contribution process, or governance rules use a separate workflow via the `proposals/` directory.

### When to propose

- The schema is missing a field your org-class genuinely needs (and it doesn't fit as `x.<domain>.<identifier>` extension)
- A standard relationship type has unintended consequences you've experienced empirically
- The contribution workflow has friction preventing legitimate contributions
- A new conformance test would catch a class of validation failures the current tests miss

### When NOT to propose

- **Domain-specific features.** If your use case is expressible as `x.<domain>.<identifier>`, use that. The schema stays minimal on purpose.
- **Wishlist items without a concrete use case.** "Wouldn't it be cool if..." without empirical motivation gets deferred.
- **Vendor-specific accommodations.** orgdef is runtime-agnostic.

### Proposal artifact format

Each proposal is a markdown file in `proposals/`, named `<short-name>.md`. The format includes Summary, Motivation, Proposed Change, Backward Compatibility, Conformance Tests, Alternatives Considered, and Open Questions.

### Proposal workflow

1. **Open** — file the proposal as a PR adding `proposals/<name>.md`
2. **Discuss** — open period for community/maintainer/strategist input
3. **Iterate** — the proposal is refined based on feedback
4. **Decide** — the orgdef-strategist files a decision in `decisions/proposal-<name>.md`: Accept | Accept with Modifications | Reject | Defer
5. **Implement** (if accepted) — the orgdef-maintainer drafts the actual schema change as a follow-on PR
6. **Version bump** — accepted spec changes bump the orgdef schema version per the rules in [SCHEMA.md](SCHEMA.md#versioning)

## Conventions for safe references

When your orgdef artifact references a roledef (in `position.role_definition`):

- **Pin to a specific version.** Use `id` + `version` + `url`; avoid floating references (no "latest").
- **Verify the URL resolves.** A roledef-reference that 404s is a broken graph; treat broken references as a FAIL condition.
- **Mirror the reference's pinning conventions.** Same shape as roledef's `metadata.derived_from`.

When your orgdef artifact references another orgdef artifact (cross-org coordination):

- v0.1 leaves cross-org references informal — declare via `coordinates_with` relationship type and a free-form `description`. v0.2+ may formalize a structured cross-org reference shape.

## Test suite (conformance)

Conformance fixtures live in `conformance/`:

- `valid_orgs/` — exemplar orgdef artifacts that demonstrate proper schema usage
- `invalid_orgs/` — counterexamples that demonstrate common errors validators must catch
- `runtime_evidence/` — per-runtime test outputs documenting how a given runtime behaves with orgdef artifacts (deferred to v0.2+ when runtime-aware tooling lands)

Contributors authoring new fixtures SHOULD add a brief README in the fixture's directory explaining what aspect of the schema the fixture exercises.

## Inter-position communication conventions

Per the canonical recommended_patterns.general entry "memos/ as the universal inter-position communication channel" (canonical-template v1.2.0), operational orgdefs SHOULD use `memos/` at the working-repo root for inter-position memos. Adopters whose layout makes this impractical (monorepos, vendor-imposed directory conventions, unusual deployment shapes) MAY declare an alternative path via the `x.org.memo_location` extension on the orgdef:Organization artifact:

```json
{
  "x.org.memo_location": "communications/inter-position/"
}
```

Validators SHOULD treat the path as relative to the artifact's working repo. The default convention when `x.org.memo_location` is absent is `memos/`. Sub-directory conventions within the location (e.g., maildir-style `inbox/`, `read/`, `archive/`) are governed by memodef-spec, not orgdef.

Adopters who previously created an alternative directory category for intra-org operational handoffs (e.g., `handoffs/`) SHOULD migrate those artifacts to `memos/` as memodef:Memo artifacts with `action_required: true`. The body content of the prior plain-text artifact carries forward as the memo's body string (or via `body_ref` to a sibling `.body.md` file per memodef v0.2+ ergonomics); metadata (from / to / subject / sent / action_required) wraps the existing content. Deletion of the prior directory completes the migration; intermediate states where both directories exist for the same artifact category SHOULD be avoided.

## Operational org-artifact filename conventions

Per the canonical-template v1.2.0 instantiation_notes (11), operational org-artifact files SHOULD be named `<id>-organization.openthing` and placed at `<project>/org/`. The `-organization` suffix encodes artifact type at the filename level so the file is self-readable in isolation; the `<id>` portion remains the org's machine identifier and matches the artifact's `id` field. Adopters whose layout makes `<project>/org/` impractical MAY declare an alternative path via the `x.org.org_location` per-org extension on the orgdef artifact, following the same escape-hatch pattern as `x.org.memo_location`. Default convention when the extension is absent is `<project>/org/<id>-organization.openthing`.

Job artifacts (`roledef:Job` per the role-vs-job distinction) live at `<project>/org/jobs/<job-id>.openthing` — no `-organization` suffix; job artifacts are self-typed via the `roledef:Job` type tag.

Adopters whose operational orgdef artifact uses the prior convention `<project>/org/<id>.openthing` (no suffix; the v1.1.0 placement convention) SHOULD migrate to `<project>/org/<id>-organization.openthing` when convenient. The artifact's `id` field is unchanged; only the filename gains the suffix. Cross-spec references that resolve org artifacts by id (e.g., `metadata.org_definition.id` in `roledef:Job` artifacts) remain valid; cross-spec references that resolve by URL (e.g., `metadata.org_definition.url`) MUST update to the new filename path.

The parallel canonical-orgs library convention (`<project>/orgs/`) currently uses a `-org` suffix on its first artifact; alignment with the operational `-organization` suffix is deferred to the v0.3 SCHEMA bundle.

## Canonical OAGP position addressing

Per the canonical-template v1.3.0 recommended_patterns.general entry "Canonical OAGP position addressing (URL-as-instruction)," OAGP-family positions are canonically addressed via URLs with three levels:

| Level | URL shape | Returns |
|---|---|---|
| Account | `<scheme>://<host>/<account>` | Ordered list of orgs the account hosts |
| Org | `<scheme>://<host>/<account>/<org>` | Ordered list of positions in this org |
| Position | `<scheme>://<host>/<account>/<org>/<position>` | Fresh-agent boot payload for this position |

Two-segment URLs (`<scheme>://<host>/<account>/<position>`) accepted as syntactic sugar when an account hosts exactly one org; resolves to the implicit org's position. (Mirrors GitHub's `github.com/<user>/<repo>` convention when `<user>` is a single-repo user.)

### Cross-protocol equivalence

The URL shape is protocol-agnostic. Examples:

- **https (git-hosted):** `https://github.com/scott/thingalog/blob/master/org/jobs/product-strategist.openthing` — for git-hosted orgs the canonical URL IS the GitHub blob URL.
- **mcp (openbraid-hosted):** `mcp.openbraid.app/scott/thingalog/product-strategist`
- **mcp (self-hosted openbraid):** `mcp.firstchurch.org/treasurer` (two-segment sugar; account hosts one org)

### Position list ordering at `<account>/<org>` — depth-first path walk

Position lists are ordered by depth-first path walk through the org-chart hierarchy, following work-stream from authority to execution to validation, then moving to sibling branches. Example for a hypothetical sales-org:

1. Strategist (authority root)
2. Implementer (execution under strategist)
3. QA (validation of implementer)
4. Marketing (sibling branch — strategist-led)
5. Sales Strategy (sibling branch — strategist-led)
6. Sales Ops (execution under sales strategy)

Rationale: a fresh AI reading the position list orients on strategy first, then execution, then verification, before context-switching to a parallel branch. Robust against shallow-vs-deep org variation.

### `x.org.org_location` extension shape

The extension carries the canonical hosting location with protocol discrimination. Single-location form (default):

```json
{
  "x.org.org_location": {
    "protocol": "git",
    "url": "https://github.com/scott/thingalog"
  }
}
```

Mirror-list form (orgs maintaining git + openbraid simultaneously):

```json
{
  "x.org.org_location": [
    { "protocol": "git", "url": "https://github.com/scott/thingalog", "authoritative": true },
    { "protocol": "mcp", "url": "mcp.openbraid.app/scott/thingalog", "authoritative": false }
  ]
}
```

When `authoritative: true` is declared on a list entry, that location is the source-of-truth; others are mirrors and SHOULD sync from authoritative. Mirror-list is steady-state (not migration-only) for orgs that want both auditability (git) AND mass-market accessibility (openbraid).

Backward compatibility: tools that read the prior path-only string form of `x.org.org_location` (shipped 2026-05-01 in the inter-position-communication-convention decision) SHOULD treat it as `{ "protocol": "filesystem", "url": "<path>" }` for backward inference; new orgs SHOULD write the structured form.

### Self-host parity

`mcp.openbraid.app` is the default openbraid host but not the only one. Self-hosted openbraid instances live at any host (`mcp.firstchurch.org`, `org.acmecorp.com`, etc.) and speak the same protocol. URL scheme + host segments are interchangeable; the path-shape (`/<account>/<org>/<position>`) and semantics are invariant. This matches the family's anti-lock-in discipline applied at the hosting layer (parallel to the canonical-orgs-library "vendors do not own the spec" framing applied at the spec layer).

### URL-as-instruction prompt collapse

A consequence of canonical position addressing: the fresh-agent instantiation prompt collapses to one invariant shape regardless of context — `"You are <name>. Read <url> for your full assignment."` The URL determines the protocol; the protocol determines the access mechanism (https GET, MCP call, etc.); the response payload determines the agent's behavior. Variant-explosion (separate prompt shapes per runtime / per protocol) is not necessary.

### Full-fidelity export as anti-lock-in escape valve

An org hosted on openbraid (or any hosted service) can export its full orgdef artifact at any time as a portable `.openthing` file. The exported artifact can be republished elsewhere (git repo, self-hosted openbraid, archived as a static file, transferred to a different hosting service). This is the load-bearing property that prevents hosting from becoming lock-in: the artifact is portable; the hosting is choice.

## Strategist bot identity

The orgdef-strategist role (forthcoming as a derivation of [`senior-open-standards-strategist`](https://roledef.org/roledefs/senior-open-standards-strategist.openthing)) operates under the bot identity `orgdef-strategist <orgdef-strategist@orgdef.org>` for commits and decision-artifact authorship. This is provisional pending governance ratification (Known Work Item, inherited from the catdef-family pattern).

## Cross-spec coordination

When an orgdef-level decision affects another catdef-family spec (e.g., a new position type that would benefit from a new roledef field, or a relationship type that requires substrate-level catdef support), the orgdef-strategist coordinates with the affected spec's strategist (catdef-strategist for substrate; roledef-strategist for role-definition concerns). Decision artifacts cross-reference each other.

## Known work items inherited from catdef-family

- **Strategist bot identity ratification** — provisional pending governance
- **Validator-as-CI-step automation** — until then, strategist self-validates in validator capacity
- **Auto-generation of `catalog.opencatalog`** — currently hand-maintained
- **Conformance test harness** — runtime-aware testing infrastructure deferred to v0.2+
