# Pull Request Checklist

## Scope

- [ ] This PR changes only public documentation, knowledge-base content, public-safe assets, validation scripts, or GitHub metadata.
- [ ] No private product source code, release binary, signing material, customer file, database, backup, raw log, token, key, certificate package, or local-only artifact is included.
- [ ] VaultPilot is used as the canonical product name. PassMan appears only for legacy compatibility context.

## Public Safety

- [ ] Screenshots use synthetic data only and show no real tenant, hostname, user, token, secret, customer URL, internal infrastructure, or support-ticket export.
- [ ] Examples use placeholders such as `<VAULTPILOT_URL>`, `<SERVER_HOST>`, `<AGENT_ID>`, `<AGENT_TOKEN>`, `<LICENSE_CODE>`, and `<REDACTED>`.
- [ ] Security reports, exploit details, raw logs, certificates, databases, backups, and sensitive support bundles are not included in this public PR.

## Documentation Quality

- [ ] English and Turkish docs remain paired where the topic exists under `docs/en` and `docs/tr`.
- [ ] English and Turkish KB articles remain paired where the topic exists under `kb/en` and `kb/tr`.
- [ ] Local Markdown links are relative and resolve inside the repository.
- [ ] Release asset names, versions, and dates match the current public GitHub Release before being documented.
- [ ] Chrome Web Store listing or privacy changes update `docs/en/chrome-web-store-listing.md`, `docs/tr/chrome-web-store-listing.md`, `PRIVACY.md`, and the Chrome Web Store review KB together.
- [ ] Public issue, PR, or repository metadata changes keep `.github/ISSUE_TEMPLATE/`, `.github/PULL_REQUEST_TEMPLATE.md`, `docs/en/public-external-surface-drift.md`, and `docs/tr/public-external-surface-drift.md` aligned.
- [ ] Account-side changes that cannot be completed by this PR are recorded in the public external surface drift register.

## Validation

```powershell
npm run validate
npm run validate:staged
git diff --check
gitleaks detect --no-git --redact --verbose --source .
```

If a validation command cannot run, explain the exact reason in the PR body.
