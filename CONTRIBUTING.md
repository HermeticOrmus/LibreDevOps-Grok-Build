# Contributing

## Ways to contribute

- **Seal a crack.** [LEDGER.md](./LEDGER.md) lists the open cracks with their evidence. Pick one, write the seal (a check that fails first, then the fix, then the doc line that now tells the truth), and open a pull request that names the crack ID.
- **Melt a pack skill into a Grok-native one.** The stubs in `stubs/skills/` each name the LibreDevOps-Claude-Code plugin that holds the depth. Melt one into a real Grok skill under `plugins/libre-devops-grok/skills/` by the rules below.
- **Report a routing miss.** When Grok picks the wrong skill, or none, the description is what needs fixing: [routing miss form](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/issues/new?template=routing-miss.yml).
- **Propose a plugin.** A job people do in DevOps that nothing here covers: [plugin proposal form](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/issues/new?template=plugin-proposal.yml). General feedback goes in the [feedback form](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/issues/new?template=feedback.yml).

## Melt, don't clone

Ports from LibreDevOps-Claude-Code must follow Liquid Gold:

1. Keep model-agnostic DevOps / IaC / CI knowledge.
2. Strip Claude-only paths, `model:` pins, Anthropic install residue, slash-command theater.
3. Ship as Grok `SKILL.md` in the `plugins/libre-devops-grok/` plugin (Grok reads `.grok-plugin/plugin.json`).
4. Teach while helping (Gold Hat).

## Skill format

```
plugins/libre-devops-grok/skills/<name>/SKILL.md   # melted skills (installed)
stubs/skills/<name>/SKILL.md                       # stub cues (not installed)
```

YAML frontmatter: `name`, `description` (quote it if it contains `: `). The description is the routing line: say what the skill does and when to use it. Body: when to use, steps, measurable checks, worked example, output shape.

When a stub melts: `git mv stubs/skills/<name> plugins/libre-devops-grok/skills/<name>`, remove its "Stub, not installed" line and the "Stub cue" prefix, and update [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

The pack entries in `.grok-plugin/marketplace.json` are generated. Run `scripts/pin-pack.sh` to move them to the pack's current commit; do not edit them by hand.

## PR bar

- Honest depth: only count what you melt. Status is `stub` or `melted` in [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).
- No "Grok killer" language. No Claude plugin/agent/command totals as this repo's inventory.
- Suite footer on README / QUICK_START / AGENTS.md: Reality OS + sibling Libre*-Grok-Build packs.
- Canonical skill bodies are `plugins/libre-devops-grok/skills/<name>/SKILL.md` (melted) and `stubs/skills/<name>/SKILL.md` (stubs). Keep `.grok/skills/<name>/SKILL.md` identical; CI checks it. Links that leave a skill's folder are absolute GitHub URLs, so they still work after install.
- No secrets in skills, templates, or examples. Never print secret values.
- Hardening and review only. No exploit steps, payloads, or attack scripts.

## This repo

This is a documentation-and-prompt suite (skills + one stub orchestrator). There is no application runtime. A useful PR either melts a stub into a real playbook or fixes install/honesty docs so a stranger can run the first teach cue in [QUICK_START.md](./QUICK_START.md).
