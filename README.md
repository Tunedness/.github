# .github

The Tunedness organization's meta repository. It holds two things:

1. **`profile/README.md`** — the page rendered at
   [github.com/Tunedness](https://github.com/Tunedness). It is the organization's
   front door: what Tunedness builds, which projects exist, and where each one lives.
2. **The org-wide community health files.** GitHub falls back to the files here for
   any repository in this organization that does not carry its own copy — the
   contributing guide, the code of conduct, the security policy, the support page and
   the issue and pull request templates.

Nothing here is code, and nothing here is published as a package.

## Layout

```
profile/README.md          the organization profile page
README.md                  this file
CONTRIBUTING.md            org-wide default; a repo's own copy wins
CODE_OF_CONDUCT.md         applies everywhere, no per-repo override expected
SECURITY.md                how to report a vulnerability privately
SUPPORT.md                 where questions go
PULL_REQUEST_TEMPLATE.md   default PR body
ISSUE_TEMPLATE/            default issue forms and the chooser's contact links
```

## What overrides what

A file in a repository always beats the one here. `Tunedness/McpGuard/SECURITY.md`,
if it exists, is the policy for McpGuard; this repository's `SECURITY.md` covers
everything that has no copy of its own.

The fallback is organization-scoped, so it reaches repositories under `Tunedness`
only. [Ragmux](https://github.com/Ragmux) and
[Contextator](https://github.com/Contextator) are separate organizations and carry
their own community health files.

## Editing the profile

`profile/README.md` is what most people see first, so it is worth keeping honest:

- Every claim about a project should be checkable in that project's README.
- Numbers stay attached to the corpus or benchmark they came from.
- A project that is not released yet says so.
- Links point at the canonical home of each project — its own organization and site
  where it has one.

Changes take effect as soon as they land on the default branch; the profile page is
not cached for long.
