---
name: iac-review
description: Review Infrastructure-as-Code for safety, clarity, and blast radius on Grok Build. Hardening-focused. Use when reviewing Terraform, Pulumi, CloudFormation, or similar.
---

# IaC Review

Review IaC without expanding attack-surface guidance into exploits. The question is "what can this change destroy, expose, or lock us out of?" — not how to break in.

Gold Hat: name the stack and the environment first, then teach blast radius while you remediate. Leave the person able to read the next module without you. Never print secret values. Never invent exploit steps.

## When to use

- Reviewing Terraform, Pulumi, CloudFormation, Bicep, or similar
- A module is about to touch prod state, networks, data stores, or IAM
- State backend, locking, or secret handling looks sloppy
- Someone asked "is this safe to apply?"

Do not use this skill as a FinOps pass (`infra-cost-scan`, stub) or a container baseline (`container-harden`, stub). Pipeline apply/plan split belongs with `ci-pipeline` (melted). Promotion via desired state in git is `gitops-flow` (stub). Credential smells beyond IaC files go to `env-secrets-hygiene` (stub). Call the stub; do not invent its depth.

Pair with LibreSecOps for a dedicated defensive review. Flag misconfigurations to *fix*. Do not provide payloads, exploit PoCs, or attack procedures.

## Operating steps

1. **Identify tool and scope.** Terraform / Pulumi / CFN / other; which stack; which env (dev vs prod). If unknown, say so.
2. **Map resources and blast radius.** What can this apply create, mutate, or destroy? Data, identity, network, state.
3. **Walk the checks below.** File + resource + current behavior. No guessed account IDs or secret values.
4. **Rank remediations** by severity (Critical → low). Cap the first patch list at what one sitting can ship.
5. **Teach one sentence.** Why this change, reusable on the next module.

Stop if you cannot name the environment. Applying a "probably staging" plan to prod is extraction.

## Review checks (measurable)

### Blast radius

| Check | Pass | Fail |
|-------|------|------|
| Scope | One env, one state; destroy limited to that stack | Prod and staging share state or a workspace name |
| Destroy guards | `prevent_destroy` (or equivalent) on data stores, state buckets, KMS/keys | Databases and state can be destroyed by a default apply |
| Targeting | Apply is the planned set; no casual `-target` as process | "Just target the instance" is the documented workflow |
| IAM / identity | Roles are job-shaped and env-scoped | Wildcard actions or a shared admin role across envs |

Write blast radius as nouns: "this apply can delete the prod relational store and the state bucket." Not adjectives.

### State, locking, backends

| Check | Pass | Fail |
|-------|------|------|
| Remote state | Remote backend; local state is not the team path | State file in the repo or on a laptop as source of truth |
| Locking | Exclusive lock (DynamoDB, native lock, or equivalent) | Two applies can race |
| Versioning | Backend store keeps versions; state is not "the backup" | No versioning; a bad apply has no prior state |
| Separation | One state per environment | Prod refresh reads staging state |

Never edit state by hand. Use the tool's move/import/rm. Never paste state file contents into chat.

### Secrets in code (never print values)

| Check | Pass | Fail |
|-------|------|------|
| Values | Variables marked sensitive; examples are placeholders | Real tokens, keys, or connection strings in `.tf`, `.tfvars`, or examples |
| Injection | Secret manager / OIDC data source | A real token or password sitting in a `default` or a comment |
| Outputs | Sensitive outputs marked; logs do not dump them | Plan/apply logs print the secret |

Name the *kind* of secret. If a value appears in the tree, say "credential-shaped string at `path`" and stop. Hand rotation to `env-secrets-hygiene` (stub).

### Common misconfigs to fix (hardening)

These are defects to close, not recipes to open:

- Storage advertised as public when the job does not require a public read
- Ingress `0.0.0.0/0` on data or management ports
- Encryption at rest or in transit left off on stores that hold user data
- Unrestricted egress from a workload that only needs a few destinations

Say what to tighten (private ACL, scoped CIDR, encryption flag). Do not describe how to abuse the open setting.

## Problem → rule → fix

| Complaint | Rule | First fix |
|-----------|------|-----------|
| "What happens if I apply?" | Blast radius | List destroyable data/identity/network; add destroy guards |
| "Two people applied at once" | Locking | Remote state + lock; stop using local state |
| "The plan printed a password" | Sensitive + no values in git | Mark sensitive; move to a secret manager; rotate |
| "The bucket is on the internet" | Least exposure | Make it private unless the job is public hosting; say so |

## Worked example — public bucket, local state, no lock

Job: host static assets for a staging site. Tool: Terraform. Env: staging (inferred from `staging.tfvars`; say if you inferred).

Weak (abridged, no real secrets):

```hcl
# Do not copy. Values are placeholders.
terraform {
  # no backend — local state
}

resource "aws_s3_bucket" "assets" {
  bucket = "my-company-staging-assets"
}

resource "aws_s3_bucket_acl" "assets" {
  bucket = aws_s3_bucket.assets.id
  acl    = "public-read"
}

resource "aws_s3_bucket_public_access_block" "assets" {
  bucket                  = aws_s3_bucket.assets.id
  block_public_acls       = false
  block_public_policy     = false
  ignore_public_acls      = false
  restrict_public_buckets = false
}

variable "deploy_token" {
  default = "replace-me" # still a smell if a real value lands here
}
```

Critique (abridged):

```markdown
## Scope
Terraform, staging assets bucket. Blast radius: this apply can create/mutate a public bucket and (with local state) lose the only record of what exists.

## Findings
1. **Critical — state.** No remote backend or lock. Two applies can race; a laptop wipe loses state. Remediation: remote backend + locking + versioning; one state for staging only.
2. **High — exposure.** ACL `public-read` and public-access block disabled. If the job is public static hosting, say so and use a tight public-read policy plus block the rest; if not, keep the bucket private and put a CDN/OAC in front.
3. **High — secrets.** `deploy_token` default in code. Remediation: remove the default; mark sensitive; inject from a secret manager or CI OIDC. Do not print any value found in git — rotate if a real token was committed.
4. **Medium — destroy.** No `prevent_destroy` on the bucket. Staging data may be disposable; still name the risk.

## Fixes now
1. Remote state + lock + versioning.
2. Decide public vs private; default private.
3. Drop the token default; mark sensitive.

## Leftovers
Apply/plan CI split → `ci-pipeline` (melted). Cost of idle buckets → `infra-cost-scan` (stub). Broader secret sweep → `env-secrets-hygiene` (stub).
```

That is a review: scope, blast radius, remediations. Not an exploit write-up.

## Output shape

```markdown
## Scope
[tool] / [stack] / [env] — [inferred or stated]

## Blast radius
[what this apply can create, mutate, or destroy]

## Findings (severity-ranked)
1. **[Critical|High|Medium|Low] — [dimension].** [where] [what] [why]
   Remediation: [exact change]
2. …

## Fixes now
1. …
2. …
3. …

## Teach
[one reusable sentence]

## Leftovers
- [skill] — [what you did not pretend to finish]
```

If the module is already tight, say so. Empty findings are allowed. Invented issues and invented account numbers are not.

## Quality bar

A pass is done when blast radius is named in nouns, every finding is remediable, and no secret value appears. Refuse "make it more secure" without a check. Refuse exploit-shaped follow-ups.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Gold Hat: [GOLD_HAT.md](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/blob/main/GOLD_HAT.md). Sibling Libre*-Grok-Build packs: [README suite footer](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/blob/main/README.md).
