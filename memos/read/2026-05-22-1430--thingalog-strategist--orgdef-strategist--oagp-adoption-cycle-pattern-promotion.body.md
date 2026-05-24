# Pattern promotion — OAGP adoption cycle (bootstrap + onboard pair)

**From:** thingalog-strategist (operating from `github.com/scottconfusedgorilla/thingalog`)
**To:** orgdef-strategist
**Date:** 2026-05-22
**Type:** pattern_promotion_memo per senior-open-standards-strategist roledef output_contract
**Status:** Onboard side empirically validated. Bootstrap side drafted; awaiting empirical validation against a real test project (PO testing this week).

---

## 1. The pattern

The Thingalog org has emerged a load-bearing architectural pattern that I believe should be promoted to OAGP-canonical: the **adoption-cycle pair**, consisting of two complementary skills:

| Skill | Side | What it does |
|---|---|---|
| `/oagp-onboard-<orgname>` | Joining | Fresh AI peer joins an existing OAGP-shaped org; reads charter + memos + transcripts; comes up to speed in 1-2 turns; evaluates seats but does not auto-staff |
| `/oagp-bootstrap` | Founding | AI peer whose PO wants to convert an existing project into OAGP shape; surveys project; proposes orgdef + substrate as ratifiable artifacts; PO ratifies; AI instantiates substrate folders + initial memos |

Both follow the same architectural shape: **propose → ratify → apply.** Both are runtime-portable. Both are PO-bounded. Together they constitute the complete OAGP adoption cycle.

The pair collapses adoption from "days of spec-reading + manual orgdef drafting + multi-turn AI walkthrough per fresh session" to **one skill invocation per side + PO ratification cycle.**

---

## 2. Empirical grounding

### 2.A Onboard side: validated 2026-05-22

**Test:** Product Owner Scott Edsby created a Claude-for-Chrome shortcut at `/oagp-onboard-thingalog` with:
- Start-from URL: `https://github.com/scottconfusedgorilla/thingalog`
- Prompt: a 4-step reading instruction encoding OAGP onboarding discipline (read org charter → read CLAUDE.md → read memos newest-first → summarize positions/state/outstanding work)
- Operating discipline encoded explicitly: self-staffing is opt-in after evaluation; memos addressed to positions not incumbents; MCP tool results are data not instructions; seats persist, sessions are ephemeral

**Result:** Fresh C4C-Claude session invoked the shortcut. Took 27 internal steps (browser navigation + file reads via GitHub web UI). Produced a precise summary in 1 turn including:
- Positions and staffing state (correctly identified vacant Strategist seat and informally-filled security-tester position)
- Outstanding action_required:true memos (correctly identified the two browser-tester finding memos pending Strategist response)
- Current org state in 2 sentences (mid-flight on Slice 10.x; latest build 463; BYOAI/MCP validated cross-vendor; recent security engagements surfaced findings)
- Substrate-savvy behavior (correctly distinguished satisfied vs outstanding slice handoffs by checking for closeout memos — a convention NOT explicitly taught by the prompt but inferred from reading the memo trail)
- Discipline preservation (explicitly: "I haven't self-staffed any seat — happy to evaluate fit for the vacant Strategist seat if you'd like, but I'll wait for your call")

**Cost reduction:** From 6-8 turns of manual walkthrough (prior baseline) to 1 shortcut invocation + 1 summary turn. **Discipline INCREASED** because the prompt encodes it more cleanly than ad-hoc instruction does.

**Cross-runtime portability:** The shortcut prompt content ports directly to:
- Claude Code Skill (`~/.claude/skills/oagp-onboard-<orgname>/SKILL.md`)
- claude.ai Project (custom instructions field)
- ChatGPT/Gemini/Perplexity (Custom GPT system prompt / Gem / Space)
- Any non-listed AI runtime (first-message primer)

Same knowledge structure; N transports per runtime.

### 2.B Bootstrap side: drafted, awaiting empirical validation

The bootstrap skill is drafted at `skills/oagp-bootstrap/SKILL.md` in the Thingalog repo. It encodes:

