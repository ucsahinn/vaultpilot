# Public Validation Fails

Use this when `npm run validate`, `npm run validate:staged`, `git diff --check`, or Gitleaks blocks a public documentation change.

## First Checks

1. Confirm you are in the public repository root.
2. Run `git status --short --branch` and confirm the failing files belong to the intended public docs change.
3. Read the exact validator message before editing. Do not guess from the file name alone.
4. If the failure is staged-only, compare `git diff` and `git diff --cached`.
5. If Gitleaks reports a secret-like value, stop and move the evidence to private review. Do not paste the value into public issues.

## Common Failures

| Failure | Meaning | Fix |
| --- | --- | --- |
| Missing paired EN/TR file | A doc or KB page exists in one language directory but not the other. | Add the paired file or remove the accidental unpaired file before publication. |
| Broken local link | A Markdown link points to a file that does not exist in the public tree. | Fix the relative path or add the intended target. |
| Required file missing | A core public surface, screenshot, visual, workflow, template, or policy file is absent. | Restore or create the required public-safe file. Do not bypass the required list. |
| Forbidden stale wording | A release, product-name, screenshot, static-site, or compatibility phrase is known to be misleading. | Replace it with current VaultPilot wording or a precise legacy compatibility explanation. |
| Encoding artifact | Text contains mojibake or replacement characters. | Rewrite the affected text as UTF-8 instead of preserving broken console output. |
| Release binary in git | An installer, archive, manifest, support script, database, or certificate package is in the git tree. | Move release delivery artifacts to GitHub Releases; do not commit them. |
| Secret-like pattern | The file contains token-like, key-like, local-path, or customer-like evidence. | Replace with placeholders and rotate/revoke any real exposed credential through private support. |
| Whitespace check failure | `git diff --check` found patch formatting, conflict markers, or trailing whitespace. | Fix the exact lines before staging. |

## Safe Recovery

- Prefer small focused edits over broad rewrites.
- Keep the validator strict. If a new public asset is legitimate, update `scripts/validate-docs.mjs` in the same change and explain why the asset is safe.
- Do not delete files or purge generated artifacts without explicit owner approval.
- Do not stage unrelated dirty files to make `validate:staged` pass.
- Rerun the failed command after every fix, then run the full publication sequence from [Public repository publication runbook](../../docs/en/publication-runbook.md).

## Evidence To Share

Public-safe review evidence can include:

- Failing command.
- Redacted error message.
- Affected public file path.
- Whether the failure is working-tree-only or staged-only.
- Final command output showing the check passed.

Do not share raw secret values, customer paths, account screenshots, databases, backups, certificates, release binaries, or unredacted logs.

## Related

- [Publication runbook](../../docs/en/publication-runbook.md)
- [Public repository boundary](../../docs/en/public-repository-boundary.md)
- [Public screenshot standards](../../docs/en/public-screenshot-standards.md)
- [Public issue redaction](public-issue-redaction.md)
