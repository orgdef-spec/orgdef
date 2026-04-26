# orgs/

The canonical orgdef library. Each `.openthing` file is a portable, validated organization-chart definition that has passed schema validation, roledef-reference resolution, and strategist sign-off.

orgdef artifacts reach this directory through the [two-stage submission workflow](../CONTRIBUTING.md#1-orgdef-submissions): submitted to `proposed-orgs/`, validated, reviewed, and promoted here at merge time.

## What's in this directory

- `.openthing` files for canonical orgdef artifacts
- `.json` mirrors (byte-equivalent) for fetcher-portability across runtimes that prefer the standard `.json` extension

## Lifecycle

Once an orgdef artifact is promoted to canonical, it gets an entry in [`../catalog.opencatalog`](../catalog.opencatalog) and a decision artifact in [`../decisions/`](../decisions/). Subsequent revisions follow the same submission workflow, with version bumps per semver.

## Status

**Empty.** v0.1 bootstrap. The first orgdef artifact (catdef-org — the catdef + roledef ecosystem org chart) is forthcoming as PR #1.
