# LibreDevOps-Grok-Build

**DevOps / IaC / CI depth for [Grok Build](https://github.com/HermeticOrmus/grok-build-reality-os)** — ported and melted from [LibreDevOps-Claude-Code](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code), not a dumb copy.

> Status: **public v0** — three skills melted (`ci-pipeline`, `iac-review`, `release-checklist`); the rest are honest stubs. See [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

## Why this exists

Shipping needs pipelines, IaC, containers, and observability — dogfooded. LibreDevOps owns that depth for Claude Code. Grok Build needs the same *job* with Grok-native skills, agents, `.grok/`, and truth-seeking voice. This repo counts only what it has melted.

## Install (<5 min)

See [QUICK_START.md](./QUICK_START.md) for clone, dogfood, project-local, and user-global paths.

```bash
git clone https://github.com/HermeticOrmus/LibreDevOps-Grok-Build.git
cd LibreDevOps-Grok-Build
# Dogfood: .grok/skills/ already has the skill bodies.
# Other project: cp -R skills/* /path/to/your-project/.grok/skills/
```

Doctrine: install [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine first. Do not replace that doctrine with this pack.

## Depth (honest)

| Artifact | This repo now | Upstream Claude |
|----------|---------------|-----------------|
| Skills | 3 melted + 5 stubs | Proof the job exists; not our inventory |
| Agents | 1 stub (`devops-orchestrator`) | Proof the job exists; not our inventory |
| Plugins | 1 core bundle stub | Proof the job exists; not our inventory |

Do not paste Claude plugin/agent/command totals here. Update [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md) when something melts.

## Skills

| Skill | Status | Job |
|-------|--------|-----|
| ci-pipeline | melted | CI hygiene: stages, cache, fail-fast, secrets, merge gates |
| iac-review | melted | IaC blast radius, state, hardening remediations |
| release-checklist | melted | Ship gates, rollback, hold window |
| container-harden | stub | Defensive image baseline |
| observability-basics | stub | Logs, metrics, traces |
| env-secrets-hygiene | stub | Env/secrets smells (no values printed) |
| infra-cost-scan | stub | Cost smell check |
| gitops-flow | stub | GitOps / desired-state flow |

Agent: `AGENTS/devops-orchestrator.md` — stub coordinator for a full DevOps pass.

## Layout (Grok Build)

```
skills/                 # canonical SKILL.md bodies
AGENTS/                 # suite agents
docs/                   # DEPTH_MATRIX, MELT_RULES
.grok/skills/           # dogfood copy of skills/ (keep in sync)
.grok/plugins/          # optional plugin bundle stub
```

Claude's `.claude/` maps to Grok skills + `AGENTS.md` + `.grok/`. Melt rules: [docs/MELT_RULES.md](./docs/MELT_RULES.md).

## Gold Hat

[GOLD_HAT.md](./GOLD_HAT.md) — empower or extract? Canonical: [gold-hat-manifesto](https://github.com/HermeticOrmus/gold-hat-manifesto).

Never embed secrets in skills, templates, or examples. Hardening only — no exploit recipes.

## Security

[SECURITY.md](./SECURITY.md) — how to report vulnerabilities. Do not file public issues with exploit details.

## Contributing

[CONTRIBUTING.md](./CONTRIBUTING.md) describes *this* repo: melt, don't clone; honest `stub` / `melted` status; keep `skills/` and `.grok/skills/` identical.

## Depth / quality

Public Grok Build repos in this suite use a shared ladder: **L0–L5**. Definitions live in [grok-build-reality-os `docs/QUALITY_LADDER.md`](https://github.com/HermeticOrmus/grok-build-reality-os/blob/main/docs/QUALITY_LADDER.md).

This pack is a v0 melt: three usable skills, five stubs, one stub agent. This pass targets **L3–L4 hygiene** (SECURITY linked, contributing matches the tree, suite map complete, inventory honest, no inflated claims). It does not claim L5.

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- This pack: [LibreDevOps-Grok-Build](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build)
- Sibling Libre*-Grok-Build packs: [Arch](https://github.com/HermeticOrmus/LibreArch-Grok-Build) · [Copy](https://github.com/HermeticOrmus/LibreCopy-Grok-Build) · [Embed](https://github.com/HermeticOrmus/LibreEmbed-Grok-Build) · [FinTech](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build) · [GameDev](https://github.com/HermeticOrmus/LibreGameDev-Grok-Build) · [GEO](https://github.com/HermeticOrmus/LibreGEO-Grok-Build) · [MLOps](https://github.com/HermeticOrmus/LibreMLOps-Grok-Build) · [MobileDev](https://github.com/HermeticOrmus/LibreMobileDev-Grok-Build) · [SecOps](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build) · [SessionFlow](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build) · [UIUX](https://github.com/HermeticOrmus/LibreUIUX-Grok-Build) · [WhatsApp](https://github.com/HermeticOrmus/LibreWhatsApp-Grok-Build)
- Skills collections: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof: [LibreDevOps-Claude-Code](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code)
- https://ormus.solutions

## License

MIT — see [LICENSE](./LICENSE).
