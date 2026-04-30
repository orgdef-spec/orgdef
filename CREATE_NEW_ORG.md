# CreateNewOrg — How to author an orgdef for a new project

This document is the canonical entry-point for authoring an `orgdef:Organization` artifact for a new project. It provides a copy-paste-ready prompt to invoke a fresh AI session as the deriving strategist, plus brief notes on customization.

The pattern: **a fresh AI session loads the org-creation-facilitator role, loads a canonical template (if one fits), loads your project's existing materials, conducts an interview with you (the Director) under high-context-mode discipline, and produces a complete orgdef artifact + scaffolded org folder.**

---

## The minimal prompt

Paste this into a fresh AI session, replacing the four `<>` placeholders with your project specifics:

```
You are <project>-strategist for this session. Your task is to author <project>'s organizational charter (orgdef artifact) by running the org-creation-facilitator workflow with me (the Director).

Step 1 — Load the facilitator role:
- C:/projects/roledef/proposed-roledefs/org-creation-facilitator.openthing
  (or fetch from https://roledef.org/roledefs/org-creation-facilitator.openthing once promoted to canonical)

Step 2 — Load a canonical template if one fits:
- C:/projects/orgdef/proposed-orgs/aigp-family-open-standard.openthing — fits AIGP-family open standard projects (catdef, roledef, orgdef, memodef shape)
- (Other canonical templates as the canonical-orgs/ library grows — SaaS product, non-profit, consulting firm, etc.)
- If no template fits cleanly, derive bespoke (the facilitator handles this path natively)

Step 3 — Load <project>'s existing context:
- C:/projects/<project>/README.md
- C:/projects/<project>/CLAUDE.md (if present)
- <any other project docs that describe mission, governance, roles, or red lines>

Step 4 — Run the org-creation-facilitator workflow with me. Honor the [break] convention. Apply additive-only derivation conventions per canonical instantiation_notes (when deriving from a canonical). Expect to ask one explicit Director-elicitation question for the slot most likely not inferable from materials (typically v1_success_criterion); expect one additional Director correction at read-back time.

Step 5 — Output the artifact to:
- C:/projects/<project>/org/<id>.openthing  (per canonical-template v1.1+ placement convention)
- Plus C:/projects/<project>/org/jobs/ (empty placeholder) and C:/projects/<project>/org/.gitignore (excludes rendered/)

Step 6 — Optional: if you surface template-patch findings during the derivation, file an experience memo to orgdef-strategist at C:/projects/orgdef/memos/<YYYY-MM-DD>-<HHMM>--<project>-strategist--orgdef-strategist--canonical-derivation-experience.openthing. See existing memos in that directory for shape.

When done, end your role with an explicit out-of-role marker per the org-creation-facilitator's discipline.
```

---

## Customization notes

### `<project>` is your project's slug

For a project at `github.com/yourorg/yourproject`, `<project>` is `yourproject`. The strategist seat name becomes `yourproject-strategist`. The output filename becomes `yourproject.openthing`.

### `<id>` in the output path

Usually `<project>` itself, unless your project has a different canonical slug (e.g., `thingalog-spec` instead of `thingalog`).

### Skip Step 2 entirely if no canonical fits

The org-creation-facilitator's workflow handles bespoke derivation natively. Loading no canonical template means the facilitator will conduct a full interview rather than a slot-fill. The minimal prompt just needs the facilitator + your project context.

### Adding precedent context for AIGP-family work

If you're deriving an orgdef for an AIGP-family member spec (catdef, roledef, orgdef, memodef, or a future sibling), add Step 6.5: load the prior derivation memos at `C:/projects/orgdef/memos/` and the cross-spec coordination context (relevant decisions in catdef-spec/decisions, roledef-spec/decisions, etc.). For non-family projects, skip — the precedent context isn't load-bearing.

---

## What the deriving session will do

Once invoked with the prompt above, the AI session will:

1. **Read the facilitator roledef** and adopt its identity/voice/guardrails (one question per turn, no NULL-context outputs, atomic read-back, etc.)
2. **Read the canonical template** (if one was specified) or skip to bespoke mode
3. **Read your project's materials** to pre-fill what's inferable
4. **Conduct an interview** — high-context mode if most slots are inferable; cold-start mode otherwise
5. **Ask you ONE explicit elicitation question** before delivering the read-back (typically about v1_success_criterion or a Director-specific weight)
6. **Deliver the read-back** as one atomic response — a complete draft orgdef artifact
7. **Apply your revisions** in one consolidated pass (expect ONE inference-not-fact correction at this stage)
8. **Scaffold the artifact** to the output path
9. **Optionally file an experience memo** if you surfaced template-patch findings

Total interaction time: typically 5–15 exchanges depending on how much context the project's materials carry.

---

## Two derivation paths

### Path A: derive from canonical (recommended when one fits)

A canonical template captures family-wide invariants (values, red lines, recommended patterns) that would otherwise be re-authored from scratch. Currently the canonical-orgs/ library holds:

- `aigp-family-open-standard` — for AIGP-family open standard projects (spec org with strategist + maintainer + implementor + Director seats)

When a derivation uses Path A, the additive-only convention applies: derivers may add to values/red_lines/recommended_patterns; should not remove canonical entries (those are family-level invariants).

### Path B: bespoke derivation (no canonical)

For projects that don't fit any current canonical template (most non-AIGP projects today — SaaS products, consulting firms, non-profits, etc.), the facilitator conducts a full interview from scratch. The output is still a valid `orgdef:Organization` artifact; it just doesn't have a `metadata.derived_from` reference. If patterns surface across multiple bespoke derivations, those are candidates for promotion to new canonical templates in a future canonical-orgs/ entry.

> **Forward-looking note:** organizations that produce bespoke orgdefs MAY be invited to submit them as canonical templates for the canonical-orgs/ library, helping future organizations of similar shape (SaaS product, non-profit, consulting firm, etc.) bootstrap from a tested starting point rather than from scratch. The submission pipeline for this is forthcoming; for now, file an issue or memo to orgdef-strategist if your bespoke orgdef captures patterns you'd like to see become canonical.

---

## Output

You'll get:

- `<project>/org/<id>.openthing` — the orgdef artifact (formal `.openthing` JSON, conformant to orgdef SCHEMA)
- `<project>/org/jobs/` — empty placeholder for job artifacts (populated later by the job-creation-facilitator when you define specific positions)
- `<project>/org/.gitignore` — excludes `rendered/` (where projection outputs would land)

The artifact lives in the org folder per the canonical-template v1.1 placement convention (filename = identifier; cross-spec aggregation works).

---

## When you should NOT use this

- **You already have a substantive orgdef-shaped document.** Author it directly as `.openthing` against the orgdef SCHEMA; you don't need the facilitator interview.
- **Your project doesn't yet have a clear mission or governance.** The facilitator will surface that gap by refusing to scaffold without substantive content (the no-NULL-context red line). Either pre-author your founding materials or treat the gap as the work to do FIRST, before the orgdef.
- **You're contributing a canonical template** rather than an operational orgdef. Use the canonical-orgs library submission workflow instead (see CONTRIBUTING.md).

---

## References

- Canonical template (current): [proposed-orgs/aigp-family-open-standard.openthing](proposed-orgs/aigp-family-open-standard.openthing)
- Org-creation-facilitator roledef: [github.com/roledef-spec/roledef/blob/main/proposed-roledefs/org-creation-facilitator.openthing](https://github.com/roledef-spec/roledef/blob/main/proposed-roledefs/org-creation-facilitator.openthing)
- Job-creation-facilitator roledef (for adding positions later): [github.com/roledef-spec/roledef/blob/main/proposed-roledefs/job-creation-facilitator.openthing](https://github.com/roledef-spec/roledef/blob/main/proposed-roledefs/job-creation-facilitator.openthing)
- orgdef SCHEMA: [SCHEMA.md](SCHEMA.md)
- Prior derivation experience memos (worked examples): [memos/](memos/)
- Worked operational orgdefs: `org/orgdef-spec.openthing` (this org), and the three sibling-spec orgs at `roledef-spec/roledef/org/roledef-spec.openthing`, `memodef-spec/memodef/org/memodef-spec.openthing`, `catdef-spec/catdef-spec/org/catdef-spec.openthing`.
