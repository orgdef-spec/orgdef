# Proposal Decision: orgdef SCHEMA v1.1.0 — charter fields, value/red_line shapes, master_url extension, edit discipline

**Disposition:** Accept (no modifications to P1–P9; two clarifying framings added in the decision text; OQs resolve to working positions; migration sweep authorized as per-org opt-in rather than mandated sweep)
**Origin:** [proposals/schema-v1.1.0-charter-fields-and-edit-discipline.md](../proposals/schema-v1.1.0-charter-fields-and-edit-discipline.md)
**Decided:** 2026-05-23 by orgdef-strategist
**Authorization:** Director (Product Owner) explicitly authorized this directional call 2026-05-23 in the strategist-seat session, responding to orgdef-strategist's review-and-recommendation report with: *"Proposal 1: I agree with all of your recommendations and decisions, proceed."* The review report carried (a) the Accept recommendation for P1–P9 as proposed; (b) two clarifying framings (P8/P9 anti-divergence framing; migration sweep as per-org opt-in); (c) OQ-resolution recommendations matching the proposal's working positions.

**Bootstrap caveat:** The proposal was filed 2026-05-17 (six days before this decision) under provisional orgdef-strategist bot identity. The decision is filed under the same bot identity by the same head. The data-vs-pattern sharpening of 2026-05-23 ([memos/read/2026-05-23-1100--thingalog-strategist--orgdef-strategist--handoff-addendum-data-vs-pattern.body.md](../memos/read/2026-05-23-1100--thingalog-strategist--orgdef-strategist--handoff-addendum-data-vs-pattern.body.md)) was reviewed for scope-clarification implications; all nine P-items are format-shape (orgdef SCHEMA, orgdef extensions, validator/runtime edit-rules grounded in orgdef artifact validity) and remain properly within orgdef-strategist scope post-sharpening. Cross-spec coordination touchpoints (roledef `recommended_capabilities`; canonical-template patches) are addressed in build directive and forward-reference resolution.

## Disposition

Accepted as drafted; no modifications to the proposed P1–P9 substantive content. Two clarifying framings added in this decision text:

1. **P8/P9 framing as anti-divergence Schelling points, not endorsements of any one runtime** — the wire-format and edit-log recommendations cite empirical openbraid implementation, but the spec's purpose in citing them is to prevent runtime divergence rather than to bless openbraid's choices. The proposal's body is mostly already on this footing; the decision reinforces explicitly.
2. **Migration sweep (Decision Request item 5) authorized as per-org opt-in rather than mandated cross-org sweep** — adopters add v1.1.0 fields (vision/values/operating_principles/policies) when they have new content to add, not for the sake of updating. Thingalog is the obvious first-mover candidate (Director has been actively shaping it); other operational orgs migrate organically as content warrants.

All four Open Questions resolve to their working positions; rationale below.

## Rationale

### Why Accept

The three convergent signals the proposal articulates (Director display ambitions; openbraid-engineer F-edit phase implementation experience; master/replicant discipline ratification) are independent and well-grounded. Each alone would warrant a spec response; together they describe the same artifact-surface area (catalog-level fields + items + edit-operation discipline + master/replicant) and benefit from coherent omnibus packaging.

The Omnibus-vs-three-proposals argument (proposal §"Why omnibus") holds:
- Three signals → three reviews → three upgrade targets is redundant work without proportional benefit.
- v1.x foundation stabilization is window-of-opportunity logic that mirrors the v0.x → v1.0.0 substrate-shape correction: six operational orgs is dramatically cheaper to upgrade than sixty.
- Single coordinated bump is the right adopter UX.

Backward compatibility is structurally enforced (every v1.0.0-valid artifact remains v1.1.0-valid; the six operational orgs continue to validate without modification). The risk profile of a minor version bump is minimal.

