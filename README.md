# skills

A collection of reusable skills for AI assistants — structured prompts that
define **how** to work on a class of tasks, not what to produce.

Each skill lives in its own directory with a `SKILL.md` file. Distributed via
[skills.sh](https://skills.sh/) — install with a single command into any
supported agent (Claude Code, Cursor, Codex, and 40+ more).

## Skills

| Skill | Description |
|-------|-------------|
| [design-process](./design-process/SKILL.md) | A disciplined process for producing design artifacts (websites, prototypes, slides, covers, mobile screens) with the AI acting as a senior designer. |
| [memory-bank](./memory-bank/SKILL.md) | Maintains a lightweight, always-current "project encyclopedia" in `.memory-bank/` — capturing architecture, stack, conventions, key entities, and active tasks. |

## Installation

### All skills

```bash
npx skills add ayusavin/skills
```

### Specific skill

```bash
npx skills add ayusavin/skills --skill design-process
```

### Global (available across all projects)

```bash
npx skills add ayusavin/skills -g
```

### Specific agent only

```bash
npx skills add ayusavin/skills -a claude-code
npx skills add ayusavin/skills -a cursor
npx skills add ayusavin/skills -a codex
```

### Install via Claude Code prompt

Paste this into Claude Code to install all skills non-interactively:

```
Run this shell command and confirm it succeeded:

  npx skills add ayusavin/skills --all -y

Then list installed skills with: npx skills list
```

To install a single skill:

```
Run this shell command and confirm it succeeded:

  npx skills add ayusavin/skills --skill design-process -a claude-code -y
```

## Structure

```
skills/
  <skill-name>/
    SKILL.md        # The skill itself
```

## Format

Each `SKILL.md` starts with a YAML front-matter block:

```yaml
---
name: Skill Name
description: One-sentence description.
when_to_use: When to apply this skill and when to skip it.
applies_to: Which AI environments / tools this skill targets.
language: en
---
```

Followed by the skill body in plain Markdown.
