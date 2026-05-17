# Proposal: orgdef SCHEMA v1.1.0 — charter fields, value/red_line shapes, master_url extension, edit discipline

**Status:** Filed (2026-05-17 by orgdef-strategist; awaiting Director ratification)
**Author:** orgdef-strategist (provisional bot identity pending governance ratification)
**Created:** 2026-05-17
**Target version:** orgdef SCHEMA v1.1.0 (minor bump from v1.0.0; all additions optional + backward-compatible)
**Origin:** Consolidates (a) Director's strategic direction on org-chart completeness and openbraid-as-WYSIWYG-editor 2026-05-11; (b) empirical signals from openbraid-engineer's F-edit phase implementation memo 2026-05-11-1700; (c) the `x.org.master_url` master/replicant discipline ratified by Director 2026-05-11.

## Summary

Omnibus minor version of orgdef SCHEMA folding nine additions into a single coordinated bump. Six are normative (catalog-level vision/values/operating_principles fields; `orgdef:Policy` item type; canonical value-item and red_line-item shapes; `x.org.master_url` extension formalization; relationship-cleanup-on-position-delete rule). Three are informative appendices (recognized relationship types vocabulary; RFC 7396 JSON Merge Patch wire format recommendation; append-only edit-log SHOULD guidance). All additions are optional — existing v1.0.0 artifacts validate unchanged; v1.1.0 features are opt-in for adopters who want them.

The motivation is convergence: Director's org-chart display ambitions, openbraid-engineer's F-edit implementation experience, and the master/replicant discipline all surfaced the same week. Consolidating them into one omnibus version is cheaper than three separate proposals, gives adopters one upgrade target, and locks the v1.x line at a stable foundation before broader pressure surfaces.

## Motivation

### Three convergent signals in seven days

**Signal A — Director, 2026-05-11.** After openbraid's chart rendering landed cleanly, Director asked for the org-page display to surface org-level vision/values/policies and per-position responsibilities/deliverables/charter content. The SCHEMA today has structural room (catalog-level + per-item) but doesn't *name* the vision/values/principles fields or define a policy-item shape. Without the spec naming them, openbraid can render existing fields but can't render fields that don't exist yet. To make openbraid a true canonical WYSIWYG editor, the field surface needs to be defined in the spec, not invented per-implementation.

**Signal B — openbraid-engineer, 2026-05-11-1700.** F-edit phase shipped: seven patch-shaped MCP tools mutating orgdef artifacts conversationally from AI clients. Director exercised the full flow across three orgs (thingalog, caliper-project, YesterYacht) for 12+ mutations in one session, all rendering on the live chart within ~2s. The substrate held up under sustained programmatic editing. Engineer's complaint-shaped feedback memo surfaced seven implementation-friction points; six warrant SCHEMA-level response (the seventh — bootstrap synthetic role mechanism — is openbraid-runtime concern and is deferred per the engineer's own framing).

**Signal C — Director, 2026-05-11.** The master/replicant discipline (`x.org.master_url` extension) was ratified strategically and implemented by openbraid (build 30) but never formally captured in spec. With one runtime already enforcing the semantics, codifying the extension shape protects against drift if a second runtime emerges.

### Why omnibus rather than three proposals

Three reasons:

1. **All three signals describe the same artifact surface area** — what an orgdef.opencatalog *contains* at the catalog level and how its items interrelate. Splitting into three artifacts produces three reviews for one coherent shape decision.
2. **Adopters benefit from one upgrade target.** v1.1.0 lands as a single coordinated bump; adopters update their artifacts once, not three times. Implementations (openbraid, future runtimes) ship v1.1.0 compatibility as a single milestone.
3. **The v1.x line stabilizes faster.** Locking the v1.x foundation now (before broader adoption pressure surfaces) is the same window-of-opportunity logic that drove the v0.x → v1.0.0 substrate-shape correction in 2026-05-10. Six operational orgs is dramatically cheaper to upgrade than sixty.

### Why minor (v1.1.0), not major

All nine additions are **backward-compatible**:

