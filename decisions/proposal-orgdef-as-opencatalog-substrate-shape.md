# Proposal Decision: orgdef as `.opencatalog` (atomic-transportable substrate shape, SCHEMA v1.0.0)

**Disposition:** Accept (no modifications; OQs ratified inline by Director during the strategic conversation)
**Origin:** [proposals/orgdef-as-opencatalog-substrate-shape.md](../proposals/orgdef-as-opencatalog-substrate-shape.md)
**Decided:** 2026-05-10 by orgdef-strategist
**Authorization:** Director ratified the directional call 2026-05-10: "Path B, all the way. This is my failure, I did not notice that we had not done this." Plus Director ratified all four key design decisions inline (jobs as items with type tag; SCHEMA v1.0.0 major bump; relationships catalog-level; per-artifact major version bump). Direct-execute mode authorized per the standing development-phase posture ("Fortunately since we are still in the development phase, I am the only user").
**Bootstrap caveat:** Same-head provenance — orgdef-strategist holds catdef-strategist + roledef-strategist + memodef-strategist informally during bootstrap. The cross-spec coordination touchpoints (catdef substrate, roledef Job type embedding, render.catdef.org rendering target, openbraid Phase E refactor) all flow through proper memo trails to the respective seats once this decision is committed. openbraid-engineer pause memo already sent 2026-05-10 11:00.

## Disposition

Accepted as drafted; no modifications. The proposal captures Director's "atomic thing" framing as substrate-shape correction; all four design decisions ratified inline; window-of-opportunity (one user, six artifacts to migrate during development phase) cleanly identified. Substantial migration work follows; decision artifact captures both the strategist call and the build directive for execution.

## Rationale

### Why Accept

Recovering original-intent substrate shape is the right move while the window is open. Director's "Fortunately since we are still in the development phase, I am the only user" framing makes the cost-benefit calculation sharp: six artifacts to migrate now vs. eighty (or more) once external adoption lands. The longer the substrate-shape miss carries forward, the more expensive the eventual correction.

The four ratified design decisions are coherent:

- **Jobs as items with `type: roledef:Job`** preserves substrate identity (each thing has a type tag; substrate validators handle items naturally). Inline jobs would be more compact but break the substrate's "everything is a typed thing" discipline. Items-with-type-tag is the family-consistent choice.
- **SCHEMA v1.0.0 major bump** correctly signals "this is the foundation landing." Pre-1.0 was experimental; 1.0.0 is substrate-aligned. Future evolution (`forward_work_items[]`, structured cross-org references, sub-org linking, `x.position.lifecycle` promotion) becomes post-1.0 minor additions. This is the right semver shape.
- **Relationships catalog-level array** keeps the lightweight thing lightweight. Relationships are typed edges between position ids; promoting them to items would add type-tag overhead without functional benefit. Promote later only if relationships gain richer per-edge structure.
- **Per-artifact major version bump** reflects the substrate-shape change at the artifact level. Operational orgs going to 2.0.0 (or proportionate major bump from their current version) records "this artifact uses the v1.0.0+ substrate shape, not the v0.x shape." Versions are clear evidence of shape, not just content.

### Why no modifications

Director ratified all four design decisions inline; proposal text reflects those ratifications faithfully. The migration plan (P6) is mechanical execution against a clear target shape; no design surface remains contested. orgdef-maintainer review remaining for schema-conformance checks but no proposal-text modifications expected.

### Direct-execute mode appropriate here

Director's "development phase" + "I am the only user" framing + "work without stopping" standing authorization aligns with direct-execute mode. The migration is mechanically bounded (eight artifacts + spec + CONTRIBUTING + SCHEMA + canonical-template); no governance-level change beyond the SCHEMA major bump (which is itself Director-ratified). orgdef-strategist executes the multi-repo migration with the orgdef-strategist@orgdef.org bot identity per the v1.1 placement-convention + 2026-05-01 naming-convention precedents.

## Resolutions to Open Questions (all ratified inline by Director)

### OQ1 → Jobs as items with type tag

**Director's call: items-with-type-tag.** Substrate identity preserved; substrate validators handle items naturally; family-consistent with how other items appear in catalogs.

### OQ2 → SCHEMA major-version 1.0.0

**Director's call: 1.0.0.** Original-intent landing as foundation; pre-1.0 was experimental; future evolution becomes post-1.0 minor additions.

