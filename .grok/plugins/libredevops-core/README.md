# libredevops-core (v0 plugin stub, kept as a dogfood copy)

This was the v0 plugin bundle. It had no manifest and no skills, so it bundled nothing: Grok saw it only as a project plugin with one agent, the stub orchestrator. It stays as the dogfood copy of `stubs/agents/devops-orchestrator.md` (the two files must match; CI checks it).

The installable plugin is now [`plugins/libre-devops-grok/`](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/tree/main/plugins/libre-devops-grok), with its own manifest. Install it with `grok plugin marketplace add HermeticOrmus/LibreDevOps-Grok-Build` and `grok plugin install libre-devops-grok@LibreDevOps-Grok-Build`.

The melted skills now live in that plugin's `skills/`; the stubs live in `stubs/skills/`. Dogfood copies of both: `.grok/skills/`.

Melted now: `ci-pipeline`, `iac-review`, `release-checklist`. The rest of the pack is still stubs. See [docs/DEPTH_MATRIX.md](../../../docs/DEPTH_MATRIX.md).
