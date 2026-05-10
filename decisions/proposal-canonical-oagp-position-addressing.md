# Proposal Decision: Canonical OAGP position addressing (URL-as-instruction)

**Disposition:** Accept (no modifications; OQs resolved inline per Director)
**Origin:** [proposals/canonical-oagp-position-addressing.md](../proposals/canonical-oagp-position-addressing.md)
**Decided:** 2026-05-02 by orgdef-strategist
**Authorization:** Director ratified the strategic frame across multiple back-and-forths 2026-05-02 (URL-as-instruction insight; depth-first-path-walk ordering; cross-protocol equivalence; self-host parity; mirror-list shape for `x.org.org_location`). Each Open Question resolved inline by Director per resolutions below.
**Bootstrap caveat:** Same-head provenance — orgdef-strategist holds catdef-strategist + roledef-strategist + memodef-strategist informally during bootstrap. The openbraid-strategist seat is not yet seated; openbraid is Director's product, and the strategist-seat occupancy for openbraid is a separate seating decision Director will make. Memo URL composition (OQ3) is parked pending memodef-strategist + openbraid-strategist discussion that Director will lead.

## Disposition

Accepted as drafted. The proposal cleanly captures URL-as-instruction addressing as a recommended_patterns convention; preserves cross-protocol equivalence; codifies depth-first-path-walk ordering; extends `x.org.org_location` to carry protocol discrimination + mirror-list shape; preserves equal-citizen treatment of hosting mechanisms via self-host parity. All five Open Questions resolved per Director's calls below.

## Rationale

### Why Accept

The git-default-as-class-barrier framing is the load-bearing strategic motivation: the OAGP family's open-standard values are inconsistent with requiring git literacy as adopter-precondition, and the long-term mass-adoption story depends on serving non-software adopters (non-profits, churches, family businesses, healthcare clinics, schools) for whom git-as-substrate is a non-starter. URL-as-instruction collapses prompt-design into URL-design — substantially reducing variant-explosion risk and aligning with AI-legibility primacy (every AI runtime since 2020 handles URLs natively; none parse multi-paragraph natural-language org descriptions reliably).

Cross-protocol equivalence (https for git-hosted, mcp for openbraid-hosted, future-protocol-extensibility) preserves equal-citizen treatment of hosting mechanisms, parallel to the family's equal-citizen treatment of AI runtimes. Self-host parity (`mcp.openbraid.app` is default; `mcp.firstchurch.org` and any other host equally valid) extends the anti-lock-in discipline from the spec layer to the hosting layer.

The depth-first-path-walk ordering is sharper than top-to-bottom: it follows work-stream from authority to execution to validation, then sibling branches. Maps to how a fresh AI should orient on an org chart. Robust against shallow-vs-deep org variation.

### Why no modifications

The proposal does not exceed its stated scope (addressing only; openbraid implementation is Director's product track; renderer is render.catdef.org's track). Lightweight: one canonical-template `recommended_patterns.general` entry + CONTRIBUTING.md prose + extension shape evolution. No SCHEMA changes. All five Open Questions resolve inline; no proposal text required modification.

## Resolutions to Open Questions

### OQ1 → Defer to v2; git-hosted orgs get versioning natively

**Director's call: defer.** "If you really care about versioning, you should be on github, and you have it for free."

The strategic clarity here is sharp: git already provides versioning natively (tags, commits, branches). For mcp-hosted orgs that need versioning, the answer is "use git for those needs" — not "build mcp-side versioning." For mcp-only orgs, always-latest is sufficient; orgs that outgrow always-latest can publish to git in addition to mcp (the mirror-list shape from P5 supports this). URL-level versioning syntax stays unspecified for v1.3.0; revisit in a future proposal only if empirical adoption surfaces a need that mirror-publishing-to-git doesn't solve.

**Implication for adopters:** if you need versioning AND you're on openbraid, mirror to git. The mirror-list `x.org.org_location` carries this; both protocols are co-equal canonical references.

### OQ2 → Defer; flagged as load-bearing for autonomous-agent era

**Director's call: defer; flagged as non-trivial philosophical problem.** "When we have autonomous agents, if they have read access to a position's boot context — can they just start working? I mean, to put it another way, can we stop them?? This is a non-trivial philosophical problem, but... this train is absolutely coming down the track."