The empirical grounding of each P-item is solid:
- **P1** (catalog-level fields): Director-articulated need for org-page display of vision/values/principles.
- **P2** (Policy items): mirrors the structural reasoning that drove positions and jobs to `items[]` (versionable, addressable by id, atomic-bundle transportable).
- **P3/P4** (canonical value/red_line shapes): openbraid-engineer signal (g) — three operational orgs self-converged on the same shape without prompting; recommended-but-not-strict is the right discipline (Alternative A4 rejection is sound).
- **P5** (master_url): already implemented by openbraid build 30; codification protects against drift if a second runtime emerges. The distinction from `x.org.org_location` (mirror discovery vs single authority) is meaningful and worth preserving as separate extensions.
- **P6** (relationship-cleanup-on-position-delete): forced by v1.0.0 internal consistency rules (relationship endpoints must resolve). Either spec forbids dangling state (this proposal) or relaxes v1.0.0 consistency (rejected); former is cleaner.
- **P7** (recognized relationship types appendix): seven types empirically derived from grepping six operational opencatalogs; appendix as Schelling point for cross-runtime portability.
- **P8** (RFC 7396 JSON Merge Patch): leveraging well-defined external standard rather than reinventing inline; null-as-deletion is AI-client-friendly.
- **P9** (append-only edit-log): empirical Director-trust UX surface; non-prescriptive on shape (event-sourced, git-history, append-only-table all permitted).

### Why no modifications to proposal text

The proposal stays within strategist scope (orgdef SCHEMA design; informative appendices in SCHEMA.md; runtime edit-operation rules grounded in artifact-validity preservation). No catdef substrate changes; no orgdef artifact-validation breaking changes; cross-spec coordination (roledef `recommended_capabilities`) routed via separate memo with non-blocking shipping cadence.

The two clarifying framings added in this decision (Schelling-point framing for P8/P9; per-org opt-in for migration sweep) are framing reinforcements in the decision artifact, NOT modifications to the proposed P-items themselves. The proposal text correctly states the substance; the decision reinforces the framing for downstream readers (including future maintainers who may extend the appendices in subsequent versions).

### On the data-vs-pattern sharpening

The proposal was filed 2026-05-17, six days before the data-vs-pattern sharpening landed 2026-05-23. All nine P-items reviewed against the sharpened categorization:

| P# | Category | Properly orgdef-strategist? |
|---|---|---|
| P1 | catalog-level orgdef SCHEMA field semantics | Yes — format-shape |
| P2 | new orgdef item type | Yes — format-shape |
| P3 | canonical orgdef value-item shape | Yes — format-shape |
| P4 | canonical orgdef red_line-item shape | Yes — format-shape |
| P5 | orgdef per-org extension formalization | Yes — format-shape |
| P6 | runtime edit-rule preserving orgdef artifact validity | Yes — format-shape (artifact-validity-grounded) |
| P7 | orgdef SCHEMA.md informative appendix | Yes — format-shape |
| P8 | informative wire-format recommendation for orgdef partial-updates | Yes — format-shape (orgdef-artifact-specific) |
| P9 | informative edit-log recommendation for orgdef artifact mutations | Yes — format-shape (orgdef-artifact-specific) |

All nine are format-shape. No re-routing to oagp-strategist required for any sub-change.

**One forward-reference flagged:** the build directive includes a canonical-template patch (`proposed-orgs/oagp-family-open-standard.opencatalog`) reflecting v1.1.0 capabilities. The canonical-template's residence (orgdef-spec vs oagp-org) post-sharpening is itself an open question — see Forward-reference resolution. The v1.1.0 canonical-template patch lands at the current residence (orgdef-spec/proposed-orgs/); if subsequent strategist coordination moves the canonical-template, the patch travels with it.

## Resolutions to Open Questions

### OQ1 → defer; flat Policy items sufficient for v1.1.0

