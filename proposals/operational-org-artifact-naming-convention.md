# Proposal: Operational org-artifact filename suffix `-organization`

**Status:** Filed (2026-05-01 by orgdef-strategist; awaiting maintainer review and decision artifact)
**Author:** orgdef-strategist (provisional bot identity pending governance ratification)
**Created:** 2026-05-01
**Target version:** canonical-template `oagp-family-open-standard.openthing` v1.2.0 (additive — adds an `instantiation_notes` clause; bundles with the inter-position v1.2.0 patch already in build directive); orgdef CONTRIBUTING.md prose addition; one-time migration of operational org-artifact filenames across the four spec repos + Thingalog
**Origin:** Director-surfaced observation 2026-05-01 — the operational placement convention `<spec>/org/<id>.openthing` (canonical-template v1.1, landed 2026-04-30) produces filenames that read as the *product* rather than the *organization* when the org's id matches a product name (e.g., `thingalog/org/thingalog.openthing` reads as describing Thingalog-the-product, not the Thingalog organization). Director ratified the directional call inline (proceed with `-organization` suffix; direct-execute mode authorized).

## Summary

Add the suffix `-organization` to operational org-artifact filenames: `<spec>/org/<id>-organization.openthing`. The filename's `<id>` portion remains the org's machine identifier (unchanged); the `-organization` suffix encodes artifact type at the filename level so the file is self-readable in isolation (file browser columns, search results, render.catdef.org cards, cross-references in commit messages and decision artifacts). The artifact's `id` field is unchanged — only the filename gains the suffix.

This proposal scopes to **operational org-artifact placement** (`<spec>/org/`). The parallel **canonical-orgs library** placement (`<spec>/orgs/<id>.openthing`) currently uses `-org` suffix on its first artifact (`catdef-org.openthing`); aligning canonical-library naming to `-organization` is deferred to the v0.3 SCHEMA bundle (where canonical-library entries face a separate filename-MUST-match-id constraint that cascades id changes into ~13 cross-references; better handled as a deliberate bundle than spread across multiple sessions).

## Motivation

### The friction is real

The convention "directory carries the type signal, filename is the identifier" works when path context is preserved. In path context, `thingalog/org/thingalog.openthing` reads correctly as "the Thingalog organization in the Thingalog repo." But filenames are routinely consumed in isolation:

- File browser columns (some layouts show only the filename, not the parent directory)
- Search result listings (filename-shaped excerpts)
- render.catdef.org cards (the renderer surfaces filename-as-title in some views)
- Cross-references in commit messages, memos, and decision artifacts (writers shorthand to the filename)
- IDE breadcrumbs (some breadcrumb formats truncate to the filename)

In isolation, `thingalog.openthing` lands as the product Thingalog, not the organization. The convention's discoverability fails the AI-legibility primacy hierarchy (memodef-spec's three-priority ordering: AI-to-AI > auditable > human-readable; "self-readable in isolation" sits on the AI-to-AI side, since the primary reader is a machine indexing artifacts across the family).

### Precedent already exists, partially

The canonical-orgs library entry `orgs/catdef-org.openthing` already uses a `-org` suffix. So one corner of the family does this; the operational `<spec>/org/` placements just don't (yet). This proposal closes the convention divergence on the operational side; the canonical-library side gets aligned in a v0.3 SCHEMA bundle (deferred per the Tier-2 reasoning below).

### Why `-organization` and not `-org`

- **AI-legibility primacy.** Explicit nouns beat abbreviations when the primary reader is a machine. `org` is also a TLD, a casual abbreviation, a Linux command (`org-mode`), and a GitHub-account naming pattern; `organization` is unambiguous.
- **Family precedent for full nouns.** `oagp-family-open-standard` not `oagp-fam-os`; `senior-open-standards-strategist` not `sr-os-strat`. The family already prefers explicit over abbreviated when the artifact is the canonical name.
- **9 chars is acceptable cost.** Filenames stay manageable (`orgdef-spec-organization.openthing` = 36 chars; `thingalog-organization.openthing` = 32 chars). Not a strain on standard tooling.

## Proposed Change

### P1. Canonical-template patch (bundled with inter-position v1.2.0)

Add to `proposed-orgs/oagp-family-open-standard.openthing` `metadata.instantiation_notes` (append; do not modify existing notes):

