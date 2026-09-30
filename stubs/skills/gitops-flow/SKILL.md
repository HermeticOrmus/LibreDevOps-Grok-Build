---
name: gitops-flow
description: "Stub cue, not installed. Review GitOps delivery flow for Grok Build repos. Full depth: the release-management plugin of LibreDevOps-Claude-Code."
---

# GitOps Flow

> Stub, not installed by the plugin. The real depth is the [`release-management`](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code/tree/main/plugins/release-management) plugin of LibreDevOps-Claude-Code, which this edition's marketplace installs: `grok plugin install release-management@libre-devops-grok`.

Desired state in git; cluster follows.

## Steps
1. Map source of truth (app repo vs env repo).
2. Check promotion path (PR → env).
3. Drift detection and sync policy.
4. Secrets not stored as plaintext in git.
5. Rollback via git revert / prior revision.
