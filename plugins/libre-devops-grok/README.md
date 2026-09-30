# libre-devops-grok

The Grok-native layer of [LibreDevOps-Grok-Build](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build): three skills melted for Grok Build.

| Skill | Job |
|-------|-----|
| `ci-pipeline` | CI hygiene: stages, cache, fail-fast, secrets, merge gates |
| `iac-review` | IaC blast radius, state, hardening remediations |
| `release-checklist` | Ship gates, rollback, hold window |

## Install

```bash
grok plugin marketplace add HermeticOrmus/LibreDevOps-Grok-Build
grok plugin install libre-devops-grok@LibreDevOps-Grok-Build
```

The same marketplace offers every LibreDevOps-Claude-Code plugin, pinned by commit.

The stubs (`container-harden`, `observability-basics`, `env-secrets-hygiene`, `infra-cost-scan`, `gitops-flow`) and the stub orchestrator are not part of this plugin. They live in [`stubs/`](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/tree/main/stubs), and each names the pack plugin with the real depth. Honest table: [docs/DEPTH_MATRIX.md](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/blob/main/docs/DEPTH_MATRIX.md).

Gold Hat: [GOLD_HAT.md](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/blob/main/GOLD_HAT.md)
