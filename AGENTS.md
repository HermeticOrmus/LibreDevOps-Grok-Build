# LibreDevOps-Grok-Build — suite agents

> Ported and melted for **Grok Build**. Not a dumb Claude clone.

**Doctrine hub:** [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md`  
**Gold filter:** Does this empower or extract? → [GOLD_HAT.md](./GOLD_HAT.md)

## How to use this suite

1. Install skills (see [QUICK_START.md](./QUICK_START.md)).
2. Keep Reality OS as the global doctrine layer.
3. Use suite skills for infra/CI work; use `AGENTS/devops-orchestrator.md` when a full multi-pillar pass is needed.
4. Pair with [LibreSecOps-Grok-Build](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build) for defensive security reviews.

Project-level `AGENTS.md` in a consumer repo wins for project rules; this file is suite guidance.

## Agents in this repo

| Agent | File | Role |
|-------|------|------|
| devops-orchestrator | `AGENTS/devops-orchestrator.md` | Coordinates CI, IaC, containers, observability, release into one pass (stub) |

## Liquid Gold

Recognize gold in LibreDevOps-Claude-Code → strip Claude residue → integrate with Grok skills / `.grok/` / MCP → dogfood.

Melted in this pack: `ci-pipeline`, `iac-review`, `release-checklist`. The other five skills and this orchestrator remain stubs. Honest counts: [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- This pack: [LibreDevOps-Grok-Build](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build)
- Sibling Libre*-Grok-Build packs: [Arch](https://github.com/HermeticOrmus/LibreArch-Grok-Build) · [Copy](https://github.com/HermeticOrmus/LibreCopy-Grok-Build) · [Embed](https://github.com/HermeticOrmus/LibreEmbed-Grok-Build) · [FinTech](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build) · [GameDev](https://github.com/HermeticOrmus/LibreGameDev-Grok-Build) · [GEO](https://github.com/HermeticOrmus/LibreGEO-Grok-Build) · [MLOps](https://github.com/HermeticOrmus/LibreMLOps-Grok-Build) · [MobileDev](https://github.com/HermeticOrmus/LibreMobileDev-Grok-Build) · [SecOps](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build) · [SessionFlow](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build) · [UIUX](https://github.com/HermeticOrmus/LibreUIUX-Grok-Build) · [WhatsApp](https://github.com/HermeticOrmus/LibreWhatsApp-Grok-Build)
- Skills collections: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof: [LibreDevOps-Claude-Code](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code)
- https://ormus.solutions
