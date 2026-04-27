# orgdef Inclusion Decision: catdef-org

**Disposition:** Accepted into canonical library
**Origin:** PR #1 (orgdef's first roledef-style submission; first orgdef artifact in canonical)
**Decided:** 2026-04-26 by orgdef-strategist (currently played by the same session arc as catdef-strategist and roledef-strategist; role-separation acknowledged)
**Validator:** orgdef-strategist self-validation in validator capacity (PASS, no notes; see PR #1 description)
**Source-project peer review:** N/A (self-extracted by the role's incumbent — the extractor IS the source per the dual-review policy inherited from roledef)

## Disposition

`catdef-org.openthing` v1.0.0 is accepted into the canonical orgdef library at `orgs/catdef-org.openthing` (with `.json` mirror at `orgs/catdef-org.json`). Catalog entry added (`items_count` 0 → 1); this decision artifact filed; sample memo fixture added at `conformance/valid_orgs/sample-memo.openthing` demonstrating the `x.memo.*` extension shape.

This is the **first orgdef artifact in canonical** and the **bootstrap-anchor for the orgdef library** — same empirical-anchor pattern as roledef (DangerStorm anchored senior-jaded-vc-associate; the catdef + roledef bootstrap anchored senior-open-standards-strategist). The catdef-org orgdef artifact describes the actual organization that built this entire stack, providing both a worked example of orgdef's expressiveness and a permanent record of the bootstrap-era org structure.

## Rationale

This artifact is a self-extraction by the orgdef-strategist incumbent (currently the same session arc as catdef-strategist and roledef-strategist — the bootstrapping session). Same provenance class as the other self-extracted artifacts in the catdef-family canonical libraries.

The artifact captures three distinct things, each load-bearing:

1. **The catdef-org's actual structure** — 12 positions across human-steward, 4 strategist roles, 3 maintainer roles, 1 validator, 1 contributor (shared), 1 canonical-implementor, 1 vacant reference-implementor. 25 relationships across 7 standard relationship types (reports_to, peer_of, derives_from, drafts_for, implements_for, validates_for, coordinates_with). Every position and relationship is grounded in documented role definitions in CLAUDE.md / CONTRIBUTING.md / roledef library / catdef.org PRs — no positions invented.

2. **The first instantiation of the `x.org.memo_location` convention** — declared as the **per-recipient working-repo `./memos/` pattern**, enforced via the **authorization-implies-write-access principle**. Each position carries an `x.position.working_directory` extension; memos to that position live in that directory's `./memos/` subdirectory. The convention separates transport (how notifications flow: human-steward today, MCP-as-notification / file-watcher / RSS / SMTP future) from content (memos as `.openthing` files in the recipient's working repo). Articulated by the human steward in conversation 2026-04-26 in two stages: first as a central `s:/memos/` location, then refined to per-recipient working-repo `./memos/` after the steward observed that authorization-implies-write-access provides belt-and-suspenders structural enforcement (sender authority enforced by repo permissions; recipient checks one place; memo+work+git history co-located; no central inbox to corrupt or lose). The corrected design ships in v1.0.0 (caught pre-merge; no v1.0.1 retrofit needed).

3. **The first specification of the `x.memo.*` extension namespace** — declared in `x.org.memo_extension_namespace` as a worked-example schema for memo `.openthing` files (from / to / subject / sent / in_reply_to / action_required / body). Initially informal x.* extensions; eventually anticipated to be promoted to a `memodef:Memo` namespaced type in a future memodef-spec/memodef consumer-spec when patterns crystallize from real use. The sample memo at `conformance/valid_orgs/sample-memo.openthing` demonstrates the extension shape as a concrete artifact.

## Notable design choices accepted

1. **Per-recipient working-repo memo location** (corrected from initial central-location draft). `x.org.memo_location` declares the convention `<recipient_position.x.position.working_directory>/memos/`, not a single literal path. Each position carries an `x.position.working_directory` extension naming the repo it operates in (e.g., catdef-canonical-implementor's working_directory is `s:/projects/catdef.org/`). A memo from `roledef-strategist` (working in `s:/projects/roledef-spec/roledef/`) to `catdef-canonical-implementor` (working in `s:/projects/catdef.org/`) lives at `s:/projects/catdef.org/memos/` — in the recipient's repo, NOT a central location, NOT the sender's repo. **Establishes precedent (revised mid-PR-#1)**: authorization-implies-write-access. Sender's authority to direct recipient is structurally enforced by repo permissions; recipient checks one place (their own repo); memo+work+git history are co-located for natural audit; no central inbox to corrupt or lose; cross-repo memos require explicit cross-repo authorization, naturally limiting org-wide ('all') broadcasts to high-authority senders. The initial draft proposed a central `s:/memos/` location; pre-merge review by the human steward surfaced the better design.

2. **Memo extension namespace declared in the org artifact, not in orgdef SCHEMA.md.** Per the human steward's articulation: "we need to extend .thing to have a sender and a receiver. Initially we can do it with an x. extension." The extension is at the catdef `.openthing` level (any thing can be a memo by carrying x.memo.* extensions), not at the orgdef:Organization level. The org artifact documents the convention (so future readers of catdef-org know what to expect on memos in this org's memo location) but doesn't extend orgdef SCHEMA.md. **Establishes precedent**: emerging extension conventions get documented at the first-instance org artifact's level; promotion to spec text happens when patterns crystallize across multiple orgs.

3. **Several positions with `status: informal`.** 7 of 12 positions are informal (operationally active but not yet roledef-extracted). This is acceptable per orgdef SCHEMA.md `status` enumeration; the artifact accurately captures the bootstrap-era reality where many roles are played but not all have been formalized as roledefs. Eventual self-extraction of these informal positions is a forward work item per strategist memory. **Establishes precedent**: orgdefs SHOULD accurately represent informal positions rather than pretend they don't exist or pretend they're staffed-with-roledef.

4. **Multi-position incumbency declared explicitly.** catdef-strategist, roledef-strategist, and orgdef-strategist all declare the same `incumbent.session_arc` (the bootstrapping session played all three roles). The role-separation discipline is enforced via decision-artifact attribution per the established convention; the orgdef artifact accurately captures the multi-role-played-by-one-session reality. **Establishes precedent**: orgdefs SHOULD declare honest incumbent attribution including multi-position cases.

5. **`x.org.notes` for operational context.** Three notes capture operational realities that don't fit cleanly into positions or relationships: the multi-role-bootstrap reality, the informal-position pattern, and the human-steward's authority flow (with memo convention as the labor-reduction mechanism). **Establishes precedent**: free-form `x.org.notes` is acceptable for operational context that's important for org consumers but doesn't fit the structured fields.

6. **Relationship type usage:** 8 reports_to, 6 peer_of (3 strategist-pairs + 3 maintainer-pairs), 3 drafts_for, 3 coordinates_with, 2 derives_from (catdef-strategist, roledef-strategist both deriving from senior-open-standards-strategist-abstract), 2 implements_for, 1 validates_for. Validates the orgdef SCHEMA.md standard relationship type set: every standard type was applicable to documented relationships in catdef-org. **No need for `x.<domain>.<identifier>` relationship type extensions** for this org — the standard set covered everything. (Future orgs may need extensions; this one didn't.)

## Items adjusted at promotion

None. Submission was authored by the strategist directly; no contributor intermediary; date and authorship metadata correct as authored.

## Workflow validation (first orgdef pass; bootstrap-anchor)

This was the **first run of orgdef's `proposed-orgs/` → `orgs/` two-stage workflow**. Workflow followed the same shape established by roledef:

1. ✓ Branch created (`submit-catdef-org`)
2. ✓ Artifact authored by orgdef-strategist incumbent (also catdef-strategist + roledef-strategist incumbent during bootstrap; role-separation acknowledged)
3. ✓ Strategist self-validation in validator capacity — PASS (12 positions / 25 relationships / all relationship from-to references resolve / 5 role_definition references resolve in canonical roledef library / position-id uniqueness check passes / all reserved-namespace constraints satisfied / x.org.* extensions properly self-described)
4. ✓ Source-project peer review skipped (self-extracted; not applicable)
5. ✓ Atomic promotion in same PR (file in proposed-orgs/ + orgs/ + .json mirror + catalog update + decision artifact + sample-memo fixture)
6. ✓ Strategist sign-off (this decision)
7. ✓ Single-merge promotion

The workflow performed as designed. No friction surfaced. Pattern is approved as the standard for future orgdef submissions.

## Forward-reference resolution

`catdef-org.metadata.related: ["roledef-spec/roledef library", "catdef-spec", "catdef.org", "render.catdef.org"]`:

These are informal references (free-form strings, not id+url). Acceptable for v0.1; future orgdef versions may formalize cross-org references with id+url shape. All four referenced repos/services exist and are operational.

`role_definition` references on positions:

- ✓ `senior-open-standards-strategist v1.0.0` resolves in canonical roledef library
- ✓ `catdef-strategist v2.0.0` resolves in canonical roledef library
- ✓ `roledef-strategist v1.0.0` resolves in canonical roledef library
- ✓ `roledef-validator v1.0.0` resolves in canonical roledef library
- ✓ `roledef-contributor v1.0.0` resolves in canonical roledef library

7 positions have no `role_definition` reference (status: informal or vacant) — acceptable per SCHEMA.md SHOULD-rule (informal positions are a recognized status). Eventual roledef-extraction is a forward work item.

## Runtime test

Runtime Turing test deferred per established v0.1 pattern. The artifact's structural correctness is verified; behavioral validation depends on orgdef-aware tooling (graph layout, role-resolution, memo-routing) which is v0.2+ work.

The artifact is **immediately useful** in two ways even before orgdef-aware tooling lands:
- Renderable in render.catdef.org (per catdef-family namespaced-type support shipped in catdef.org PR #2 — the artifact's `type: "orgdef:Organization"` will trigger single-thing rendering with all top-level fields displayed)
- Readable as documentation: any human or AI session can read the artifact and reconstruct the catdef-org's structure

## Strategist memory work items

The following pattern observations from this PR will be considered for promotion to orgdef CLAUDE.md / SCHEMA.md / CONTRIBUTING.md guidance:

1. **`x.org.memo_location` SHOULD-pattern (per-recipient working-repo form)** — orgs that operate via inter-position handoffs SHOULD declare their memo convention at the org level. The catdef-org form is `<recipient_position.x.position.working_directory>/memos/`, enforcing authorization-implies-write-access. Recommend documenting in orgdef SCHEMA.md as a recognized SHOULD pattern after a second org artifact uses the same pattern.

2. **`x.position.working_directory` SHOULD-pattern on positions** — positions that are memo-addressable SHOULD declare their working repo via `x.position.working_directory`. Positions without this extension are not directly memo-addressable (memos to them flow via human-steward routing or via positions they operate from). Recommend documenting in orgdef SCHEMA.md as a SHOULD-pattern after second-org adoption.

3. **`x.memo.*` extension namespace as a memo-message convention** — emerging convention; document as adopter-defined extension pattern initially; promote to a memodef-spec/memodef consumer-spec when 2+ orgs use the convention with consistent shape. Forward-work item: bootstrap memodef-spec when patterns crystallize.

4. **Authorization-implies-write-access discipline as a design principle** — articulated by the human steward 2026-04-26 in the context of memo addressing. Beyond memos, this principle applies to any inter-role direction: if role A wants to direct role B, A must have write access to B's working repo. Same model as PR-based code review. **Recommend strategist consider promoting as a CLAUDE.md / governance-design principle for any catdef-family ecosystem with multi-role coordination.**

5. **Honest informal-position disclosure** — orgdefs SHOULD accurately represent operationally-active-but-not-yet-roledef-extracted positions as `status: informal` rather than omitting them or pretending they're staffed. catdef-org is the first instance; recommend documenting in orgdef CONTRIBUTING.md as a SHOULD-pattern after one more orgdef uses it.

6. **Multi-position-incumbency disclosure** — when one session plays multiple positions during bootstrap or transition, orgdefs SHOULD declare honest `incumbent.session_arc` attribution including multi-role cases. Same precedent-setting / future-promotion pattern.

7. **Sample-memo fixture in `conformance/valid_orgs/`** — the sample memo demonstrates an emerging convention as a worked-example artifact. Useful pattern for future emerging conventions in catdef-family specs: document in the spec, demonstrate in conformance fixtures, formalize when patterns settle.

8. **Pre-merge convention refinement as a workflow strength** — the memo convention in this PR was corrected pre-merge (initial draft proposed central `s:/memos/`; refined to per-recipient working-repo `./memos/` after human-steward review surfaced authorization-implies-write-access). The two-stage workflow (proposed-orgs/ → orgs/) gave the human steward a natural review checkpoint. **Recommend documenting in orgdef CONTRIBUTING.md that pre-merge review SHOULD surface design-level corrections, not just schema-level corrections.**

## Notes

- **Strategist bot identity:** this decision is provisionally attributed to `orgdef-strategist <orgdef-strategist@orgdef.org>` pending governance ratification (Known Work Item, inherited from the catdef-family pattern).

- **Library state after this PR:** 1 orgdef artifact in canonical (catdef-org). The orgdef library is no longer empty.

- **Memo convention status:** declared in this artifact; first operational memo already sent at `s:/projects/catdef.org/memos/2026-04-26-2030--roledef-strategist--catdef-canonical-implementor--pr5-string-raw-template-literal.openthing` (PR #5 brief in catdef.org repo, addressed to brother-canonical-implementor). The convention is operationally validated via that first memo. The sample memo at `conformance/valid_orgs/sample-memo.openthing` is a fixture demonstrating the extension shape and announcing the convention to all positions.

- **Forward work item: memodef-spec/memodef consumer-spec.** When the `x.memo.*` extension pattern is used by 2+ orgs OR proves to need a richer schema than free-form extensions support, bootstrap a `memodef-spec/memodef` consumer-spec following the same catdef-family pattern (own GitHub org, own canonical repo, own SCHEMA / CONTRIBUTING / CLAUDE / catalog / etc.). The memodef-strategist would derive from senior-open-standards-strategist, joining catdef-strategist / roledef-strategist / orgdef-strategist as siblings.

- **Forward work item: orgdef-strategist roledef.** orgdef-strategist is currently played informally by the catdef + roledef strategist session arc. Eventual self-extraction as a roledef (derivation of senior-open-standards-strategist) is a forward work item — same procedure as catdef-strategist v2.0.0 and roledef-strategist v1.0.0.

- **The recursive case continues.** Just as the strategist roledef was authored by the strategist (PR #18 in roledef), the catdef-org orgdef artifact is authored by the catdef-org's strategists. The org describes itself; the artifact's authors are positions within the artifact. catdef-family eats its own dogfood.

## Cross-references

- PR: https://github.com/orgdef-spec/orgdef/pull/1
- Org artifact: [`../orgs/catdef-org.openthing`](../orgs/catdef-org.openthing) (mirror: [`../orgs/catdef-org.json`](../orgs/catdef-org.json))
- Catalog entry: [`../catalog.opencatalog`](../catalog.opencatalog)
- Sample memo fixture: [`../conformance/valid_orgs/sample-memo.openthing`](../conformance/valid_orgs/sample-memo.openthing)
- Schema reference: [`../SCHEMA.md`](../SCHEMA.md)
- Referenced roledefs (all in roledef-spec/roledef canonical library): senior-open-standards-strategist, catdef-strategist v2.0.0, roledef-strategist v1.0.0, roledef-validator, roledef-contributor
- Sister catdef-family orgs: catdef-spec (substrate; no orgdef artifact yet — same org, but declared once here), catdef.org (ecosystem-services repo), render.catdef.org (rendering service)
- Source materials: catdef-spec/CLAUDE.md, roledef CLAUDE.md + CONTRIBUTING.md, all 8 published roledefs in canonical, catdef.org PRs #1-#3 + in-flight #4, strategist memory file