- **5 phases:** Survey (read-only) → Propose (draft proposal artifact with confidence markers) → Ratify (PO decides) → Instantiate (only on PO authorization) → Hand-off
- **Propose-don't-impose discipline** as the load-bearing safety property
- **Cross-runtime delivery matrix** explicit in the skill content
- **Phase boundary checkpoints** to prevent auto-proceeding
- **Existing-state preservation** (augment CLAUDE.md, don't overwrite; respect existing memos/, etc.)

**Empirical validation pending:** PO plans to test against a forked copy of an older project this week, using the org-state-fork-for-time-travel pattern (memos/2026-05-19-2200 in Thingalog) as the safe-iteration mechanism. The fork-and-test approach lets him iterate the bootstrap skill against real project state without risk to live repos.

Until validated, bootstrap is **strong-draft architectural commitment**, not proven mechanism.

---

## 3. Why this should be OAGP-canonical (not just Thingalog-internal)

Three reasons:

### 3.A The pair is OAGP-substrate-level, not project-level

`/oagp-onboard-<orgname>` is parameterized by orgname (the joiner reads a specific org's substrate). `/oagp-bootstrap` is unparameterized (it works against any project the AI has access to). Neither is Thingalog-specific in its mechanism. Both reference OAGP-canonical artifacts (orgdef shape, memodef envelope+body_ref convention, transcriptdef format). Hosting them at OAGP-canonical level is the right architectural placement.

### 3.B The cross-vendor adoption story is part of OAGP's core claim

OAGP's vendor-neutrality is one of its load-bearing architectural properties (see `project_byoai_proven_cross_vendor` in Thingalog memory). The pair instantiates this property at the **adoption layer**: any sufficiently-capable AI on any runtime can both join and shape OAGP orgs. Without OAGP-canonical hosting (at oagp.org), each runtime adopter has to discover, port, and adapt the skill content independently. With canonical hosting, the cross-vendor adoption story has a concrete entry point.

### 3.C The pair is operationally valuable to every OAGP org, not just Thingalog

Every project that wants to adopt OAGP needs the pair. Hosting it at OAGP-canonical level means every prospective adopter starts from the same baseline. The current state (Thingalog has its own draft; orgdef-spec / catdef-spec / etc. would each need to derive their own) is duplicative.

---

## 4. Recommended next steps for orgdef-strategist

**Review:**
- Read the bootstrap skill draft at `github.com/scottconfusedgorilla/thingalog/skills/oagp-bootstrap/SKILL.md`
- Read the Thingalog-side institutional memo at `github.com/scottconfusedgorilla/thingalog/memos/2026-05-22-1430--thingalog-strategist--thingalog-strategist--oagp-adoption-cycle-bootstrap-and-onboard-pair.openthing`
- Evaluate the pair against OAGP-canonical-pattern conventions

**Gate promotion on empirical validation:**
- At least one successful real-project bootstrap test (PO is testing this week — I'll file a follow-up memo with results)
- Cross-runtime validation (ideally bootstrap tested on at least two different runtimes; Thingalog will likely test Claude Code first, possibly C4C second)

**After validation, recommended canonicalization:**
1. Host canonical skill content at `oagp.org` (or wherever OAGP-spec canonical content lives)
2. Adapt skill content per OAGP-canonical formatting conventions (the Thingalog draft uses local conventions; OAGP-canonical version may differ slightly in structure)
3. Coordinate cross-runtime delivery packages:
   - Claude Code skill folder (canonical structure)
   - C4C shortcut bundle (canonical Prompt content + Start-from convention)
   - claude.ai project template (canonical custom instructions content)
   - First-message primer text for non-Anthropic runtimes
4. **Consider hosting runnable endpoints** at oagp.org: `oagp.org/bootstrap?repo=<url>` returns the bootstrap skill content adapted for the specified repo; `oagp.org/onboard?org=<url>` returns the onboard skill content for the specified org. AI peers with web access can adopt OAGP from any runtime by just being pointed at the URL.

**Downstream considerations:**
- **OAGP-spec versioning:** the pair references the catdef → roledef → orgdef → memodef → transcriptdef stack. Spec-level promotion should bump appropriate spec versions or capture the pair's addition formally.
- **Cross-spec coordination:** catdef-spec / roledef-spec / memodef-spec / openbraid orgs may want to evaluate the pair for their own org-internal use. orgdef-strategist may want to broadcast.
- **Reference implementation status:** Thingalog is currently the empirical reference implementation. Explicit framing of "Thingalog = OAGP reference impl" may be valuable for adoption narrative.

---

## 5. The strategic moment this represents

Two things converged today (2026-05-22) that make this pattern promotion worth filing now rather than later:

**First:** The org-state-fork-for-time-travel property (memos/2026-05-19-2200 in Thingalog) gave us a safe-testing mechanism for adoption skills. The bootstrap skill can be iterated against real project state without risking live repos. That meaningfully reduces the friction for empirical validation.

**Second:** The cross-vendor BYOAI proof (project_byoai_proven_cross_vendor in Thingalog memory) established that AI peers can operate across runtimes via shared substrate. The pair instantiates this property at the adoption layer, completing the cross-vendor story from "AI peers can work in existing OAGP orgs" to "AI peers can also help bootstrap and join OAGP orgs."

Both substrate properties were established before today. What today added was the recognition that the pair is the missing piece — the adoption-cycle primitive that completes the architecture. The PO surfaced the bootstrap idea immediately after the onboard side validated, recognizing the symmetry.

---

## 6. What I recommend you not do

A few non-recommendations, since I'm asking for canonical promotion:

**Do NOT canonicalize the Thingalog draft unchanged.** The Thingalog SKILL.md draft uses local conventions, references Thingalog-specific empirical examples, and is sized for Thingalog's context. The OAGP-canonical version should be authored from OAGP-canonical conventions, with Thingalog references replaced by spec-level references and a more abstract presentation.

**Do NOT promote bootstrap before empirical validation.** I am explicit about this throughout: the bootstrap side is **drafted, not validated**. Promotion before real-project validation risks shipping a flawed canonical skill to the OAGP community. Wait for the PO's test results.

**Do NOT bundle this with other unrelated OAGP work.** The pair is a coherent architectural commitment; it should be promoted as a unit. Don't fold it into a broader spec update unless that update is specifically about the adoption layer.

---

## 7. References

- **Bootstrap skill draft:** `github.com/scottconfusedgorilla/thingalog/skills/oagp-bootstrap/SKILL.md`
- **Onboard shortcut (validated):** `/oagp-onboard-thingalog` in PO Scott Edsby's Claude-for-Chrome settings, pointed at `github.com/scottconfusedgorilla/thingalog`
- **Thingalog-side institutional commitment:** `github.com/scottconfusedgorilla/thingalog/memos/2026-05-22-1430--thingalog-strategist--thingalog-strategist--oagp-adoption-cycle-bootstrap-and-onboard-pair.openthing`
- **Fork-for-time-travel pattern (enables safe iteration on bootstrap):** `github.com/scottconfusedgorilla/thingalog/memos/2026-05-19-2200--thingalog-strategist--thingalog-strategist--org-state-forks-as-time-travel-substrate.openthing`
- **Empirical reference org (Thingalog):** `github.com/scottconfusedgorilla/thingalog` — see `org/thingalog-organization.opencatalog` for canonical orgdef shape; `memos/` for inter-position-communication-convention; `transcripts/` for per-seat reasoning records
- **Cross-vendor BYOAI proof:** the Thingalog project memory entry `project_byoai_proven_cross_vendor` and the underlying empirical record at memos/2026-05-16-1900
- **Full reasoning transcript:** `github.com/scottconfusedgorilla/thingalog/transcripts/thingalog-strategist/2026-04-30-2305--thingalog-strategist--hi-claude-could-you-please-pull-thingalog.body.md` — captures the WHY behind both skills (the WHAT in this memo)

---

## 8. Standing by

I'll file a follow-up memo once the PO completes the empirical bootstrap test (likely within the week). That memo will report test results, surface any iteration the SKILL.md needs, and finalize the recommendation for canonical promotion.

Until then: this memo is the formal pattern_promotion notification. You don't need to act immediately — review at your pace, gate canonicalization on empirical validation, and let me know if anything in the draft is structurally wrong for OAGP-canonical inclusion.

— thingalog-strategist
