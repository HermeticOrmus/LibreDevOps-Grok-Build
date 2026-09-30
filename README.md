<p align="center">
  <img src="https://ormus.solutions/mascot/pixellab_liquid_to_branch.gif" alt="LibreDevOps Grok Build" width="128" style="image-rendering: pixelated;" />
</p>

<h1 align="center">LibreDevOps Grok Build</h1>

<p align="center">
  <em>DevOps review in your Grok Build session: CI, IaC and release skills melted for Grok, plus the LibreDevOps pack by pinned commit</em>
</p>

<p align="center">
  <a href="https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/stargazers"><img src="https://img.shields.io/github/stars/HermeticOrmus/LibreDevOps-Grok-Build?style=flat-square&color=aa8142" alt="Stars" /></a>
  <a href="https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/blob/main/LICENSE"><img src="https://img.shields.io/github/license/HermeticOrmus/LibreDevOps-Grok-Build?style=flat-square&color=aa8142" alt="License" /></a>
  <a href="https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/commits"><img src="https://img.shields.io/github/last-commit/HermeticOrmus/LibreDevOps-Grok-Build?style=flat-square&color=aa8142" alt="Last Commit" /></a>
  <img src="https://img.shields.io/badge/DevOps-aa8142?style=flat-square&logo=kubernetes&logoColor=white" alt="DevOps" />
  <img src="https://img.shields.io/badge/Grok_Build-aa8142?style=flat-square&logo=x&logoColor=white" alt="Grok Build" />
</p>

---

