# Proposal: Canonical-template v1.1 + operational orgdef placement convention

**Status:** Accepted (2026-04-30 by orgdef-strategist; see [decisions/proposal-canonical-template-v1.1-and-placement-convention.md](../decisions/proposal-canonical-template-v1.1-and-placement-convention.md))
**Author:** orgdef-strategist (provisional bot identity pending governance ratification)
**Created:** 2026-04-30
**Target version:** canonical-orgs `aigp-family-open-standard` v1.1.0 + orgdef CONTRIBUTING placement-convention guidance
**Origin:** Empirical findings from three independent derivations against canonical v1.0.0 (memodef-spec, roledef-spec, catdef-spec), surfaced in `orgdef-spec/orgdef-spec-org/memos/`. Plus Director-surfaced post-scaffold finding on org-folder naming.

## Summary

Bundles refinements to the `aigp-family-open-standard` canonical template based on three independent derivation experiences, plus a filesystem-convention change for operational orgdef placement that preserves cross-spec aggregation. All template revisions are content patches (no schema changes); the placement convention is a CONTRIBUTING-level documentation update plus a one-time migration of four spec repos (orgdef-spec, memodef-spec, roledef-spec, catdef-spec).

This proposal does NOT include orgdef SCHEMA additions surfaced from the same derivations (`forward_work_items[]`, `x.position.lifecycle` formal field promotion, structured cross-org reference shape per M3 deferral). Those land in a separate v0.3 schema proposal — different scope, different review path.

## Motivation

Three derivations against canonical v1.0.0 (memodef-spec, roledef-spec, catdef-spec) produced experience memos identifying recurring friction points. Several findings are triple-confirmed (strongest empirical signal); others surfaced once but are well-grounded. Synthesis is in `orgdef-spec/orgdef-spec-org/memos/2026-04-30-1700--orgdef-strategist--catdef-strategist--derivation-review-passes.openthing`.

Plus: post-scaffold conversation with the Director surfaced a structural problem with the current `<spec>/<spec>-org/orgdef.openthing` placement convention — all leaf nodes are uniformly named `orgdef.openthing`, which forecloses any aggregation that uses filenames as identifiers (MCP-mediated cross-spec queries, render.catdef.org-style multi-org browsing, family-wide indexing). Catdef-strategist's recommendation — `<spec>/org/<id>.openthing` matching the existing catdef-family library convention — solves the aggregation case while staying internally consistent with how every other catdef-family folder already behaves.

## Proposed Change

### Canonical-template v1.1 patches

**P1. Mission slot example: three shapes, not one.**

Current canonical example shape (bootstrap-only) misfit memodef (coordinative) and catdef (substrate). Add multiple example shapes:

```
[SLOT: 1–2 sentences stating what THIS spec defines and the open machine-readable artifact it produces. Example shapes by spec category:
- Bootstrap-shaped (loading-AI-into-role): "Define X in an open, machine-readable way that bootstraps any AI worker into Y with zero context backfill."
- Coordinative (inter-position handoff): "Define X-message exchange between positions in an open, machine-readable way that bootstraps a recipient AI session into an inter-position handoff with zero context backfill."
- Substrate (format-providing): "Define X in an open, machine-readable way that provides the substrate format on which consumer specs build."]
```

**P2. Vision slot: drop the orgdef-specific introduction-artifact clause.**

Current canonical's second clause — *"...when stakeholders engage with this spec's artifacts, they may exchange them as the introduction artifact between organizations"* — is orgdef-specific and was rewritten by all three follow-on derivers. Drop the clause; replace with neutral framing:

```
"Part of the AI Governance Pattern (AIGP) family — alongside catdef, roledef, orgdef, and memodef — defining the pattern of [SLOT: what aspect of AI-first organization this spec addresses]. The primary reader of [SLOT: this spec's primary artifact type] is an AI; [SLOT: any spec-specific framing of the cross-org or cross-runtime use case]."
```

**P3. Vision slot: subdivide into noun-phrase fill vs boilerplate.**

Three of three derivations observed vision is one slot doing two jobs. Subdivide:

```
"vision_first_clause": "Part of the AI Governance Pattern (AIGP) family ... defining the pattern of [SLOT: noun-phrase].",
"vision_invariant_clause": "The primary reader of [SLOT: spec's primary artifact type] is an AI."
```

Or — simpler implementation — keep `vision` as one field but document the two-clause shape in instantiation_notes so derivers know to fill the noun-phrase precisely without rewriting boilerplate.

**P4. Completeness value: broader rephrasing.**

Current canonical's "the spec's primary artifact bundle" framing fits roledef and catdef but misfit memodef. Replace with:

```
"description": "[SLOT: spec's primary artifact] MUST be sufficient — alone or composed with other AIGP-family artifacts — for a fresh AI runtime to act on its content with zero context backfill."
```

**P5. recommended_roles representational convention: formalize.**

Canonical v1.0.0 mixed bare-string and full-coordinate-object representations across its four entries. Memodef + roledef + catdef each independently noted the inconsistency. Formalize in canonical instantiation_notes:

> Use bare-string `role` values for in-org roles or for roles whose canonical roledef hasn't yet been published. Use full coordinate objects (`{id, version, url}`) for externally-published-and-stable roles per the `metadata.role_definition` shape.

**P6. v1_success_criterion: two shapes acknowledged.**

Three of three follow-on derivations went retrospective (Gordian-knot framing) rather than the canonical's forward-looking-recursive example. Acknowledge both shapes in instantiation_notes:

> v1_success_criterion may be expressed prospectively (forward-looking-recursive: "v1 ships when this orgdef exists as a self-describing artifact") or retrospectively (Gordian-knot: "v1 has already been achieved; here's the evidence"). Mature standards that shipped before the orgdef bootstrap typically use the retrospective shape.

**P7. Director-elicitation step + at-read-back-correction pattern: promote to canonical workflow.**

Two of three derivations surfaced both: pre-read-back Director-elicitation (one strategist-identified slot) AND at-read-back Director correction (one inference-not-fact catch). Promote from "recommended workflow patch" to canonical part of high-context mode in the org-creation-facilitator's workflow steps:

> In high-context mode, anticipate two Director-driven calls per derivation: (a) elicit ONE explicit Director answer for the slot most likely not inferable from materials, before delivering the read-back; (b) expect ONE additional inference-not-fact correction to surface AT read-back time, even if the rest of the artifact is approved as-is.

**P8. Governance terminology vocabulary mismatch note.**

Older specs (catdef, predating AIGP-family naming conventions) use seat names like "Chief Strategist" or "steward" rather than the canonical's `senior-open-standards-strategist`. Acknowledge in instantiation_notes:

> Derivers MAY rename a recommended-roles seat for spec-internal-naming-convention alignment (e.g., catdef's "Chief Strategist") as long as the role's bounded-authority discipline is preserved. The canonical's `senior-open-standards-strategist` is the role; the seat name within a derived org is the deriver's call.

**P9. REPLACE convention: soft note, not new category.**

All three derivations echoed canonical structure even when REPLACE-labeled (mission/vision). Roledef-strategist's observation that REPLACE oversells the deviation is triple-confirmed. The proposal explicitly does NOT add a SLOT-FILL category between REPLACE and INHERIT/REFINE; instead, add a soft note to the conventions table:

> REPLACE for mission, vision, and scope still expects family-resemblance in shape. Derivers' REPLACE artifacts SHOULD echo the canonical's structural framing (zero-context-backfill, AIGP-family identification, primary-reader-is-AI) even when the noun-phrases differ.

### Operational orgdef placement convention (Option C)

**P10. Migrate placement from `<spec>/<spec>-org/orgdef.openthing` to `<spec>/org/<id>.openthing`.**

Current convention forecloses aggregation (all leaf nodes named identically). New convention:

```
<spec>/
├── org/
│   ├── <spec>.openthing          ← the orgdef artifact (e.g., catdef-spec.openthing)
│   ├── jobs/
│   │   └── <job-id>.openthing    ← job artifacts
│   ├── rendered/                  ← projected outputs (gitignored)
│   └── .gitignore                 ← excludes rendered/
```

Matches the established catdef-family library convention (`canonical-orgs/<id>.openthing`, `proposed-roledefs/<id>.openthing`, etc.) where filename = identifier.

**Migration of four spec repos** (executed alongside this proposal landing):
- `orgdef-spec/orgdef/orgdef-spec-org/` → `orgdef-spec/orgdef/org/orgdef-spec.openthing` + jobs/ + .gitignore
- `roledef-spec/roledef/roledef-spec-org/` → `roledef-spec/roledef/org/roledef-spec.openthing` + jobs/ + .gitignore
- `memodef-spec/memodef/memodef-spec-org/` → `memodef-spec/memodef/org/memodef-spec.openthing` + jobs/ + .gitignore
- `catdef-spec/catdef-spec/catdef-spec-org/` → `catdef-spec/catdef-spec/org/catdef-spec.openthing` + jobs/ + .gitignore

**Cross-spec coordination needed:**
- Update `org-creation-facilitator.openthing` (in `roledef-spec/roledef/proposed-roledefs/`) — `output_contract.schema` path string
- Update `job-creation-facilitator.openthing` — `output_contract.destination` path string

Director (per role authority across all four spec orgs) authorized executing the migration directly rather than coordinating per-repo PRs. Bot identity: `orgdef-strategist@orgdef.org` for all migration commits in the four spec repos plus the canonical-template patch in orgdef-spec.

## Backward Compatibility

Canonical-template v1.1 is purely additive on top of v1.0.0:
- All existing v1.0.0 derivations remain valid (their content carries forward; the new instantiation_notes guidance applies to future derivations, not retroactively)
- v1.1's slot example shapes are documentation refinements, not structural changes — derivers reading v1.1 see clearer guidance; v1.0.0 readers continue to function

Placement convention migration is one-time:
- Four spec repos affected, each in its own commit (no cross-repo atomicity required)
- Derived orgdef artifacts have their `metadata.repository` URLs updated as part of the migration
- The canonical template's `derived_from.url` fields in derivations don't change (they reference the canonical's location, which isn't migrating — the canonical lives in a library directory, not an org folder)

No version bump for orgdef SCHEMA from this proposal alone (canonical-template revisions are content patches, not schema changes). The companion v0.3 SCHEMA proposal (filed separately) bumps the schema version.

## Conformance Tests

For canonical-template v1.1:
- The three existing operational derivations (memodef-spec, roledef-spec, catdef-spec) serve as the in-the-wild conformance fixtures — they were authored against v1.0.0 but conform to v1.1 too (v1.1 doesn't break them)
- A new `valid_orgs/canonical-derived-with-v1.1-shapes.openthing` exemplar can be authored alongside the canonical's v1.1 patch, demonstrating each new instantiation_notes recommendation in concrete form

For placement convention:
- Validator MAY warn (not FAIL) on artifacts found at the legacy `<spec>-org/` path, recommending migration
- The canonical-template's instantiation_notes update includes the new path convention; future derivations will use it natively

## Alternatives Considered

### Alt 1: Defer the v1.1 patch until canonical-orgs library has more entries

Wait until 5+ canonical templates exist to batch revisions across them.

**Rejected because:** the four AIGP-family operational orgdefs are landing now; future derivers (e.g., when catdef.org PRs reference the canonical) will be guided by the v1.1 form. Delaying means new derivers either learn the wrong shape from v1.0.0 or wait for v1.1 to land.

### Alt 2: Split the canonical-template patches and the placement convention into two proposals

Treat them as orthogonal: template content patches vs filesystem convention.

**Rejected because (per Director's bundling instruction):** they co-arose from the same derivation experience and the same Director-conversation; bundling reduces review overhead and lands the migration alongside the template patch that authorizes the new convention.

### Alt 3: Add a SLOT-FILL inheritance category for mission/vision

Per memodef-strategist's original suggestion: insert SLOT-FILL between REPLACE and INHERIT/REFINE.

**Rejected (P9) because:** all three derivations echoed canonical structure under the REPLACE label without needing a new category; a soft note in the conventions table solves the friction without overcomplicating the discipline.

## Open Questions

1. **Whether to subdivide vision into structurally-separate fields (`vision_first_clause`, `vision_invariant_clause`) vs document the two-clause shape in instantiation_notes only.** Author leans toward instantiation_notes documentation (lighter touch, no schema change) unless tooling needs structural access. The structural option remains available for v1.2 if patterns surface that need it.
2. **Whether the new placement convention (`<spec>/org/<id>.openthing`) should be MUST or SHOULD.** Author leans SHOULD — some adopter contexts (monorepos, vendor-specific layouts) may legitimately use different conventions. SHOULD-with-documented-aggregation-cost preserves flexibility.
3. **Whether to retroactively migrate the orgdef-spec org folder** (which is the meta-self-reference case — the spec defining the convention also using it). Author leans yes, for internal consistency; included in the migration plan above.

## Acceptance Criteria

If accepted (and given Director-bootstrap authority):

1. **Canonical template patched** at `orgdef-spec/orgdef/proposed-orgs/aigp-family-open-standard.openthing` to v1.1.0 — all P1–P9 patches applied, instantiation_notes updated
2. **Four spec repos migrated** per P10 — orgdef-spec, memodef-spec, roledef-spec, catdef-spec
3. **Org-creation-facilitator and job-creation-facilitator updated** — path string changes
4. **CONTRIBUTING.md** in orgdef-spec updated to document the new placement convention
5. **Cross-spec coordination memo to roledef-strategist** filed — describes the facilitator-roledef edits and the rationale
6. **Companion v0.3 SCHEMA proposal** filed separately — `forward_work_items[]`, `x.position.lifecycle` formal field, structured cross-org reference shape

## References

- memodef-strategist experience memo: `orgdef-spec/orgdef-spec-org/memos/2026-04-30-1000--memodef-strategist--orgdef-strategist--canonical-derivation-experience.openthing`
- roledef-strategist experience memo: `orgdef-spec/orgdef-spec-org/memos/2026-04-30-1300--roledef-strategist--orgdef-strategist--canonical-derivation-experience.openthing`
- catdef-strategist experience memo (with org-folder addendum): `orgdef-spec/orgdef-spec-org/memos/2026-04-27-1500--catdef-strategist--orgdef-strategist--canonical-derivation-experience.openthing`
- orgdef-strategist review of catdef derivation: `catdef-spec/memos/2026-04-30-1700--orgdef-strategist--catdef-strategist--derivation-review-passes.openthing`
- orgdef-strategist review of memodef derivation: `memodef-spec/memos/2026-04-30-1100--orgdef-strategist--memodef-strategist--derivation-review-passes.openthing`
- orgdef-strategist retroactive review of roledef derivation: `roledef-spec/roledef/memos/2026-04-30-1705--orgdef-strategist--roledef-strategist--derivation-review-passes-retro.openthing`
- Director conversation surfacing org-folder-naming-convention friction: 2026-04-30, captured in catdef-strategist's experience memo (g) section
