# Proposal Decision: Charter shape additions (vision / values / red_lines / recommended_patterns) + SSoT rule + position.job_definition

**Disposition:** Accept with Modifications
**Origin:** [proposals/charter-shape-additions.md](../proposals/charter-shape-additions.md)
**Decided:** 2026-04-26 by orgdef-strategist
**Composes with:** [`roledef-spec/roledef/decisions/proposal-role-vs-job-distinction.md`](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-role-vs-job-distinction.md), [`roledef-spec/roledef/decisions/proposal-job-placement-and-charter-slots.md`](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-job-placement-and-charter-slots.md) — incorporates the SSoT rule (M3 carryover) and `position.job_definition` follow-on (M7) per cross-spec coordination obligation.
**Cross-spec:** Decision filed at the orgdef seat; the roledef-side coordination is already complete via the two referenced decisions. Memo to roledef-strategist forthcoming as a courtesy notification (no roledef-side action required).
**Bootstrap caveat:** Orgdef-strategist authority currently held by the same head as roledef-strategist authority during the catdef-family bootstrap. Per role discipline, the artifact trail still goes through originating-repo `proposals/` and receiving-repo `decisions/`; this decision is the orgdef-side decision-of-record despite the same-head provenance.

## Disposition

The charter-shape-additions package — adding `vision`, `values`, `red_lines`, `recommended_patterns` to `orgdef:Organization`, plus `position.job_definition` to `orgdef:Position`, plus articulating the SSoT rule from the orgdef side, plus documenting the org-folder filesystem convention and two-section charter discipline in CONTRIBUTING.md — is **Accepted with three modifications** described below. The empirical grounding is strong (dogfood demonstrated each addition), the cross-spec coordination is complete (roledef-side decisions already landed), and the schema additions are purely additive (existing v0.1 orgdefs remain valid).

The three modifications resolve issues that surfaced during the migration of the orgdef-spec orgdef artifact from markdown to formal `.openthing` — issues that only became visible when actually populating the proposed schema with real content.

## Rationale

### Why Accept

The proposal correctly identifies five content-shapes from the orgdef-spec dogfood that don't fit v0.1's fields, and articulates each with a clear rationale grounded in real authored content. The cross-spec coordination obligations (SSoT rule, position.job_definition) are mechanical follow-ons from already-accepted roledef-side decisions; declining them would put orgdef out of sync with the family. The filesystem and two-section conventions are observed-in-practice patterns that deserve documentation.

The proposal's "values with rationale" innovation is the most consequential addition: it elevates value statements from folk wisdom to defensible MUSTs by requiring the *why*. The completeness-as-hallucination-prevention example is the proof — the same statement framed as preference would be vulnerable to bikeshed; framed as a technical rule grounded in machine-reader behavior, it survives challenge. This pattern is borrowed by `red_lines` and `recommended_patterns.general` for the same reason.

The seven open questions are all answerable inline; none require deferral. Resolutions below.

### Why Modifications

The migration of `orgdef-spec/orgdef-spec-org/orgdef.md` to `orgdef-spec/orgdef-spec-org/orgdef.openthing` (executed in tandem with this decision drafting) surfaced three issues that the proposal as drafted didn't anticipate. Two are minor schema tightenings; the third is a documented-as-known-gap to defer to v0.3.

## Resolutions to Open Questions

### OQ1 → keep `red_lines`

**Strategist call: keep.** Author's weak preference. Empirically anchored from the dogfood (the markdown form used "Red lines" as the section header). Alternatives (`non_negotiables`, `prohibitions`, `refusals`) are weaker — `non_negotiables` is verbose, `prohibitions` reads punitive, `refusals` is awkward as a noun. `red_lines` carries the right register: clear, somewhat colloquial, matches how Directors and strategists actually talk about org-level commitments.

### OQ2 → RFC 2119 vocabulary for `recommended_roles.priority`

**Strategist call: RFC 2119 (MUST/SHOULD/MAY).** Author's weak preference. Family consistency wins; the rest of the spec ecosystem already uses MUST/SHOULD/MAY everywhere a priority enum appears. Switching to alternative vocabularies (required/recommended/optional) for one field would require readers to context-switch.

### OQ3 → `recommended_patterns.general` as array of objects (with rationale)

**Strategist call: array of objects.** Author's weak preference. The rationale parallel with `values` and `red_lines` is the load-bearing reason — pattern recommendations without rationale become cargo-cult prescriptions. Object shape `{pattern, description, rationale}` adds verbosity but earns it. Bare-string form rejected.

### OQ4 → SHOULD universal; MUST for canonical-library-eligible orgdefs

**Strategist call: differentiated.** The two-section charter discipline is genuinely load-bearing for canonical-library entries (which exist to be derived) but is overhead for bespoke private orgdefs that won't be derived from. Validator enforces MUST only for orgdefs in the `canonical-orgs/` directory; SHOULD elsewhere with a non-blocking lint warning.

