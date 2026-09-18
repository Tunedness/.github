# Security Policy

This is the organization-wide default. **A repository's own `SECURITY.md` wins over this
file.**

## Reporting a vulnerability

**Do not open a public issue, pull request or discussion.** Do not post it in a
discussion thread or a comment on an existing issue either.

Report it privately, in this order of preference:

1. **GitHub private vulnerability reporting** — on the affected repository, open the
   **Security** tab and choose **Report a vulnerability**. This is the fastest route and
   it keeps the whole exchange attached to the repository.
2. **Email** — `hello@tunedness.com`, with `SECURITY` and the project name in the
   subject.
3. If neither works, reach the maintainer through
   [muhammetsafak.com.tr](https://www.muhammetsafak.com.tr/en/) and ask for a private
   channel. Do not put the details in that first message.

## What to include

- Which project and which version, commit or container tag.
- What an attacker can do with it, and what they need in order to do it — network
  position, an account, a particular configuration.
- The smallest reproduction you have: the requests, the config, the policy file.
- Whether it is already public anywhere.

A working exploit is useful but not required, and you do not need a suggested fix.

## What happens next

| | |
| --- | --- |
| Acknowledgement | within 72 hours |
| First assessment — severity, affected versions, rough plan | within 7 days |
| Fix or a dated plan | depends on severity; you will be told which |

You will be kept updated while it is open, including when the answer is "this is
working as intended" and why.

## Disclosure

Coordinated. A fix is released first, then an advisory naming the affected versions and
the mitigation. Reporters are credited by the name they choose, or not at all if they
prefer. Please give the fix a chance to ship before publishing; if a deadline matters to
you, say so in the first message and it will be respected rather than negotiated at the
last minute.

## Scope

In scope: anything in the code of a Tunedness project that lets someone read data they
should not, bypass a control the project claims to enforce, execute code, escalate a
role, or forge or erase an audit record.

A few things worth calling out, because they are what these tools are for:

- A payload that gets past an injection scanner, or a way to make it pass one.
- A path that leaks provider credentials, tokens or PII the project claims to mask.
- A way to reach another tenant's project, documents or vectors.
- A way to break the hash chain of an audit log without it being detectable.
- A way to bypass a budget, rate limit or access rule that is configured as enforcing.

Out of scope: findings against a deployment that is configured against its own
documentation, missing hardening on a default that the README explicitly tells you to
change before exposing it to a network, automated scanner output with no demonstrated
impact, and vulnerabilities in third-party dependencies — report those upstream, though
telling us which one is affected is appreciated.

## Supported versions

The latest release of each project is supported. These are pre-1.0 projects: fixes land
on the default branch and in the next release rather than being backported, unless a
repository states otherwise.
