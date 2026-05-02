# Proposal Decision: Operational org-artifact filename suffix `-organization`

**Disposition:** Accept (no modifications; OQs resolved inline)
**Origin:** [proposals/operational-org-artifact-naming-convention.md](../proposals/operational-org-artifact-naming-convention.md)
**Decided:** 2026-05-01 by orgdef-strategist
**Authorization:** Director (Product Owner) explicitly ratified the directional call inline 2026-05-01: "Proceed, -organization, direct. This is still early days, we can do a bit of cowboying." Direct-execute mode authorized — strategist drafts proposal + decision + executes the multi-repo migration in one session, rather than the maintainer-review-first sequencing.
**Bootstrap caveat:** Same-head provenance — orgdef-strategist holds catdef-strategist + roledef-strategist + memodef-strategist informally during bootstrap. The migration touches five working repos (orgdef-spec, memodef-spec, roledef-spec, catdef-spec, thingalog) under one head; commits use the orgdef-strategist bot identity for migration commits; the operational org artifact in each repo is the only file touched per repo (plus thingalog's roledef + catdef-spec's local conventions, addressed below).

## Disposition

Accepted as drafted; no modifications. The proposal cleanly captures the structural call (operational `org/` filename suffix `-organization`); explicitly defers Tier 2 (canonical-library `orgs/` rename + id cascading) to the v0.3 SCHEMA bundle; bundles the canonical-template patch with the in-flight inter-position v1.2.0 patch. All three Open Questions resolve to the working positions stated in the proposal.

## Rationale

### Why Accept

The Director-surfaced friction is empirically grounded: `thingalog/org/thingalog.openthing` reads as the product Thingalog when consumed in isolation (file browser, search, render.catdef.org cards, commit-message shorthand), failing AI-legibility primacy. The fix is structural — a filename suffix that encodes artifact type so the file is self-readable without path context.

The choice of `-organization` over `-org` (the canonical-library precedent) is defended by AI-legibility primacy: explicit nouns beat abbreviations for machine readers. The 9-character cost per filename is acceptable; family precedent for full nouns over abbreviations exists (`oagp-family-open-standard`, `senior-open-standards-strategist`).

The decision to keep the artifact's `id` field unchanged (only filename gains the suffix) preserves cross-spec id references — `metadata.org_definition.id` in roledef:Job artifacts, cross-spec memo references, validators that resolve org references by id — all stay valid. The AI-legibility win is at the filename level, not the id level; id is consumed in machine-readable references where its meaning is unambiguous.

The Tier 2 deferral (canonical-library rename + id cascade) is the right call: bundling with v0.3 SCHEMA work that's already pending consolidates review effort and avoids spreading similar-shape content updates across multiple sessions.

### Why no modifications

The proposal does not exceed its stated scope (operational `org/` only; canonical library Tier-2-deferred). The three OQs have defensible working positions (`x.org.org_location` extension parallel to memo_location; per-artifact version bumps; v0.3 SCHEMA bundle for Tier 2). No changes to the proposal text required.

### Direct-execute mode caveat

Director authorized direct-execute mode in light of the early-bootstrap arc state. Execution proceeds in this same session: proposal + decision + canonical-template patch + CONTRIBUTING.md patch + five-repo migration + per-repo commits + push. This collapses the proposal-review-decision-implement sequence into one strategist-driven pass; appropriate for low-controversy, well-bounded changes during bootstrap where same-head provenance is the operational reality.

The artifact trail is preserved: proposal + decision filed in orgdef-spec proper; migration commits use orgdef-strategist bot identity; cross-references in CONTRIBUTING.md and canonical-template instantiation_notes record the convention so future sessions inherit the discipline.

## Resolutions to Open Questions

### OQ1 → Yes, `x.org.org_location` extension parallel to `x.org.memo_location`

**Strategist call: yes.** Author's working position. Same SHOULD-with-machine-discoverable-escape-hatch shape established in the inter-position-communication-convention decision (where `x.org.memo_location` is the per-org override for memo placement). For the org-artifact placement, `x.org.org_location` provides the same escape hatch for monorepo and vendor-imposed-layout adopters.

