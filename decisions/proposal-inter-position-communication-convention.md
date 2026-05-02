# Proposal Decision: Inter-position communication convention (memos/ + x.org.memo_location)

**Disposition:** Accept (no modifications; OQs resolved inline)
**Origin:** [proposals/inter-position-communication-convention.md](../proposals/inter-position-communication-convention.md)
**Decided:** 2026-05-01 by orgdef-strategist
**Authorization:** Director (Product Owner) explicitly authorized this directional call 2026-05-01 in response to the Thingalog product-strategist's `handoffs/` proposal (the precipitating case). Director also authorized drafting of this decision artifact directly without a maintainer-review pass given (a) the proposal's strict additivity (no SCHEMA changes; one new `recommended_patterns.general` entry + CONTRIBUTING.md prose), (b) the cross-spec coordination already settled (memodef v0.2.0 `body_ref` shipped same-day, FYI memo received), and (c) the time-sensitivity of the first-real-org-adopter precedent.
**Bootstrap caveat:** Same-head provenance — orgdef-strategist holds catdef-strategist + roledef-strategist + memodef-strategist informally during bootstrap. The cross-spec coordination memo to memodef-strategist (case-2-trigger memo) was authored from this seat; the response (body_ref v0.2.0 ship) was authored from the memodef-strategist seat in a parallel session arc. Both sides flow through proper repos (originating proposal in memodef-spec/proposals/; receiving FYI memo in orgdef-spec/memos/) for future audit.

## Disposition

Accepted as drafted; no modifications. The proposal cleanly captures the structural call (memos/ as universal channel; x.org.memo_location escape hatch) without taking on adjacent concerns (memodef ergonomics, which resolved independently same-day). All three Open Questions resolve to the working positions stated in the proposal; rationale below.

## Rationale

### Why Accept

The structural argument against `handoffs/` is independent of the ergonomic argument that motivated it. The ergonomic concern (body-as-JSON-string for hand-authored multi-paragraph operational content) was a real friction; the structural cost of `handoffs/` (family-level bifurcation propagating to every adopter, AI-legibility primacy violation, first-real-adopter precedent) was a separate and load-bearing argument. The proposal correctly separates these: `memos/` as universal channel is a placement-shape call inside orgdef-spec scope; ergonomics is a memodef-spec scope concern.

