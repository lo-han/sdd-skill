# sdd-skill

A [Claude Code](https://docs.claude.com/en/docs/claude-code) plugin that adds the
**`spec-driven-development`** skill: a four-phase workflow that turns a vague feature
idea into written requirements, a reasoned task breakdown, and reviewed implementation.

The point isn't paperwork. It's that decisions get made explicitly, in writing, before
they get expensive. A wrong assumption caught in `spec.md` costs a sentence; the same
assumption caught in code review costs a day.

## The four phases

| Phase | Produces | Question it answers |
|---|---|---|
| 1. Constitution | `docs/specs/constitution.md` | How does this project do things? |
| 2. Specify | `docs/specs/<feature>/spec.md` | What are we building, and why? |
| 3. Plan | `docs/specs/<feature>/plan.md` + `tasks.md` | How, concretely, and in what order? |
| 4. Implement | Code + updated `tasks.md` | Build it, one task at a time. |

Each phase ends with your sign-off before the next begins, and each writes a durable
file to disk that you can diff, commit, and hand to a teammate.

## Requirements

- A recent version of Claude Code (with `/plugin` marketplace support). Run `claude update` if `/plugin` is not recognised.

## Installation

Install straight from this repository over SSH. In an interactive Claude Code session:

```
/plugin marketplace add git@github.com:lo-han/sdd-skill.git
/plugin install sdd@sdd-skill
```

- The first command registers this repo as a plugin marketplace (`sdd-skill`).
- The second installs the `sdd` plugin from it. Restart Claude Code if prompted.

### Verify

```
/plugin
```

`sdd` should appear under installed plugins. The `spec-driven-development` skill is then
available to Claude automatically.

### Update

```
/plugin marketplace update sdd-skill
```

### Uninstall

```
/plugin uninstall sdd@sdd-skill
/plugin marketplace remove sdd-skill
```

## Usage

Once installed, Claude invokes the skill on its own when you ask for something that
benefits from specs first. Phrasings that trigger it include:

- "Let's spec this out before coding."
- "Spec-driven development for a new billing service."
- "Write the requirements first, then break it into tasks."
- "Pick up the existing spec in `docs/specs/oauth-login/` and continue."

You can also just describe a non-trivial feature and let Claude decide. It works out
which phase you're actually at — it won't re-run the constitution phase on a project
that already has one, and it won't jump to implementation without a spec.

Small, well-understood changes don't need the full ceremony; the skill offers a short
version (a few lines of spec, a task list, go) when the work doesn't warrant four phases.

## What it creates in your project

```
docs/specs/
├── constitution.md          # project-wide, shared by every feature
└── <feature-name>/          # kebab-case, e.g. oauth-login
    ├── spec.md
    ├── plan.md
    └── tasks.md
```

The constitution sits above the feature folders because it governs all of them. Features
are folders so several can be in flight at once without stepping on each other.

## Repository layout

```
.claude-plugin/
  plugin.json          Plugin manifest
  marketplace.json     Marketplace entry (lets this repo be added as a marketplace)
skills/
  spec-driven-development/
    SKILL.md           Skill entry point
    references/        Per-phase reference files (constitution, specify, plan, implement)
```

## License

[MIT](LICENSE) © lo-han
