---
name: spec-driven-development
description: Run a four-phase spec-driven development workflow (constitution → specify → plan → implement) that turns a feature idea into written requirements, a reasoned task breakdown, and reviewed implementation. Use this whenever the user wants to build a non-trivial feature, service, or project and would benefit from writing things down before coding — including phrasings like "spec driven development", "SDD", "let's spec this out", "write requirements first", "break this into tasks", "plan before you code", or when they mention a constitution, spec.md, plan.md, or tasks.md. Also use it when picking up an existing spec folder to continue or re-plan work, or when the user asks to implement tasks one at a time with sub-agents.
---

# Spec-Driven Development

Turn a vague feature idea into working code through four phases, each producing a durable
artifact on disk. The value is not the paperwork — it is that decisions get made explicitly,
in writing, before they get expensive. A wrong assumption caught in `spec.md` costs a
sentence; the same assumption caught in review costs a day.

## The four phases

| Phase | Produces | Question it answers |
|---|---|---|
| 1. Constitution | `docs/specs/constitution.md` | How does this project do things? |
| 2. Specify | `docs/specs/<feature>/spec.md` | What are we building and why? |
| 3. Plan | `docs/specs/<feature>/plan.md` + `tasks.md` | How, concretely, in what order? |
| 4. Implement | Code + updated `tasks.md` | Build it, one task at a time. |

Read the matching reference file when you enter a phase — each contains the templates and
the interviewing technique for that phase:

- `references/constitution.md`
- `references/specify.md`
- `references/plan.md`
- `references/implement.md`

## Layout on disk

```
docs/specs/
├── constitution.md            # project-wide, shared by all features
└── <feature-name>/            # kebab-case, e.g. oauth-login
    ├── spec.md
    ├── plan.md
    └── tasks.md
```

The constitution sits above the feature folders because it governs all of them. Features are
folders so several can be in flight at once without stepping on each other.

## Starting up

Before anything else, work out where the user actually is. Running phase 1 on a project that
already has a constitution wastes everyone's time, and jumping to implement without a spec
produces confident nonsense.

1. Check what exists: `ls docs/specs/ 2>/dev/null` and, if a feature is named, list its folder.
2. Resume at the first phase whose artifact is missing or stale. Say which phase you're
   starting at and why, so the user can correct you in one sentence.
3. If the user explicitly names a phase ("just do the plan"), honour that — but read any
   earlier artifacts that exist first, since each phase builds on the previous one.

If the repo has no `docs/specs/` at all and the user has only said something like "let's build
X", start at phase 1.

## Gates between phases

Each phase ends with the user's sign-off before the next begins. This is the core discipline
of the workflow — the artifacts are worthless if they were never really agreed to. At the end
of a phase, show the artifact (or a tight summary of it if long), name the two or three
decisions inside it you are least sure about, and ask whether to proceed.

Do not silently roll from spec into plan into implementation. A user who wanted the whole
chain in one go will say so, and then you can proceed with lighter check-ins — but that should
be their call, not an assumption.

## Handling the artifacts

Keep them alive rather than pristine. When something learned in a later phase contradicts an
earlier artifact — the plan reveals the spec was ambiguous, the implementation reveals the
plan missed a dependency — go back and amend the earlier file, then tell the user what you
changed. An artifact that no longer matches reality is worse than none, because people trust it.

Write the files with the actual filesystem tools rather than pasting long documents into chat.
The user needs to be able to diff them, commit them, and hand them to a teammate. Create the
target directory first (`mkdir -p docs/specs/<feature-name>`) — on a fresh repo none of these
paths exist yet.

## Scaling to the task

A small, well-understood change does not need four ceremonial phases. If the user asks for
something that is genuinely one task, say so and offer the short version: a few lines of spec,
a task list, and go. Reserve the full treatment for work where the requirements are actually
uncertain, several people are involved, or the cost of building the wrong thing is high.

Conversely, if a "quick change" starts sprouting open questions during the interview, that is
the signal to slow down and write the spec properly.
