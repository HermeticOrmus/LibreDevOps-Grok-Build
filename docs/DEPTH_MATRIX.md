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

Dogfood copies of every skill live at `.grok/skills/<name>/SKILL.md` and must match `skills/<name>/SKILL.md`.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Sibling Libre*-Grok-Build packs: [README suite footer](../README.md).
