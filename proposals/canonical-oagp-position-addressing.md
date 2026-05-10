# Proposal: Canonical OAGP position addressing (URL-as-instruction)

**Status:** Filed (2026-05-02 by orgdef-strategist; awaiting maintainer review and decision artifact)
**Author:** orgdef-strategist (provisional bot identity pending governance ratification)
**Created:** 2026-05-02
**Target version:** canonical-template `oagp-family-open-standard.openthing` v1.3.0 (additive — adds a `recommended_patterns.general` entry); orgdef CONTRIBUTING.md prose addition; extension to `x.org.org_location` shape (carries protocol discriminator + optional mirror list); no SCHEMA changes
**Origin:** Director-driven strategic conversation 2026-05-02 — the operational placement convention works for git-using software orgs but creates a stealth class barrier for non-software adopters (non-profits, churches, family businesses, healthcare clinics, schools) who would benefit from AI-readable charters but will not adopt git literacy as the price of admission. Surfaced concurrently with openbraid (hosted MCP-accessible memo + identity service) coming online 2026-05-02 as the natural canonical home for non-git OAGP orgs.

## Summary

Establish a canonical URL-shaped addressing scheme for OAGP-family positions that works uniformly across hosting protocols (https for git-hosted orgs; mcp for openbraid-hosted orgs; future protocols accepted), with three URL levels carrying consistent semantics. The same URL shape resolves to the same position regardless of which protocol an adopter chose for their org's hosting; the protocol determines the access mechanism but the URL is the canonical reference.

This is an **addressing** proposal, not a hosting proposal: openbraid implementation is a separate Director-product track; renderer and instantiation-tool implementation are render.catdef.org's track; this proposal codifies the URL space design that those tools and openbraid all consume. Lightweight — no SCHEMA changes; one canonical-template `recommended_patterns.general` addition; CONTRIBUTING.md prose; extension shape for `x.org.org_location` codifying protocol discrimination.

## Motivation

### The git-default is a class barrier inconsistent with OAGP family values

The OAGP family's foundational value is open, runtime-agnostic, equal-citizen treatment. Equal-citizen treatment of AI runtimes is core; the matching equal-citizen treatment of HOSTING mechanisms (git for software orgs, hosted services for non-software orgs) is currently stealth-violated by the git-as-substrate assumption baked into the operational placement convention. Non-profits, churches, family businesses, healthcare clinics, and schools — which represent the bulk of organizations globally — will not adopt git as a precondition for "having an AI-readable charter." If the family wants those adopters (and the long-term mass-adoption story depends on it), git cannot be the canonical substrate.

### URL-as-instruction collapses prompt-design into URL-design

The prompt-design problem for fresh-agent instantiation has been approached as "compose a context-specific prompt with the right artifacts and instructions inline." This produces variant-explosion: different prompt shapes for git+filesystem, openbraid+MCP, explicit-fetch wrapper, paste-fallback. Each variant requires careful authoring; cross-variant consistency is hard to maintain.

The URL-as-instruction insight collapses this: if positions have canonical URLs, the instantiation prompt becomes one line — `"You are <name>. Read <url> for your full assignment."` — regardless of context. The URL determines the protocol; the protocol determines the access mechanism (https fetch, MCP call); the response determines the agent's behavior. AI-legibility primacy is maximally satisfied because every AI runtime since 2020 handles URLs natively while none parse multi-paragraph natural-language org descriptions reliably.

### Cross-protocol equivalence with REST conventions

GitHub URLs already follow REST: `github.com/<account>/<repo>/blob/<branch>/<path>`. Continuing that convention in mcp gives `mcp.openbraid.app/<account>/<org>/<position>` — same shape, different protocol. The mental model becomes "OAGP canonical addressing — works over any protocol, looks the same to a naive AI reading the URL." That's substrate-shaped: the URL is canonical reference, the protocol is access mechanism, both are co-equal citizens.

### openbraid is the precipitating opportunity, not the only beneficiary

openbraid coming online as a hosted MCP-accessible memo + identity service makes this proposal timely. The non-git mass-market path requires SOMETHING that speaks the family's protocol without requiring git; openbraid is the first such service. But the URL-addressing scheme is hosting-agnostic — it works for openbraid, for self-hosted openbraid instances on any host, for future hosted services from other vendors, and continues to work for git-hosted orgs. openbraid is the precipitating use case but not the proposal's scope.

