# orgdef

**An open standard for organization-chart definitions.**

orgdef is a [catdef-family](https://github.com/catdef/catdef-spec) consumer specification for describing organizational structure: the roles in an organization, the relationships between them (reports-to, peer-of, derives-from, validates-for, implements-for, coordinates-with), the incumbents currently occupying each role (human, AI session, vacant), and the authority boundaries that govern the org.

orgdef sits in the catdef family alongside [roledef](https://github.com/roledef-spec/roledef):

- **catdef** is the substrate (open standard for catalog definitions)
- **roledef** describes individual AI roles (one role per artifact)
- **orgdef** describes how roles compose into organizations (one org chart per artifact, referencing roledefs by id+url for the roles it contains)

> **Status:** v0.1 bootstrap. Spec scaffolding only. The first orgdef artifact will be the catdef ecosystem org chart itself — same empirical-anchor pattern as roledef (DangerStorm anchored senior-jaded-vc-associate; the catdef + roledef bootstrap anchored senior-open-standards-strategist; the catdef-family ecosystem org will anchor orgdef).

## What's in an orgdef

An `orgdef:Organization` artifact captures:

- **Identity:** id, name, mission, governance model, scope
- **Positions** (`orgdef:Position`): the roles/seats in the org chart
  - Each position may carry a `role_definition` reference (id + version + url) pointing at a roledef that defines what the role IS
  - Each position has a `status` (staffed / vacant / shared)
  - Each position may name an `incumbent` (human, AI-session arc, role-portable per roledef)
- **Relationships:** typed edges between positions
  - `reports_to` — hierarchical authority
  - `peer_of` — collaborative co-equal
  - `derives_from` — derivation lineage (when one role is a specialization of another, mirroring roledef's `metadata.derived_from`)
  - `validates_for` — validator → contributor pattern
  - `implements_for` — implementor → spec pattern
  - `coordinates_with` — cross-spec / cross-org coordination
- **Cross-org references:** when this org collaborates with another org (e.g., catdef-org coordinating with roledef-org-related artifacts), reference by id+url

## What orgdef is NOT (yet)

- **Not a project-management tool.** orgdef describes *who has what authority*, not *who is doing what task*. Task tracking is out of scope.
- **Not an HR system.** orgdef describes roles + relationships, not personnel records, compensation, performance, etc.
- **Not a workflow engine.** orgdef captures structure; the `roledef` references describe behavior.
- **Not visualization.** v0.1 is spec-only. Rendering as a clickable org chart in [render.catdef.org](https://render.catdef.org) is a v0.2+ deliverable.

## File extensions

orgdef artifacts use the catdef substrate's universal formats:

- `<id>.openthing` for a single org definition (`type: "orgdef:Organization"`)
- `<id>.opencatalog` for a catalog of orgs (`type: "orgdef:Library"`)

The renderer at [render.catdef.org](https://render.catdef.org) auto-detects catdef-family namespaced types (per the change shipped in catdef.org PR #2) and renders orgdef artifacts as single-thing detail views without rendering changes. v0.2+ will add graph layout for the org chart visualization.

## Repository layout

```
orgdef/
├── README.md                           ← this file
├── SCHEMA.md                           ← v0.1 schema (orgdef:Organization, Position, relationship types)
├── CONTRIBUTING.md                     ← submission workflow + governance
├── CLAUDE.md                           ← AI-maintainer operating manual
├── LICENSE                             ← MIT
├── catalog.opencatalog                 ← canonical orgdef library index
├── orgs/                               ← canonical orgdef library
│   └── <id>.openthing
├── proposed-orgs/                      ← submission staging
│   └── <id>.openthing
├── decisions/                          ← strategist decision artifacts
│   ├── <id>.md
│   └── proposal-<name>.md
├── proposals/                          ← spec change proposals
│   └── <name>.md
└── conformance/                        ← conformance fixtures + runtime evidence
    ├── valid_orgs/
    ├── invalid_orgs/
    └── runtime_evidence/
```

## Governance

Same model as catdef + roledef:

- **The standard is open.** MIT-licensed; anyone can publish their own orgdef library at any URL using the same format.
- **The canonical library is curated.** Entries in `orgs/` go through the two-stage `proposed-orgs/` → `orgs/` workflow with strategist sign-off and human-maintainer merge.
- **Vendors don't own the spec.** No single AI vendor, runtime, or organization owns orgdef. Implementations are equal citizens.
- **Bounded AI authority.** AI-assisted maintenance follows the catdef-family pattern: AI sessions draft, validate, decide, sign off; human maintainers merge.

The strategist role for orgdef will be derived from [`senior-open-standards-strategist`](https://roledef.org/roledefs/senior-open-standards-strategist.openthing) — same abstract parent as catdef-strategist and roledef-strategist. (Forthcoming; once the bootstrap stabilizes.)

## Roadmap

**v0.1 (bootstrap, in flight):**
- [x] Repo scaffold + LICENSE
- [ ] SCHEMA.md skeleton (this PR scope)
- [ ] CONTRIBUTING.md skeleton
- [ ] CLAUDE.md skeleton
- [ ] First orgdef artifact: `catdef-org` — the catdef + roledef ecosystem as an orgdef:Organization (PR #1)
- [ ] orgdef-strategist roledef (derivation of senior-open-standards-strategist; PR #2 in roledef-spec/roledef)

**v0.2 (visualization):**
- [ ] Mermaid / graphviz rendering for org charts
- [ ] Interactive graph layout in render.catdef.org (clickable nodes drilling into roledefs)
- [ ] Multiple orgdef artifacts (catdef-org, plus one or two real-product orgs to validate the schema generalizes)

**v0.3+ (ecosystem):**
- [ ] Cross-org references (one org chart linking to another)
- [ ] Authority-boundary visualization (does/does-not heat-mapping per role)
- [ ] Runtime conformance evidence (does an orgdef-aware runtime correctly understand reports-to vs derives-from semantics?)

## Related specs

- [catdef](https://github.com/catdef/catdef-spec) — substrate spec
- [roledef](https://github.com/roledef-spec/roledef) — sister consumer spec; orgdef references roledef artifacts for role definitions

## Status

**v0.1 bootstrap.** The spec is being authored; nothing is canonical yet. Watch this space (and `decisions/` once it accumulates) to see the spec take shape.