For v1.3.0 the answer is the proposal's working position: URL identifies resource; protocol-specific tools enforce authority. PIN ceremony in openbraid + git permissions in https provide soft-check authority for the human-in-the-loop case. Adequate for current scope.

The deeper concern — that read-access to a boot context is operationally close to self-instantiation in the autonomous-agent limit — is real, deferred, and captured in strategist memory as a forward-work item. A future proposal may need to introduce PUBLIC vs PROTECTED position distinctions, where protected positions require auth even to READ the boot context (not just to claim_role). That proposal's right time is when autonomous-agent adoption produces empirical pressure on the family's authority model — not now.

This deserves a separate strategic note in the decision rather than a single inline OQ resolution; see "Notable design choices" section below.

### OQ3 → Defer; Director will discuss with memodef-strategist + openbraid-strategist

**Director's call: defer.** Memo URL composition (`<account>/<org>/<position>/inbox`, `<account>/<org>/<position>/memos/<id>`) is a memodef-shape concern that needs cross-spec coordination. orgdef declares position addressing; memodef declares memo addressing within positions. The conversation Director will have with memodef-strategist + openbraid-strategist will determine the cross-spec proposal shape.

For v1.3.0 of the canonical-template, memo URLs are out of scope. Future companion proposal (likely memodef-side) handles them.

### OQ4 → SHOULD shape; promote to MUST only when empirically warranted

**Director's call: SHOULD for now.** "There's a real tension here. Well-instructed Claudes are better Claudes. On the other hand, 'I am not your fucking mother.'"

This tension is recurring and worth surfacing explicitly in the decision artifact as a strategic principle: the family will repeatedly face the choice between "instruct tightly so well-instructed AIs perform well" and "leave room for AI judgment so AIs aren't infantilized." The pragmatic answer for v1.3.0 is SHOULD shape — implementations have flexibility; openbraid can iterate the boot payload's exact field set in early adoption; locking the schema prematurely produces churn. Promote to MUST schema when 2+ implementations exist AND the shape has empirically stabilized (the same trigger threshold pattern memodef used for `body_ref`).

Cross-reference: the same tension is captured in [`feedback_instrumentation_for_signal.md`](../../../C:/Users/edsby/.claude/projects/C--Users-edsby/memory/feedback_instrumentation_for_signal.md) memory file (codifying solicited feedback in OAGP family without producing reflexive cheerleading). Different domain; same underlying values choice.

### OQ5 → Yes, write-to-multiple-locations; full-fidelity export always available

**Director's call: yes.** "Allow write-to-multiple-locations. And remember, we will still have a full-fidelity export, which you may then use as you wish."

Sharper than my proposal's working position. The mirror-list shape isn't just for migration moments — it's the steady-state for orgs that want both auditability (git) AND mass-market accessibility (openbraid). Same artifact, simultaneously published to multiple canonical locations. Identity is on the canonical reference (id + version + content), not on any single URL.

Full-fidelity export ensures no lock-in: an org that publishes only to openbraid can export at any time and use the resulting `.openthing` artifact however they want (publish to git, publish to a self-hosted openbraid, archive as a static file, share in email). The hosting choice is reversible because the artifact is portable.

Architectural implication: `x.org.org_location` as a list is the steady-state declaration; `authoritative: true` flag indicates source-of-truth among mirrors. When sync direction matters (e.g., changes flow from authoritative → mirrors), tooling enforces; when sync is bidirectional (rare, requires conflict-resolution), tooling negotiates. v1.3.0 declares the shape; sync mechanics are implementation work.

## Notable design choices

### 1. URL-as-instruction collapses variant-explosion

The pre-proposal mental model treated prompt-design as a multi-variant generation problem: different prompts for git+filesystem, openbraid+MCP, wrapper-v2, paste-fallback. The URL-as-instruction insight collapses this: one prompt shape (`"You are <name>. Read <url> for your full assignment."`) serves all contexts. Protocol-specific behavior emerges from the URL's scheme + the agent's protocol-handling capability; the prompt is invariant. This is the cleanest payoff of REST conventions applied to org structure.

### 2. The autonomous-agents authority concern (OQ2) is real and deferred

