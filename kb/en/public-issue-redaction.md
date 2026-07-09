# Public Issue Redaction

Use this article when an operator or support engineer wants to open a public issue but the evidence may contain tenant, host, user, secret or license data.

## Symptom

The issue is documentation, install, update, browser extension, Discovery, DC Agent or sharing related, but the available screenshots or logs include environment-specific values.

## Public-Safe Evidence

You may include:

- VaultPilot version and affected component name.
- Windows Server version.
- Public release tag or asset name.
- Redacted timestamp and error state.
- Browser name and extension ID when relevant.
- Placeholder host shape such as `<VAULTPILOT_URL>` or `<SERVER_HOST>`.
- Short log excerpts after token, host, user, path and secret values are replaced with `<REDACTED>`.

## Redact Before Posting

Replace these values before posting publicly:

- Customer, tenant, domain, OU, group and user names.
- Internal URLs, IP addresses, machine names and local paths.
- Vault record titles, usernames, URLs, notes, files and custom fields.
- Agent IDs, agent tokens, API client IDs, API secrets, license codes and private license material.
- Session IDs, cookies, certificate subjects and certificate private material.

## Do Not Post Publicly

Do not attach databases, backups, certificate packages, private keys, PFX/P12 files, MSI evidence bundles, raw logs, support exports or screenshots that still reveal real vault data.

## Decision

- If the evidence is fully redacted and the question is public documentation or product behavior, use the public issue template.
- If any required evidence cannot be redacted without losing the issue, use private support.

Related: [Support policy](../../SUPPORT.md), [public repository boundary](../../docs/en/public-repository-boundary.md), [support evidence pack](../../docs/en/support-evidence-pack.md).
