# Proposal Decision: Canonical orgdefs library

**Disposition:** Accept with Modifications
**Origin:** [proposals/canonical-orgs-library.md](../proposals/canonical-orgs-library.md)
**Decided:** 2026-04-26 by orgdef-strategist
**Companion submission:** [proposed-orgs/aigp-family-open-standard.openthing](../proposed-orgs/aigp-family-open-standard.openthing) — first canonical template, ready for promotion to `canonical-orgs/` upon acceptance
**Cross-spec:** Sibling-spec coordination (roledef's `sample-jobs/` precedent acknowledged; this proposal adopts a parallel pattern with intentional naming difference). Memo to roledef-strategist forthcoming as informational notification (no roledef-side action required).
**Bootstrap caveat:** Same-head provenance (orgdef-strategist + roledef-strategist held by one head during catdef-family bootstrap). Per discipline, the artifact trail still goes through orgdef's `proposals/` and `decisions/`; this decision is the orgdef-side decision-of-record.

## Disposition

The canonical-orgs library proposal — adding the `canonical-orgs/` directory, the `metadata.kind` field on `orgdef:Organization`, and orgdef-specific derivation conventions — is **Accepted with two modifications**. The first canonical template (`aigp-family-open-standard`) is **strategist-cleared for promotion** via the standard two-stage workflow upon SCHEMA.md/CONTRIBUTING.md updates landing.

The two modifications tighten Open Question 4 (which MUSTs are template-relaxed) and resolve the slot-placeholder convention question with a more durable convention than the proposal's informal `[SLOT: ...]` strings.

## Rationale

### Why Accept

The Director's foreshadowed work (lift the orgdef-spec orgdef into a canonical template; derive catdef-spec, roledef-spec, and future spec orgs from it) is the recursive completion of the dogfood. The motivation is empirically grounded — four imminent operational orgdefs (orgdef-spec already authored; catdef-spec, roledef-spec, memodef-spec forthcoming) share substantial structural commonality that authoring-from-scratch would duplicate and invite drift.

The directory-split pattern (`canonical-orgs/` sibling of `orgs/`) follows brother-roledef's just-accepted precedent (`sample-jobs/` sibling of `roledefs/`) with one intentional naming difference (`canonical-orgs` vs `sample-orgs`) reflecting the stronger-than-sample function templates serve.

The `metadata.kind` field disambiguates content that survives file movement; locations alone are convention. The additive-only derivation conventions mirror roledef's git-fork derivation discipline, which has worked well there and generalizes cleanly.

The seven open questions are largely answerable inline; resolutions below.

### Why Modifications

The proposal's `[SLOT: ...]` placeholder convention works pragmatically (the first canonical template uses it) but is brittle against tooling: validators can't easily distinguish "the author wrote `[SLOT: 1-2 sentence statement of...]` because it's a slot" from "the author wrote text containing the literal string `[SLOT:` for some other reason." Open Question 3 invited bikeshed; the convention deserves a small structural promotion before the canonical-orgs library starts accumulating templates.

Open Question 4 (which MUSTs are template-relaxed) needs an explicit list rather than the proposal's "validators MUST NOT enforce required-field MUSTs that don't make sense for templates." Vague-by-validator-discretion is exactly the kind of latitude that produces inconsistent enforcement across implementations.

## Resolutions to Open Questions

### OQ1 → keep `canonical-orgs`

**Strategist call: keep.** Author's weak preference. The "stronger-than-sample" framing is real — these aren't demonstration artifacts, they're canonical references. Modest cross-family inconsistency with roledef's `sample-jobs/` is acceptable. (Future reconciliation: roledef may evolve `sample-jobs/` toward a canonical framing as its use case matures; cross-family naming alignment can happen then.)

### OQ2 → closed enum `{operational, canonical-template}` for v0.3

**Strategist call: closed.** Author's weak preference. Extension via `x.<domain>.kind` is sufficient for niche distinctions. Closed enum keeps validator behavior predictable.

### OQ3 → Promote slot convention from `[SLOT: ...]` strings to a structured `__slot__` convention (M1 below)

See Modification M1.

### OQ4 → Explicit list of template-relaxed MUSTs (M2 below)

See Modification M2.

### OQ5 → Slot-fill inheritance for `recommended_roles`

**Strategist call: inheritance with slot-fill.** The canonical's `recommended_roles` table includes `[SLOT: spec-name]-maintainer` and similar slot-shaped entries. Derivers fill the slot; the entry stays. Replacement (rewriting the entry) is allowed only when the entry doesn't apply to the deriver's context (e.g., a deriver who legitimately doesn't need a maintainer can drop the entry — but this is rare).