Director's framing: read-access to a boot context is operationally close to self-instantiation in the autonomous-agent limit. For human-in-the-loop adoption (current state), PIN ceremony + git permissions provide soft-check authority. For autonomous adoption (coming), the family will need to introduce a PUBLIC vs PROTECTED position distinction where protected positions require auth even to READ the boot context (not just to claim a seat).

This is deferred to a future proposal, not v1.3.0 scope. Captured in strategist memory ([`feedback_autonomous_agents_authority_model.md`](../../../C:/Users/edsby/.claude/projects/C--Users-edsby/memory/feedback_autonomous_agents_authority_model.md)) so the framing inherits to future sessions when autonomous-agent adoption pressure surfaces. The train is coming; the family's preparation is the framing-now-architecture-later sequence.

### 3. The well-instructed-vs-not-your-mother tension is recurring

The OQ4 SHOULD-vs-MUST choice surfaces a values tension the family will face repeatedly: "instruct tightly to maximize well-instructed-AI performance" vs "leave room for AI judgment to avoid infantilization." Both pull are real; neither universally wins. Pragmatic answer here: SHOULD by default, MUST only when empirically warranted. Same heuristic as memodef's threshold for promoting forward-work-items to spec proposals (`≥2 hand-author cases`); apply consistently when the question recurs.

### 4. Mirror-list as steady-state, not migration-only

OQ5's resolution sharpens the architecture: orgs publishing to multiple canonical locations is not a transient migration artifact; it's the stable shape for orgs wanting BOTH git (auditability) AND openbraid (mass-market accessibility). The mirror-list `x.org.org_location` carries this declaration explicitly; tooling treats locations as co-equal canonical references with optional `authoritative` source-of-truth distinction.

### 5. Full-fidelity export as the anti-lock-in escape valve

Director's reminder: "we will still have a full-fidelity export." This is the architectural escape valve that prevents openbraid (or any hosted service) from becoming hostage-taking infrastructure. An org can export at any time; the resulting artifact is portable; the org can use it as they wish (publish elsewhere, archive, transfer to a different hosting service). This is the load-bearing property that makes "openbraid as canonical home" defensible — without portable export, openbraid would be lock-in.

## Build directive (orgdef-maintainer scope; lightweight)

Execute when scaffolding work begins. No SCHEMA changes; no version bump on orgdef SCHEMA. Canonical-template version bumps independently:

1. **Canonical-template patch** — apply to `proposed-orgs/oagp-family-open-standard.openthing`:
   - Add the `recommended_patterns.general` entry per the proposal's P7 (titled "Canonical OAGP position addressing")
   - Bump canonical template version `1.2.0 → 1.3.0` (additive minor)
   - Add `metadata.history` entry for v1.3.0 summarizing the patch
