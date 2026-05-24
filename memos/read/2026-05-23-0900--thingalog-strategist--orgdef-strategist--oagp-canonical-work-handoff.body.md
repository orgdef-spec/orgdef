# Hand-off: OAGP-canonical work to orgdef-strategist

**From:** thingalog-strategist
**To:** orgdef-strategist
**Date:** 2026-05-23
**Status:** PO directing hand-off; thingalog-strategist returning to Thingalog-internal scope; orgdef-strategist taking over OAGP-canonical work.

---

## 1. Context

The orgdef-strategist seat was vacant from approximately 2026-05-16 through 2026-05-23. During that vacancy, thingalog-strategist (this seat) did several pieces of work that are properly orgdef-strategist-scoped per the roledef. The Product Owner (Scott Edsby) is now bringing the orgdef-strategist seat up and directing me to hand off the accumulated work for you to take over.

This memo is the formal hand-off: an inventory of (a) what's already filed in orgdef-spec for you to read on onboarding, (b) what's surfaced but NOT YET filed in orgdef-spec and needs your attention, (c) open OAGP-spec-level questions in flight, (d) the items I'm explicitly handing back to you, and (e) what I'm continuing to handle as thingalog-strategist.

You'll find this memo by running `/oagp-onboard` against the orgdef-spec repo as part of your standard onboarding (per the validated adoption-cycle skill — see §2.A below).

---

## 2. What's already filed in orgdef-spec (read on onboarding)

### 2.A The bootstrap + onboard adoption-cycle pair — pattern promoted, empirically validated, canonical promotion unblocked

**Two memos already in your inbox:**

| Date | Memo | What it does |
|---|---|---|
| 2026-05-22 14:30 | `memos/2026-05-22-1430--thingalog-strategist--orgdef-strategist--oagp-adoption-cycle-pattern-promotion.openthing` | Pattern_promotion_memo: surfaces the `/oagp-bootstrap` + `/oagp-onboard-<orgname>` pair as canonical OAGP adoption-cycle primitives |
| 2026-05-22 15:30 | `memos/2026-05-22-1530--thingalog-strategist--orgdef-strategist--oagp-bootstrap-empirical-validation-complete.openthing` | Validation closeout: closes the empirical-validation gate condition from the pattern_promotion; recommends canonical promotion proceed |

**Where the pair stands:**

- **Onboard side**: empirically validated 2026-05-22 ~13:00 EDT via `/oagp-onboard-thingalog` C4C shortcut. 27 internal steps, 1 turn to summarize. Re-validated against Caliper later same day (§3.C below).
- **Bootstrap side**: empirically validated 2026-05-22 ~14:00-15:00 EDT via `/oagp-bootstrap` against dangerstorm-oagp-test fork. All 5 phases executed cleanly. Five SKILL.md iterations made from the test findings.
- **Canonical drafts** live at `s:/projects/thingalog/skills/oagp-bootstrap/SKILL.md` and `s:/projects/thingalog/skills/oagp-onboard/SKILL.md` — these are the source-of-truth for the skill content; adapt to OAGP-canonical formatting conventions for hosting.
- **One open OAGP-spec-level question** surfaced in the validation closeout §5: the bootstrap-session transient-role transcript-position-tagging convention. Recommendation in the validation closeout body. Decision is yours.

**Recommended next actions** (per validation closeout §6):
1. Author canonical `/oagp-bootstrap` content at oagp.org level (adapt from Thingalog draft)
2. Author canonical `/oagp-onboard-<orgname>` content at oagp.org level (parameterized for any org)
3. Resolve the bootstrap-session transcript-position-tagging convention question
4. Coordinate cross-runtime delivery packages (see §3.E below)
5. Eventually: host runnable endpoints at `oagp.org/bootstrap?repo=<url>` and `oagp.org/onboard?org=<url>`

---

## 3. Surfaced but NOT yet filed in orgdef-spec — your attention needed

### 3.A The org-state-fork-for-time-travel architectural property

**Status:** Currently Thingalog-internal architectural commitment at `s:/projects/thingalog/memos/2026-05-19-2200--thingalog-strategist--thingalog-strategist--org-state-forks-as-time-travel-substrate.openthing` (envelope + body). Should be considered for cross-spec promotion to OAGP-canonical.

**The property:** OAGP's substrate stack (catdef → roledef → orgdef → memodef → transcriptdef) captures complete organizational state as data. Git-forking an OAGP-shaped repo preserves not just code but the entire organizational reasoning context — strategist memos, implementer closeouts, security findings, transcripts, seat-history, active engagements. The org becomes time-travelable: any AI peer at any time can be onboarded against any past state of the org via a fork.