The same-day shipping of memodef v0.2.0 `body_ref` removed the underlying ergonomic friction without requiring orgdef-side wording adjustment (per memodef-strategist's FYI memo at [memos/2026-05-01-2000--memodef-strategist--orgdef-strategist--body-ref-v0.2-shipped-no-patch-needed.openthing](../memos/2026-05-01-2000--memodef-strategist--orgdef-strategist--body-ref-v0.2-shipped-no-patch-needed.openthing)). This is empirical confirmation that placement and ergonomics belong in different specs and should ship independently — exactly the rationale the proposal's Alternative 2 articulated.

The SHOULD-with-`x.org.memo_location`-escape-hatch shape preserves discipline (default is universal across the family) while leaving room for monorepo + vendor-imposed-layout adopters to declare deviations machine-discoverably. The catdef-substrate's `x.<domain>.<identifier>` namespace already permits the extension; no orgdef-spec schema work is required to enable it.

### Why no modifications

The proposal does not reach beyond its stated scope (no SCHEMA changes proposed, no normative behavior changes for the validator beyond informational notes, no breaking changes for existing operational orgdefs). The recommended_patterns.general entry is one new array element; the CONTRIBUTING.md additions are two prose sections (the new "Inter-position communication conventions" section + the migration prose). All three OQs have defensible resolutions stated below; none required changes to the proposal text itself.

The proposal correctly excluded preemptive parallel-pattern work (e.g., `x.org.proposals_location` for proposals/ placement) per OQ3's working position. Avoiding the architecture-astronaut tax of solving theoretical adopters' problems is the right discipline; cross-spec patterns get codified when an adopter actually surfaces friction, not before.

## Resolutions to Open Questions

### OQ1 → single string

**Strategist call: single string.** Author's working position. Multi-location implies inbox-routing rules ("memos to position X go here, memos to position Y go there") which approach memodef-side concerns about per-recipient routing. orgdef declares the org-level default; finer routing within the recipient's working tree is memodef-governed (maildir vs flat, per the sibling-spec layer separation already established).

If a future adopter surfaces a legitimate multi-location need, the SHOULD-pattern leaves room: the adopter declares `x.org.memo_location` as a string AND uses an additional org-specific extension (e.g., `x.<adopter>.memo_location_overrides`) for the per-recipient routing. Multi-location-as-list could be promoted via a future proposal once empirically grounded.

### OQ2 → no warning by default; informational note acceptable

**Strategist call: no warning by default.** Author's working position. The extension is a legitimate escape hatch declared in the orgdef:Organization artifact's metadata; firing a structured warning would treat declared deviation as suspect, contradicting the SHOULD-with-escape-hatch shape. Validator implementations MAY surface an informational note in human-readable output (e.g., "this org declares a non-default memo location at `x.org.memo_location: communications/inter-position/`") for human-aided audit; structured warnings reserved for actual conformance violations (broken cross-references, malformed memos, etc.).

### OQ3 → do not preempt; flag for future-proposal triage

**Strategist call: noted, no action this cycle.** Author's working position. The `proposals/` (orgdef + roledef) and `decisions/` (orgdef + roledef + catdef) directory placements follow per-spec convention without an `x.org.<dir>_location` extension. If a future adopter raises analogous "where do proposals/decisions live" questions, this proposal's `x.org.memo_location` shape composes cleanly with `x.org.proposals_location` / `x.org.decisions_location` parallel extensions (additive, single-string, escape-hatch-shaped). Filing those preemptively without an empirical adopter need is over-engineering; flag for future-proposal triage when surfaced.

## Build directive (for orgdef-maintainer when scaffolding work begins)

Execute in this order:

1. **Canonical template patch (P1)** — apply to `proposed-orgs/oagp-family-open-standard.openthing`:
   - Add the new `recommended_patterns.general` entry per the proposal's P1 section, verbatim
   - Bump canonical template version `1.1.0 → 1.2.0` (additive minor)
   - Update `metadata.history` with a v1.2.0 entry summarizing the patch (added inter-position-communication-channel pattern entry)
2. **CONTRIBUTING.md update (P2 + P3)** — add the new "Inter-position communication conventions" section per the proposal's P2 section, verbatim, including the migration-path prose from P3.
3. **Conformance fixtures (deferred until empirical need)** — no new conformance fixtures required for v0.1; the canonical template demonstrates the pattern by example. A future canonical-orgs entry that uses `x.org.memo_location` as a non-default value would serve as the reference fixture for the extension's use; queue when an adopter (operational or canonical) genuinely needs it.
4. **No SCHEMA.md changes** — this proposal is content-only (recommended_patterns.general entry + CONTRIBUTING prose); the `x.org.memo_location` extension lives in the catdef-substrate's `x.<domain>.<identifier>` namespace and requires no orgdef SCHEMA additions.
5. **No version bump on orgdef SCHEMA** — same reasoning as item 4. Canonical template version bumps independently; orgdef SCHEMA stays at current minor.

## Cross-spec coordination

Already complete and recorded:

- **memodef-spec coordination:** case-2 trigger memo filed at `memodef-spec/memodef/memos/inbox/2026-05-01-1430--orgdef-strategist--memodef-strategist--body-ref-case-2-trigger.openthing` (now in `memos/read/` per receiver-commits convention canonized same-day in memodef). FYI memo from memodef-strategist confirming v0.2.0 shipped exactly as proposed (no orgdef-side patch needed) at [`memos/2026-05-01-2000--memodef-strategist--orgdef-strategist--body-ref-v0.2-shipped-no-patch-needed.openthing`](../memos/2026-05-01-2000--memodef-strategist--orgdef-strategist--body-ref-v0.2-shipped-no-patch-needed.openthing).
- **thingalog (first-real-adopter org) coordination:** initial memo conveying the directional call at `thingalog/memos/2026-05-01-1430--orgdef-strategist--thingalog-strategist--inter-position-communication-convention.openthing` (committed 2026-05-01 17:38 by thingalog-strategist; memo's migration ask was acted on — Thingalog's first inter-position memodef:Memo at `thingalog/memos/2026-05-01-1730--thingalog-strategist--implementer--slice-1-task-1-pwa-manifest.openthing` is the empirical first-real-org adoption of the convention). Follow-up memo at `thingalog/memos/2026-05-01-2230--orgdef-strategist--thingalog-strategist--body-ref-now-shipped.openthing` informs thingalog-strategist that body_ref is now available for future handoffs (slice-1-task-1 retro-conversion is strategist's call, not required).
- **catdef-strategist + roledef-strategist:** no cross-spec action required for this proposal (inter-position memo placement is orgdef + memodef coordination only). When/if catdef-spec or roledef-spec orgdefs gain `x.org.memo_location` declarations, that's adopter-side application of the canonical pattern, not cross-spec coordination.

## Notable design choices

1. **Placement-vs-ergonomics separation.** This proposal scoped to placement (orgdef-side); ergonomics scoped to memodef v0.2 (memodef-side). The two-spec separation was empirically validated by the same-day independent shipping of both: placement convention here, body_ref over there. Future cross-cutting concerns SHOULD attempt the same separation early; if an unscoped concern emerges that cuts across orgdef + memodef, surface as a coordination call before drafting either side.
2. **SHOULD with machine-discoverable escape hatch (x.org.memo_location), not MUST.** The discipline of "default is universal; deviation requires explicit declaration in the orgdef artifact" is the right shape for cross-family conventions. MUST forecloses on legitimate adopter shapes (monorepos, vendor-imposed layouts); SHOULD-without-escape-hatch creates ambiguity over what "non-default" looks like; SHOULD-with-machine-discoverable-escape-hatch preserves both discipline and adopter sovereignty.
3. **First-real-adopter precedent as load-bearing rationale.** The proposal cited Thingalog's first-real-adopter status as a reason to act now rather than defer. This precedent argument generalizes: future calls affecting how OAGP-family-derived orgs structure their working trees SHOULD weight the first-real-adopter dynamic. The four spec-org operational orgdefs (catdef, roledef, memodef, orgdef) bootstrapped each other; Thingalog is the first non-spec adopter, and patterns landing here will be copied. Treat first-real-adopter calls with appropriate weight.
4. **Build-directive-only canonical-template patch (no schema work).** The proposal explicitly does not reach into SCHEMA.md. The recommended_patterns.general slot was designed for guidance like this; using it is internally consistent with how the canonical already carries patterns ("Senior strategist role separation," "Two-section charter discipline," "Recursive self-describing v1 milestone"). The build directive's items 4 and 5 are explicit "do nothing" pointers — preemptively closing two design questions ("does this need a schema bump?" "does this need a version bump?") that downstream readers might otherwise have to re-derive.

## Items not incorporated

None. The proposal's three Open Questions resolve inline; no proposal text required modification.

## Workflow validation

- **Strategist scope check:** This is a SHOULD-pattern addition to the canonical template + CONTRIBUTING.md prose. Both fall within strategist scope per the orgdef-strategist roledef output_contract.strategist_deliverables (drafted proposal artifacts; design calls; library-curation rulings). No catdef substrate changes; no roledef-side changes; memodef-side coordination already settled in parallel.
- **Cross-spec discipline:** Same-head provenance flagged in Bootstrap caveat above. The artifact trail goes through proper repos (orgdef-spec proposal in this repo's `proposals/`; memodef-spec coordination memo and FYI response in their respective repos) per the no-shortcut-the-artifact-trail discipline.
- **Director ratification:** Directional call ratified 2026-05-01; this decision artifact drafted for Director review per Director's explicit instruction. Build directive items execute under standard maintainer-scope discipline once decision is committed.

## Forward-reference resolution

- **Canonical-orgs library promotion** (per the canonical-orgs-library decision's foreshadowed downstream work): once `proposed-orgs/oagp-family-open-standard.openthing` is promoted to `canonical-orgs/oagp-family-open-standard.openthing` (currently strategist-cleared, awaiting orgdef SCHEMA v0.3 land per the canonical-orgs-library decision), the v1.2.0 patch from this proposal SHOULD be applied at promotion time (or as a follow-on patch) to ensure the canonical reflects the inter-position pattern.
- **Future v0.3 SCHEMA proposal (forward_work_items[], x.position.lifecycle, structured cross-org reference shape):** independent of this proposal. The two ship in different review paths (recommended_patterns vs SCHEMA fields); no coupling.

## Notes

- The Director articulated this case as "really an oversight" in the directional ratification — meaning that the universal-channel-via-memos/ convention had been operating implicitly across the four spec orgs without explicit canonization, and the first non-spec adopter (Thingalog) surfaced the gap by reasonably proposing an alternative. This is exactly the kind of empirical surfacing that the canonical-orgs library + canonical-template + recommended_patterns shape is designed to produce: implicit conventions get codified at the moment a real adopter surfaces friction, not preemptively.
- The same-day shipping cadence (proposal at 14:30 → directional ratification → orgdef proposal filed → memodef coordination memo filed → memodef v0.2.0 shipped → FYI memo back → orgdef decision artifact drafted, all in one calendar day) is empirically encouraging for the parallel-strategist-seats arrangement during bootstrap. Tracking informally; if this pattern holds across additional cross-spec coordination cases, worth noting in strategist memory as a workflow validation point.

## References

- Originating proposal: [proposals/inter-position-communication-convention.md](../proposals/inter-position-communication-convention.md)
- Director ratification: 2026-05-01 conversation in orgdef-strategist chair
- Precipitating thingalog-strategist proposal: surfaced via Director quote 2026-05-01; thingalog product-strategist roledef's `handoff_prompt_to_implementer` output_contract entry: [`thingalog/org/jobs/product-strategist.openthing`](https://github.com/scottconfusedgorilla/thingalog/blob/master/org/jobs/product-strategist.openthing)
- Cross-spec coordination memos:
  - Outgoing case-2-trigger to memodef-strategist (now in memodef-spec `memos/read/`): commit `9b29931` includes its receipt
  - Incoming FYI from memodef-strategist closing the loop: [`memos/2026-05-01-2000--memodef-strategist--orgdef-strategist--body-ref-v0.2-shipped-no-patch-needed.openthing`](../memos/2026-05-01-2000--memodef-strategist--orgdef-strategist--body-ref-v0.2-shipped-no-patch-needed.openthing)
- thingalog-side adoption artifacts:
  - Initial memo (committed by thingalog-strategist 17:38): [`thingalog/memos/2026-05-01-1430--orgdef-strategist--thingalog-strategist--inter-position-communication-convention.openthing`](https://github.com/scottconfusedgorilla/thingalog/blob/master/memos/2026-05-01-1430--orgdef-strategist--thingalog-strategist--inter-position-communication-convention.openthing)
  - First adopter inter-position memo (Thingalog's first body-as-string handoff): [`thingalog/memos/2026-05-01-1730--thingalog-strategist--implementer--slice-1-task-1-pwa-manifest.openthing`](https://github.com/scottconfusedgorilla/thingalog/blob/master/memos/2026-05-01-1730--thingalog-strategist--implementer--slice-1-task-1-pwa-manifest.openthing)
  - Follow-up memo (body_ref now shipped): [`thingalog/memos/2026-05-01-2230--orgdef-strategist--thingalog-strategist--body-ref-now-shipped.openthing`](https://github.com/scottconfusedgorilla/thingalog/blob/master/memos/2026-05-01-2230--orgdef-strategist--thingalog-strategist--body-ref-now-shipped.openthing)
- memodef-spec implementation: commits `49d4640` (proposal), `c7049d8` (decision), `9b29931` (implementation, version bump 0.1.0 → 0.2.0)
- Sibling-spec precedents:
  - Canonical-template v1.1 + placement-convention decision: [`decisions/proposal-canonical-template-v1.1-and-placement-convention.md`](proposal-canonical-template-v1.1-and-placement-convention.md) — the v1.1 → v1.2 cadence here mirrors the v1.0 → v1.1 cadence that landed canonical-template-shape patches and placement convention as separate proposals
  - Canonical-orgs-library decision: [`decisions/proposal-canonical-orgs-library.md`](proposal-canonical-orgs-library.md) — the canonical-template patch in this decision applies to the `oagp-family-open-standard` artifact whose promotion to `canonical-orgs/` was strategist-cleared in that earlier decision
