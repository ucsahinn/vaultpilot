# Public Repository Publication Runbook

Use this runbook when preparing public VaultPilot documentation, KB, screenshot, policy, or release-note changes for review. It is intentionally conservative: validate the working tree first, validate the git index before commit, and keep account-side publication separate from repository edits.

This runbook does not grant permission to publish, tag, release, upload store assets, enable Issues, add license terms, or change repository settings. Those actions require repository-owner approval.

## Safe Local Sequence

| Step | Command or evidence | Stop condition |
| --- | --- | --- |
| Inspect scope | `git status --short --branch` | Unrelated source, generated artifact, local secret, build output, database, certificate, installer, ZIP, or account-state file is mixed into the public docs change. |
| Validate docs | `npm run validate` | Broken local links, EN/TR parity drift, missing required assets, stale release wording, forbidden public-site leftovers, encoding artifacts, release binaries, or secret-like patterns are reported. |
| Check whitespace | `git diff --check` | Trailing whitespace, conflict markers, or patch formatting errors are reported. |
| Scan secrets | `gitleaks detect --no-git --redact --verbose --source .` | Any leak is reported. Treat secret-like evidence as compromised until reviewed privately. |
| Review diff | `git diff --stat` and targeted `git diff -- <path>` | The diff includes accidental deletions, raw release assets, customer data, local paths, or files outside the intended public docs scope. |
| Stage explicit files | Explicit `git add <file>` commands only | Do not stage by directory or with `git add .` unless every visible change is intentionally included. |
| Validate index | `npm run validate:staged` and `git diff --cached --check` | The staged tree differs from the validated working tree, or index-only validation fails. |
| Review staged diff | `git diff --cached --stat` and targeted `git diff --cached -- <path>` | Staged files contain unrelated work, secrets, release binaries, generated scratch files, or unreviewed account instructions. |

## What To Commit

Commit only reviewed public-safe files:

- Markdown docs, KB articles, localized READMEs, release notes, and policy files.
- Public validation scripts and GitHub workflow definitions.
- Public-safe screenshots and visuals listed by `scripts/validate-docs.mjs`.
- GitHub issue templates, pull request template, and documentation-only repo metadata files.

Do not commit:

- MSI, EXE, ZIP, PFX, P12, DB, SQLite, backup, dump, log, coverage, cache, temp, or local browser artifacts.
- Update manifests, component manifests, PowerShell support scripts, and release packages that belong on GitHub Releases.
- Private product source code, signing material, customer evidence, unredacted screenshots, account exports, or Chrome Web Store dashboard screenshots.
- License terms unless the repository owner approved a root `LICENSE` or `LICENSE.md`.

## Account-Side Gates

These tasks are not completed by a git commit:

| Surface | Required owner action |
| --- | --- |
| GitHub repository description, homepage, topics, social preview, Issues, Discussions, security policy toggles | Change in GitHub repository settings after owner approval. |
| GitHub Release title, notes, and asset uploads | Change on the GitHub Release record with release-owner approval. |
| Chrome Web Store listing, screenshots, privacy practices, and publication | Change in the Chrome Web Store publisher account. |
| License publication | Add owner-approved root `LICENSE` or `LICENSE.md`, then update docs that currently state no license terms are published. |
| Search Console, analytics, verified publisher status | Account-side verification; do not store tokens or verification secrets in this repository. |

## Final Evidence To Record

Before asking for review or publication, record:

- Branch and remote from `git status --short --branch`.
- Validation commands and outcomes.
- Whether `validate:staged` was run.
- Files intentionally staged or intentionally left untracked.
- Any gated owner/account-side actions that remain.
- Whether [Public external surface drift](public-external-surface-drift.md) has been updated with the latest GitHub Release and Chrome Web Store observations.
- Any checks that could not run, with exact command and failure reason.

## If Validation Fails

Use [Public validation failure KB](../../kb/en/public-validation-fails.md). Fix the cause instead of weakening the validator. If the validator blocks a legitimate new public asset, update the manifest and add a focused reason in the same change.

Related:

- [Public repository boundary](public-repository-boundary.md)
- [Public discoverability](public-discoverability.md)
- [Public external surface drift](public-external-surface-drift.md)
- [GitHub repository profile](github-repository-profile.md)
- [Chrome Web Store listing and privacy](chrome-web-store-listing.md)
- [Contribution rules](../../CONTRIBUTING.md)