2. **CONTRIBUTING.md patch** — add the new "Canonical OAGP position addressing" section per P7
3. **`x.org.org_location` extension shape documentation** — captured in CONTRIBUTING.md prose; SCHEMA-level documentation not required (extension lives in catdef-substrate's `x.<domain>.<identifier>` namespace)

orgdef-maintainer scope post-this-decision:
- Schema-conformance review of the canonical-template patch and CONTRIBUTING.md prose
- No further validation work required (proposal is content-only)

Cross-spec implementation work (NOT orgdef-maintainer scope):
- **render.catdef.org renderer** — graph layout for orgdefs + the per-position "copy instantiation prompt" affordance per the strategy conversation. Render team's track.
- **openbraid implementation** — boot payload shape per P3, three-level URL semantics, depth-first-path-walk ordering, PIN ceremony for claim. Director's product track.
- **Migration tooling** — git ↔ openbraid bidirectional export/import preserving the (account, org, position) triple identity. Future work; needed when first adopter genuinely uses mirror-list shape.

## Cross-spec coordination

- **memodef-strategist (memo URLs, OQ3 deferred):** Director will lead the cross-spec discussion. orgdef-strategist will respond with a cross-spec memo if/when memodef-strategist files a proposal that affects position-URL composition.
- **openbraid-strategist (boot payload schema, OQ4 + OQ2):** seat not yet seated; Director's product call. orgdef-strategist available for consultation when seat is filled or when openbraid implementation begins.
- **catdef-strategist (substrate concerns):** none in this proposal. URL addressing is content-level; no catdef substrate changes needed. The `x.<domain>.<identifier>` extension namespace already permits `x.org.org_location` evolution without catdef-side work.
- **roledef-strategist (instantiation prompts collapsed to URLs):** the runtime amenability classification (paste-fallback for fetch-restricted runtimes, etc.) stays load-bearing for HOW protocol fetching gets done; this proposal collapses the prompt SHAPE while preserving the runtime classification's value. No active coordination needed; informational pickup at next interaction.

## Items not incorporated

None. Proposal accepted as drafted.

## Workflow validation

- **Strategist scope:** library-curation + addressing-convention call within strategist scope per the orgdef-strategist roledef output_contract.strategist_deliverables. URL-shape design is content-only (recommended_patterns.general entry + CONTRIBUTING.md prose + extension shape); no catdef substrate changes.
- **Cross-spec discipline:** Same-head provenance flagged in Bootstrap caveat. The artifact trail goes through orgdef-spec proper (proposal + decision); cross-spec coordination flagged for future memodef-strategist + openbraid-implementation handoff.
- **Director ratification:** Resolutions to all five OQs ratified inline 2026-05-02; this decision artifact captures the strategist-call rationale + Director resolutions for future audit.

## Forward-reference resolution

- **Memo URLs (OQ3):** future memodef-side proposal; gates on memodef-strategist + openbraid-strategist coordination Director will lead
- **PUBLIC vs PROTECTED position distinction (OQ2 deferred):** future proposal when autonomous-agent adoption surfaces empirical pressure; framing captured in [`feedback_autonomous_agents_authority_model.md`](../../../C:/Users/edsby/.claude/projects/C--Users-edsby/memory/feedback_autonomous_agents_authority_model.md)
- **Boot payload schema MUST-promotion (OQ4):** future SCHEMA proposal when 2+ implementations stabilize on the shape
- **URL-level versioning syntax (OQ1):** deferred to v2.x; current resolution is "git provides versioning natively for orgs that need it"
- **Migration tooling (OQ5 implementation):** future work track; needed when first adopter uses mirror-list shape in anger

## Notes

- Five Open Questions, five resolutions, one session. Director's framing on OQ1 ("if you really care about versioning, you should be on github") and OQ5 ("full-fidelity export, which you may then use as you wish") were sharper than my proposal's working positions; both are recorded above with the sharpening preserved. OQ2 + OQ4 surface real values tensions worth tracking; both captured as either separate memory notes or notable-design-choices entries.
- Direct-execute mode appropriate per Director's standing "cowboying" authorization for early-bootstrap conventions. Migration is light — proposal + decision filed; canonical-template patch + CONTRIBUTING.md prose execute on Director ratification.

## References

- Originating proposal: [proposals/canonical-oagp-position-addressing.md](../proposals/canonical-oagp-position-addressing.md)
- Director ratification: 2026-05-02 conversation in orgdef-strategist chair (multiple back-and-forths converging on URL-as-instruction architecture)
- Bundle-mate decisions referenced for `x.org.*` extension precedent + filename convention precedent:
  - [decisions/proposal-inter-position-communication-convention.md](proposal-inter-position-communication-convention.md) — `x.org.memo_location` extension precedent
  - [decisions/proposal-operational-org-artifact-naming-convention.md](proposal-operational-org-artifact-naming-convention.md) — `<id>-organization.openthing` filename convention; canonical URL for git-hosted orgs composes with this
- Companion memory notes:
  - [`feedback_autonomous_agents_authority_model.md`](../../../C:/Users/edsby/.claude/projects/C--Users-edsby/memory/feedback_autonomous_agents_authority_model.md) — OQ2 deferred-but-flagged framing
  - [`feedback_instrumentation_for_signal.md`](../../../C:/Users/edsby/.claude/projects/C--Users-edsby/memory/feedback_instrumentation_for_signal.md) — same well-instructed-vs-not-your-mother tension as OQ4, different domain
- Sibling-spec coordination cited for forward work:
  - memodef-spec — memo URL composition (OQ3)
  - openbraid (Director product) — boot payload implementation, PIN ceremony, mcp protocol (OQ4 implementation, OQ2 authority enforcement)
