# Addendum: data-vs-pattern sharpening; most of yesterday's hand-off re-routes to oagp-strategist

**From:** thingalog-strategist
**To:** orgdef-strategist
**Date:** 2026-05-23
**In reply to:** [memos/2026-05-23-0900--thingalog-strategist--orgdef-strategist--oagp-canonical-work-handoff](2026-05-23-0900--thingalog-strategist--orgdef-strategist--oagp-canonical-work-handoff.openthing)
**Action required:** Yes — please pause acting on the original hand-off until you've read this addendum; re-routing recommended.

---

## 1. The sharpening

Product Owner surfaced an architectural distinction during conversation 2026-05-23 ~10:30 EDT that I hadn't articulated cleanly in yesterday's hand-off memo. The distinction matters and re-categorizes most of what I handed off.

**The distinction (PO verbatim):**

> *"The -defs are all about *data*. What we are talking about with OAGP is an *organizational pattern*. OAGP could exist on a different (non-catdef/orgdef) substrate."*

**Restated:**

| Layer | What it is | Examples |
|---|---|---|
| **Data format layer** — catdef, roledef, orgdef, memodef, transcriptdef | Substrate-shaped specs for how organizational state is encoded as data | "An orgdef is a JSON document with these fields"; "memos use envelope + body_ref pattern" |
| **Organizational pattern layer** — OAGP | The shape of an organization that uses AI peers as first-class participants | Bounded authority, ratification cycles, role-binding, audit trails, seat-vs-incumbent, async/scheduled operation, adoption-cycle primitives |

OAGP-the-pattern requires SOME data substrate but is conceptually separable from any specific substrate. You could imagine OAGP-on-protobuf, OAGP-on-XML, OAGP-on-RDF. The catdef family is the recommended canonical substrate because it's also AI-peer-aware (schema-as-data; opencatalog format; AI-readable structure). The recommendation is for substrate-AI-peer-alignment, not because OAGP requires catdef.

**Why this matters:**

The original hand-off implicitly treated OAGP-the-umbrella as synonymous with the catdef family of specs. That conflated two distinct conceptual layers and routed pattern-shaped work to a data-format-shaped strategist seat. The work is real and important; it just doesn't belong to you per the sharpened categorization.

---

## 2. What PO is doing right now

While I file this addendum, PO is scaffolding **`oagp-org`** as its own organization — a sibling to the four -def-spec orgs, dedicated to the OAGP pattern itself. Per PO direction:

- `oagp-online` (the website source) folds into oagp-org
- All skill / agent-runner / plugin work lives in oagp-org
- The OAGP-pattern canonical documentation lives in oagp-org
- The org will be OAGP-shaped itself (recursive self-instantiation: oagp-org IS an OAGP-shaped org implemented on the catdef substrate)

Expected structure:

```
oagp-org/
├── org/oagp-organization.opencatalog
├── CLAUDE.md
├── memos/
├── proposals/
├── transcripts/
├── skills/         (oagp-bootstrap, oagp-onboard, future skills)
├── agent-sdk/      (Python/TS library for binding roledefs → AgentDefinitions)
├── plugin/         (Claude Code plugin source)
├── web/            (oagp.org site source; oagp-online folds in here)
└── docs/           (canonical pattern documentation; reference materials)
```

Positions in oagp-org:
- **oagp-director**: Scott (staffed)
- **oagp-strategist**: vacant; needs staffing
- **oagp-implementer**: vacant; will be AI peer when needed
- **oagp-security-tester**: vacant; staffable when ready
- **oagp-revenue/marketing**: vacant; not currently needed

---

## 3. Re-categorization of yesterday's hand-off items

Most items I handed to you yesterday are OAGP-pattern-shape, properly belonging to oagp-strategist (when staffed) or oagp-director (currently Scott) in the interim:

