# Phase 3 — Plan

Turn requirements into an ordered set of concrete tasks. Two things make this phase different
from just writing a to-do list: you reason through the approach in the open before committing
to it, and you ground the work in examples the user provides.

Produces `docs/specs/<feature>/plan.md` (the reasoning and the approach) and
`docs/specs/<feature>/tasks.md` (the executable list).

## Step A — Collect examples from the user first

Do this before designing anything. Ask the user for concrete examples, and say plainly why you
want them: the difference between code that fits a codebase and code that merely works is
almost entirely in conventions that are never written down, and examples transmit those
conventions far more efficiently than any description.

Ask for two to three of:

- **A file they consider exemplary** — the shape they want new code to look like. Paths are
  enough; read them yourself.
- **A previous feature done well** — its PR, its commit series, or its own spec/task list,
  showing the granularity of task they like.
- **An input/output pair** — for anything with a data shape: a sample request and response,
  a row before and after, the exact CLI invocation and its expected stdout.
- **A counter-example** — something in the codebase they dislike and don't want repeated.
  These are unusually informative and users rarely volunteer them unprompted.

If the user has none to give, do not just proceed as if the question was never asked. Go find
candidates yourself: locate the two or three files in the repo most analogous to what is being
built, show them, and ask "should the new code look like this?" A confirmed guess is worth
nearly as much as a volunteered example, and it keeps the phase moving.

Record what you gathered in the plan's Examples section, with the specific convention each one
established — "handlers return `(T, error)` and never panic", not just a file path. That is
the part a sub-agent in phase 4 can actually act on, since it may never see the original file.

## Step B — Reason before you decide

Think the approach through step by step, and show that reasoning in `plan.md` rather than only
presenting the conclusion. The point is not ceremony: a stated chain of reasoning is something
the user can interrupt at the exact step where they disagree, which is much cheaper than
discovering the disagreement in the code.

Work through, in order:

1. **Restate the objective** in your own words from the spec. Mismatches surface here.
2. **Identify what the change touches** — the modules, data, contracts, and tests involved.
3. **Consider at least two approaches.** Name the tradeoff between them honestly, and say
   which you recommend and why. If there is genuinely only one sane approach, say that and say
   why, rather than inventing a strawman alternative.
4. **Sequence the work.** What must exist before what else can be tested?
5. **Name the risks.** Where is this likely to go wrong, and what's the early warning sign?

Then decompose into tasks — but derive them from the sequencing above, so each task has a
visible reason for existing and for sitting where it does in the order.

## Step C — Write the tasks

A good task is one focused change: it can be described in a sentence, verified on its own, and
reviewed without reading the other tasks. If a task needs "and" to describe it, it is probably
two tasks. If it takes a paragraph to explain what "done" means, the spec was unclear —
go back rather than papering over it.

Each task carries: an ID, a one-line description, the requirement it satisfies, the files it
is expected to touch, its dependencies, a verification step, and a size estimate (S/M/L).
The verification step matters most — it is what phase 4 uses to decide whether a task
actually landed.

Mark tasks that are independent of each other, since those are the candidates for parallel
sub-agents in phase 4.

## Templates

`plan.md`:

```markdown
# Plan: <Feature Name>

## Objective restated
## Surface area
Modules, data, contracts, and tests this touches.

## Examples provided
| Example | Source | Convention it establishes |
|---|---|---|

## Approaches considered
### Option A — <name>
Tradeoffs.
### Option B — <name>
Tradeoffs.
**Chosen:** <option> because ...

## Sequencing
Why the tasks are ordered the way they are.

## Risks
| Risk | Likelihood | Early signal | Mitigation |
|---|---|---|---|
```

`tasks.md`:

```markdown
# Tasks: <Feature Name>

Status key: [ ] pending · [~] in progress · [x] done · [M] manual (user) · [-] skipped

- [ ] **T-1** — <one-line description>
  - Satisfies: FR-1
  - Files: `path/to/file.go`
  - Depends on: none
  - Verify: `go test ./internal/auth/...` passes
  - Size: S
```

## Closing the phase

Present the chosen approach and the task list, and ask two things specifically: whether the
sequencing is right, and whether any task is too coarse to review comfortably. Get sign-off
before implementing.