CONTRIBUTING.md prose addition documents the extension; no SCHEMA changes required (extensions live in the catdef-substrate's `x.<domain>.<identifier>` namespace).

### OQ2 → Per-artifact version bump

**Strategist call: per-artifact.** Author's working position. Each org artifact has its own version-history-arc; synchronized version bumps would muddle that. Each artifact takes a minor bump (or patch, at strategist discretion when applying) from its current version, with `metadata.history` capturing the rename rationale. Concrete plan executed in this session:

| Repo | Current version | Post-rename version |
|---|---|---|
| orgdef-spec | 1.0.0 | 1.1.0 (additive minor — filename rename + history entry) |
| memodef-spec | TBD (read at execute time) | minor bump from current |
| roledef-spec | TBD (read at execute time) | minor bump from current |
| catdef-spec | TBD (read at execute time) | minor bump from current |
| thingalog | 1.3.1 | 1.3.2 (patch — the substantive content unchanged; only placement) |

(Per-artifact version values resolved at migration execution time; the discipline is "minor bump if metadata.history change is substantive; patch if purely-cosmetic placement change.")

### OQ3 → Tier 2 deferred to v0.3 SCHEMA bundle

**Strategist call: defer.** Author's working position. Canonical-library rename + id cascading is a 13-cross-reference fan-out; bundling with the v0.3 `__slot__` migration + structured cross-org references + `metadata.kind` enforcement work consolidates review effort. Filed as a forward-work item; no concrete date.

Cross-cost: the temporary divergence between operational `<spec>/org/<id>-organization.openthing` and canonical-library `<spec>/orgs/<id>-org.openthing` is real but acceptable — both conventions are self-readable in their own right; the divergence is a known parking issue, not a permanent design choice.

## Build directive (this session — orgdef-strategist executes per Director authorization)

Execute in this order:

1. **Canonical-template patch** — apply to `proposed-orgs/oagp-family-open-standard.openthing`:
   - Append the operational-filename clause to `metadata.instantiation_notes` per P1 of the proposal
   - This patch BUNDLES with the inter-position-convention v1.2.0 patch already in the orgdef-maintainer build directive: BOTH changes land in canonical-template version `1.2.0` as one cohesive update. (Maintainer applies both decision artifacts together; this decision and the inter-position decision are co-equal inputs to v1.2.0.)
2. **CONTRIBUTING.md patch** — extend the "Inter-position communication conventions" section (or a new "Org-artifact filename conventions" subsection if cleaner) per P2 of the proposal
3. **Per-repo operational-org-artifact migration** (in this order, one repo at a time, per the parallel-session-aware push hygiene from the project memory):
   1. orgdef-spec: `git mv org/orgdef-spec.openthing org/orgdef-spec-organization.openthing`; update metadata.repository + history; commit + push
   2. memodef-spec: `git mv org/memodef-spec.openthing org/memodef-spec-organization.openthing`; update metadata.repository + history; commit + push
   3. roledef-spec: `git mv org/roledef-spec.openthing org/roledef-spec-organization.openthing`; update metadata.repository + history; commit + push
   4. catdef-spec: `git mv org/catdef-spec.openthing org/catdef-spec-organization.openthing`; update metadata.repository + history; commit + push (note: catdef-spec local git config defaults to catdef-maintainer bot; commits override --author to orgdef-strategist)
   5. thingalog: `git mv org/thingalog.openthing org/thingalog-organization.openthing`; update metadata.repository + history; commit + push
4. **Cross-reference updates** in each repo's `metadata.org_definition.url` references (in roledef:Job artifacts at `org/jobs/`) — update from old to new filename path
5. **README.md / SCHEMA.md prose updates** in orgdef-spec where the example placement is cited
6. **Final verification** — all five operational org artifacts at new path; all metadata.repository URLs match; no stale references to old filename in tracked files

orgdef-maintainer scope (post-this-session):
- Schema-conformance review of the canonical-template patch and CONTRIBUTING.md prose
- Independent audit that no cross-references to the old filename remain unaccounted-for in family-wide artifacts (decision artifacts, memos, render.catdef.org configurations, etc.)

## Cross-spec coordination

This decision is orgdef-spec-side only. The migration touches four sibling-spec repos (memodef-spec, roledef-spec, catdef-spec) and one adopter repo (thingalog), but the touch is mechanical rename + metadata update — not a strategist-level call in those specs' scopes. Per the v1.1 placement-convention precedent, Director authorization for cross-repo execution under one head's authority is appropriate during bootstrap; future ratification can audit via the migration commits in each repo.

No memos to sibling-spec strategists are required for this change. The convention is documented in canonical-template + CONTRIBUTING.md; sibling specs inherit the convention as adopters of the canonical.

## Notable design choices

1. **Filename suffix vs id change.** Choosing to add the suffix at filename-only (not at id) preserves cross-spec id references and limits migration cost. The AI-legibility win is at filename consumption (file browser, search, renderer cards, shorthand) — not at id-as-machine-reference, where the id's meaning is already unambiguous in context. Right shape for the right cost.
2. **Bundle with inter-position v1.2.0.** Co-targeting canonical-template version `1.2.0` for two patches (inter-position recommended_patterns entry + operational-filename instantiation_notes clause) avoids version churn and keeps the canonical-template's v-history clean. Both patches are additive; both ratified in adjacent decision artifacts.
3. **Tier 2 deferral.** The canonical-library rename's 13-cross-reference cascade is real cost; bundling with the in-flight v0.3 SCHEMA work that ALSO touches canonical-library content (`__slot__` migration) is the natural consolidation. Doing it now would produce two parallel modifications-of-the-same-content, which costs more in review and conflict-resolution than waiting.
4. **Direct-execute mode is appropriate during bootstrap, not after.** This decision relies on Director's "we can do a bit of cowboying" authorization; once governance ratifies the bot identities and a separate orgdef-maintainer seat exists, the proposal-review-decision sequence should re-engage. Direct-execute is the bootstrap operational reality, not the steady-state operating posture.

## Items not incorporated

None. Proposal accepted as drafted.

## Workflow validation

- **Strategist scope:** library-curation + placement-convention call within strategist scope per the orgdef-strategist roledef output_contract.strategist_deliverables (design calls, scope decisions, library-curation rulings).
- **Cross-spec discipline:** This decision is orgdef-spec-side; cross-repo execution under Director authorization. No call made in catdef/roledef/memodef strategist scopes.
- **Director ratification:** Directional call ratified inline 2026-05-01; direct-execute mode authorized; this decision artifact captures the strategist-call rationale for future audit.

## Forward-reference resolution

- **Tier 2 (canonical-library rename):** filed as a forward-work item; bundles with the v0.3 SCHEMA work pending per the canonical-orgs-library decision's build directive
- **`x.org.org_location` extension formalization:** documented in CONTRIBUTING.md prose; formal SCHEMA-level documentation deferred until adopted by an actual adopter

## Notes

- This is the second placement-convention decision in the OAGP family arc (after canonical-template v1.1 + placement-convention 2026-04-30). The pattern emerging: small placement conventions surface organically from real adopter friction (Thingalog, Director-noticed product-vs-org filename ambiguity); strategist call + canonical-template patch + multi-repo migration is the right scaling shape. Tracking informally; if a third placement convention surfaces with similar shape, worth canonizing the workflow itself.
- Director used the phrase "early days" + "cowboying" — direct-execute mode is appropriate here. Logging for retrospective review when bootstrap stabilizes: which conventions ended up requiring proposal-first sequencing, and which ended up well-served by direct-execute, to inform when to switch postures.

## References

- Originating proposal: [proposals/operational-org-artifact-naming-convention.md](../proposals/operational-org-artifact-naming-convention.md)
- Director ratification: 2026-05-01 conversation in orgdef-strategist chair
- Bundle-mate decision (co-targeting canonical-template v1.2.0): [decisions/proposal-inter-position-communication-convention.md](proposal-inter-position-communication-convention.md)
- Prior placement-convention decision (precedent for direct-execute under Director authorization): [decisions/proposal-canonical-template-v1.1-and-placement-convention.md](proposal-canonical-template-v1.1-and-placement-convention.md)
- Canonical-orgs-library decision (cited for Tier 2 deferral rationale): [decisions/proposal-canonical-orgs-library.md](proposal-canonical-orgs-library.md)
