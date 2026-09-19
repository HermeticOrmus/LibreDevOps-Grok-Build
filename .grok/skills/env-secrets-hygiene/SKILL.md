---
name: env-secrets-hygiene
description: Env and secrets hygiene for Grok Build. Never print secret values.
---

# Env / Secrets Hygiene

Find smells; never echo secret values.

## Steps
1. Locate .env examples vs real secrets (examples only in git).
2. Prefer secret managers / OIDC over long-lived keys.
3. Flag secrets in CI logs, Dockerfiles, or commits.
4. Rotate guidance when exposure is suspected — no credential dumping.
5. Document required env vars without values.