### OQ3 → Relationships catalog-level array

**Director's call: catalog-level.** Lightweight stays lightweight; promote to items only if richer per-edge structure surfaces empirically.

### OQ4 → Per-artifact major version bump

**Director's call: per-artifact major.** Each migrated orgdef bumps major version (e.g., thingalog 1.3.3 → 2.0.0; orgdef-spec-organization 1.1.0 → 2.0.0). Records substrate-shape transition at the artifact level.

## Notable design choices

### 1. opencatalog substrate reuse, not new substrate type

orgdef:Organization adopts the existing catdef substrate opencatalog primitive rather than defining a new catdef-level type. Reuse is the right call: opencatalog is purpose-built for "catalog of typed items"; orgdef:Organization is exactly that pattern; adding a new catdef-level type would require catdef SCHEMA changes the family doesn't need. Same substrate-portability story as roledefs reusing openthing — substrate primitives are the family's load-bearing infrastructure; consumer specs map onto them rather than introducing parallel primitives.

### 2. The 1.0.0 landing is principled, not aspirational

Past pre-1.0 → 1.0 transitions in the family (catdef hit 1.0 with v1.4 release; roledef hit 1.0 with the rename + cross-runtime conformance methodology + library v0.1) followed empirical-validation patterns. orgdef's 1.0 lands when the substrate shape stabilizes. This is the substrate shape landing; therefore this is the 1.0 moment. The framing is principled (substrate-shape stable means foundation stable; foundation stable means 1.0); not aspirational (it's not "1.0 when we feel ready"; it's "1.0 when the substrate shape is correct, which is now").

### 3. Folding Tier 2 canonical-library rename into this proposal

