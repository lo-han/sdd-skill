# Phase 2 — Specify

Capture what is being built and why, in enough detail that someone could disagree with it.
A spec that nobody could object to is usually too vague to be useful.

Write to `docs/specs/<feature-name>/spec.md`. Derive the feature name from the user's
description in kebab-case, and confirm it — the folder name sticks around.

## The stance to take

Read the constitution first; anything it already settles does not belong in the spec.

Then interview, but interview like someone who will have to build the thing. The failure mode
is accepting the user's framing wholesale and writing down a tidier version of what they
already said. Your value here is finding the parts they haven't thought about yet.

Productive lines of questioning:

- **Who is this for, and what do they do today instead?** The current workaround reveals the
  real requirement more reliably than a feature description does.
- **What does success look like, numerically?** "Faster" is not a requirement. "P95 under
  200ms" is.
- **What are the edges?** Empty states, concurrent access, failure of the third party,
  the user with 10,000 of the thing instead of 3.
- **What's explicitly not in this feature?** Non-goals prevent scope creep more effectively
  than any amount of planning.
- **What must not break?** Existing behaviour, data, integrations, contracts.

Ask these in small batches — two or three at a time — rather than as a questionnaire. Offer
your own proposed answer alongside each question where you have one; it is far easier for a
user to correct a concrete suggestion than to fill a blank.

## Requirements worth writing

Each requirement should be testable. Prefer the form "the system shall <observable behaviour>
when <condition>", and number them (`FR-1`, `NFR-1`) so the plan and tasks can reference them.
That numbering is what makes traceability possible later: every task should point back to a
requirement, and any requirement with no task pointing at it is a gap.

Record open questions explicitly rather than resolving them with a guess. A visible
`OQ-1: unresolved` is a decision the team can make; a silent assumption is a bug.

## Template

```markdown
# Spec: <Feature Name>

**Status:** draft | approved
**Date:** <date>

## Problem
What's wrong today, for whom, and what it costs them.

## Objectives
Numbered outcomes, each with a measure of success.

## Users and scenarios
Short narrative scenarios — actor, trigger, expected outcome.

## Functional requirements
FR-1. The system shall ...
FR-2. ...

## Non-functional requirements
NFR-1. Performance / security / availability / accessibility ...

## Constraints
Existing systems, deadlines, dependencies, team limits.

## Non-goals
Explicitly out of scope for this feature.

## Acceptance criteria
Observable conditions that mean this is done. Map each back to an FR/NFR.

## Open questions
OQ-1. <question> — owner, blocking or not.
```

## Closing the phase

Show the spec and call out the open questions and the requirements you inferred rather than
heard. Ask the user to confirm the objectives and non-goals specifically — those two sections
cause the most rework when wrong. Get sign-off before planning.