### OQ5 → keep single `vision` field

**Strategist call: single field.** Author's weak preference. The existing `mission` already covers the concrete-deliverable side; `vision` covers the aspirational side. Splitting `vision` further (e.g., into `vision` + `north_star` or similar) is unmotivated by current empirical evidence.

### OQ6 → conformance fixture is a copy with `metadata.history` mirror note

**Strategist call: copy with mirror metadata.** The conformance fixture and the operational orgdef have different lifecycles: the fixture is pinned at the published version; the operational artifact evolves with the project. Linking via `metadata.history` notes (the fixture says "mirrored from operational at version X.Y.Z, date") preserves traceability without coupling the two for updates.

### OQ7 → structural-only at write-time; URL resolution at read-time/runtime

**Strategist call: structural-only at write-time.** Author's weak preference. Consistent with how `metadata.role_definition.url` resolution works on the roledef side per [`proposal-role-vs-job-distinction`](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-role-vs-job-distinction.md). Network-fetch at validation time creates flakiness, gates on private-repo accessibility, and slows the validator. Read-time/runtime resolution is the right separation.

## Modifications (surfaced during dogfood migration)

### M1. Promote `v1_success_criterion` to top-level field on `orgdef:Organization`

**Background:** The migration tried to express orgdef-spec's recursive v1 success criterion ("ship when you can self-describe using your own pattern"). Initially placed inside `metadata.v1_success_criterion`, but during the migration it became clear this is a *charter-level commitment*, not a metadata note about the artifact. Other orgdefs derived from canonical templates will need their own v1 success criteria, and they belong with the other charter-level fields (mission, vision, scope) rather than buried in metadata.

**Modification:** Add `v1_success_criterion` as an optional top-level field on `orgdef:Organization`:

```json
"v1_success_criterion": "<string or polymorphic, 1–3 sentences stating the testable criterion for v1 ship>"
```

Cardinality: SHOULD for orgdefs in active development; MAY otherwise. Format: prose, polymorphic per catdef i18n. The recursive self-describing-milestone pattern (already documented in `recommended_patterns.general`) is one shape; orgs may use other shapes.

### M2. Add optional `description` field to `orgdef:Position`

**Background:** The migration needed to describe positions that don't yet have a `job_definition` (orgdef-spec's `maintainer` and `canonical-implementor` positions whose jobs are forthcoming) and the human `director` position (which has neither role_definition nor job_definition, since humans are not derived from roledefs). v0.1's `orgdef:Position` has `id` and `name` but no place to describe the position's purpose when no job/role artifact carries that description.

**Modification:** Add `description` as an optional field on `orgdef:Position`:

```json
{
  "id": "director",
  "name": "Director",
  "description": "Human Director with final tiebreaker authority. No role_definition (humans are not derived from roledefs)."
}
```

Cardinality: OPTIONAL. RECOMMENDED for positions without `role_definition` or `job_definition`; otherwise the artifact is incomplete (no description anywhere).

### M3. Cross-org reference shape: documented gap, deferred to v0.3

**Background:** The migration tried to express coordination edges from `orgdef-spec.strategist` to `catdef-spec.strategist` and `roledef-spec.strategist` — cross-org `coordinates_with` relationships. v0.1's `orgdef.relationships.from`/`to` schema expects intra-org position IDs. Cross-org references are mentioned informally in CONTRIBUTING.md ("v0.1 leaves cross-org references informal — declare via coordinates_with relationship type and a free-form description") but no concrete shape exists.

The migration used an ad-hoc `external:<position-id>` prefix as a placeholder. This is unprincipled but pragmatic.

**Modification:** Document this as a known gap targeted at v0.3:

> v0.2 SCHEMA.md notes: cross-org references in `orgdef.relationships.from`/`to` are not yet formally specified. Authors MAY use the placeholder convention `external:<position-id>` (or similar prefix) with a free-form `description` to express such edges informally; validators MAY skip resolution for any reference matching the `external:` prefix. v0.3 will formalize a structured cross-org reference shape (likely mirroring the `metadata.org_definition` pattern: `{org_id, position_id, version, url}`).

This is a CONTRIBUTING.md addition + SCHEMA.md note, not a v0.2 schema change. The actual schema work happens in v0.3.

## Final shape (post-modifications)

`orgdef:Organization` gains:

```json
{
  "vision": "<string or polymorphic, SHOULD>",
  "values": [
    {"name": "<string>", "description": "<polymorphic>", "rationale": "<polymorphic>"},
    "..."
  ],
  "red_lines": [
    {"rule": "<polymorphic>", "rationale": "<polymorphic>"},
    "..."
  ],
  "recommended_patterns": {
    "general": [
      {"pattern": "<string>", "description": "<polymorphic>", "rationale": "<polymorphic>"}
    ],
    "recommended_roles": [
      {
        "role": "<string-id OR full-coordinate-object>",
        "priority": "<MUST | SHOULD | MAY>",
        "why": "<polymorphic>"
      }
    ]
  },
  "v1_success_criterion": "<string or polymorphic, SHOULD-when-applicable>"
}
```

