---
name: ci-pipeline
description: Design or critique CI pipelines for Grok Build projects.
---

# CI Pipeline

Make CI fast, clear, and fail-useful.

## Steps
1. Map stages: lint → test → build → deploy gates.
2. Check caching, parallelism, and flake risk.
3. Ensure secrets via vault/OIDC — never in logs.
4. Require status checks before merge where appropriate.
5. List top 5 improvements with effort estimate.
