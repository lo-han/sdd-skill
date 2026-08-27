# Phase 1 — Constitution

The constitution holds the standing rules of the project: the things that are true for every
feature, so they don't have to be re-litigated in every spec. Language and version, testing
expectations, error-handling conventions, what "done" means, what the project deliberately
refuses to do.

It exists so later phases can be short. If the constitution says "all HTTP handlers return
RFC 7807 problem details", no spec ever has to mention error shapes again.

## Where it comes from

Offer three routes and let the user pick:

1. **Import global** — `~/.claude/constitution.md`. Check whether it exists first
   (`test -f ~/.claude/constitution.md`). If it does, read it and show the user a summary
   rather than the whole file, then create `docs/specs/` if it does not exist
   (`mkdir -p docs/specs`) and copy the file to `docs/specs/constitution.md`.
2. **Import and adapt** — copy the global one, then interview about project-specific
   overrides. This is usually the right default when a global file exists, since a global
   constitution is by nature generic.
3. **Create local from scratch** — no global file, or the project is unlike the user's others.

If the local `docs/specs/constitution.md` already exists, do not overwrite it. Read it, and
ask whether the user wants to amend it or move on to phase 2.

## Inferring from the repo

Before interviewing, look at what the project already tells you: the language and its version,
the test framework, the linter config, the CI workflow, existing directory conventions, the
README's stated goals. A constitution that contradicts the repo is a constitution nobody
follows. Bring these observations to the user as proposed entries — "your CI runs
`golangci-lint` with these rules, so I've written that in" — rather than asking questions they
have already answered in their own config files.

## Interviewing

Aim for a page, not a manifesto. The useful questions:

- What language, runtime, and version floor?
- What is the testing expectation — coverage target, unit vs integration, is TDD the norm?
- Which architectural patterns are house style, and which are banned?
- What are the non-negotiables: security, accessibility, performance budgets, data handling?
- How does work get delivered — branch naming, commit format, PR review, changelog?
- What is explicitly out of scope for this project, permanently?

Push back on entries that are too vague to act on. "Write clean code" cannot be followed or
violated; "functions over 50 lines need a comment explaining why" can.

## Template

```markdown
# Project Constitution

**Project:** <name>
**Last updated:** <date>
**Source:** <imported from ~/.claude/constitution.md | created locally | imported + adapted>

## Purpose
One paragraph: what this project is and who it serves.

## Technology
- Language / runtime / version:
- Key frameworks and libraries:
- Datastores and external services:

## Engineering standards
- Testing:
- Error handling:
- Logging and observability:
- Naming and structure:

## Architectural principles
Numbered, each with a one-line rationale.

## Non-negotiables
Security, privacy, accessibility, performance, licensing.

## Delivery
Branching, commits, review, release.

## Out of scope
Things this project will not do, and why.
```

## Closing the phase

Write the file, show the user the sections that came from your inference rather than from
them (those are the likeliest to be wrong), and ask for sign-off before moving to specify.