`orgdef:Position` gains:

```json
{
  "id": "...",
  "name": "...",
  "description": "<string or polymorphic, OPTIONAL but RECOMMENDED when no role/job_definition>",
  "role_definition": "<existing field>",
  "job_definition": {"id": "...", "version": "...", "url": "..."}
}
```

Plus the SSoT rule articulation in SCHEMA.md (orgdef.relationships authoritative; placement on jobs is denormalized snapshot) and the cross-org-reference v0.3 deferral note.

## Build directive (for orgdef-maintainer)

When schema work begins:

1. **orgdef SCHEMA.md update** — define all new fields per Final Shape above; add SSoT rule statement; add cross-org-reference deferral note; add `position.job_definition` per the role-vs-job-distinction follow-on (M7); document that positions SHOULD declare at least one of `role_definition` or `job_definition` (SHOULD, not MUST, to preserve v0.1 backward compat).

2. **orgdef CONTRIBUTING.md update** — add the org-folder filesystem convention section (`<project>/<orgname>-org/` layout); add the two-section charter discipline section (SHOULD universal, MUST for canonical); add the `recommended_roles` bootstrapping checklist pattern; add the cross-org-reference informal-placeholder convention.

3. **Conformance fixtures** — per the proposal's Conformance Tests section. The migrated `orgdef-spec/orgdef-spec-org/orgdef.openthing` becomes the reference exemplar (`valid_orgs/canonical-aigp-family-spec.openthing` or similar), copied with `metadata.history` mirror note per OQ6 resolution.

4. **Validator updates** — per the proposal's validator-rules section, with M1/M2 additions: validate `v1_success_criterion` shape if present; treat `position.description` as optional but warn if a position has no `description` AND no `role_definition` AND no `job_definition` (an entirely-blank position is a likely authoring error).

5. **Version bump** — orgdef SCHEMA from v0.1.0 to v0.2.0 (additive, minor bump).

## Migration of dogfood artifact

Per the proposal's acceptance criteria #5: `orgdef-spec/orgdef-spec-org/orgdef.md` migrated to formal `.openthing` JSON form 2026-04-26 in coordination with this decision (the migration is dated the same day; the migration drove M1, M2, M3 surfaces). The migrated artifact lives at `orgdef-spec/orgdef-spec-org/orgdef.openthing` and exercises all the new fields plus the `position.job_definition` reference (the strategist position references `orgdef-strategist.openthing`).

The old `.md` form remains in place pending Director's call on cleanup (delete vs retain for compare).

## Cross-spec coordination

The SSoT rule and `position.job_definition` field are coordinated with roledef-strategist via the already-accepted [`proposal-role-vs-job-distinction`](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-role-vs-job-distinction.md) (M7) and [`proposal-job-placement-and-charter-slots`](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-job-placement-and-charter-slots.md) (M3, M6). This decision articulates the orgdef-side of the same coordination; no further roledef-side action required.

A courtesy memo to roledef-strategist is forthcoming announcing that the orgdef-side decision is filed and the migration is complete. action_required: false (informational).

## Foreshadowing: canonical template extraction

Per the proposal's Acceptance Criteria #7, the next major work item (separate proposal/PR) is to lift the migrated `orgdef-spec/orgdef-spec-org/orgdef.openthing` into a canonical-library entry — working title `canonical-orgs/oagp-family-open-standard.openthing` — that catdef-spec and roledef-spec can derive their own orgdefs from. This is the recursive completion of the dogfood: orgdef-spec doesn't just bootstrap itself, it produces the canonical template other OAGP-family specs use to bootstrap themselves.

That extraction is deliberately scoped out of this decision; it requires its own proposal-and-decision cycle, and surfaces fresh design questions (what generalizes vs what's orgdef-spec-specific; how to encode "fill these slots when deriving" in the template form; etc.).

## References

- Originating proposal: [proposals/charter-shape-additions.md](../proposals/charter-shape-additions.md)
- Empirical exemplar (now formal): [orgdef-spec-org/orgdef.openthing](../orgdef-spec-org/orgdef.openthing)
- Companion job artifact (already migrated): [orgdef-spec-org/jobs/orgdef-strategist.openthing](../orgdef-spec-org/jobs/orgdef-strategist.openthing)
- Cross-spec parent: [`roledef-spec/roledef/decisions/proposal-role-vs-job-distinction.md`](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-role-vs-job-distinction.md)
- Cross-spec sibling: [`roledef-spec/roledef/decisions/proposal-job-placement-and-charter-slots.md`](https://github.com/roledef-spec/roledef/blob/main/decisions/proposal-job-placement-and-charter-slots.md)
- Originating conversation: Director (Scott) + orgdef-strategist, 2026-04-26 (orgdef-spec org bootstrap dogfood, post-roledef-acceptance follow-on session, decision-and-migration tandem session)
