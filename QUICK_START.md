# Quick Start — LibreDevOps for Grok Build

> From a clean machine to one pipeline or IaC critique in under 5 minutes.

Doctrine first: put [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine (global Grok doctrine). This pack does not replace it.

## Prerequisites

- `git`
- Grok Build installed and able to see skills under `.grok/skills/` or `~/.grok/skills/`
- A repo with CI, IaC, or a release you own, **or** this repo as the working tree

## Layout this file assumes

Verified against this repository (do not invent extra folders):

```
skills/<name>/SKILL.md          # canonical skill bodies (copy these)
AGENTS/devops-orchestrator.md
docs/DEPTH_MATRIX.md
docs/MELT_RULES.md
.grok/skills/<name>/SKILL.md    # dogfood copy; must match skills/
.grok/plugins/libredevops-core/ # plugin stub; not required for first run
```

Melted (usable now): `skills/ci-pipeline/SKILL.md`, `skills/iac-review/SKILL.md`, `skills/release-checklist/SKILL.md`.
Still stubs: the other five skills + the orchestrator. Honest table: [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

## Install (pick one)

### A. Dogfood this repo (fastest)

```bash
git clone https://github.com/HermeticOrmus/LibreDevOps-Grok-Build.git
cd LibreDevOps-Grok-Build
# Skills are already at .grok/skills/ — open this folder in Grok Build.
```

### B. Install into your project

```bash
git clone https://github.com/HermeticOrmus/LibreDevOps-Grok-Build.git ~/LibreDevOps-Grok-Build
cd /path/to/your-project
mkdir -p .grok/skills
cp -R ~/LibreDevOps-Grok-Build/skills/* .grok/skills/
```

Confirm the copy landed:

```bash
test -f .grok/skills/ci-pipeline/SKILL.md
test -f .grok/skills/iac-review/SKILL.md
test -f .grok/skills/release-checklist/SKILL.md
ls .grok/skills
```

You should see eight skill directories, matching `skills/` in this repo.

### C. User-global

```bash
git clone https://github.com/HermeticOrmus/LibreDevOps-Grok-Build.git ~/LibreDevOps-Grok-Build
mkdir -p ~/.grok/skills
cp -R ~/LibreDevOps-Grok-Build/skills/* ~/.grok/skills/
```

Same three `test -f` checks as B, under `~/.grok/skills/`.

### Optional project rules (merge, do not replace)

Copy `AGENTS/devops-orchestrator.md` only when you want a multi-pillar pass. It is still a stub coordinator. Do not overwrite Reality OS doctrine.

## First-run teach cue

In Grok Build, on a real pipeline, module, or release you own:

1. **CI** — "Run ci-pipeline on our GitHub Actions / CI config: stages, caching, fail-fast. Do not print secret values."
2. **IaC** — "Run iac-review on this Terraform/module for blast radius and state hygiene."
3. **Ship** — "Run release-checklist on the next tag: notes, candidate SHA, rollback, on-call."

You used melted LibreDevOps depth on Grok — not a Claude paste, not a fake plugin count.

## Hard rules

- Never embed or echo real secrets.
- Hardening and review only. No exploit steps, payloads, or attack scripts.
- Pair with [LibreSecOps-Grok-Build](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build) for a dedicated defensive pass.

## Smoke checklist

- [ ] `ci-pipeline`, `iac-review`, and `release-checklist` files exist at the install path you chose
- [ ] Grok can see those three skills
- [ ] One CI or IaC critique with severity-ranked findings (or one release gate walk)
- [ ] No secrets in prompts, examples, or output

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- This pack: [LibreDevOps-Grok-Build](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build)
- Sibling Libre*-Grok-Build packs: [Arch](https://github.com/HermeticOrmus/LibreArch-Grok-Build) · [Copy](https://github.com/HermeticOrmus/LibreCopy-Grok-Build) · [Embed](https://github.com/HermeticOrmus/LibreEmbed-Grok-Build) · [FinTech](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build) · [GameDev](https://github.com/HermeticOrmus/LibreGameDev-Grok-Build) · [GEO](https://github.com/HermeticOrmus/LibreGEO-Grok-Build) · [MLOps](https://github.com/HermeticOrmus/LibreMLOps-Grok-Build) · [MobileDev](https://github.com/HermeticOrmus/LibreMobileDev-Grok-Build) · [SecOps](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build) · [SessionFlow](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build) · [UIUX](https://github.com/HermeticOrmus/LibreUIUX-Grok-Build) · [WhatsApp](https://github.com/HermeticOrmus/LibreWhatsApp-Grok-Build)
- Skills collections: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof (upstream, not this inventory): [LibreDevOps-Claude-Code](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code)
- https://ormus.solutions