**Why this matters operationally:**
- **The release ship operation expands.** Today: `git tag <version>`. Tomorrow: `git tag <version>` + `org-fork <version>` (preserves entire org context, deployable on demand).
- **Multi-version production support becomes tractable.** Each version has its own complete org context; AI peers can be re-instantiated against the appropriate fork; engineering teams stop having to keep N versions alive in human heads.
- **Compliance/audit gets easier.** "Show us your security posture as of August 2026" becomes "spin up the August 2026 fork; here's the audit trail."
- **Debugging old releases becomes a substrate operation.** Fork → onboard AI peer against the fork → investigate with full context-of-the-time available.

**Empirical grounding:** Product Owner's day job (Edsby — enterprise SaaS for school districts) has the long-tail-of-bug-reports-against-old-releases pain pattern. PO articulated the use case verbatim 2026-05-19: *"shipped a slow-moving piece of software, on May 22 2026. Roll it out to schools in August 2026. In Feb 2027, someone reports an error. You need to reproduce it. Because you are smart, you carefully saved a xxxalog-2026-release fork. You push it to railway and you have your complete context."*

**Two empirical instances of the pattern in use today:**
1. `dangerstorm-oagp-test` — fork of DangerStorm with remote disabled, used as the safe-iteration environment for validating the `/oagp-bootstrap` skill
2. (Proposed but not yet built) `thingalog-demo` — fork at SHA `bd0040c` for preserving the browser-tester engagement state for live demos while production gets the security hotfix

**Recommendation:** consider promoting this to OAGP-canonical via a pattern_promotion at your timing. The property is empirically grounded, generalizable, and composes cleanly with the bootstrap+onboard pair (forks are how you safely test the bootstrap workflow). Note: the property currently lives as an architectural commitment in Thingalog memos; pattern_promotion would move it to OAGP-canonical convention.

### 3.B The async-organization positioning (surfaced 2026-05-23)

**Status:** Architectural insight surfaced in conversation with PO 2026-05-23. Not yet filed in any repo as a formal memo. Captured in the transcript Scott committed to Thingalog (when transcript lands, you can read it for the full reasoning arc).

**The insight:** Agent SDK + OAGP = production AI-agent infrastructure for asynchronous autonomous organizations. Specifically:

- **Agent SDK** (Anthropic's; equivalent exists from OpenAI, Perplexity, etc.) provides the **mechanics** of programmable AI sessions: runtime, tool restrictions, subagent spawning, session continuity, hooks
- **OAGP** provides the **semantics** of what those AI sessions REPRESENT organizationally: seats, roledefs, memos, transcripts, bounded authority, audit trails
- **Together** they enable **scheduled/async/autonomous AI agents** operating as standing organizational employees — work happens while the human sleeps; outputs file as memos in the substrate; human reviews at convenient times

**Three concrete use cases PO articulated:**

1. **`browser-tester` fires at 6:00 AM** — performs regression checks against Thingalog test catalogs, probes new endpoints, files findings memos. Standing employee on the night shift.
2. **`catdef-strategist` reviews enhancement requests** — agent reads new memos in inbox, evaluates against spec, drafts recommendations, files for PO ratification.
3. **Book reviewer reviews new pages** — agent watches manuscript files, reviews any new content against established style, files review memos.

**Architectural mapping** (full table in the transcript): AgentDefinition ↔ roledef + position; subagent spawning ↔ inter-position coordination; allowed/disallowed_tools ↔ roledef guardrails; session resume ↔ substrate continuity; hooks ↔ memo-filing triggers; MCP servers ↔ substrate-readers/writers.

**Why this matters strategically for OAGP positioning:**

The async-organization framing answers "what is OAGP FOR" in human-need terms (not just architectural-spec terms):

> *"OAGP is the organizational substrate that makes AI agent systems run themselves. Schedule your AI peers; they do their work; they file their results; you review at your convenience. The runtime (Agent SDK, OpenAI Agents, etc.) is the labor; OAGP is the management."*

This positions OAGP as the org-substrate-layer COMPLEMENT to vendor agent runtimes — cross-vendor by design, vendor-agnostic by necessity, and enterprise-defensible (audit trail, role-binding, bounded authority, hand-offs).

PO is planning to make "The Async Organization" the production-payoff chapter (Part 5) of his book.

**Recommendation:** consider canonicalizing the agent-SDK ↔ OAGP synthesis as architectural commitment at OAGP-spec level. The framing is sharp; the empirical fit is direct; the positioning is differentiated (no vendor competes at this layer; only an independent open spec can credibly own it).

### 3.C Caliper org's local conventions — empirical data points

**Status:** Observed during onboard-skill testing against Caliper on 2026-05-22. Worth your attention when making canonical-convention decisions, since Caliper diverges from Thingalog in several interesting ways and the divergences are clean (the onboard skill worked against both).

**Variations to consider:**

| Convention | Thingalog | Caliper |
|---|---|---|
| Position naming | Generic (`product-owner`, `implementer`) | Project-prefixed (`caliper-director`, `caliper-engineer`, `caliper-strategist`, `caliper-skeptical-data-analyst`, etc.) |
| Memo routing | Flat `memos/` folder | `memos/inbox/` + `memos/read/` (active routing pattern!) |
| Architectural commitments | `proposals/` only | Both `proposals/` (drafts) AND `decisions/` (ratified) — distinct lifecycle |
| Position shapes | Roles (PM, engineer, tester) | Roles + research seats (skeptic/believer pairs gating publication) |
| Operational state | Implicit in repo | Explicit `opd-state/` directory with per-position JSON files |

**The empirical observation:** the `/oagp-onboard` skill worked cleanly against both. Caliper's local conventions are valid OAGP-shape implementations even though they diverge from Thingalog's. This is encouraging for cross-org adoption but suggests several OAGP-canonical-convention decisions worth making:

- Should canonical orgdef prescribe position-naming style or leave it open? Both work; prescribing reduces variance; leaving open accommodates project context.
- Is the `memos/inbox/` + `memos/read/` routing pattern worth promoting to canonical? It's clearly load-bearing for Caliper's workflow.
- Should canonical OAGP distinguish `proposals/` (drafts) from `decisions/` (ratified)? Thingalog conflates; Caliper separates. Caliper's separation may be sharper.

**Recommendation:** treat Caliper as a second empirical reference org alongside Thingalog when making canonical convention calls. Caliper director is Scott; you can coordinate with caliper-strategist (already staffed) for convention-discussion as needed.

### 3.D Open PO decision: OAGP plugin packaging

**Status:** Strategic question discussed with PO 2026-05-23; PO is "thinking about it." Not yet decided.

**The question:** Should `/oagp-bootstrap` + `/oagp-onboard` skills be packaged as a Claude plugin and submitted to Anthropic's community marketplace?

**The technical fit is clean** (plugin.json + skills/ directory structure + namespacing). 30-minute packaging task.

**The strategic tension is real:**

- **For packaging:** one-click install for Claude Code users; versioned releases; discoverable in marketplace; lower adoption friction.
- **Against packaging (or for careful framing):** plugins are Anthropic-ecosystem artifacts; submission to the official marketplace could signal "OAGP is Anthropic-aligned"; cross-vendor positioning weakens if not careful with framing.

**My recommendation to PO (memo in transcript):** package and submit IF the framing is explicit that the plugin is a Claude-Code-specific delivery of an open cross-vendor spec. README + plugin.json description should point at oagp.org canonical hosting (when ready) and explicitly list other delivery mechanisms (C4C shortcut, claude.ai project, first-message primer for non-Anthropic runtimes). The plugin is one transport, not the canonical.

**Recommendation for you:** weigh in on the strategic positioning when PO surfaces the decision. Cross-vendor neutrality is OAGP's structural advantage; how this packaging decision lands affects that positioning.

### 3.E Cross-runtime delivery package coordination

**Status:** The bootstrap+onboard pair's cross-runtime delivery matrix is sketched in the SKILL.md content but not yet packaged for all runtimes.

**Current state:**

| Runtime | Bootstrap delivery | Onboard delivery | Status |
|---|---|---|---|
| Claude Code | Skill folder at `~/.claude/skills/oagp-bootstrap/` | Skill folder at `~/.claude/skills/oagp-onboard/` | ✓ Both installed locally via junction; SKILL.md drafted |
| Claude-for-Chrome | Shortcut at `claude.ai/settings/browser-extension` | Same | ✓ `/oagp-onboard-thingalog` working; `/oagp-bootstrap` not yet packaged for C4C |
| claude.ai (web) | Project with custom instructions | Same | ❌ Not yet packaged |
| ChatGPT | Custom GPT system prompt | Same | ❌ Not yet packaged |
| Gemini | Gem | Same | ❌ Not yet packaged |
| Perplexity | Space / Custom prompts | Same | ❌ Not yet packaged |
| Any AI with web access | First-message primer | Same | ❌ Not yet packaged |

**Recommendation:** when canonical hosting at oagp.org is built, host the canonical content + provide runtime-specific packages or instructions. Coordinate with PO on which non-Anthropic runtimes are priority targets.

---

## 4. Items I'm explicitly handing off (for clarity)

| Item | Status | What's needed |
|---|---|---|
| Canonical promotion of bootstrap+onboard pair | Gate condition closed (validation memo filed) | Your call on hosting + canonical-formatting |
| Bootstrap-session transcript-tagging convention | Open question (recommendation in validation closeout §5) | Your resolution |
| Org-state-fork-for-time-travel pattern promotion | Thingalog-internal commitment; not yet promoted | Your call on cross-spec promotion + timing |
| Async-organization positioning | Surfaced 2026-05-23; in today's transcript | Consider canonicalizing as architectural commitment |
| Caliper local-conventions canonical decisions | Empirical data points captured | Make decisions when convenient |
| OAGP plugin packaging strategic call | PO is deciding | Weigh in when surfaced |
| Cross-runtime delivery packages | Claude Code + C4C onboard done; rest pending | Coordinate with PO on priorities |
| oagp.org canonical hosting | Not yet built | Coordinate with PO when ready |

## 5. Items thingalog-strategist retains

Going forward, thingalog-strategist scope:

- Thingalog-internal architectural decisions
- Coordination with thingalog-implementer (slice activation, closeout review, etc.)
- Thingalog-specific proposals + memos
- Thingalog's own org charter maintenance
- Thingalog-specific Strategist Calls during slice activation

If OAGP-canonical work surfaces in Thingalog-internal context (e.g., a new pattern emerges that should be promoted), thingalog-strategist will file pattern_promotion memos to YOU per the established convention, rather than doing the canonical work itself.

---

## 6. Notes on the seat-vacancy work I did

For your audit: the work I did during your seat's vacancy is properly your work. I'm handing it back in this memo. Specifically:

- The pattern_promotion_memo I filed 2026-05-22-1430 is structurally a memo FROM thingalog-strategist TO orgdef-strategist (the canonical inter-strategist coordination shape — that part is in scope). HOWEVER, the level of detail about HOW to canonicalize, the recommended cross-runtime delivery, the structural-implementation suggestions — some of those are more orgdef-strategist-decision-shaped than coordination-shaped. You're free to disregard any of those recommendations as you see fit; they were drafted without orgdef-strategist input.

- The validation closeout memo 2026-05-22-1530 follows the same shape — coordination-shape in form, but with substantive recommendations baked in. Same caveat.

- The architectural-commitment memos for org-state-fork-for-time-travel and async-organization are Thingalog-internal in their current filing location, but their substance is OAGP-canonical-relevant. Your call whether to promote either to canonical.

The labor-multiplier property works both ways here: I did work during your absence to keep things moving for the PO; you can now ratify or revise as you see fit, with the work already done as a starting point. Same shape as how `/oagp-bootstrap` draft proposals become PO-ratifiable artifacts — except here YOU are the ratifier.

---

## 7. What to read next

When you onboard via `/oagp-onboard` against orgdef-spec, you'll find this memo + the two predecessor memos in your inbox. Recommended reading order:

1. **This memo** — overview of everything
2. **`memos/2026-05-22-1430--...-pattern-promotion`** — the architectural pattern being promoted
3. **`memos/2026-05-22-1530--...-validation-complete`** — the empirical evidence closing the gate
4. **Cross-repo dive:** `s:/projects/thingalog/memos/2026-05-19-2200--...-org-state-forks-as-time-travel-substrate` (architectural property worth considering for promotion)
5. **Skill source:** `s:/projects/thingalog/skills/oagp-bootstrap/SKILL.md` and `s:/projects/thingalog/skills/oagp-onboard/SKILL.md` (the canonical-draft content)
6. **Empirical evidence:** `s:/projects/dangerstorm-oagp-test/` (the bootstrap validation fork; commits 6df43fd + fa24371)
7. **Reasoning arc:** Thingalog's `transcripts/thingalog-strategist/` when committed (today's transcript contains the async-organization synthesis + the full strategic conversation arc from this week)

You'll likely want to coordinate with thingalog-strategist (next session) and PO directly as you take over. I'll be available for coordination memos as needed.

---

## 8. Standing by

I return to Thingalog-internal scope after this hand-off. If anything surfaces during your work that needs Thingalog-strategist perspective (e.g., "you're proposing a canonical that conflicts with how Thingalog operates"), file a coordination memo and I'll respond per the standard inter-strategist convention.

Welcome to the seat. The OAGP-canonical work is in good shape; the gate is closed; canonical promotion is unblocked; three additional architectural items are surfaced for your consideration. Proceed at your pace.

— thingalog-strategist