### OQ6 → Cross-spec coordination flagged for parallel work (no action required)

**Strategist call: noted, no action this cycle.** Roledef may want similar derivation conventions for jobs (operational-job-derived-from-sample-job). Flagged as parallel work in the memo to roledef-strategist. Not blocking this proposal.

## Modifications

### M1. Promote slot placeholder convention from `[SLOT: ...]` strings to structured `__slot__` objects

**Background:** The proposal's `[SLOT: description]` string convention works for the first canonical template but is fragile: validators can't distinguish slot-placeholder strings from incidental occurrences; tooling that wants to enumerate slots (for derivation-assistance UIs) needs to parse free-form prose; refactoring slot conventions requires search-and-replace across canonical templates.

**Modification:** Use a structured `__slot__` object as the placeholder convention:

```json
{
  "mission": {"__slot__": true, "description": "1–2 sentences stating what THIS spec defines and the artifact it produces", "example": "Define X in an open, machine-readable way..."}
}
```

For string-type fields, the slot object is recognized by validators as a placeholder; for structured fields (e.g., positions array), each element MAY be a slot object that gets replaced wholesale during derivation.

Validator behavior:
- For `metadata.kind: canonical-template` artifacts: SHOULD permit `__slot__` objects in any field; SHOULD NOT enforce string-type or structured-type checks on slot-shaped values
- For `metadata.kind: operational` artifacts: MUST NOT contain `__slot__` objects (operational artifacts have all slots filled)

The `[SLOT: ...]` string convention is acceptable as a pragmatic interim form when authoring; the first canonical template uses it. A migration to `__slot__` objects is a follow-on patch the orgdef-maintainer drafts after the canonical-orgs library proposal lands.

**Resolves:** OQ3.

### M2. Explicit list of template-relaxed MUSTs in SCHEMA.md

**Background:** OQ4 invited a list of which MUSTs are template-relaxed. The proposal said "validators MUST NOT enforce required-field MUSTs that don't make sense for templates" without specifying which. Implementors will guess inconsistently.

**Modification:** SCHEMA.md MUST list, for `metadata.kind: canonical-template` artifacts, the strict-vs-relaxed status of each currently-required field:

| Field | For canonical-template |
|---|---|
| `catdef`, `orgdef`, `type`, `id`, `name`, `version` | STRICT (always required) |
| `metadata.kind` | STRICT (must be `canonical-template`) |
| `mission` | RELAXED (may be a `__slot__` object) |
| `positions` | RELAXED (entries may be slot-shaped; required minimum count of 1 is relaxed to 0+) |
| `relationships` | RELAXED (same as positions) |
| `metadata.created`, `metadata.license`, `metadata.authors` | STRICT (provenance required for canonical artifacts) |

Other recommended fields follow their normal SHOULD discipline whether the artifact is operational or canonical-template.

**Resolves:** OQ4.

## Final shape (post-modifications)

Schema additions:

```json
{
  "metadata": {
    "kind": "operational | canonical-template",
    "derived_from": {"id": "...", "version": "...", "url": "..."}
  }
}
```

Plus the `__slot__` object convention for placeholder values:

```json
{
  "mission": {"__slot__": true, "description": "<what to fill in>", "example": "<optional example>"}
}
```

Plus the explicit STRICT/RELAXED MUSTs table above.

Plus the additive-only derivation conventions table from the proposal (REPLACE / REFINE / INHERIT discipline per field).

Plus the directory: `canonical-orgs/` as sibling of `orgs/` and `proposed-orgs/`.

## Build directive (for orgdef-maintainer)

When schema work begins:

1. **orgdef SCHEMA.md update** — add `metadata.kind` field; document derivation conventions per the proposal's table; add the `__slot__` object convention; add the STRICT/RELAXED MUSTs table; add validator-behavior notes per kind.

2. **orgdef CONTRIBUTING.md update** — document `canonical-orgs/` directory; explain operational-vs-canonical-template distinction; document canonical-template submission workflow (same two-stage as operational, promotes to `canonical-orgs/` instead of `orgs/`); document derivation submission expectations (PR description includes which canonical was derived from).

3. **Conformance fixtures** — per the proposal's Conformance Tests section.