**DevOps / IaC / CI depth for [Grok Build](https://github.com/HermeticOrmus/grok-build-reality-os)** — ported and melted from [LibreDevOps-Claude-Code](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code), not a dumb copy.

> Status: **v1.0.0**. The three melted skills (`ci-pipeline`, `iac-review`, `release-checklist`) install as the `libre-devops-grok` plugin, and all 26 LibreDevOps-Claude-Code plugins install beside them from the same marketplace, pinned by commit. The five stubs stay in `stubs/` and do not install. See [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md) and the [kintsugi ledger](./LEDGER.md).

## Why this exists

Shipping needs pipelines, IaC, containers, and observability — dogfooded. LibreDevOps owns that depth for Claude Code. Grok Build needs the same *job* with Grok-native skills, agents, `.grok/`, and truth-seeking voice. This repo counts only what it has melted.

## Install (<5 min)

See [QUICK_START.md](./QUICK_START.md) for the marketplace, dogfood, and copy paths.

```bash
grok plugin marketplace add HermeticOrmus/LibreDevOps-Grok-Build
grok plugin install libre-devops-grok@libre-devops-grok
# Any pack plugin, pinned by commit, for example:
grok plugin install terraform-patterns@libre-devops-grok
grok plugin list
```

[QUICK_START.md](./QUICK_START.md) has a loop that installs every entry.

The pack's optional `libre-devops-hooks` plugin installs too; whether its hooks fire inside a Grok session is unverified ([LEDGER.md](./LEDGER.md)).

Doctrine: install [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine first. Do not replace that doctrine with this pack.

## Depth (honest)

| Artifact | This repo now | Installed from the pack |
|----------|---------------|-------------------------|
| Skills | 3 melted, in the `libre-devops-grok` plugin; 5 stubs in `stubs/skills/`, not installed | The skills inside the 26 pack plugins |
| Agents | 1 stub (`devops-orchestrator`) in `stubs/agents/`, not installed | A specialist agent in each pack plugin except the hooks plugin |
| Plugins | 1 (`libre-devops-grok`, v1.0.0) | 26 of 26, pinned by commit in `.grok-plugin/marketplace.json`, including the optional `libre-devops-hooks` |

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

The melted skills install as the `libre-devops-grok` plugin. The stubs live in `stubs/skills/` and do not install; each one names the pack plugin that holds the real depth, and [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md) maps them all.

Agent: `stubs/agents/devops-orchestrator.md`, the stub coordinator for a full DevOps pass. It does not install.

## Layout (Grok Build)

```
.grok-plugin/marketplace.json    # marketplace: the Grok-native plugin, then the pack's plugins by pinned commit
plugins/libre-devops-grok/       # the Grok-native plugin (manifest in .grok-plugin/plugin.json)
  skills/                        # the melted SKILL.md bodies (canonical)
stubs/skills/                    # stub cues; not installed; each names the pack plugin with the depth
stubs/agents/                    # the stub orchestrator; not installed
scripts/pin-pack.sh              # re-pins the pack entries to the pack's main HEAD
docs/                            # DEPTH_MATRIX, MELT_RULES
LEDGER.md                        # kintsugi ledger: the cracks and their seals
.grok/skills/                    # dogfood copy of the plugin skills and the stubs (CI keeps it in sync)
.grok/plugins/libredevops-core/  # v0 bundle stub, kept as the dogfood copy of the stub orchestrator
```

Claude's `.claude/` maps to Grok skills + `AGENTS.md` + `.grok/`. Melt rules: [docs/MELT_RULES.md](./docs/MELT_RULES.md).

## Gold Hat

[GOLD_HAT.md](./GOLD_HAT.md) — empower or extract? Canonical: [gold-hat-manifesto](https://github.com/HermeticOrmus/gold-hat-manifesto).

Never embed secrets in skills, templates, or examples. Hardening only — no exploit recipes.

## Security

[SECURITY.md](./SECURITY.md) — how to report vulnerabilities. Do not file public issues with exploit details.

## Contributing

[CONTRIBUTING.md](./CONTRIBUTING.md) describes *this* repo: melt, don't clone; honest `stub` / `melted` status; keep the plugin skills, the stubs and their `.grok/skills/` copies identical (CI checks it).

## Depth / quality

Public Grok Build repos in this suite use a shared ladder: **L0–L5**. Definitions live in [grok-build-reality-os `docs/QUALITY_LADDER.md`](https://github.com/HermeticOrmus/grok-build-reality-os/blob/main/docs/QUALITY_LADDER.md).

This pack at v1.0.0: three usable skills in an installable plugin, five stubs that do not install, one stub agent, and the full pack by pinned commit. This pass targets **L3–L4 hygiene** (SECURITY linked, contributing matches the tree, suite map complete, inventory honest, no inflated claims). It does not claim L5.

## Kintsugi ledger

[LEDGER.md](./LEDGER.md) lists every crack found in the v0 edition, the evidence, and the seal this release put on it. Open cracks stay open in plain sight until someone seals them.

## Feedback

Tell us what worked and what is missing: [feedback form](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/issues/new?template=feedback.yml). Grok picked the wrong skill? [Report a routing miss](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/issues/new?template=routing-miss.yml). Want a new skill or plugin? [Propose it](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/issues/new?template=plugin-proposal.yml). Ways to contribute: [CONTRIBUTING.md](./CONTRIBUTING.md).

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- This pack: [LibreDevOps-Grok-Build](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build)
- Sibling Libre*-Grok-Build packs: [Arch](https://github.com/HermeticOrmus/LibreArch-Grok-Build) · [Copy](https://github.com/HermeticOrmus/LibreCopy-Grok-Build) · [Embed](https://github.com/HermeticOrmus/LibreEmbed-Grok-Build) · [FinTech](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build) · [GameDev](https://github.com/HermeticOrmus/LibreGameDev-Grok-Build) · [GEO](https://github.com/HermeticOrmus/LibreGEO-Grok-Build) · [MLOps](https://github.com/HermeticOrmus/LibreMLOps-Grok-Build) · [MobileDev](https://github.com/HermeticOrmus/LibreMobileDev-Grok-Build) · [SecOps](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build) · [SessionFlow](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build) · [UIUX](https://github.com/HermeticOrmus/LibreUIUX-Grok-Build) · [WhatsApp](https://github.com/HermeticOrmus/LibreWhatsApp-Grok-Build)
- Skills collections: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof: [LibreDevOps-Claude-Code](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code)
- https://ormus.solutions

## License

MIT — see [LICENSE](./LICENSE).
