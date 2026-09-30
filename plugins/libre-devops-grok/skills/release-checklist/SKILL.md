---
name: release-checklist
description: Ship checklist for Grok Build releases. Use before tagging, promoting, or deploying to a live environment.
---

# Release Checklist

A release is a reversible decision with a named owner, not a hope that CI was green.

Gold Hat: name what is shipping and who is on the hook if it fails, then teach the rollback while you check the boxes. Leave the person able to ship the next version without you. Never print secret values.

## When to use

- Before a tag, store publish, or production promote
- After CI is green and someone said "just ship it"
- When rollback, flags, or migrations are hand-waved
- Writing or reviewing release notes for a real change

Do not use this skill as a pipeline design pass (`ci-pipeline`, melted) or an IaC blast-radius review (`iac-review`, melted). Desired-state promotion and drift are `gitops-flow` (stub). SLI/dashboard depth is `observability-basics` (stub). Image hardening is `container-harden` (stub). Call the stub; do not invent its depth.

## Operating steps

1. **Name the release.** Artifact + version + environment + user-visible change. If the version is unstated, stop and ask.
2. **Walk the gates below.** For each item: pass, fail, or **unverified** (and how to verify). No silent skips.
3. **Name rollback before go.** Command or revert path, who runs it, how you will know it worked.
4. **Cap "ship now" work.** Blockers first. Nice-to-haves go to leftovers.
5. **Teach one sentence.** The rule this release almost violated.

A checklist with every box ticked and no rollback named is theater.

## Gates (measurable)

### Notes and version

| Check | Pass | Fail |
|-------|------|------|
| Version | Semver (or the project's scheme) matches the tag and the artifact | Tag `v2` on an artifact that still says `1.4.0-dev` |
| Changelog | User-visible changes in the project's notes format | Empty notes, or a dump of every commit subject |
| Audience | Breaking changes called out with a migration hint | Silent break on a public API |

### Confidence from CI (do not re-litigate the whole pipeline)

| Check | Pass | Fail |
|-------|------|------|
| Green on *this* candidate | The release SHA is green on the required jobs | "Main was green yesterday" |
| Required jobs | Lint/test/build (and the project's extra gates) are the ones that ran | A skipped required check |
| Artifact identity | Digest or checksum recorded; the thing you deploy is the thing you tested | Rebuild-on-promote with no digest pin |

If you did not open the run, mark CI **unverified**.

### Data and flags

| Check | Pass | Fail |
|-------|------|------|
| Migrations | Forward-only in the release; reverse plan written (expand/contract, dual-write, or restore) | Destructive migrate with no reverse |
| Flags | Risky behavior behind a flag with a default-safe value | New path is the only path, no toggle |
| Backfill | One-shot jobs named, idempotent, owner assigned | "We'll run a script" with no owner |

### Rollback and operate

| Check | Pass | Fail |
|-------|------|------|
| Rollback path | Named: revert tag, helm rollback, prior revision, flag off | "We'll figure it out" |
| Hold window | Who watches, for how long, which signal | Ship and leave |
| Observability | One dashboard or query for errors/latency of *this* change | "We have Grafana" with no panel named |
| On-call | Human named for the hold window | A rotating alias nobody will page |

Hand dashboard design to `observability-basics` (stub). For this skill, one named signal is enough.

### Strategy (pick one; do not collect them)

| Strategy | When it fits | Rollback |
|----------|--------------|----------|
| Straight replace | Small blast, easy revert | Prior artifact / git revert |
| Flag toggle | Behavior change, instant off | Turn the flag off |
| Canary / staged | High traffic, need a % hold | Abort to previous healthy |
| Blue/green | Need an instant cut | Flip traffic back |

If the repo has no canary machinery, do not invent Argo Rollouts. Name the strategy it actually has.

## Problem → gate → fix

| Complaint | Gate | First fix |
|-----------|------|-----------|
| "What did we even ship?" | Notes + version | Write the user-visible delta; align tag and artifact |
| "CI was green" | Candidate SHA | Re-run or inspect the run on *this* commit |
| "We can always roll back" | Rollback path | Write the command and the success signal |
| "Migrations are fine" | Reverse plan | Expand/contract or a restore step; no silent drops |

## Worked example — library tag without a rollback

Job: publish `1.3.0` of an API library to the package registry. User-visible change: new required field on `createInvoice`. Env: public registry (prod).

Weak: changelog is empty, `main` was green two SHAs ago, no migration note, no owner for the first hour.

Walkthrough (abridged):

```markdown
## Release
`invoice-sdk` 1.3.0 → public registry. Breaking: `createInvoice` requires `currency`.

## Gates
1. **Fail — notes.** No changelog entry; README still shows 1.2.x examples. Remediation: add a 1.3.0 note + a one-line migration (`currency` required, ISO 4217).
2. **Unverified — CI.** Required jobs not inspected on the tag SHA. Remediation: open the run for that SHA; do not ship on a neighbor commit.
3. **Fail — data/API.** Breaking field with no flag and no dual-accept window. Remediation: either 2.0.0, or 1.3.0 accepts omitted `currency` with a documented default for one minor.
4. **Fail — rollback.** "Unpublish" is not a plan (registry rules vary; users may have already installed). Remediation: yank/deprecate policy named; next patch 1.3.1 ready; announce the break.
5. **Fail — on-call.** No human for the hold window. Remediation: name an owner for 60 minutes post-publish; watch install errors / issue tracker.

## Ship now
1. Write 1.3.0 notes + migration.
2. Confirm required CI on this SHA (or say unverified and stop).
3. Decide 1.3.0 compatible vs 2.0.0 break.
4. Name rollback (deprecate + 1.3.1) and the watcher.

## Leftovers
Pipeline shape → `ci-pipeline` (melted). Registry image signing → `container-harden` (stub). Error-rate panel → `observability-basics` (stub).
```

That is a release pass: named artifact, fail/unverified, rollback. Not a vibe "LGTM".

## Output shape

```markdown
## Release
[artifact] [version] → [env] — [user-visible change]

## Gates
- [Pass|Fail|Unverified] — [gate]. [evidence]
  Remediation: [exact change]  # if not pass

## Rollback
[command or revert] — [who] — [success signal] — [hold window]

## Ship now
1. …
2. …
3. …

## Teach
[one reusable sentence]

## Leftovers
- [skill] — [what you did not pretend to finish]
```

If the release is ready, say **ready to ship** and still name rollback. Invented dashboards and fake on-call names are not allowed.

## Quality bar

A pass is done when every gate is pass, fail, or unverified, rollback is a sentence a tired human can run, and no secret appears. Refuse "just ship it" without the SHA and the rollback.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Gold Hat: [GOLD_HAT.md](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/blob/main/GOLD_HAT.md). Sibling Libre*-Grok-Build packs: [README suite footer](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build/blob/main/README.md).