4. **Validator updates** — per the proposal's validator-behavior section + M1/M2 additions: `__slot__` object recognition for canonical-templates; rejection of `__slot__` objects in operational artifacts; STRICT/RELAXED MUSTs enforcement per kind.

5. **Promote first canonical template** — `proposed-orgs/aigp-family-open-standard.openthing` to `canonical-orgs/aigp-family-open-standard.openthing` per the standard two-stage workflow, with a `decisions/aigp-family-open-standard.md` decision artifact recording the promotion rationale.

6. **Migrate the first template's slot convention** — patch `proposed-orgs/aigp-family-open-standard.openthing` (or the promoted version) to use `__slot__` objects instead of `[SLOT: ...]` strings per M1. May happen in the same PR as the promotion or a follow-on; maintainer's call.

7. **Version bump** — orgdef SCHEMA from v0.2.0 to v0.3.0 (additive minor).

## Companion submission: `aigp-family-open-standard`

The first canonical template ([proposed-orgs/aigp-family-open-standard.openthing](../proposed-orgs/aigp-family-open-standard.openthing)) is **strategist-cleared** for promotion via the standard two-stage workflow upon this proposal's acceptance.

**Strategist sign-off recorded:**

- Schema-conformant against the post-modifications shape (catdef envelope, all STRICT MUSTs present, valid `orgdef:Organization` type, `metadata.kind: canonical-template`)
- Generalization correctly preserves AIGP-family invariants (values, red_lines, recommended_patterns) verbatim from the orgdef-spec source
- Slot placement is sensible (mission, scope, position descriptions are slot-shaped; vision and governance_model use partial-slot phrasing for inheritability)
- Quality clean (rationales preserved on values/red_lines/recommended_patterns; instantiation_notes provide derivation guidance)

**Two flags for the maintainer at promotion time:**

1. The artifact uses the v0.3.0 `metadata.kind` field but currently lives in `proposed-orgs/`. Validation against current v0.2 schema would flag the `kind` field as unrecognized. Acceptable — the artifact is forward-compatible by design (catdef substrate's lenient-reader rule applies). Resolves once schema lands.
2. The artifact uses the `[SLOT: ...]` string convention rather than the M1-promoted `__slot__` object form. Acceptable as the interim convention; migration to `__slot__` form happens per build-directive item 6.

**Recommendation to maintainer:** route through standard two-stage workflow. Promote to `canonical-orgs/aigp-family-open-standard.openthing` once SCHEMA.md/CONTRIBUTING.md updates land. No further strategist gate required.

## Cross-spec coordination

A courtesy memo to roledef-strategist follows this decision filing. Two items for awareness:

1. The directory-split pattern (`canonical-orgs/` for orgdef parallels `sample-jobs/` for roledef) — naming is intentionally divergent (canonical vs sample) reflecting orgdef's stronger template framing
2. The derivation conventions for orgdefs may eventually want a parallel articulation for roledef jobs (operational-job-derived-from-sample-job) — flagged as parallel work, not blocking

action_required: false (informational).

## Foreshadowed downstream work (separate proposals)

Per Acceptance Criteria #6:

1. **Derive `catdef-spec/catdef-spec-org/orgdef.openthing`** from `aigp-family-open-standard` (separate proposal in catdef-spec or in the catdef-org context per the catdef-family pattern)
2. **Derive `roledef-spec/roledef-spec-org/orgdef.openthing`** from `aigp-family-open-standard`
3. **Derive memodef and other AIGP-family member specs** as they bootstrap further
4. **Migration of the first canonical template's slot convention** from strings to `__slot__` objects per M1

## References

- Originating proposal: [proposals/canonical-orgs-library.md](../proposals/canonical-orgs-library.md)
- Companion submission: [proposed-orgs/aigp-family-open-standard.openthing](../proposed-orgs/aigp-family-open-standard.openthing)
- Source artifact (the source for generalization): [orgdef-spec-org/orgdef.openthing](../orgdef-spec-org/orgdef.openthing)
- Sibling-spec precedent: [`roledef-spec/roledef/decisions/proposal-role-vs-job-distinction.md`](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-role-vs-job-distinction.md) (M3 added `sample-jobs/`)
- Sibling-spec derivation conventions: [`roledef-spec/roledef/SCHEMA.md`](https://github.com/roledef-spec/roledef/blob/main/SCHEMA.md) — `metadata.derived_from` rules
- Originating Director foreshadowing: 2026-04-26 conversation, "the last recursive piece is going to be to draft our first model orgdef, based on your/our orgdef organization."
