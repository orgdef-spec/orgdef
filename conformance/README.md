# conformance/

Conformance fixtures and runtime-evidence artifacts for orgdef.

## Subdirectories

### `valid_orgs/`

Exemplar orgdef artifacts that demonstrate proper schema usage. Each fixture exercises a specific aspect of the schema. Use as reference when authoring new orgdef artifacts.

### `invalid_orgs/`

Counterexamples that demonstrate common errors validators must catch (missing MUST fields, dangling relationship references, reserved-namespace misuse, broken roledef references, internal-consistency violations).

### `runtime_evidence/`

Per-runtime test outputs documenting how a given runtime behaves with orgdef artifacts. v0.2+ work; deferred until orgdef-aware tooling lands.

## Status

**Empty.** v0.1 bootstrap. Fixtures will accumulate as the schema and the library mature.
