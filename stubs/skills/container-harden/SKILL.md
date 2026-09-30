---
name: container-harden
description: "Stub cue, not installed. Harden Docker/OCI images defensively for Grok Build. No exploit recipes. Full depth: the docker-orchestration and container-registry plugins of LibreDevOps-Claude-Code."
---

# Container Harden

> Stub, not installed by the plugin. The real depth is in the [`docker-orchestration`](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code/tree/main/plugins/docker-orchestration) and [`container-registry`](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code/tree/main/plugins/container-registry) plugins of LibreDevOps-Claude-Code, which this edition's marketplace installs: `grok plugin install docker-orchestration@libre-devops-grok`, `grok plugin install container-registry@libre-devops-grok`.

Defensive image baseline.

## Steps
1. Prefer minimal/distroless bases; pin digests when possible.
2. Non-root user; drop unnecessary capabilities.
3. Multi-stage builds; no secrets in layers.
4. Scan for known CVEs; track update cadence.
5. Document run-as and healthcheck expectations.