```
**Operational org-artifact filename convention.** Operational org-artifact files SHOULD be placed at `<spec>/org/<id>-organization.openthing` per the orgdef-spec org-artifact-naming-convention decision (2026-05-01). The `-organization` suffix encodes artifact type at the filename level so the file is self-readable in isolation; the `<id>` portion remains the org's machine identifier and matches the artifact's `id` field. Canonical-library placements (`<spec>/orgs/`) follow a parallel-but-distinct convention pending a v0.3 SCHEMA bundle alignment.
```

This patch bundles with the inter-position-communication-convention v1.2.0 patch already in the orgdef-maintainer build directive: BOTH changes land in canonical-template version `1.2.0`, applied as one cohesive update.

### P2. CONTRIBUTING.md prose addition

Add to `CONTRIBUTING.md` under the "Inter-position communication conventions" section (also being added per the inter-position decision; this proposal extends that section):

> **Operational org-artifact filename convention.** Operational org-artifact files SHOULD be named `<id>-organization.openthing` and placed at `<spec>/org/`. The `-organization` suffix is purely a filename-level disambiguation; the artifact's `id` field is unchanged from the org's machine identifier. Adopters whose layout makes `<spec>/org/` impractical MAY declare an alternative path via the `x.org.org_location` per-org extension on a separate orgdef artifact, following the same escape-hatch pattern as `x.org.memo_location`. Default convention when the extension is absent is `<spec>/org/<id>-organization.openthing`.

### P3. One-time migration of existing operational org artifacts

Five operational org artifacts to rename:

| Repo | Current path | New path |
|---|---|---|
| `orgdef-spec/orgdef` | `org/orgdef-spec.openthing` | `org/orgdef-spec-organization.openthing` |
| `memodef-spec/memodef` | `org/memodef-spec.openthing` | `org/memodef-spec-organization.openthing` |
| `roledef-spec/roledef` | `org/roledef-spec.openthing` | `org/roledef-spec-organization.openthing` |
| `catdef-spec` | `org/catdef-spec.openthing` | `org/catdef-spec-organization.openthing` |
| `thingalog` | `org/thingalog.openthing` | `org/thingalog-organization.openthing` |