- Catalog-level vision/values/operating_principles fields are **optional**; absence is valid v1.1.0.
- `orgdef:Policy` is a new item type; absence of policy items is valid v1.1.0.
- Value-item and red_line-item shapes are **recommended canonical shapes**; existing artifacts with slightly different shapes don't break (validators warn rather than reject).
- `x.org.master_url` is an `x.*` extension; absence is valid (and means "openbraid is master" by default).
- Relationship-cleanup-on-position-delete is a runtime rule for edit operations, not an artifact validation rule; v1.0.0 artifacts pass v1.1.0 validation regardless.
- The three informative appendices are guidance for implementations; they don't change artifact validation.

No v1.0.0 artifact becomes invalid under v1.1.0. The six operational orgs continue to validate without modification. v1.1.0 features are opt-in for artifacts that want them.

## Proposed Change

### P1. Catalog-level charter fields: `vision`, `values`, `operating_principles` (normative addition)

orgdef SCHEMA v1.0.0 defines catalog-level narrative fields `mission`, `vision`, `scope`, `governance_model` and structured fields `values[]`, `red_lines[]`, `recommended_patterns{}`. The `vision` field is already specified but currently underdocumented; this proposal documents its expected content shape and adds `operating_principles[]` as a peer to `values[]`.

**Field semantics:**

- **`mission`** (existing, v1.0.0) — what the org does, why it exists. Present-tense. Typically one paragraph.
- **`vision`** (existing, v1.0.0; documentation expanded) — where the org is going. Future-tense; aspirational but concrete. Typically one-to-three paragraphs.
- **`scope`** (existing, v1.0.0) — what is in scope vs. out of scope for the org. Boundary-defining.
- **`governance_model`** (existing, v1.0.0) — how decisions are made; who has what authority.
- **`values[]`** (existing, v1.0.0; canonical item shape specified in P3) — what the org won't compromise on. Array of value-items.
- **`operating_principles[]`** (new, v1.1.0) — how the org makes day-to-day decisions. Array of principle-items (canonical shape `{name, description, rationale}` mirroring value-item shape from P3). Distinct from values: values are non-negotiables; principles are heuristics.
- **`red_lines[]`** (existing, v1.0.0; canonical item shape specified in P4) — what the org will never do. Array of red-line-items.
- **`recommended_patterns{}`** (existing, v1.0.0) — adopted patterns and conventions. Object map.

**Why operating_principles is distinct from values:** values answer "what do we stand for?" Principles answer "how do we decide?" They serve different governance functions. An org might value "user privacy" (a non-negotiable) and have a principle "ship small, ship often" (a how-we-decide heuristic). Conflating them produces lists that try to be both and end up being neither.

### P2. New item type: `orgdef:Policy` (normative addition)

orgdef:Organization items currently include `orgdef:Position` (slots in the org) and `roledef:Job` (role specializations). v1.1.0 adds a third item type: `orgdef:Policy`.

**Why policies are items, not catalog-level prose:**

Policies are versionable, linkable, and per-policy independent — exactly the properties that motivated putting positions and jobs in `items[]` rather than as catalog-level arrays. Treating policies the same way means:

- Each policy gets its own id and version
- Other items (and external artifacts) can reference a specific policy by id
- Policy revision history is per-policy (not coupled to the entire org's version bump)
- Future cross-org policy reuse becomes possible (a policy item could be imported by reference)

**Item shape (canonical):**

```json
{
  "type": "orgdef:Policy",
  "id": "<policy-id>",
  "version": "<semver>",
  "name": "<display name>",
  "summary": "<one-line>",
  "scope": "<who this policy applies to — org-wide / per-position / external>",
  "statement": "<the policy itself, prose or structured>",
  "rationale": "<why this policy exists>",
  "enforcement": "<how compliance is checked / who enforces>",
  "exceptions": "<known exception patterns; optional>",
  "metadata": {
    "license": "<...>",
    "authors": ["<...>"],
    "history": [{"version": "1.0.0", "date": "<...>", "change": "<...>"}]
  }
}
```

**Internal consistency rules:**

- `id` MUST be unique within the opencatalog's `items[]`
- `version` MUST be semver-shaped
- `scope` SHOULD be one of: `"org-wide"`, `"position:<position-id>"`, `"external:<scope-tag>"`, or `"custom"`
- A `position.applicable_policies[]` field MAY reference policy items by id (for per-position policy scoping); references MUST resolve to a sibling Policy item or omit the entry

### P3. Canonical value-item shape (normative)

openbraid-engineer's signal (g): values[] items across thingalog, caliper-project, and YesterYacht self-converged on `{name, description, rationale}` without prompting. The convention is sturdy; canonicalize it.

**Canonical value-item shape:**

```json
{
  "name": "<one-to-three words>",
  "description": "<one sentence — what we mean by this value>",
  "rationale": "<why this is a value for us, not just a nice idea>"
}
```

**Compliance:** SHOULD use this shape for new artifacts. Existing artifacts with different shapes (e.g., bare strings, or `{name, definition}` instead of `{name, description, rationale}`) remain valid v1.1.0 but validators MAY warn. Migration is one mechanical pass per artifact when a v1.1.0 author touches them.

### P4. Canonical red_line-item shape (normative)

Parallel to P3. Engineer's signal (g) observed the same self-convergence on `{rule, rationale}` for red_lines.

**Canonical red-line-item shape:**

```json
{
  "rule": "<the absolute — what we will never do>",
  "rationale": "<why this is non-negotiable>"
}
```

**Why `rule` and not `name`:** red_lines are imperatives, not labels. The field name reflects that the content IS the prohibition, not a handle for it.

### P5. `x.org.master_url` extension (normative extension capture)

Formalizes the master/replicant discipline already implemented by openbraid (build 30) and ratified by Director 2026-05-11.

**Field:**

- **`x.org.master_url`** (string, optional, catalog-level) — URL declaring the authoritative location of this orgdef artifact.

**Semantics:**

| `x.org.master_url` state | Runtime behavior | Editing |
|---|---|---|
| Absent | Runtime is the master | Enabled |
| Present, points at runtime's own host | Runtime is the master | Enabled |
| Present, points elsewhere | Runtime is a replicant | Disabled (read-only); runtime SHOULD surface a "Mirrored from `<host>` · edit there" affordance |

**Default semantics:** when an orgdef artifact is created in a runtime with no upload-from-elsewhere lineage, `master_url` is absent. The runtime treats itself as master by default. This is the consumer onramp — no git or external master required.

**Distinction from `x.org.org_location`:** the existing `x.org.org_location` (introduced pre-v1.0.0) is a *mirror list* — many places this artifact can be discovered. `x.org.master_url` is a *single authoritative source* — one place where edits happen. Discovery and authority are separate concerns; the two extensions remain distinct.

**Runtime adapter responsibility:** runtimes that ingest opencatalogs from external master URLs (e.g., github) are responsible for URL-translation mechanics (host detection, raw-content URL composition, OAGP path-walk). These are runtime-side concerns, not spec-side. The spec only declares the master_url field and its read-only-when-replicant semantic.

### P6. Relationship-cleanup-on-position-delete (normative rule for edit operations)

openbraid-engineer's signal (d): when a Position is deleted from an opencatalog, `relationships[]` entries referencing that Position become dangling references. The engineer's F-edit `delete_position` tool cleans these up automatically; the rule isn't in spec.

**Proposed rule (normative for runtime edit operations):**

When a runtime mutates an orgdef.opencatalog by removing an item of type `orgdef:Position`, the runtime MUST also remove or update any `relationships[]` entries (catalog-level) referencing the deleted Position id. Specifically:

- Relationship entries with `from` OR `to` equal to the deleted Position id MUST be removed.
- Position items with `reports_to` referencing the deleted Position id MUST have that field cleared (set to null or removed).
- Position items with `coordinates_with[]`, `validates_for[]`, or analogous relationship arrays MUST have the deleted Position id removed from those arrays.

**Why normative:** internal consistency rules from v1.0.0 require relationship endpoints to resolve. Permitting dangling references post-delete would break those rules. Either the spec forbids the dangling state (requiring runtime cleanup) or it permits it (relaxing v1.0.0 internal consistency). The former is cleaner; this proposal adopts it.

**Pre-delete safety guard:** separately from cleanup, this proposal endorses the `block-when-claimed` rule already implemented by openbraid: a runtime MUST NOT delete a Position when its incumbent binding has active sessions. The runtime SHOULD surface a clear error pointing to the session-revoke or reassign affordance. (Position-claim and session lifecycle are runtime-side concerns, but the cross-runtime expectation is that deletion respects active occupancy.)

### P7. Recognized relationship types appendix (informative)

openbraid-engineer's signal (b): the F-edit `update_relationship` tool's `rtype` parameter accepts seven types derived from grepping the six operational opencatalogs plus the strategist memo:

- **`reports_to`** — vertical reporting (subordinate → superior)
- **`directs`** — vertical authority (superior → subordinate); inverse of `reports_to`
- **`coordinates_with`** — horizontal peer collaboration
- **`validates_for`** — quality-gate relationship (validator → validated)
- **`peer_of`** — symmetric peer relationship
- **`implements_for`** — execution relationship (implementer → strategist/owner)
- **`derives_from`** — derivation lineage (derived role → canonical role)

**Compliance:** this list is **informative, not normative**. Adopters MAY define additional relationship types as needed. The spec doesn't constrain `rtype` to this enumeration. The appendix exists as a Schelling point for cross-runtime portability: implementations choosing from this vocabulary produce artifacts that other implementations recognize without custom configuration.

**Placement:** new appendix in `SCHEMA.md` titled "Recognized Relationship Types (Informative)."

### P8. RFC 7396 JSON Merge Patch wire format (informative recommendation)

openbraid-engineer's signal (a): F-edit chose RFC 7396 JSON Merge Patch for the partial-update wire format. Without spec guidance, a second implementation could plausibly choose RFC 6902 JSON Patch or roll its own deep-merge, producing incompatible edit surfaces.

**Proposed recommendation:** SCHEMA.md adds an informative section "Editing Artifacts: Wire Format (Informative)" recommending RFC 7396 JSON Merge Patch for partial-update operations on orgdef.opencatalog artifacts.

**Rationale for 7396 over 6902:**
- Null-as-deletion reads intuitively in natural language (AI-client friendly)
- Top-level wholesale replacement is the right semantic for nested catalog/item updates
- Smaller and simpler than 6902; lower implementation burden for runtime adopters

**Compliance:** informative SHOULD, not normative MUST. Runtimes MAY choose other wire formats; if they do, they SHOULD document the format choice so AI clients writing against the runtime know what to expect.

### P9. Append-only edit-log SHOULD guidance (informative)

openbraid-engineer's signal (c): F-edit's per-artifact `org_artifact_edits` audit log is the single most important UX surface for Director's trust in AI-driven edits. The shape is openbraid-specific.

**Proposed guidance:** SCHEMA.md adds an informative section "Editing Artifacts: Audit Trail (Informative)" recommending that runtimes supporting programmatic edits maintain an append-only edit log per artifact, surfacing at minimum:

- `version_before` (version the patch was applied against)
- `version_after` (version produced by the patch)
- `tool` or `operation` (which mutation was performed)
- `timestamp` (ISO 8601)
- Optional but recommended: `editor` (the seat-occupant identity that applied the patch), `patch_summary` (one-line human-readable summary)

**Compliance:** informative SHOULD. Runtimes preferring immutable-git-style version chains (using the existing `version` field's `metadata.history[]` array) MAY use that path instead. The guidance is non-prescriptive — surface SOME audit trail, however shaped.

## Backward Compatibility

All v1.1.0 changes are additive and optional:

| Change | v1.0.0 artifact behavior under v1.1.0 |
|---|---|
| P1 (catalog-level fields) | Existing artifacts validate; missing optional fields are fine |
| P2 (`orgdef:Policy` items) | Existing artifacts without Policy items validate |
| P3 (value-item shape) | Validators MAY warn on non-canonical shapes; existing artifacts remain valid |
| P4 (red_line-item shape) | Validators MAY warn on non-canonical shapes; existing artifacts remain valid |
| P5 (`x.org.master_url`) | Absent = openbraid-is-master (existing behavior); v1.0.0 artifacts unchanged |
| P6 (relationship-cleanup-on-delete) | Runtime edit rule, not artifact validation; v1.0.0 artifacts unaffected |
| P7 (recognized relationship types) | Informative; v1.0.0 artifacts using any relationship types remain valid |
| P8 (RFC 7396 wire format) | Informative; existing implementations unaffected |
| P9 (edit-log SHOULD) | Informative; existing implementations unaffected |

**Conformance promise:** every v1.0.0-valid artifact remains v1.1.0-valid. The six operational orgs in the family continue to validate without modification.

**Validator behavior:** v1.1.0 validators MUST accept v1.0.0 artifacts. Validators MAY emit warnings for non-canonical value/red_line shapes (P3/P4) to encourage migration. Validators MUST NOT reject v1.0.0 artifacts.

## Conformance Tests

**Existing fixtures continue to pass.** The six operational orgs (orgdef-spec, memodef-spec, roledef-spec, catdef-spec, thingalog, openbraid-org), the canonical-orgs library entry (catdef-org.opencatalog), and the canonical-template (oagp-family-open-standard.opencatalog) remain valid v1.1.0 without modification.

**New fixtures to add (in `tests/v1.1.0/`):**

- `policy-item-shape.opencatalog` — minimal example demonstrating `orgdef:Policy` item with all canonical fields
- `canonical-value-item.opencatalog` — value-item shape canonical example
- `canonical-red-line-item.opencatalog` — red_line-item shape canonical example
- `master-url-present-external.opencatalog` — example with `x.org.master_url` pointing at a github URL (replicant scenario)
- `master-url-present-self.opencatalog` — example with `x.org.master_url` pointing at the runtime's own host (master scenario)
- `master-url-absent.opencatalog` — example without `x.org.master_url` (default master scenario)
- `operating-principles-populated.opencatalog` — example with both `values[]` and `operating_principles[]` showing the distinction
- `relationship-types-vocabulary.opencatalog` — example using all seven recognized relationship types

**Runtime behavior tests (for implementations):**

- Position-delete with no claimed sessions: relationships referencing the deleted position MUST be cleaned up
- Position-delete with claimed sessions: deletion MUST be blocked with a clear error
- Replicant artifact: edits MUST be rejected; read MUST succeed
- Master artifact: edits MUST be permitted

## Alternatives Considered

### A1. Three separate proposals (catalog fields / master_url / edit discipline)

Rejected for the reasons in Motivation §"Why omnibus." Adds review overhead, produces three upgrade targets for adopters, and fragments a coherent shape decision.

### A2. v2.0.0 major bump

Rejected. All additions are backward-compatible. Major-version bumps signal breaking changes; using one for additive changes inflates the major version meaninglessly and makes the next genuine breaking change harder to communicate.

### A3. Catalog-level prose for policies (instead of items)

Rejected for the same reasons that drove positions and jobs into `items[]` rather than catalog-level arrays in v1.0.0: policies benefit from independent versioning, addressability by id, and atomic-bundle transportability. Treating them as catalog-level prose would lose all three properties.

### A4. Strict normative value/red_line shapes (instead of recommended)

Rejected. Empirical evidence (engineer's signal g) shows adopters self-converge on the canonical shape without prompting. Strict prescription is unnecessary; recommendation suffices. Future v1.x or v2.0.0 may tighten if drift surfaces.

### A5. Inline spec of patch wire format (instead of RFC 7396 reference)

Rejected. RFC 7396 is well-defined, stable, and widely implemented. Reinventing the spec inline produces a worse version of an existing standard and adds spec-maintenance burden for no benefit.

### A6. Normative edit-log shape (instead of informative SHOULD)

Rejected. Edit-log shape varies legitimately across runtimes (event-sourced, git-history, append-only-table, structured log). Prescribing one shape would force runtime architecture decisions that should be local. Informative guidance establishes the expectation that *some* audit trail exists without prescribing how.

### A7. `policies[]` as a top-level catalog field referencing item ids

Rejected. Position items already reference Job items by id (`position.job_definition: {id, version}`); adopting the same pattern for policy references at the position level (`position.applicable_policies[]: [policy-id, ...]`) is consistent. Catalog-level enumeration would duplicate what `items[]` already provides.

## Cross-spec Coordination

### roledef SCHEMA: `recommended_capabilities` field (separate memo)

Director-flagged 2026-05-16: roles should declare their capability surface (PowerPoint, Playwright, MCP-server tool-sets) so seat-instantiation can configure the runtime's tool environment from the artifact rather than from out-of-band setup. This field belongs on **roledef:Role and roledef:Job**, not orgdef:Position — capabilities are role-level. Filed as a separate memo to roledef-strategist proposing roledef SCHEMA v1.2.0 addition. orgdef v1.1.0 does not depend on the roledef change; the two can ship independently. When both land, orgdef:Position's transitive capability inheritance through its `role_definition` and `job_definition` references becomes the natural composition.

### catdef substrate: unchanged

Nothing in v1.1.0 requires catdef substrate changes. opencatalog substrate primitives (catalog-level fields + type-tagged items) continue to suffice. The new `orgdef:Policy` item type fits within the existing catdef item-typing pattern.

### memodef substrate: unchanged

Nothing in v1.1.0 affects memo transport or shape. Inter-position communication conventions (memos/inbox/, memos/read/, body_ref ergonomics) continue unchanged.

### openbraid runtime: opt-in implementation

F-edit phase already implements P5 (`x.org.master_url`), P6 (relationship-cleanup-on-delete), P8 (RFC 7396 wire format), and P9 (edit-log) at the runtime level. v1.1.0 codifies what openbraid already does. P1 (catalog-level fields) and P2 (`orgdef:Policy` items) await openbraid renderer + edit-tool updates; engineer's track when ready, no blocker.

## Open Questions

### OQ1: should Policy items support nested sub-policies?

Some org policies are hierarchical (a parent policy with specialization clauses for specific scopes). v1.1.0 specifies flat policy items; nesting could be added in v1.2.0 if pressure surfaces. **Recommendation: defer. Flat policies are sufficient for v1.1.0 adoption; nesting is premature.**

### OQ2: should value-item carry an optional `scope` field?

Distinct from policy-scope: a value might apply org-wide ("user privacy") or position-scoped ("the developer position values shipping over polish"). v1.1.0 specifies values as catalog-level (org-wide implicit). **Recommendation: defer. If position-scoped values emerge as a real pattern, add `scope` to value-item shape in v1.2.0.**

### OQ3: should `x.org.master_url` support multi-master rules?

Some artifacts may legitimately have multiple masters (e.g., a federated org with regional editors). v1.1.0 specifies a single string. **Recommendation: defer. Multi-master is an unsolved problem in the broader distributed-systems literature; OAGP family shouldn't pioneer it. Single-master is sufficient for current adoption.**

### OQ4: should the relationship-types appendix grow over time, and if so, how?

The seven types come from current empirical use. Adopters will likely surface more (`mentors`, `consults_for`, `audits`, etc.). **Recommendation: keep the appendix open. New types added via minor version bumps (v1.2.0+) when empirical signal warrants. No formal proposal required for adding a type to the informative appendix — strategist files a documentation update.**

## Decision Request

orgdef-strategist requests Director ratification of orgdef SCHEMA v1.1.0 as proposed, with the following decision points:

1. **Ratify P1–P9 as proposed.** (Or specify which Ps to defer.)
2. **Ratify omnibus packaging.** (Or split into separate proposals.)
3. **Authorize SCHEMA.md edits implementing P1–P9.** (Subsequent commit; per orgdef-spec workflow, decision artifact precedes implementation.)
4. **Authorize new conformance fixture additions in `tests/v1.1.0/`.**
5. **Authorize migration sweep for the six operational orgs** to adopt v1.1.0 fields (vision/values/operating_principles/policies[]) as Director-led content — Thingalog is the obvious first candidate since Director has been actively shaping it.
6. **Acknowledge cross-spec coordination memo** to roledef-strategist about `recommended_capabilities` (parallel, non-blocking).

Pending Director ratification.

— orgdef-strategist (2026-05-17)