The prior naming-convention decision (2026-05-01) deferred canonical-library `orgs/catdef-org.openthing` → `orgs/catdef-organization.openthing` to v0.3 SCHEMA bundle. This proposal IS the v0.3 → v1.0 substrate bundle; the canonical-library rename naturally folds in. `orgs/catdef-org.openthing` → `orgs/catdef-org.opencatalog` (preserving the `-org` shortname per the canonical-library convention's distinct shape). Tier 2 resolved as part of this migration.

### 4. openbraid Phase E refactor SIMPLIFIES rather than complicates

Director's framing throughout: openbraid Phase E's discovery surfaced the gap; openbraid Phase E's refactor against the new substrate shape is the consequence. But the net effect is simpler implementation for openbraid: one artifact type to ingest (opencatalog) instead of two (openthing-orgdef + openthing-job-bundle); jobs become local items inside the orgdef (no separate fetch); export is one file (no bundle assembly). Phase E becomes E1 (ingest opencatalog), no E2 (jobs are E1 items), E3 unchanged, E4 unchanged, E5 simpler. Pause + refactor target update + resume is cheaper than the alternative of building E2 against the wrong shape.

### 5. development-phase "clean break" is the right window-of-opportunity call

The family's discipline has been backward-compatible additive changes (canonical-template v1.1, v1.2, v1.3; org-artifact filename suffix; inter-position memo convention). This proposal breaks v0.x compatibility deliberately. The justification is Director's "development phase + one user" framing: the cost of a clean break with six artifacts is dramatically lower than the cost of carrying v0.x compatibility shims forward indefinitely. The window is now; close it cleanly.

## Build directive (orgdef-strategist + orgdef-maintainer execute per Director's "work without stopping" authorization)

Execute in this order:

### Phase 1 — Spec-level changes (orgdef-spec repo)

1. **SCHEMA.md substantive rewrite** — define orgdef:Organization as opencatalog-shape; define orgdef:Position item shape; reference roledef:Job item shape; define catalog-level field requirements (MUST/SHOULD); define `metadata.kind` enforcement (operational / canonical-template); define inheritance via `metadata.derived_from`. Mark as orgdef v1.0.0.
2. **CONTRIBUTING.md substantive rewrite** — update placement convention (still `<project>/org/`), filename convention (`<id>-organization.opencatalog`), derivation discipline, "Job artifacts as items, not files" new section. Carry forward previously-shipped sections (Inter-position communication, Operational org-artifact filename, Canonical OAGP position addressing) with shape-updated examples.
3. **Canonical-template migration** — `proposed-orgs/oagp-family-open-standard.openthing` → `proposed-orgs/oagp-family-open-standard.opencatalog`. Version 1.3.0 → 2.0.0. Compose existing canonical-template content into opencatalog shape; positions become slot-shaped items; instantiation_notes update for the new shape.
4. **Conformance fixtures** — `conformance/valid_orgs/` exemplars + `conformance/invalid_orgs/` counterexamples for v1.0.0 shape.

Commit per spec change with `orgdef-strategist@orgdef.org` author identity. Push.

### Phase 2 — Canonical-orgs library migration (orgdef-spec repo)

5. **`orgs/catdef-org.openthing` → `orgs/catdef-org.opencatalog`** — compose catdef-org orgdef into opencatalog shape (positions as items; if catdef-org has job artifacts referenced in any orgdef-spec/orgs/ way, fold them; this is also Tier 2 of the prior naming-convention decision). Update `catalog.opencatalog` library index accordingly.

### Phase 3 — Operational org migrations (five other repos, one per commit per repo)

6. **orgdef-spec** — `org/orgdef-spec-organization.openthing` + `org/jobs/orgdef-strategist.openthing` → `org/orgdef-spec-organization.opencatalog`. Delete `org/jobs/` directory. Bump org version 1.1.0 → 2.0.0; metadata.history entry.
7. **memodef-spec** — `org/memodef-spec-organization.openthing` + `org/jobs/` (empty placeholder; skip jobs-as-items) → `org/memodef-spec-organization.opencatalog`. Bump version major.
8. **roledef-spec** — `org/roledef-spec-organization.openthing` + `org/jobs/` (empty) → `org/roledef-spec-organization.opencatalog`. Bump version major.
9. **catdef-spec** — `org/catdef-spec-organization.openthing` + `org/jobs/` (empty) → `org/catdef-spec-organization.opencatalog`. Bump version major. Note: catdef-spec local git config defaults to catdef-maintainer; override --author to orgdef-strategist for the migration commit.
10. **thingalog** — `org/thingalog-organization.openthing` + `org/jobs/implementer.openthing` + `org/jobs/product-strategist.openthing` → `org/thingalog-organization.opencatalog`. Delete `org/jobs/`. Bump version 1.3.3 → 2.0.0.
11. **openbraid-org** — `org/openbraid-org.openthing` + `org/jobs/openbraid-director.openthing` + `org/jobs/openbraid-engineer.openthing` + `org/jobs/openbraid-strategist.openthing` → `org/openbraid-org-organization.opencatalog`. Note: also renames per the 2026-05-01 filename convention; openbraid-org's prior org file didn't have the `-organization` suffix. Delete `org/jobs/`. Bump version major.

Commit per repo with `orgdef-strategist@orgdef.org` author identity. Pull --rebase + push per the parallel-session push-hygiene discipline from project memory.

### Phase 4 — Cross-spec memos (post-Phase-3)

12. **Follow-up Phase E memo to openbraid-engineer** — new target shape committed; pause can lift; refactor against the simpler opencatalog ingest path. Filed in openbraid-org's inbox.
13. **Informational memo to roledef-strategist** — `roledef:Job` is now embedded as items in orgdef.opencatalog rather than authored as standalone files; roledef SCHEMA unchanged; informational + cross-spec courtesy. Filed in roledef-spec's memos/.
14. **Informational memo to catdef-strategist** — orgdef-as-opencatalog is consistent with catdef substrate; no catdef changes needed; courtesy notification. Filed in catdef-spec's memos/.
15. **Memo to render.catdef.org team** — rendering target shifts from .openthing to .opencatalog for orgdefs. Should be small renderer change since opencatalog rendering is already supported. Filed wherever render.catdef.org's coordination channel is; if no clear channel, file in catdef-spec memos/ with Director-relay framing.

### Phase 5 — Memory updates

16. **Update project_orgdef.md** — capture the substrate-shape change at v1.0.0; update Recent state; update Open work items (Phase E coordination unblocked once openbraid-engineer refactors).
17. **MEMORY.md index** — no new memory files needed; project_orgdef.md update captures everything.

## Cross-spec coordination

Already captured in the proposal's Cross-spec coordination section:

- **catdef-strategist:** informational notification once decision committed
- **roledef-strategist:** informational notification + clarification that Job type embedding context differs but Job SCHEMA unchanged
- **memodef-strategist:** no direct impact; memo URL composition (deferred OQ3 from canonical-OAGP-addressing decision) still pending Director-led discussion
- **openbraid-engineer:** URGENT pause memo already sent; follow-up Phase E refactor-target memo follows decision commit
- **render.catdef.org team:** rendering target update; small change

## Items not incorporated

None. Proposal accepted as drafted with all four OQs ratified inline by Director during the strategic conversation.

## Workflow validation

- **Strategist scope:** substrate-shape decision is library-curation + pattern-promotion + scope-narrowing all combined; within orgdef-strategist scope per the roledef output_contract.strategist_deliverables. The SCHEMA major-version bump is the largest single decision; Director-ratified.
- **Cross-spec discipline:** same-head provenance flagged; cross-spec memos flow through proper repos for future audit.
- **Director ratification:** all four OQs ratified inline 2026-05-10; direct-execute mode authorized.

## Forward-reference resolution

- **Tier 2 canonical-library rename** (deferred from 2026-05-01 operational-org-artifact-naming-convention): RESOLVED in Phase 2 of this build directive (`orgs/catdef-org.openthing` → `orgs/catdef-org.opencatalog`).
- **openbraid Phase E coordination:** RESUMABLE after Phase 3 + Phase 4 step 12 (follow-up Phase E memo with new target shape).
- **Future post-1.0 minor additions** (`forward_work_items[]`, structured cross-org references, sub-org linking, `x.position.lifecycle` formal promotion): UNCHANGED; these remain post-1.0 minor proposals filed when empirical pressure surfaces. The 1.0 landing doesn't preempt their future filing.

## Notes

- This is the largest single migration the orgdef-spec family has undertaken (eight artifacts across six repos + SCHEMA + CONTRIBUTING + canonical-template + canonical-orgs library). Window-of-opportunity (one user, development phase) makes it executable in one focused arc; deferred any longer and the cost grows.
- The "atomic-orgdef" framing is the kind of insight that lands cleanly only when Director catches a mismatch between original-intent and current-implementation. The fact that openbraid Phase E surfaced the gap is empirical validation that the substrate-shape miss was real-world consequential, not just theoretical.
- Phase E refactor is the canary for whether the new shape is genuinely simpler; if openbraid-engineer reports significant friction in refactoring against opencatalog rather than openthing-bundle, the spec might want minor adjustments before broader adoption.

## References

- Originating proposal: [proposals/orgdef-as-opencatalog-substrate-shape.md](../proposals/orgdef-as-opencatalog-substrate-shape.md)
- Director ratification: 2026-05-10 strategic conversation in orgdef-strategist chair (verbatim quotes: "Path B, all the way," "This is my failure, I did not notice that we had not done this," "An orgdef should be an atomic thing," "Fortunately since we are still in the development phase, I am the only user," plus four OQ ratifications)
- URGENT pause memo to openbraid-engineer (already sent): `s:/projects/openbraid-org/openbraid/memos/inbox/2026-05-10-1100--orgdef-strategist--openbraid-engineer--phase-e-pause-orgdef-substrate-change-incoming.openthing`
- Prior decisions folded in or referenced:
  - [decisions/proposal-operational-org-artifact-naming-convention.md](proposal-operational-org-artifact-naming-convention.md) — Tier-2 canonical-library rename resolved here
  - [decisions/proposal-canonical-orgs-library.md](proposal-canonical-orgs-library.md) — canonical-orgs library shape carries forward
  - [decisions/proposal-canonical-oagp-position-addressing.md](proposal-canonical-oagp-position-addressing.md) — URL semantics unaffected; positions are now items but their URLs still resolve them
  - [decisions/proposal-canonical-template-v1.1-and-placement-convention.md](proposal-canonical-template-v1.1-and-placement-convention.md) — placement convention carries forward
  - [decisions/proposal-inter-position-communication-convention.md](proposal-inter-position-communication-convention.md) — memos/ convention unaffected
- catdef substrate spec (opencatalog primitive): [`https://github.com/catdef/catdef-spec/blob/main/CATIO_SPEC.md`](https://github.com/catdef/catdef-spec/blob/main/CATIO_SPEC.md)
- Eight artifacts to migrate (enumerated in proposal P6):
  - Six operational orgs: orgdef-spec, memodef-spec, roledef-spec, catdef-spec, thingalog, openbraid-org
  - One canonical-library entry: orgs/catdef-org
  - One canonical-template: proposed-orgs/oagp-family-open-standard
