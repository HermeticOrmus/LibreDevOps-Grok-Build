---
name: ci-pipeline
description: Design or critique CI pipelines for Grok Build projects. Use for CI hygiene — stages, caching, fail-fast, secrets, and merge gates.
---

# CI Pipeline

Make CI fast, clear, and fail-useful. A green check that hides a flake or a leaked token is not hygiene.

Gold Hat: name the user job of the pipeline first (what merge confidence does this buy?), then teach the rule while you patch. Leave the person able to judge the next workflow without you. Never print secret values.

## When to use

- Designing or reviewing GitHub Actions, GitLab CI, or another YAML pipeline
- CI is slow, flaky, or "green but we don't trust it"
- Secrets, OIDC, or log redaction need a pass
- Merge gates / required checks are missing or theater

Do not use this skill as a full ship audit. After the pipeline is named, hand deploy/rollback to `release-checklist` (melted) and desired-state promotion to `gitops-flow` (still a stub). Image baseline is `container-harden` (stub). Credential smells beyond CI logs go to `env-secrets-hygiene` (stub). Call the stub; do not invent its depth.

Pair with LibreSecOps for a dedicated defensive review. Hardening only — no exploit steps, payloads, or attack scripts.

## Operating steps

1. **Name the job.** What must be true before merge or release? (lint clean, tests pass, image builds, plan-only on PR.)
2. **Map stages.** lint → test → build → deploy gates. Say which jobs are required vs optional.
3. **Walk the checks below.** Record only findings you can point at (file + job + current behavior).
4. **Rank by severity.** Critical → high → medium → low. Cap the first patch list at what one sitting can ship.
5. **Teach one sentence.** Why this change, in language the next engineer can reuse.

Stop if you cannot name the pipeline's job. Ask. Guessing a deploy gate is extraction.

## Hygiene checks (measurable)

### Stages and fail-useful signal

| Check | Pass | Fail |
|-------|------|------|
| Order | Lint/type before slow tests; build before deploy | Deploy job can start while lint is still running |
| Fail-fast | Cheap jobs fail the PR in minutes | 20-minute build is the first red signal |
| Required checks | Named status checks block merge on the protected branch | "CI" is optional; main merges on a yellow or skipped run |
| Job names | A failing job name states the gate (`lint`, `unit`, `build`) | One `build` job that does lint + test + publish |

### Caching, parallelism, flake

| Check | Pass | Fail |
|-------|------|------|
| Cache key | Includes lockfile hash (and toolchain version) | Cache key is the branch name only |
| Restore | Cache miss still produces a correct install | Pipeline assumes a warm cache |
| Matrix | Independent versions/OS in parallel; `fail-fast: false` when you need the full report | Serial version loop; one cell hides the rest |
| Flake | Retry is bounded and named; flake is a ticket | `retry: 3` with no owner; tests that pass only on retry |

If you did not measure wall time or cache hit rate, say **unverified**. Do not invent a "50% faster" claim.

### Secrets and identity (never print values)

| Check | Pass | Fail |
|-------|------|------|
| Cloud auth | OIDC / workload identity; short-lived tokens | Long-lived access keys in CI secret stores |
| Scope | Deploy credentials only on the deploy job + protected ref | Plan job can apply; fork PRs inherit write secrets |
| Logs | Secret masks on; `echo` of env dumps forbidden | `printenv`, debug dumps, or "just this once" token in YAML |
| Pins | Actions/images pinned to a digest (or a reviewed immutable tag) | `uses: org/action@main` or floating `latest` |

Name the *kind* of secret (OIDC role, npm token, deploy key). Never echo the value. If exposure is suspected, hand rotation to `env-secrets-hygiene` (stub) — no credential dumping.

### Permissions and supply chain

Start at deny. Add only what the job needs (`contents: read` to checkout, `id-token: write` for OIDC, `packages: write` only on the publish job).

Untrusted PR code must not run with write secrets. Fork PRs get a plan/test path, not apply.

## Problem → rule → fix

| Complaint | Rule | First fix |
|-----------|------|-----------|
| "CI takes forever" | Fail-fast + cache | Split lint; key cache on the lockfile |
| "It's green but we still break prod" | Required checks + real tests | Name the merge gate; stop skipping the suite |
| "Sometimes it fails, rerun works" | Flake is a defect | Quarantine or fix; do not hide with retry |
| "Someone pasted a key in the workflow" | OIDC + no values in git | Remove the key, rotate, switch to identity |

## Worked example — PR pipeline that can leak and lie

Job: give merge confidence on a library PR. Gates: lint, unit tests, build. No production deploy from a PR.

Weak (abridged, values omitted on purpose):

```yaml
# .github/workflows/ci.yml — do not copy
on: [push]
jobs:
  all:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm i && npm test && npm run build
      - run: echo "token=$DEPLOY_TOKEN"
        env:
          DEPLOY_TOKEN: ${{ secrets.DEPLOY_TOKEN }}
```

Critique (abridged):

```markdown
## Job
Reviewer needs lint + unit + build before merge. No deploy from this workflow.

## Findings
1. **Critical — secrets.** Workflow echoes a deploy token into logs. Remediation: delete the step; rotate the token (do not print it); PR CI should not hold deploy credentials.
2. **High — stages.** One `all` job hides which gate failed and skips a cheap lint-first fail. Remediation: `lint` then `test` then `build`; require those names on the protected branch.
3. **High — identity.** Long-lived `DEPLOY_TOKEN` on every push. Remediation: drop it from PR CI; production publish uses OIDC on a protected ref only.
4. **Medium — cache / pins.** `npm i` with no lockfile cache; `checkout@v4` is a moving major. Remediation: cache on `package-lock.json`; pin the action to a digest.

## Fixes now
1. Remove the echo; rotate; strip deploy secrets from PR CI.
2. Split jobs; mark them required.
3. Pin + cache; measure duration (unverified until you run it).

## Leftovers
Ship/rollback → `release-checklist` (melted). Image scan → `container-harden` (stub). Secret-smell sweep → `env-secrets-hygiene` (stub).
```

Stronger shape (no secrets, PR-only):

```yaml
name: ci
on:
  pull_request:
  push:
    branches: [main]
permissions:
  contents: read
jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4 # pin to a digest in the real file
      - run: npm ci && npm run lint
  test:
    needs: lint
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci && npm test
```

That is hygiene: stages, no token in logs, merge-sized job. Not a `/10` scorecard.

## Output shape

```markdown
## Job
[what merge/release confidence this pipeline buys]

## Findings (severity-ranked)
1. **[Critical|High|Medium|Low] — [dimension].** [file/job] [what] [why]
   Remediation: [exact change]
2. …

## Fixes now (≤5, effort-tagged)
1. [change] — [S/M/L]
2. …

## Teach
[one reusable sentence]

## Leftovers
- [skill] — [what you did not pretend to finish]
```

If the pipeline is already clean, say so. Empty findings are allowed. Invented issues are not.

## Quality bar

A pass is done when every finding is specific, ranked, and remediable, and no secret value appears in the output. Refuse vibe-only notes ("make CI nicer") — translate them through the checks or drop them.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Gold Hat: [GOLD_HAT.md](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/blob/main/GOLD_HAT.md). Sibling Libre*-Grok-Build packs: [README suite footer](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/blob/main/README.md).
