---
name: container-harden
description: Harden Docker/OCI images defensively for Grok Build. No exploit recipes.
---

# Container Harden

Defensive image baseline.

## Steps
1. Prefer minimal/distroless bases; pin digests when possible.
2. Non-root user; drop unnecessary capabilities.
3. Multi-stage builds; no secrets in layers.
4. Scan for known CVEs; track update cadence.
5. Document run-as and healthcheck expectations.
