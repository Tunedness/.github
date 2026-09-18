# Contributing

This is the organization-wide default. **A repository's own `CONTRIBUTING.md` wins over
this file** — read that one first if it exists.

Every project here is self-hosted infrastructure that other people run in production.
That shapes what a good contribution looks like: small, explained, and safe to deploy
without reading the diff.

## Before you write code

**Open an issue first for anything that is not a small fix.** A new feature, a
dependency, a change to a config key, a change to the wire format or the database
schema — these are cheaper to discuss in an issue than to un-merge. Bug fixes,
documentation, and tests do not need one.

**Say what you are picking up.** A comment on the issue is enough. It stops two people
writing the same patch.

**Check the project's `.ssot/` documents if it has them.** Several projects keep their
PRD and architecture decision records there. A change that contradicts a recorded
decision needs to argue with the decision, not work around it.

## Working on a change

- **One concern per pull request.** A bug fix plus a refactor plus a rename is three
  reviews wearing one coat.
- **Match the surrounding code.** Naming, comment density, error handling, test style —
  the local idiom beats your preferred idiom.
- **Keep the build green.** Each repository documents its own commands; run the
  formatter, the linter, the type check and the tests before pushing.
- **Add a test when you fix a bug.** It should fail before the fix and pass after.
- **Update the docs in the same change.** A new flag, env var or endpoint that is not
  in the README does not exist.
- **Do not bump versions or edit the changelog** unless the repository asks you to;
  releases are cut by the maintainer.

## Commits and pull requests

- Write commit messages in English, in the imperative: `add pgvector HNSW index`, not
  `added` or `adding`.
- The subject line says what changes; the body says why, if why is not obvious.
- The pull request description covers what the change does, why, and how you verified
  it. The template asks for exactly that.
- Rebase on the default branch rather than merging it back in, and keep the history
  readable. You do not have to squash to a single commit.

## Review

The maintainer reviews everything. Expect questions about edge cases, failure modes and
operational impact — that is the review working, not an objection to the change.

A pull request may be declined because it is out of scope, or because the cost of
carrying it forever outweighs the benefit. Neither is a judgment of the work; ask on the
issue first to avoid finding out afterwards.

## Security

**Never open a public issue or pull request for a vulnerability.** Follow
[SECURITY.md](SECURITY.md) instead.

## Performance and detection claims

Several projects publish measured numbers — detection rates, false positive rates,
latency percentiles. If your change touches a path those numbers describe, re-run the
committed benchmark and report the before and after in the pull request. A change that
moves a published number and does not say so is the one kind of patch that gets
reverted on sight.

## Licensing

By contributing you agree that your contribution is licensed under the repository's
license: `AGPL-3.0-or-later` for Ragmux and Contextator, `Apache-2.0` for McpGuard and
AgentFuse. Where a repository requires a contributor license agreement, its `CLA.md`
says so and the pull request will tell you.
