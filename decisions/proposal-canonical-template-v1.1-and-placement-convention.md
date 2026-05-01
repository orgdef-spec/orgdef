# Proposal Decision: Canonical-template v1.1 + operational orgdef placement convention

**Disposition:** Accept
**Origin:** [proposals/canonical-template-v1.1-and-placement-convention.md](../proposals/canonical-template-v1.1-and-placement-convention.md)
**Decided:** 2026-04-30 by orgdef-strategist
**Authorization:** Director explicitly authorized executing the placement-convention migration directly across all four spec repos (per Director's role authority across all four organizations) rather than coordinating per-repo PRs.
**Bootstrap caveat:** Same-head provenance — orgdef-strategist holds catdef + roledef + memodef strategist seats during bootstrap; the placement convention's cross-spec migration happens within one head, but commits use distinct bot identities (`orgdef-strategist@orgdef.org` for migrations driven by this proposal; existing seat identities for in-repo provenance per CLAUDE.md).

## Disposition

Accepted as drafted, no modifications. The empirical grounding is unusually strong (three independent derivations producing reinforcing findings; one Director-surfaced post-scaffold finding). The patches are well-scoped (canonical-template content + filesystem convention; no schema changes). Migration is bounded (four spec repos, ~1 hour total). Director authorization to execute the migration directly is explicit.

## Rationale

### Why Accept (no modifications)

The proposal accurately captures the synthesis from three derivation experiences. Each adopted patch (P1–P10) is grounded in either triple-confirmed observations or Director-surfaced empirical findings — no speculative additions. The rejected SLOT-FILL category (P9) is rejected for the right reason (overcomplicating conventions when a soft note suffices).

The placement-convention migration (P10) is the largest single mechanical change but is internally bounded: four spec repos, well-defined source/target paths, cross-spec coordination already accounted for (org-creation-facilitator and job-creation-facilitator path-string updates).

The companion v0.3 SCHEMA proposal (forward_work_items[], x.position.lifecycle, cross-org reference shape) is correctly scoped out of this proposal — different review path (schema vs canonical-template vs filesystem convention).

### Why no modifications

Open Question 1 (vision subdivision shape) — instantiation_notes documentation only for v1.1; structural option preserved for v1.2 if patterns surface. Right call.

Open Question 2 (placement convention strength) — SHOULD with documented aggregation cost. Right call; preserves flexibility for monorepo and vendor-specific contexts.

Open Question 3 (retroactive migration of orgdef-spec org folder) — yes, for internal consistency. Right call; the meta-self-reference case is exactly where convention-consistency matters most.

## Build directive (for orgdef-maintainer / strategist during bootstrap)

Execute in this order:

1. **Canonical-template patch** — apply P1–P9 to `orgdef-spec/orgdef/proposed-orgs/oagp-family-open-standard.openthing`; bump version to v1.1.0; update history with patch summary.
2. **Facilitator path-string updates** — patch `roledef-spec/roledef/proposed-roledefs/org-creation-facilitator.openthing` (`output_contract.schema`) and `job-creation-facilitator.openthing` (`output_contract.destination`) to reflect Option C placement (`<spec>/org/<id>.openthing` and `<spec>/org/jobs/<job-id>.openthing`).
3. **Spec repo migrations** — for each of the four spec repos (orgdef-spec, memodef-spec, roledef-spec, catdef-spec):
   - Move/rename `<spec>/<spec>-org/orgdef.openthing` → `<spec>/org/<spec>.openthing`
   - Move `<spec>/<spec>-org/jobs/` → `<spec>/org/jobs/`
   - Move `<spec>/<spec>-org/.gitignore` → `<spec>/org/.gitignore`
   - Update each artifact's `metadata.repository` URL to reflect new path
   - Delete old `<spec>-org/` directory
   - Commit with `orgdef-strategist@orgdef.org` author identity
4. **CONTRIBUTING.md update** in orgdef-spec — document new placement convention
5. **Cross-spec coordination memo** to roledef-strategist (in `roledef-spec/roledef/memos/`) — describes the facilitator path-string edits and rationale
6. **Push to all four spec repos** — main branches updated atomically per repo (no cross-repo atomicity required; each repo is internally consistent)

## Cross-spec coordination

Already captured in the proposal (P10 references org-creation-facilitator + job-creation-facilitator updates). The coordination memo in step 5 of the build directive completes the artifact trail to roledef-strategist.

The companion v0.3 SCHEMA proposal (filed separately under `proposals/v0.3-schema-additions.md` or similar) is the proper home for `forward_work_items[]`, `x.position.lifecycle` formal promotion, and structured cross-org reference shape. That proposal's decision will reference back to this one for the empirical grounding.

## References

- Originating proposal: [proposals/canonical-template-v1.1-and-placement-convention.md](../proposals/canonical-template-v1.1-and-placement-convention.md)
- Three experience memos cited in the proposal's References section
- Three review-passes memos cited in the proposal's References section
- Director conversation surfacing the org-folder-naming-convention finding: 2026-04-30