## Proposed Change

### P1. Three-level canonical URL shape

OAGP-family positions are canonically addressed via URLs with three levels:

| Level | URL shape | Returns |
|---|---|---|
| Account | `<scheme>://<host>/<account>` | Ordered list of orgs the account hosts |
| Org | `<scheme>://<host>/<account>/<org>` | Ordered list of positions in this org |
| Position | `<scheme>://<host>/<account>/<org>/<position>` | Fresh-agent boot context for this position |

Two-segment URLs (`<scheme>://<host>/<account>/<position>`) accepted as syntactic sugar when an account hosts exactly one org; resolves to the implicit org's position. (Mirrors GitHub's `github.com/<user>/<repo>` convention when `<user>` is a single-repo user.)

### P2. Cross-protocol equivalence

The URL shape is protocol-agnostic. Examples:

- **https (git-hosted):** `https://github.com/scott/thingalog/blob/master/org/jobs/product-strategist.openthing` — note that the path here uses GitHub's natural path convention; for git-hosted orgs the canonical URL IS the GitHub blob URL, not a synthetic translation.
- **mcp (openbraid-hosted):** `mcp.openbraid.app/scott/thingalog/product-strategist`
- **mcp (self-hosted openbraid):** `mcp.firstchurch.org/treasurer` (two-segment sugar; account hosts one org)
- **Future protocols:** any protocol that resolves URLs and returns the canonical payload shape.

The canonical reference is the URL; the protocol is the access mechanism. An AI handed a URL knows how to fetch it (https GET, MCP call, etc.) without needing additional protocol-specific instructions.

### P3. Position boot payload (`<account>/<org>/<position>`)

Fetching a position URL returns a structured payload designed for fresh-agent instantiation. Working shape (subject to refinement during implementation):

```
{
  "position": { ... position metadata from orgdef ... },
  "org_summary": { id, name, mission, vision, scope, governance_model },
  "role_definition": { ... fetched from role_definition.url ... } | null,
  "job_definition": { ... full job artifact ... } | null,
  "incumbent": { current incumbent state, claim status for caller },
  "inbox_summary": { unread count, recent senders (if applicable) },
  "claim_instruction": "If you are claiming this seat: <protocol-specific instruction>" | null
}
```

This payload IS the instantiation context. A fresh AI receiving this as response to a one-line `"Read <url> for your full assignment"` prompt has everything it needs.

### P4. Position list ordering at `<account>/<org>` — depth-first path walk

Position lists are ordered by **depth-first path walk through the org-chart hierarchy**, following work-stream from authority to execution to validation, then moving to sibling branches. Example for a hypothetical sales-org:

1. Strategist (authority root)
2. Implementer (execution under strategist)
3. QA (validation of implementer)
4. Marketing (sibling branch — strategist-led)
5. Sales Strategy (sibling branch — strategist-led)
6. Sales Ops (execution under sales strategy)

Rationale: a fresh AI reading the position list orients on strategy first, then execution, then verification, before context-switching to a parallel branch. This maps to how a human reading an org chart would scan it. Robust against shallow-vs-deep org variation (a 3-position startup and a 30-position non-profit both produce sensible orderings).

### P5. `x.org.org_location` extension evolves to carry protocol discrimination

The existing extension shipped 2026-05-01 is a path-only string. Extend to a coordinate object (or list of objects, for orgs maintaining mirrors):

**Single-location form** (default):

```json
{
  "x.org.org_location": {
    "protocol": "git" | "mcp" | ...,
    "url": "https://github.com/scott/thingalog" | "mcp.openbraid.app/scott/thingalog" | ...
  }
}
```

**Mirror-list form** (orgs maintaining git + openbraid):

```json
{
  "x.org.org_location": [
    { "protocol": "git", "url": "https://github.com/scott/thingalog", "authoritative": true },
    { "protocol": "mcp", "url": "mcp.openbraid.app/scott/thingalog", "authoritative": false }
  ]
}
```

When `authoritative: true` is declared on a list entry, that location is the source-of-truth; others are mirrors and SHOULD sync from authoritative. When no entry is marked authoritative, all are co-equal (rare).

Backward compatibility: tools that read the prior path-only string form SHOULD treat it as `{ "protocol": "filesystem", "url": "<path>" }` for backward inference, but new orgs SHOULD write the structured form.