For each artifact:
1. `git mv <old-path> <new-path>`
2. Update `metadata.repository` URL to reflect new path
3. Append entry to `metadata.history` recording the rename
4. Bump artifact `version` (additive; minor or patch — per-artifact at strategist's discretion)
5. id field UNCHANGED

### What's not changing

- The artifact's `id` field — stays as `orgdef-spec`, `memodef-spec`, `roledef-spec`, `catdef-spec`, `thingalog`. Cross-references using the id (e.g., `metadata.org_definition.id` in roledef:Job artifacts) remain valid.
- The directory `<spec>/org/` — singular, unchanged.
- Canonical-library `<spec>/orgs/<id>.openthing` placements — currently use `-org` suffix on `catdef-org.openthing`; Tier 2 work, deferred.
- The canonical template's existing `instantiation_notes` clauses — strictly additive append.

## Backward Compatibility

Strictly additive at the SCHEMA level (no SCHEMA changes). One-time migration breaks any pinned cross-spec reference that uses the OLD filename path; cross-references using the org's `id` (the recommended pattern, per existing canonical-template guidance) are unaffected because id is unchanged.

Audit of cross-spec id-vs-filename references (orgdef-strategist sweep before filing):
- `metadata.org_definition.url` in roledef:Job artifacts (e.g., `org/jobs/orgdef-strategist.openthing`'s job artifact) reference the org by URL: `https://github.com/orgdef-spec/orgdef/blob/main/org/orgdef-spec.openthing` — these MUST update to the new filename
- `metadata.repository` in each org artifact — same; updates as part of the rename
- README.md / CONTRIBUTING.md / SCHEMA.md prose references — update where they cite the example path

Migration completes when all five operational artifacts are renamed AND all `metadata.repository` + `metadata.org_definition.url` references are updated.

## Conformance Tests

No new conformance fixtures required. The renamed artifacts ARE the conformance evidence — five operational orgs across the OAGP family using the new convention.

## Alternatives Considered

### Alt 1: `-org` suffix (canonical-library precedent)

Use `-org` instead of `-organization`. Matches the existing `orgs/catdef-org.openthing` precedent; shorter (3 chars vs 12).

Rejected per AI-legibility primacy: explicit nouns beat abbreviations when the primary reader is a machine. The brevity savings (~9 chars per filename) doesn't outweigh the disambiguation value.

A side-effect of choosing `-organization` is that the canonical-library entry's `-org` suffix becomes a parallel-but-distinct convention pending Tier 2 alignment. That divergence is acceptable temporarily — both conventions are self-readable in their own right; Tier 2 will align them.

### Alt 2: Keep current convention; rely on directory context

Don't add the suffix; readers should consume filenames in path context.

Rejected: filename-in-isolation use cases (file browser, search, renderer cards, commit-message shorthand) are common enough that relying on path context fails AI-legibility primacy. The convention is currently failing those cases empirically; the Director-surfaced friction is the empirical signal.

### Alt 3: Add the suffix to the artifact's `id` field too (filename and id both gain `-organization`)

Change `id: thingalog` → `id: thingalog-organization` so filename matches id (matching the canonical-orgs-library convention).

Rejected: cascades id change into all cross-spec references (metadata.org_definition.id in every roledef:Job artifact pointing at this org; cross-spec memo references; SCHEMA-conformance validators). The cost-benefit is poor — the AI-legibility win is at the FILENAME level, not the id level. id is consumed in machine-readable references where its meaning is unambiguous (no product-vs-org ambiguity in `metadata.org_definition.id`). Keep id stable.

### Alt 4: Bundle with canonical-library (Tier 2 in same session)

Do canonical-library `catdef-org` rename + id change in the same session as operational rename.

Rejected: the canonical-library SCHEMA's filename-MUST-match-id constraint cascades the id change into 13 cross-references (memos, decisions, README files, SCHEMA.md, catalog.opencatalog, conformance fixtures). That's a substantive sub-project that's better bundled with the v0.3 SCHEMA work already pending (canonical-orgs-library `__slot__` migration, structured cross-org references, etc.). Doing canonical-library now in isolation produces a worse change-set than waiting and bundling.

## Open Questions

### OQ1. Should an `x.org.org_location` extension exist for adopters whose layout makes `<spec>/org/` impractical?

**Working position: yes, parallel to `x.org.memo_location`.** Same SHOULD-with-machine-discoverable-escape-hatch shape established in the inter-position-communication-convention decision. The CONTRIBUTING.md prose in P2 mentions this; formal documentation of the extension belongs in the same section.

**Resolution invited from:** maintainer review.

### OQ2. Should the artifact `version` bump be uniform (all five artifacts go to a synchronized version) or per-artifact?

**Working position: per-artifact.** Each org artifact has its own version-history-arc (orgdef-spec is at v1.0.0, Thingalog at v1.3.1, others vary). Forcing synchronization muddles the per-artifact history. Each artifact gets a minor bump from its current version to capture the rename; rationale recorded in `metadata.history`.

**Resolution invited from:** maintainer review.

### OQ3. Tier 2 (canonical-library rename) — when to schedule?

**Working position: bundle with v0.3 SCHEMA work.** The canonical-orgs-library v0.3 work is already pending (`__slot__` migration per canonical-orgs-library decision M1; `metadata.kind` enforcement; structured cross-org reference shape; etc.). Adding the canonical-library rename to that bundle is natural; the rename's id-cascading work is a similar shape to the `__slot__` migration's content-update work, so review effort consolidates.

**Resolution invited from:** future strategist-triage when v0.3 SCHEMA work activates.

## References

- Director ratification: 2026-05-01 conversation in orgdef-strategist chair, "Proceed, -organization, direct."
- Inter-position-communication-convention proposal (the prior 2026-05-01 placement-convention work): [`proposals/inter-position-communication-convention.md`](inter-position-communication-convention.md)
- Inter-position-communication-convention decision (the v1.2.0 canonical-template patch this proposal bundles with): [`decisions/proposal-inter-position-communication-convention.md`](../decisions/proposal-inter-position-communication-convention.md)
- Canonical-template v1.1 + placement-convention decision (the prior placement migration that established `<spec>/org/`): [`decisions/proposal-canonical-template-v1.1-and-placement-convention.md`](../decisions/proposal-canonical-template-v1.1-and-placement-convention.md)
- Canonical-orgs-library decision (filename-MUST-match-id constraint cited in motivation for Tier 2 deferral): [`decisions/proposal-canonical-orgs-library.md`](../decisions/proposal-canonical-orgs-library.md)
- Source artifacts to be renamed (five operational org files; one in each of the five OAGP-family + Thingalog working repos)