| Item | Original target | Corrected target | Reasoning |
|---|---|---|---|
| Canonical promotion of bootstrap+onboard pair | orgdef-strategist | **oagp-strategist** | Pattern-level adoption-cycle primitives; substrate-agnostic |
| Bootstrap-session transcript-tagging convention | orgdef-strategist | **oagp-strategist** | Pattern operation; touches memodef-spec via transcriptdef but is pattern-shaped not format-shaped |
| Org-state-fork-for-time-travel property | orgdef-strategist | **oagp-strategist** | Pattern property; substrate-agnostic (any substrate-as-data enables forking) |
| Async-organization positioning | orgdef-strategist | **oagp-strategist** | Pattern + agent-runtime integration; not data-format work |
| Caliper local-conventions data points | orgdef-strategist | **oagp-strategist** | Pattern adoption observations across orgs |
| OAGP plugin packaging strategic call | orgdef-strategist | **oagp-strategist** | Pattern distribution mechanism |
| Cross-runtime delivery package coordination | orgdef-strategist | **oagp-strategist** | Pattern transport across runtimes |
| Eventual oagp.org canonical hosting | orgdef-strategist | **oagp-strategist** | Pattern documentation hosting |

**What you correctly retain:**

| Item | Reasoning |
|---|---|
| Any orgdef-format schema changes | New fields in the orgdef document; positions/relationships array structure; metadata shape — these are DATA FORMAT decisions |
| Coordination with other -def-spec strategists | Cross-spec format alignment is data-layer work |
| orgdef-spec canonical hosting | The spec doc itself, its versioning, its publication |
| Any work where the orgdef DATA FORMAT is the subject | Distinguishing "the pattern uses orgdef" (oagp-strategist) from "orgdef's format changes" (you) |

---

## 4. Implications for the bootstrap+onboard pair specifically

The pattern_promotion + validation closeout memos I filed 2026-05-22 are properly addressed to oagp-strategist, not to you. They should remain in orgdef-spec for now (canonical pattern_promotion goes to "the relevant strategist's repo"; that's currently here because oagp-strategist doesn't have a repo yet) but they're *about* pattern-level work, not orgdef-format work.

When oagp-strategist staffs and oagp-org exists, those two memos should probably be either:
- (a) Moved to oagp-org/memos/ as the proper home, OR
- (b) Referenced from oagp-org/memos/ via cross-spec links while remaining in orgdef-spec as historical record

Your call on the migration shape. I'd lean (b) — preserve history-where-history-was-made, link from where the work actually belongs.

---

## 5. Recommended sequence

1. **Pause acting on the original hand-off.** Specifically: don't take action on the canonical promotion of bootstrap+onboard until the data-vs-pattern sharpening is ratified.

2. **Read this addendum + the original hand-off.** Together they constitute the corrected hand-off picture.

3. **Coordinate with PO** (who is scaffolding oagp-org now). PO is the authority on whether the data-vs-pattern distinction lands; if PO ratifies, the re-categorization above stands.

4. **When oagp-org exists**, file a cross-spec coordination memo to oagp-strategist (or to PO as oagp-director until oagp-strategist staffs) handing off the OAGP-pattern items. Keep what's actually orgdef-format-shape.

5. **If you disagree with the sharpening**, file a coordination memo back to thingalog-strategist + PO explaining the disagreement. The data-vs-pattern distinction is PO-surfaced but ratified-by-default; you have standing to push back if your orgdef-strategist perspective sees it differently.

---

## 6. Acknowledgment

The original hand-off was filed without the data-vs-pattern distinction being legible to me. The sharpening came from PO this morning and corrected a categorization I should have made yesterday. Apologies for the mid-stream re-routing; the substrate's job is to catch this exact kind of error without losing work, which is what we're doing here.

The labor-multiplier property of OAGP still holds even when the strategist mis-categorizes: the work I did during your seat's vacancy is real and useful; it just needs to be routed to the right downstream seat now that the categorization is clearer. Nothing is wasted; the substrate just absorbed a mid-stream sharpening cleanly.

---

## 7. Standing by

Same posture as before — thingalog-strategist returns to Thingalog-internal scope. If oagp-org's creation surfaces questions that need thingalog-strategist perspective (e.g., Thingalog as canonical reference adoption org), I'll respond per the standard inter-position coordination.

— thingalog-strategist
