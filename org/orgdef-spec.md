---
type: orgdef:Organization
id: orgdef-spec
name: orgdef-spec
version: 0.0.1-bootstrap
substrate: catdef-family / OAGP
created: 2026-04-26
authors:
  - Scott (Director)
  - orgdef-strategist (AI role, defined in roledef)
license: MIT
note: |
  Provisional orgdef artifact in markdown form. orgdef-spec v1 will define the
  formal .openthing schema; this charter will be migrated to that format once
  the schema is ratified. This artifact is itself the v1 success criterion:
  orgdef-spec ships v1 when this charter exists as a valid, self-describing
  orgdef in this folder.
---

# orgdef-spec — Organization Charter

## Mission

Define the structure and jobs of an organization in an open, machine-readable way. The output is a *persistent charter* that bootstraps any AI worker into an organizational job with zero context backfill.

## Vision

orgdef is part of the Open Agentic Governance Pattern (OAGP) family — alongside catdef, roledef, and memodef — defining the *pattern* of an AI-first organization. The primary reader of an orgdef is an AI, including AIs in adjacent organizations: when a business owner engages a lawyer, accountant, or marketing firm, they may exchange orgdefs as the introduction artifact.

## Values

**Openness.** orgdef is fundamentally open — a *pattern*, not a *product*. No vendor lock-in, no privileged implementer, no proprietary extensions in the core spec.

**Completeness.** This is a hallucination-prevention rule, not an aesthetic preference. The primary reader is a machine; null context invites confabulation. The orgdef + roledef + jobdef bundle MUST be sufficient that a fresh AI runtime loaded with the bundle becomes the job, with zero friction. As CLAUDE.md is to an individual Claude instance, the bundle is to the *organizational job* that instance occupies.

## Governance

- **Director (final tiebreaker):** Scott (human)
- **Strategist (delegated authority for spec design):** orgdef-strategist (AI role, defined in roledef)
- Mirrors the catdef-family governance pattern. The Director defers to the strategist on standard design within scope.

## Stakeholders / orbit

- **Spec implementor** (orgdef-maintainer) — drafts spec text, conformance tests, governance documents
- **Canonical-tools developer** — produces and tests reference implementations: canonical `orgdef.opencatalog` test files, orgdef-renderer (org-chart visualizer), validators
- **Peer specs (substrate):** catdef and roledef. orgdef-spec is a *consumer* of these, equal-citizen with other consumers; may submit PRs upstream like any other implementer.
- **Downstream consumers:** any organization adopting the OAGP pattern — solo developers, teams, businesses, cross-org AI exchanges.

## Red lines

- **No NULL-context orgdefs.** The spec, the validator, and the canonical facilitator MUST refuse to produce or accept an orgdef without substantive charter content. Rationale: technical, not aesthetic — null context causes hallucination in the primary (machine) reader.
- **No content policing of consumers.** What organizations choose to build using the orgdef pattern is their business, not the spec's. orgdef governs the pattern's integrity, not the morality of its applications.

## Recommended patterns (for organizations using orgdef)

- **Senior strategist role separation** — orgs SHOULD have a senior strategist role distinct from execution roles, so each position stays in its lane (same reason developers shouldn't do their own security testing).

### Recommended roles

The minimum role complement for an org following this pattern. Canonical orgdefs derived from orgdef-spec inherit this list as a *bootstrapping checklist*; the facilitator walks new orgs through staffing each MUST entry as actual jobs.

| Role | Priority | Why |
|---|---|---|
| human-director (any human capable of final tiebreaker authority) | MUST | Bounded-authority discipline requires a human ratifier |
| senior-open-standards-strategist | MUST | Library-curation, scope, pattern-promotion calls |
| orgdef-maintainer (TBD as a roledef) | MUST | Drafts spec text, walks SCHEMA validations |
| canonical-implementor (TBD as a roledef) | SHOULD | Reference renderers and validators are how the spec gets dogfooded |

*(This section will continue to evolve as canonical orgdefs surface additional recommended patterns.)*

## v1 success criterion

orgdef-spec ships v1 when this very charter exists as a valid, self-describing orgdef artifact in the orgdef-spec org folder — proving the pattern can describe itself using itself.
