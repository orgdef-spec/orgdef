# proposed-orgs/

Submission staging area for new orgdef artifacts. Artifacts in this directory are **in flight** — submitted but not yet promoted to the canonical library at [`../orgs/`](../orgs/).

## Why this directory exists

The two-stage workflow (per [CONTRIBUTING.md](../CONTRIBUTING.md#the-two-stage-workflow)) gives in-flight submissions a publicly visible home. Anyone browsing the repo can see what's pending without needing to query GitHub PRs.

## Lifecycle

An artifact lands here when a contributor opens a PR. It leaves here in one of two ways:

1. **Approved** — at merge time, the maintainer atomically moves the file from `proposed-orgs/` to `../orgs/`, updates `../catalog.opencatalog`, and records a decision in `../decisions/<id>.md`. Single merge action.
2. **Rejected** — the PR is closed without merge. Rationale is in the PR's closing comment.

## Submitting

See [CONTRIBUTING.md §1 orgdef Submissions](../CONTRIBUTING.md#1-orgdef-submissions) for the full process.