**Strategist call: working position accepted.** Nested sub-policies (parent policy with specialization clauses for specific scopes) are real but premature. v1.1.0 ships flat Policy items; nesting can be added in v1.2.0 if empirical pressure surfaces from real adopter use. The flat shape is sufficient for the bootstrap adopter case (Thingalog policies for Director's stated display purposes).

### OQ2 → defer; value-items remain catalog-level (org-wide)

**Strategist call: working position accepted.** Position-scoped values are a coherent pattern but unproven empirically. v1.1.0 specifies values as catalog-level (org-wide implicit). If position-scoped values emerge as a real adopter pattern, add optional `scope` field to value-item shape in v1.2.0.

### OQ3 → defer; single-master `x.org.master_url` sufficient

**Strategist call: working position accepted.** Multi-master is an unsolved problem in broader distributed-systems literature; the OAGP family should not pioneer a solution. Single-master `x.org.master_url` is sufficient for current adoption (every empirical case to date — openbraid as master, github as master, runtime-as-default-master — is single-master). Federated orgs with regional editors are hypothetical; defer until empirical case surfaces.

### OQ4 → keep appendix open; new types added via minor bumps without formal proposal

**Strategist call: working position accepted with one clarification.** The recognized relationship types appendix is informative and Schelling-point-shaped; adopters MAY define additional types as needed. New types added via minor version bumps (v1.2.0+) when empirical signal warrants — orgdef-strategist files a documentation update (no formal proposal artifact required for appendix expansion within the same major version). When/if the appendix grows substantially or relationship semantics become entangled with validation rules (which would shift them from informative to normative), formal proposal returns.

**Clarification added:** the no-formal-proposal-for-appendix-additions exception applies ONLY to informative appendices, not to normative content. P1, P2, P3, P4, P5, P6 (all normative) require formal proposal artifacts for any future changes; P7, P8, P9 (informative) can be extended via documentation updates within the same major version.

## Build directive (for orgdef-maintainer when scaffolding work begins)

Execute in this order:

1. **SCHEMA.md normative edits (P1–P6)** — apply to `SCHEMA.md`:
   - Document expanded semantics for catalog-level `vision`, `mission`, `scope`, `governance_model` fields per P1
   - Add `operating_principles[]` as catalog-level field per P1 (mirroring value-item shape from P3)
   - Add `orgdef:Policy` item type specification per P2 (canonical item shape; internal consistency rules; optional `position.applicable_policies[]` reference)
   - Add canonical value-item shape `{name, description, rationale}` per P3 (SHOULD recommendation with validator-warning allowance)
   - Add canonical red_line-item shape `{rule, rationale}` per P4 (SHOULD recommendation with validator-warning allowance)
   - Add `x.org.master_url` extension specification per P5 (semantic table; distinction from `x.org.org_location` preserved)
   - Add relationship-cleanup-on-position-delete normative rule per P6 (with pre-delete safety guard for active sessions)
2. **SCHEMA.md informative appendix additions (P7–P9)** — append to `SCHEMA.md`:
   - "Recognized Relationship Types (Informative)" appendix per P7 (seven types with descriptions)
   - "Editing Artifacts: Wire Format (Informative)" section per P8 (RFC 7396 recommendation with rationale; explicit anti-divergence framing per clarifying framing 1)
   - "Editing Artifacts: Audit Trail (Informative)" section per P9 (append-only edit-log SHOULD with minimum-fields list; explicit anti-divergence framing per clarifying framing 1)
3. **SCHEMA version bump** — `orgdef` field bumps `1.0.0 → 1.1.0` in SCHEMA.md; semver-shaped minor bump (additive, backward-compatible). SCHEMA.md version history updated with v1.1.0 entry.
4. **Conformance fixtures** — add to `tests/v1.1.0/`:
   - `policy-item-shape.opencatalog` (P2 exemplar)
   - `canonical-value-item.opencatalog` (P3 exemplar)
   - `canonical-red-line-item.opencatalog` (P4 exemplar)
   - `master-url-present-external.opencatalog` (P5 replicant scenario)
   - `master-url-present-self.opencatalog` (P5 master scenario)
   - `master-url-absent.opencatalog` (P5 default-master scenario)
   - `operating-principles-populated.opencatalog` (P1 distinction with values)
   - `relationship-types-vocabulary.opencatalog` (P7 all-seven-types example)
   - Each fixture gets a brief README in the fixture directory per CONTRIBUTING.md conformance convention.
5. **Canonical template patch (P1/P2 capabilities reflection)** — apply to `proposed-orgs/oagp-family-open-standard.opencatalog`:
   - Bump canonical-template version `2.0.0 → 2.1.0` (additive minor)
   - Add example `operating_principles[]` entries (parallel to existing `values[]`) demonstrating P1
   - Add one example `orgdef:Policy` item demonstrating P2
   - Update `metadata.history` with a v2.1.0 entry summarizing the patch
   - Per the Bootstrap caveat above and Forward-reference resolution below: this patch lands at the current canonical-template residence (`orgdef-spec/proposed-orgs/`); if subsequent strategist coordination moves the canonical-template to oagp-org or splits it, the patch travels accordingly.
6. **catalog.opencatalog index entry update** — if new canonical-orgs entries land as part of v1.1.0 promotion, update `catalog.opencatalog`. (Currently no new canonical-orgs in v1.1.0 itself; this directive is forward-prepared.)
7. **Migration sweep authorization (per-org opt-in)** — operational orgs MAY adopt v1.1.0 fields (vision/values/operating_principles/policies[]) on their own cadence as adopters generate new content. NOT a mandated cross-org sweep. Thingalog is the obvious first-mover candidate. orgdef-spec's own orgdef MAY adopt as part of subsequent strategist work; not required for v1.1.0 ship.
8. **Validator-behavior implementation** — when validator tooling exists (currently deferred per Known Work Items inherited from catdef-family), v1.1.0 validators MUST accept v1.0.0 artifacts and MAY warn on non-canonical value/red_line shapes per P3/P4. Until validator tooling exists, strategist self-validation per inherited orgdef-spec discipline.

## Cross-spec coordination

- **roledef-spec:** separate memo to roledef-strategist proposing roledef SCHEMA v1.2.0 addition of `recommended_capabilities` field (Director-flagged 2026-05-16). Already filed per proposal §Cross-spec Coordination. orgdef v1.1.0 ship does NOT depend on roledef change; the two ship independently. When both land, orgdef:Position's transitive capability inheritance through `role_definition` and `job_definition` references becomes the natural composition.
- **catdef substrate:** unchanged. opencatalog substrate primitives (catalog-level fields + type-tagged items) continue to suffice for all P-items. The new `orgdef:Policy` item type fits within the existing catdef item-typing pattern; no substrate change required.
- **memodef substrate:** unchanged. v1.1.0 does not affect memo transport or shape; inter-position communication conventions continue unchanged.
- **transcriptdef substrate:** unchanged. v1.1.0 does not affect transcript shape or conventions.
- **openbraid runtime:** F-edit phase (shipped 2026-05-11) already implements P5 (master_url), P6 (relationship-cleanup), P8 (RFC 7396 wire format), and P9 (edit-log) at the runtime level. v1.1.0 codifies what openbraid already does. P1 (catalog-level field display) and P2 (Policy item rendering + edit-tool) await openbraid renderer + edit-tool updates; engineer's track when ready. No spec-side blocker.
- **oagp-org / oagp-strategist (post-sharpening cross-org coordination):** Informational FYI memo to oagp-strategist about v1.1.0 ship recommended (per the canonical-orgs library residence forward-reference). Not blocking; orgdef-strategist files when convenient.

## Notable design choices

1. **Omnibus packaging preserved.** Three convergent signals describing one artifact-surface area packaged into one minor bump. Adopters get one upgrade target; reviewers get one coherent shape decision; v1.x foundation stabilizes faster. Alternative A1 (three separate proposals) rejection is sound under the omnibus argument.
2. **Backward-compatible additive-only discipline.** Every v1.1.0 change is optional; every v1.0.0 artifact remains v1.1.0-valid. Minor version bump signals the right thing (additive capability expansion); major version bump (Alternative A2) would inflate semantic versioning meaninglessly.
3. **SHOULD-recommended shapes for value/red_line (P3/P4), not MUST-prescribed.** Empirical self-convergence justified recommendation discipline (Alternative A4 rejection). Validator warnings encourage migration without rejecting valid v1.0.0 artifacts. Future v1.x or v2.0.0 may tighten if drift surfaces.
4. **Policies as items, not catalog-level prose.** Independent versioning, addressability by id, atomic-bundle transportability — same properties that drove positions and jobs to items in v1.0.0. Alternative A3 (catalog-level prose) rejection is structurally consistent.
5. **Per-org opt-in migration over mandated sweep.** Adopters update when they have new content to add (vision, principles, policies), not for the sake of updating. Reduces administrative overhead; respects per-org cadence; preserves adopter sovereignty.
6. **Schelling-point framing for informative recommendations (P7/P8/P9).** Informative SHOULD/MAY language with explicit anti-divergence framing. Spec recommends specific approaches not to bless any one implementation but to prevent fragmentation. Equal-citizen-runtime discipline preserved.
7. **No-formal-proposal-for-appendix-additions exception (OQ4 clarification).** Informative appendices grow via documentation updates within the same major version; normative content requires formal proposal artifacts. Discipline boundary made explicit to prevent future drift in either direction.

## Items not incorporated

None substantively. Two clarifying framings added in decision text:

1. **P8/P9 anti-divergence framing** — proposal body is mostly already on this footing; decision reinforces. No proposal text modification.
2. **Migration sweep as per-org opt-in** — Decision Request item 5 from the proposal authorizes a sweep; decision reframes as per-org opt-in. Adjusts execution discipline without changing the substantive ratification.

Both framings are decision-level execution discipline, not proposal-text modifications.

## Workflow validation

- **Strategist scope check:** All nine P-items are orgdef SCHEMA-shape, informative SCHEMA.md appendices, or runtime edit-rules grounded in artifact validity. All within orgdef-strategist scope per the orgdef-strategist roledef output_contract.strategist_deliverables. Cross-spec coordination routed via separate memo (roledef) per proposal § Cross-spec Coordination; no other spec coordination required for v1.1.0 ship.
- **Cross-spec discipline:** roledef `recommended_capabilities` coordination is non-blocking and parallel-shipping. No same-head provenance concerns for v1.1.0 itself (the roledef-side decision is roledef-strategist's, not held same-head with orgdef-strategist during this decision).
- **Data-vs-pattern sharpening check:** all nine P-items verified format-shape post-sharpening (see Rationale § "On the data-vs-pattern sharpening"). One forward-reference flagged for canonical-template residence (see below).
- **Director ratification:** Directional call authorized 2026-05-23 by Director "I agree with all of your recommendations and decisions, proceed" directive responding to strategist review report. This decision artifact drafted for Director acceptance per standard pattern.

## Forward-reference resolution

- **canonical-orgs library residence post-data-vs-pattern-sharpening:** the existing canonical-template `oagp-family-open-standard` (and any future canonical-templates) lives in `orgdef-spec/proposed-orgs/`. Post-sharpening, the question of whether canonical-orgs templates for OAGP-shaped organizational patterns properly belong in orgdef-spec, oagp-org, or both is open. This decision's build directive (P5 — canonical-template patch) lands at current residence; if subsequent strategist coordination relocates or splits the canonical-orgs library, the v1.1.0 patches travel accordingly. Tracking via the separate ai-pair-built-saas deferred decision (filing pending coordination memo to oagp-strategist).
- **roledef SCHEMA v1.2.0 `recommended_capabilities`** — parallel cross-spec proposal in flight per proposal § Cross-spec Coordination. orgdef:Position transitive capability inheritance through `role_definition` and `job_definition` references becomes the natural composition when both ship. Not blocking; tracking informally for forward awareness.
- **openbraid renderer + edit-tool updates for P1/P2** — engineer's track; no spec-side blocker. Future openbraid memo confirming P1/P2 rendering + editing will close the implementation loop.
- **Validator-as-CI-step automation** — listed in inherited Known Work Items; v1.1.0 validator-behavior expectations (accept v1.0.0; warn on non-canonical shapes) come online when validator tooling lands. Until then, strategist self-validation.
- **Future v1.2.0+ proposals for OQ-deferred items** — Policy nesting (OQ1), value-item scope (OQ2), multi-master master_url (OQ3) become candidate v1.2.0+ proposals if empirical adopter pressure surfaces. No commitment this cycle; flagged for future-proposal triage.
- **Migration sweep follow-through** — Thingalog as first-mover candidate; other operational orgs adopt v1.1.0 fields on their own cadence as new content warrants. No mandated cross-org sweep; tracking organically.

## Notes

- This is the first substantive orgdef SCHEMA decision filed by orgdef-strategist post-data-vs-pattern-sharpening. The sharpening cleanly preserves all nine P-items as format-shape; the proposal's filing date (2026-05-17) predates the sharpening (2026-05-23) but the substantive content held up under post-sharpening review without modification.
- The omnibus packaging (3-into-1) is a useful workflow precedent worth noting: when multiple convergent signals describe the same artifact-surface area within a short interval, omnibus packaging reduces review overhead and produces one upgrade target. The reverse discipline (splitting unrelated changes into separate proposals) remains correct when changes describe DIFFERENT artifact-surface areas; the omnibus exception requires shared surface-area as the load-bearing predicate.
- The Schelling-point framing for informative recommendations (P7/P8/P9) is a useful pattern for spec-level guidance that empirically grounds in one runtime's implementation choices but serves cross-runtime anti-divergence purposes. Worth keeping as a framing precedent for future informative-appendix work.
- The "no formal proposal for appendix additions within same major version" exception (OQ4 clarification) is a small operational discipline that prevents informative-appendix updates from being blocked by formal-proposal overhead. Discipline boundary made explicit; normative content remains formal-proposal-gated.

## References

- Originating proposal: [proposals/schema-v1.1.0-charter-fields-and-edit-discipline.md](../proposals/schema-v1.1.0-charter-fields-and-edit-discipline.md)
- Director ratification: 2026-05-23 conversation in orgdef-strategist chair ("Proposal 1: I agree with all of your recommendations and decisions, proceed.")
- Originating signals:
  - Signal A: Director 2026-05-11 (org-page display ambitions)
  - Signal B: [memos/read/2026-05-11-1700--openbraid-engineer--orgdef-strategist--programmatic-edit-experience.openthing](../memos/read/2026-05-11-1700--openbraid-engineer--orgdef-strategist--programmatic-edit-experience.openthing) (F-edit phase implementation experience)
  - Signal C: Director 2026-05-11 (master/replicant discipline ratification)
- Sibling decisions for shape-comparison:
  - [proposal-inter-position-communication-convention.md](proposal-inter-position-communication-convention.md) (closest shape precedent — content-only convention addition)
  - [proposal-orgdef-as-opencatalog-substrate-shape.md](proposal-orgdef-as-opencatalog-substrate-shape.md) (precedent for substrate-shape changes; the v0.x → v1.0.0 substrate-shape correction this builds atop)
  - [proposal-canonical-template-v1.1-and-placement-convention.md](proposal-canonical-template-v1.1-and-placement-convention.md) (precedent for canonical-template patch coordination)
- Data-vs-pattern sharpening (for post-sharpening scope verification): [memos/read/2026-05-23-1100--thingalog-strategist--orgdef-strategist--handoff-addendum-data-vs-pattern.body.md](../memos/read/2026-05-23-1100--thingalog-strategist--orgdef-strategist--handoff-addendum-data-vs-pattern.body.md)
- Cross-spec coordination memos:
  - To roledef-strategist (recommended_capabilities, parallel v1.2.0 proposal): filed per proposal § Cross-spec Coordination; recipient repo path TBD per cross-spec memo convention
  - To oagp-strategist (v1.1.0 ship FYI; canonical-orgs library residence forward-reference): TBD when orgdef-strategist files; not blocking v1.1.0
- canonical-template currently patched at v2.1.0 (per Build directive item 5): [proposed-orgs/oagp-family-open-standard.opencatalog](../proposed-orgs/oagp-family-open-standard.opencatalog)
- Conformance fixtures landing in `tests/v1.1.0/` per Build directive item 4
