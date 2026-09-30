---
name: env-secrets-hygiene
description: "Stub cue, not installed. Env and secrets hygiene for Grok Build. Never print secret values. Full depth: the secret-management plugin of LibreDevOps-Claude-Code."
---

# Env / Secrets Hygiene

> Stub, not installed by the plugin. The real depth is the [`secret-management`](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code/tree/main/plugins/secret-management) plugin of LibreDevOps-Claude-Code, which this edition's marketplace installs: `grok plugin install secret-management@libre-devops-grok`.

Find smells; never echo secret values.

## Steps
1. Locate .env examples vs real secrets (examples only in git).
2. Prefer secret managers / OIDC over long-lived keys.
3. Flag secrets in CI logs, Dockerfiles, or commits.
4. Rotate guidance when exposure is suspected — no credential dumping.
5. Document required env vars without values.
