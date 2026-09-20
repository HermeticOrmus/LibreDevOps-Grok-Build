# Contributing

## Melt, don't clone

Ports from LibreDevOps-Claude-Code must follow Liquid Gold:

1. Keep model-agnostic DevOps / IaC / CI knowledge.
2. Strip Claude-only paths, `model:` pins, Anthropic install residue, slash-command theater.
3. Ship as Grok `SKILL.md` / agents under `.grok/` conventions.
4. Teach while helping (Gold Hat).

## Skill format

```
skills/<name>/SKILL.md
```

YAML frontmatter: `name`, `description`. Body: when to use, steps, measurable checks, worked example, output shape.

## PR bar

- Honest depth: only count what you melt. Status is `stub` or `melted` in [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).
- No "Grok killer" language. No Claude plugin/agent/command totals as this repo's inventory.
- Suite footer on README / QUICK_START / AGENTS.md: Reality OS + sibling Libre*-Grok-Build packs.
- Canonical skill body is `skills/<name>/SKILL.md`. Keep `.grok/skills/<name>/SKILL.md` identical.
- No secrets in skills, templates, or examples. Never print secret values.
- Hardening and review only. No exploit steps, payloads, or attack scripts.

## This repo

This is a documentation-and-prompt suite (skills + one stub orchestrator). There is no application runtime. A useful PR either melts a stub into a real playbook or fixes install/honesty docs so a stranger can run the first teach cue in [QUICK_START.md](./QUICK_START.md).