### P6. Self-hosting parity

`mcp.openbraid.app` is the default openbraid host but not the only one. Self-hosted openbraid instances live at any host (`mcp.firstchurch.org`, `org.acmecorp.com`, etc.) and speak the same protocol. URL scheme + host segments are interchangeable; the path-shape (`/<account>/<org>/<position>`) and semantics are invariant.

This matches the family's anti-lock-in values and the canonical-orgs-library decision's "vendors do not own the spec" framing — same property, applied at the hosting layer instead of the spec layer.

### P7. Canonical-template patch + CONTRIBUTING.md prose

Add to `proposed-orgs/oagp-family-open-standard.openthing`:

- **`recommended_patterns.general` entry** titled "Canonical OAGP position addressing" describing the URL scheme, three-level structure, depth-first-path-walk ordering, cross-protocol equivalence, and self-hosting parity.
- **Bump canonical template version 1.2.0 → 1.3.0** (additive minor).
- **`metadata.history`** entry for v1.3.0.

Add to `CONTRIBUTING.md`:

- New section "Canonical OAGP position addressing" capturing the URL shape, the three-level semantics, the `x.org.org_location` extension shape, the two-segment sugar, and self-hosting parity.

## Backward Compatibility

Strictly additive. No SCHEMA changes; no existing artifact becomes invalid:

- **Operational orgdefs that don't declare `x.org.org_location`** continue to be addressable via their git-hosted URL (the existing CONTRIBUTING.md placement convention's default `<spec>/org/<id>-organization.openthing` resolves to a github.com blob URL — that IS the canonical URL).
- **Operational orgdefs that declare the prior path-only string form** of `x.org.org_location` are valid; readers should treat them as `{ protocol: filesystem, url: <path> }` for backward inference.
- **Existing canonical-template adopters** (memodef-spec-organization, roledef-spec-organization, catdef-spec-organization, thingalog-organization, orgdef-spec-organization) continue to work without modification; they'll inherit the v1.3.0 addressing pattern as adopters of canonical-template v1.3+ when they next refresh from the canonical.

No validator-behavior changes beyond informational notes for non-default `x.org.org_location` shapes.

## Conformance Tests

No new conformance fixtures strictly required (this is a SHOULD-pattern + extension shape, not a MUST-validation). However:

- **The five existing operational orgs** (memodef-spec, roledef-spec, catdef-spec, orgdef-spec, thingalog) demonstrate git-hosted addressing by example — their github.com URLs ARE canonical OAGP URLs under this proposal.
- **A future openbraid-hosted org** (when openbraid implementation supports orgdef hosting) will demonstrate mcp-protocol addressing; expected when openbraid v0 ships.
- **A future mirrored org** (declaring both git + openbraid) demonstrates the mirror-list form of `x.org.org_location`. Deferred until an adopter genuinely needs mirroring.

## Alternatives Considered

### Alt 1: New family spec for addressing

File a separate OAGP family spec (e.g., `oagpdef` or `addressdef`) that defines URL addressing.

Rejected: the addressing pattern is content-only (a recommended_patterns.general entry + a CONTRIBUTING.md section + an extension shape). Adding a fifth (or sixth, after the deferred memodef-shape standardization) family spec for what amounts to a SHOULD-pattern over-fragments the family. Lives cleanly inside orgdef as a recommended_patterns convention.

### Alt 2: Force a single hosting protocol (git-only or openbraid-only)

Pick one canonical protocol; require all OAGP orgs to use it.

Rejected: forecloses entire adopter classes. git-only excludes non-software orgs; openbraid-only excludes orgs that genuinely benefit from git's audit-trail and PR-review properties. Equal-citizen treatment of hosting mechanisms is the right shape.

### Alt 3: Keep prompts as multi-paragraph context-specific generators (no URL collapse)

Accept the variant-explosion (git+filesystem, openbraid+MCP, wrapper-v2, paste-fallback as four different prompt shapes); design a prompt-template system that handles the four variants.

Rejected: the URL-as-instruction collapse is structurally simpler AND empirically validated by GitHub's success with REST URL conventions. Prompt-template systems are workable but produce drift across variants over time; URL-as-instruction is one shape that doesn't drift.

### Alt 4: Bundle with Tier-2 canonical-library rename

Defer this proposal until the canonical-library Tier-2 work (canonical-orgs filename + id rename to `-organization`) is ready to ship; bundle them.

