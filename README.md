# sdd-skill

A Claude Code plugin providing the `spec-driven-development` skill.

## Layout

```
.claude-plugin/
  plugin.json         Plugin manifest
  marketplace.json    Marketplace entry (lets this repo be added as a marketplace)
skills/
  spec-driven-development/
    SKILL.md           Skill entry point
    references/         Per-phase reference files
```

## Install

```
/plugin marketplace add <path-or-git-url-to-this-repo>
/plugin install sdd@sdd-skill
```
