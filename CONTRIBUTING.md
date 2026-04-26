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

## Strategist bot identity

The orgdef-strategist role (forthcoming as a derivation of [`senior-open-standards-strategist`](https://roledef.org/roledefs/senior-open-standards-strategist.openthing)) operates under the bot identity `orgdef-strategist <orgdef-strategist@orgdef.org>` for commits and decision-artifact authorship. This is provisional pending governance ratification (Known Work Item, inherited from the catdef-family pattern).

## Cross-spec coordination

When an orgdef-level decision affects another catdef-family spec (e.g., a new position type that would benefit from a new roledef field, or a relationship type that requires substrate-level catdef support), the orgdef-strategist coordinates with the affected spec's strategist (catdef-strategist for substrate; roledef-strategist for role-definition concerns). Decision artifacts cross-reference each other.

## Known work items inherited from catdef-family

- **Strategist bot identity ratification** — provisional pending governance
- **Validator-as-CI-step automation** — until then, strategist self-validates in validator capacity
- **Auto-generation of `catalog.opencatalog`** — currently hand-maintained
- **Conformance test harness** — runtime-aware testing infrastructure deferred to v0.2+
