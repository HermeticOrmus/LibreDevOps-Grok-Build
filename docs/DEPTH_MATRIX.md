# Depth matrix

Update this table when melting. Status words mean what they say:

| Status | Meaning |
|--------|---------|
| stub | Thin cue only. Usable as a reminder, not a playbook. |
| melted | Real Grok skill: when-to-use, steps, measurable checks, example, output shape. |

Never copy Claude plugin / agent / command totals into this inventory. Upstream [LibreDevOps-Claude-Code](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code) is proof that the *job* exists, not a count this repo has earned.

| ID | Kind | Status | Source (Claude, for melt) | Notes |
|----|------|--------|---------------------------|-------|
| ci-pipeline | skill | melted | plugins/github-actions | Stages, cache, OIDC, required checks. No secret values. |
| iac-review | skill | melted | plugins/terraform-patterns | Blast radius, state/lock, hardening remediations. No exploits. |
| release-checklist | skill | melted | plugins/release-management | Gates, rollback, hold window. Not a fake Argo playbook. |
| container-harden | skill | stub | plugins/docker-orchestration | Defensive image cue only. |
| observability-basics | skill | stub | plugins/monitoring-observability | SLI/log/trace cue only. |
| env-secrets-hygiene | skill | stub | plugins/secret-management | Smell cue only; never print values. |
| infra-cost-scan | skill | stub | plugins/cost-optimization | Cost-smell cue only. |
| gitops-flow | skill | stub | plugins/configuration-management | Desired-state cue only. |
| devops-orchestrator | agent | stub | suite coordinator | Coordinates the skills; not a melted specialist. |

This repo now: **3 melted skills**, **5 stub skills**, **1 stub agent**.

Dogfood copies of every skill live at `.grok/skills/<name>/SKILL.md` and must match their source: `plugins/libre-devops-grok/skills/<name>/SKILL.md` for melted skills, `stubs/skills/<name>/SKILL.md` for stubs. CI checks it.

## v1.0.0: where each row lives

Melted skills install as the `libre-devops-grok` plugin. Stubs stay in `stubs/` and never install; each names the pack plugin that holds the real depth. The 26 pack plugins install from the same marketplace, pinned to one commit of [LibreDevOps-Claude-Code](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code) (see `.grok-plugin/marketplace.json`). They are installed depth, not this repo's inventory.

| ID | Lives at | Installs | Real depth, installed by this marketplace |
|----|----------|----------|-------------------------------------------|
| ci-pipeline | `plugins/libre-devops-grok/skills/ci-pipeline/` | yes, in `libre-devops-grok` | this skill |
| iac-review | `plugins/libre-devops-grok/skills/iac-review/` | yes, in `libre-devops-grok` | this skill |
| release-checklist | `plugins/libre-devops-grok/skills/release-checklist/` | yes, in `libre-devops-grok` | this skill |
| container-harden | `stubs/skills/container-harden/` | no | `docker-orchestration` and `container-registry` |
| observability-basics | `stubs/skills/observability-basics/` | no | `monitoring-observability` |
| env-secrets-hygiene | `stubs/skills/env-secrets-hygiene/` | no | `secret-management` |
| infra-cost-scan | `stubs/skills/infra-cost-scan/` | no | `cost-optimization` |
| gitops-flow | `stubs/skills/gitops-flow/` | no | `release-management` |
| devops-orchestrator | `stubs/agents/devops-orchestrator.md` | no | a specialist agent in each pack plugin |

The `gitops-flow` row above names `release-management`, not the `configuration-management` source listed in the first table: the pack's GitOps depth (ArgoCD) lives in `release-management` ([LEDGER.md](../LEDGER.md)).

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Sibling Libre*-Grok-Build packs: [README suite footer](../README.md).
