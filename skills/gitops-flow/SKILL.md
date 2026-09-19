---
name: gitops-flow
description: Review GitOps delivery flow for Grok Build repos.
---

# GitOps Flow

Desired state in git; cluster follows.

## Steps
1. Map source of truth (app repo vs env repo).
2. Check promotion path (PR → env).
3. Drift detection and sync policy.
4. Secrets not stored as plaintext in git.
5. Rollback via git revert / prior revision.
