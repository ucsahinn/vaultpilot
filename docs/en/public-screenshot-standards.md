# Public Screenshot Standards

Use this page when adding, replacing, or reviewing VaultPilot screenshots in the public repository. Public screenshots are documentation fixtures. They help an operator recognize the screen and workflow, but they are not release evidence, production guidance, or customer-environment proof.

## Source Rules

- Capture only from an isolated VaultPilot runtime prepared for documentation.
- Use synthetic tenant, host, user, group, vault, record, file, finding, package, license, and update data.
- Do not show real hostnames, usernames, email addresses, customer names, paths, database names, support tickets, logs, token values, license values, vault records, secret titles, passwords, private keys, or certificate material.
- Keep browser chrome, desktop notifications, local folders, terminal windows, account dashboards, and personal profile data out of the frame.
- Treat visible counts, timestamps, filenames, package sizes, hashes, domains, findings, and action states as fixtures that must not be used as release verification data.

## Approved Screenshot Manifest

The validator accepts only the public screenshot files listed below and verifies the machine-readable inventory at [`assets/screenshots/MANIFEST.json`](../../assets/screenshots/MANIFEST.json). That manifest records each surface name, PNG dimensions, byte size, SHA-256 hash, and synthetic fixture note so visual replacements are explicit and reviewable.

| Surface | File |
| --- | --- |
| Login lock screen | `assets/screenshots/login-lock-screen.png` |
| Security posture dashboard | `assets/screenshots/overview-security-posture.png` |
| Secret records list | `assets/screenshots/passwords-record-list.png` |
| Server System settings | `assets/screenshots/server-settings.png` |
| Discovery run scope | `assets/screenshots/discovery-run.png` |
| Discovery findings | `assets/screenshots/discovery-findings.png` |
| Discovery import candidates | `assets/screenshots/discovery-import.png` |
| Update Center | `assets/screenshots/update-center-vaultpilot-2.png` |
| Browser extension management | `assets/screenshots/browser-extension-management-vaultpilot-2.png` |
| Active Directory sync tree | `assets/screenshots/active-directory-sync-tree-vaultpilot-2.png` |
| Sharing package flow | `assets/screenshots/sharing-package-flow-vaultpilot-2.png` |

The retired legacy compatibility-line capture set must not be restored, linked or used as walkthrough evidence. Current public screenshots use VaultPilot-named filenames and are enforced by `scripts/validate-docs.mjs`.

## Acceptance Checklist

- File is a PNG under 2 MB.
- Filename is lowercase kebab-case.
- File appears in `assets/screenshots/MANIFEST.json` and in the approved path list inside `scripts/validate-docs.mjs`.
- Manifest dimensions, byte size, SHA-256 hash, surface label, and synthetic fixture note match the final PNG.
- Markdown uses descriptive alt text that names the surface, not a generic "screenshot" label.
- Caption states that visible values are synthetic fixtures when the screenshot could be mistaken for operational evidence.
- The image is linked from the relevant guide or from the visual reference table, not from a raw screenshot directory link.
- The page explains exact surface context, product version context, and the workflow being shown.
- The screenshot has been manually inspected for secrets, customer identifiers, local operator paths, browser profile data, and account dashboard data.

## Replacement Process

1. Capture the candidate from an isolated documentation runtime.
2. Inspect the image at full size before adding it to git.
3. Place the PNG under `assets/screenshots/`.
4. Update the guide that embeds it and the visual table in `docs/README.md`.
5. Update `assets/screenshots/MANIFEST.json` with the final dimensions, byte size, SHA-256 hash, surface label and synthetic fixture note.
6. Update the approved screenshot path list in `scripts/validate-docs.mjs` if the file path changes.
7. Update this page if the accepted manifest changes.
8. Run:

```powershell
npm run validate
git diff --check
gitleaks detect --no-git --redact --verbose --source .
```

If files are staged later, also run:

```powershell
npm run validate:staged
git diff --cached --check
```

## If A Screenshot Is Unsafe

Do not commit or attach the image publicly. Replace the image with a synthetic-data capture. If the image exposed a token, secret value, certificate private material, license private material, customer credential, or private account data, treat that value as compromised until it is reviewed privately and rotated or revoked where applicable.

Use [Public screenshot redaction](../../kb/en/public-screenshot-redaction.md) for the incident path and [Public issue redaction](../../kb/en/public-issue-redaction.md) when deciding whether evidence belongs in a public issue.

Related: [Documentation gateway](../README.md), [Public repository boundary](public-repository-boundary.md), [Publication runbook](publication-runbook.md), [Chrome Web Store listing and privacy](chrome-web-store-listing.md), [Contributing](../../CONTRIBUTING.md).
