---
name: iac-review
description: Review Infrastructure-as-Code for safety, clarity, and blast radius on Grok Build. Hardening-focused.
---

# IaC Review

Review IaC without expanding attack surface guidance into exploits.

## Steps
1. Identify tool (Terraform, Pulumi, CFN, etc.) and scope.
2. Map resources and blast radius (what can this destroy?).
3. Check state backend, locking, and secrets handling (no values printed).
4. Flag open security groups / public buckets as misconfigs to fix.
5. Propose concrete remediations ranked by severity.
