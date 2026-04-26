# decisions/

Strategist decision artifacts capturing the rationale behind library-inclusion calls and accepted spec proposals. The directory is the load-bearing institutional-memory layer for orgdef governance.

## File patterns

### `<id>.md` — orgdef inclusion decisions

One decision artifact per accepted orgdef artifact promotion. Authored at promotion time, before the merge button is pushed. Captures: disposition, rationale, notable design choices, items not incorporated, workflow validation, forward-reference resolution, runtime-test status, strategist memory work items, notes, cross-references.

### `<id>-v<N>.md` — version-bump retrofit decisions

When an existing orgdef artifact is bumped to a new major version (e.g., to retrofit derivation lineage), the decision artifact carries a version suffix. Predecessor decisions are preserved unchanged for audit-trail continuity.

### `proposal-<name>.md` — spec proposal decisions

When a spec proposal in `../proposals/` is decided (Accept / Accept-with-modifications / Reject / Defer), the strategist files the decision here.

### Other

Cross-cutting decisions that don't fit the above patterns (e.g., bootstrap-event records, governance ratifications) are filed with descriptive names.

## Status

**Empty.** v0.1 bootstrap. First decision artifact will be filed when the catdef-org submission lands as PR #1.
