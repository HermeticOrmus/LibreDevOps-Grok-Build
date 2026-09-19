# Quick Start — LibreDevOps for Grok Build

> From zero to a pipeline critique in under 5 minutes.

## Prerequisites

- Grok Build installed and working
- A repo with CI, IaC, or containers

## Install skills (repo-local)

```bash
git clone https://github.com/HermeticOrmus/LibreDevOps-Grok-Build.git
cd your-project
mkdir -p .grok/skills
cp -R /path/to/LibreDevOps-Grok-Build/skills/* .grok/skills/
```

Or user-global:

```bash
mkdir -p ~/.grok/skills
cp -R /path/to/LibreDevOps-Grok-Build/skills/* ~/.grok/skills/
```

## First-run teach cue

1. **CI** — "Run ci-pipeline on our GitHub Actions / CI config: stages, caching, fail-fast."
2. **IaC** — "Run iac-review on this Terraform/module for blast radius and state hygiene."
3. **Secrets** — "Run env-secrets-hygiene: find secret smells without printing values."

## Smoke checklist

- [ ] Skills visible to Grok
- [ ] One CI or IaC critique with measurable notes
- [ ] No secrets pasted into chat or skills