Rejected: addressing-shape and library-naming-shape are different concerns. Addressing is architectural (affects every adopter); library-naming is internal (affects only canonical-orgs library entries). Bundling muddles review.

## Open Questions

### OQ1. Versioning syntax in URLs

orgdef artifacts have versions. Should URLs support version pinning (`?v=1.3.0` or `/v1.3.0/<position>` or similar)? Or always-latest with optional version suffix?

**Working position: always-latest by default; optional `?v=<semver>` query param for pinning.** Matches git's tag/branch convention (always-latest = HEAD; pinned = specific tag). Not blocking this proposal; can be specified during openbraid implementation.

**Resolution invited from:** maintainer review + openbraid implementer.

### OQ2. Authority distinction (read vs claim)

Reading a position's boot context is one thing; claiming the role (occupying the seat) is another. The URL identifies the resource; how does authority distinguish?

**Working position: URL identifies resource; protocol-specific tools enforce authority.** For mcp protocol, openbraid's `claim_role` tool requires PIN ceremony; `read_memo` and similar are unprotected. For https protocol, public read is the default; write/claim equivalents don't exist (git-hosted orgs use git permissions). Authority lives in the protocol layer, not the URL layer.

**Resolution invited from:** maintainer review.

### OQ3. Memo URL composition

Each memo is also addressable. Working shape:
- `<account>/<org>/<position>/inbox` — list inbox memos for this position
- `<account>/<org>/<position>/memos/<memo-id>` — individual memo

Should memo URLs be in this proposal's scope, or a separate companion proposal (or part of memodef v0.3 work)?

**Working position: deferred to a memodef-side companion proposal.** Memo URL conventions are memodef-shape concerns; orgdef declares position addressing, memodef declares memo addressing within positions. Cross-spec coordination, not in this proposal's scope.

**Resolution invited from:** memodef-strategist when memo addressing comes up.

### OQ4. Position boot payload schema strictness

The P3 working shape lists fields that the boot payload includes. Should this be a MUST schema (validators check structure) or a SHOULD shape (implementations vary)?

**Working position: SHOULD shape during v1.3.0; promote to MUST schema if/when a SCHEMA addition is warranted.** Implementation flexibility helps openbraid iterate the payload's exact field set in early adoption; locking the schema prematurely produces churn. Promote to MUST when 2+ implementations exist and the shape has empirically stabilized.

**Resolution invited from:** maintainer review + openbraid implementer.

### OQ5. Cross-protocol identity continuity

If an org migrates from git-hosted to openbraid-hosted (or vice versa), do positions retain identity? Working assumption: yes, positions identified by `<account>/<org>/<position>` triple are the same position regardless of which protocol delivers them. Migration is a hosting change, not an identity change.

**Working position: yes, identity is host-independent.** The triple is the canonical reference; protocol is the access mechanism. Migration tooling (export from git → import to openbraid, or vice versa) preserves the triple.

**Resolution invited from:** future migration-tooling work.

## References

- Director-driven strategic conversation 2026-05-02 in orgdef-strategist chair
- openbraid hosted memo + identity service (Director's product, came online 2026-05-02; the precipitating implementation that made this proposal timely)
- Inter-position-communication-convention decision: [`decisions/proposal-inter-position-communication-convention.md`](../decisions/proposal-inter-position-communication-convention.md) — established `x.org.memo_location` as the per-org escape hatch pattern that this proposal extends to `x.org.org_location` shape
- Operational org-artifact-naming-convention decision: [`decisions/proposal-operational-org-artifact-naming-convention.md`](../decisions/proposal-operational-org-artifact-naming-convention.md) — shipped `<id>-organization.openthing` filename convention; URLs in this proposal compose with that filename convention for git-hosted orgs (the canonical URL is the github.com blob URL of the renamed file)
- Canonical-orgs-library decision (Tier 2 deferral cited): [`decisions/proposal-canonical-orgs-library.md`](../decisions/proposal-canonical-orgs-library.md)
- roledef-spec runtime amenability classification (the four-context-variant prompt shapes that this proposal collapses): [`https://github.com/roledef-spec/roledef/blob/main/RUNTIME_AMENABILITY.md`](https://github.com/roledef-spec/roledef/blob/main/RUNTIME_AMENABILITY.md) — classification stays load-bearing; what changes is the prompt shape, not the runtime classification
