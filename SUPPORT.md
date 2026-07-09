# Support

## Before Requesting Support

Collect only redacted operational information:

- VaultPilot version shown in the console, plus the legacy PassMan version only when the host was upgraded from a PassMan-branded install.
- Windows Server version.
- MSI file name and signature status.
- Configured host and port.
- License state and active user count.
- Whether the issue affects login, secrets, sharing, extension, AD sync, backup, update, or installer flow.
- Relevant timestamps.
- Redacted server or installer log excerpts.

Do not send plaintext secrets, master passwords, AD bind passwords, agent tokens, license private keys, certificate private keys, database files, or screenshots containing secret values.

For public-safe documentation or operational questions, use the repository's redacted support issue template only when public Issues are enabled by the repository owner. For licensed customer support or any evidence that cannot be fully redacted, use the support channel provided in your purchase or onboarding materials instead of a public issue.

Public issue decision:

- Use the [redacted support issue template](.github/ISSUE_TEMPLATE/redacted-support.yml) only when public Issues are enabled and the full evidence set is safe for a public repository.
- Use the [documentation correction template](.github/ISSUE_TEMPLATE/documentation.yml) for typo, stale wording, broken link or translation fixes when public Issues are enabled.
- Use private licensed support when the issue needs unredacted logs, screenshots, customer data, certificates, databases, backups, license material or secret-bearing evidence.

## Useful Docs

- [Redacted support issue template](.github/ISSUE_TEMPLATE/redacted-support.yml)
- [Documentation correction issue template](.github/ISSUE_TEMPLATE/documentation.yml)
- [EN support evidence pack](docs/en/support-evidence-pack.md)
- [TR destek kanıt paketi](docs/tr/support-evidence-pack.md)
- [EN public repository boundary](docs/en/public-repository-boundary.md)
- [TR public repo sınırı](docs/tr/public-repository-boundary.md)
- [EN public issue redaction KB](kb/en/public-issue-redaction.md)
- [TR public issue redaction KB](kb/tr/public-issue-redaction.md)
- [TR troubleshooting](docs/tr/troubleshooting.md)
- [EN troubleshooting](docs/en/troubleshooting.md)
- [EN knowledge base](kb/en/README.md)
- [TR bilgi bankası](kb/tr/README.md)
- [Login 401/403 after unlock KB](kb/en/session-401-after-login.md)
- [DC Agent 401/install/repair KB](kb/en/dc-agent-service.md)
- [Release notes](RELEASES.md)
