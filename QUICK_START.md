# Quick Start — LibreDevOps for Grok Build

> From a clean machine to one pipeline or IaC critique in under 5 minutes.

Doctrine first: put [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine (global Grok doctrine). This pack does not replace it.

## Prerequisites

- Grok Build installed: `curl -fsSL https://x.ai/cli/install.sh | bash`, then `grok --version`. Plugin commands need no login.
- `git` (only for the dogfood and copy paths); `jq` for the install-everything loop
- A repo with CI, IaC, or a release you own, **or** this repo as the working tree

## Layout this file assumes

Verified against this repository (do not invent extra folders):

```
.grok-plugin/marketplace.json                     # the marketplace: libre-devops-grok, then the pack's plugins by pinned commit
plugins/libre-devops-grok/.grok-plugin/plugin.json
plugins/libre-devops-grok/skills/<name>/SKILL.md  # the melted skills (canonical)
stubs/skills/<name>/SKILL.md                      # stub cues; not installed
stubs/agents/devops-orchestrator.md               # stub coordinator; not installed
docs/DEPTH_MATRIX.md
docs/MELT_RULES.md
.grok/skills/<name>/SKILL.md                      # dogfood copy; must match its source above
.grok/plugins/libredevops-core/                   # v0 bundle stub; dogfood copy of the stub orchestrator
```

Melted (usable now): `plugins/libre-devops-grok/skills/ci-pipeline/SKILL.md`, `plugins/libre-devops-grok/skills/iac-review/SKILL.md`, `plugins/libre-devops-grok/skills/release-checklist/SKILL.md`.
Still stubs, in `stubs/`: `container-harden`, `observability-basics`, `env-secrets-hygiene`, `infra-cost-scan`, `gitops-flow`, plus the orchestrator. Each stub names the pack plugin with the real depth. Honest table: [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

## Install (pick one)

### A. Marketplace (recommended)

One marketplace brings the Grok-native plugin and every LibreDevOps-Claude-Code plugin, each pinned to a commit:

```bash
grok plugin marketplace add HermeticOrmus/LibreDevOps-Grok-Build
grok plugin install libre-devops-grok@libre-devops-grok
grok plugin install terraform-patterns@libre-devops-grok
```

Every entry at once (needs `jq`):

```bash
for p in $(curl -fsSL https://raw.githubusercontent.com/HermeticOrmus/LibreDevOps-Grok-Build/main/.grok-plugin/marketplace.json | jq -r '.plugins[].name'); do
  grok plugin install "$p@libre-devops-grok"
done
```

Confirm what landed:

```bash
grok plugin list
grok plugin details libre-devops-grok
```

You should see `libre-devops-grok` (three skills: `ci-pipeline`, `iac-review`, `release-checklist`) plus the pack plugins you installed. The optional `libre-devops-hooks` plugin installs its hooks, but whether they fire inside a Grok session is unverified ([LEDGER.md](./LEDGER.md)).

Only the Grok-native plugin, without the marketplace:

```bash
grok plugin install HermeticOrmus/LibreDevOps-Grok-Build#plugins/libre-devops-grok
```

Do not install the repo root itself (`grok plugin install HermeticOrmus/LibreDevOps-Grok-Build`): since v1.0.0 the root holds no skills, so Grok installs an empty plugin.

### B. Dogfood this repo

```bash
git clone https://github.com/HermeticOrmus/LibreDevOps-Grok-Build.git
cd LibreDevOps-Grok-Build
# Dogfood copies of the melted skills and the stubs are at .grok/skills/; open this folder in Grok Build.
```

### C. Install into your project (copy, no plugin manager)

```bash
git clone https://github.com/HermeticOrmus/LibreDevOps-Grok-Build.git ~/LibreDevOps-Grok-Build
cd /path/to/your-project
mkdir -p .grok/skills
cp -R ~/LibreDevOps-Grok-Build/plugins/libre-devops-grok/skills/* .grok/skills/
```

Confirm the copy landed:

```bash
test -f .grok/skills/ci-pipeline/SKILL.md
test -f .grok/skills/iac-review/SKILL.md
test -f .grok/skills/release-checklist/SKILL.md
ls .grok/skills
```

You should see three skill directories, matching `plugins/libre-devops-grok/skills/` in this repo. The stubs are not copied: they are cues, not skills.

### D. User-global copy

```bash
git clone https://github.com/HermeticOrmus/LibreDevOps-Grok-Build.git ~/LibreDevOps-Grok-Build
mkdir -p ~/.grok/skills
cp -R ~/LibreDevOps-Grok-Build/plugins/libre-devops-grok/skills/* ~/.grok/skills/
```

Same three `test -f` checks as C, under `~/.grok/skills/`.

### Optional project rules (merge, do not replace)

Copy `stubs/agents/devops-orchestrator.md` only when you want a multi-pillar pass. It is still a stub coordinator, and no install path ships it. Do not overwrite Reality OS doctrine.

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

- [ ] `grok plugin list` shows `libre-devops-grok` (or the three skill files exist at the copy path you chose)
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
