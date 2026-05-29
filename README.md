# PassMan Enterprise Vault Console

Public release, documentation and knowledge-base hub for PassMan.

PassMan is a self-hosted, zero-knowledge enterprise password and secrets vault for Windows Server. It is installed with an MSI, runs on the customer's own Windows server, and is accessed from browsers through the server IP or DNS name.

This repository is intentionally public. It contains product documentation, knowledge-base articles, release notes and links to GitHub Release downloads. The product source code, signing workflow, license issuer material and private build history remain private.

## Public Hub

| Surface | Link |
| --- | --- |
| GitHub Pages hub | https://ucsahinn.github.io/passman-releases/ |
| Documentation index | https://ucsahinn.github.io/passman-releases/docs/ |
| Knowledge base | https://ucsahinn.github.io/passman-releases/kb/ |
| Latest GitHub Release | https://github.com/ucsahinn/passman-releases/releases/latest |

GitHub Pages is deployed from `.github/workflows/pages.yml`. Pages should be configured to build with GitHub Actions. If automatic enablement is required, configure `PASSMAN_PAGES_ADMIN_TOKEN` as a repository secret with Pages administration rights.

## Current Stable Release

**PassMan Enterprise Vault Console 1.5.3**

| Asset | Link |
| --- | --- |
| Windows MSI | https://github.com/ucsahinn/passman-releases/releases/latest/download/PassMan-1.5.3-x64.msi |
| Signed update manifest | https://github.com/ucsahinn/passman-releases/releases/latest/download/passman-update.json |
| Chromium extension ZIP | https://github.com/ucsahinn/passman-releases/releases/latest/download/passman-chromium-extension.zip |
| Offline Share Decrypter ZIP | https://github.com/ucsahinn/passman-releases/releases/latest/download/passman-share-decrypter.zip |
| PassMan DC Agent installer | https://github.com/ucsahinn/passman-releases/releases/latest/download/passman-ad-agent.ps1 |

## Component Versions

| Component | Version | Delivery |
| --- | ---: | --- |
| PassMan Enterprise Vault Console | 1.5.3 | Windows MSI |
| Chromium browser extension | 3.1.8 | Managed rollout or ZIP fallback |
| Offline Share Decrypter | 1.2.0 | Release ZIP and MSI support component |
| PassMan DC Agent Service | 1.0.10 | PowerShell service installer and MSI support component |

The Update Center exposes the main MSI and browser extension as actionable update surfaces. Offline Share Decrypter and PassMan DC Agent Service are support components refreshed with the MSI and documented in release notes.

## Documentation

| Area | Turkish | English |
| --- | --- | --- |
| Overview | [TR](docs/tr/overview.md) | [EN](docs/en/overview.md) |
| Windows Server installation | [TR](docs/tr/install-windows-server.md) | [EN](docs/en/install-windows-server.md) |
| First run, owner and license | [TR](docs/tr/first-run-owner-license.md) | [EN](docs/en/first-run-owner-license.md) |
| Public host and HTTPS | [TR](docs/tr/public-host-https-certificate.md) | [EN](docs/en/public-host-https-certificate.md) |
| Update Center | [TR](docs/tr/update-center.md) | [EN](docs/en/update-center.md) |
| Browser extension | [TR](docs/tr/browser-extension.md) | [EN](docs/en/browser-extension.md) |
| Active Directory agent | [TR](docs/tr/active-directory-agent.md) | [EN](docs/en/active-directory-agent.md) |
| Sharing and offline decrypter | [TR](docs/tr/sharing-and-offline-decrypter.md) | [EN](docs/en/sharing-and-offline-decrypter.md) |
| Backups and restore | [TR](docs/tr/backups-and-restore.md) | [EN](docs/en/backups-and-restore.md) |
| Audit and security posture | [TR](docs/tr/audit-and-security-posture.md) | [EN](docs/en/audit-and-security-posture.md) |
| Troubleshooting | [TR](docs/tr/troubleshooting.md) | [EN](docs/en/troubleshooting.md) |
| FAQ | [TR](docs/tr/faq.md) | [EN](docs/en/faq.md) |

## Knowledge Base

Use the [Knowledge Base](kb/index.html) for fast, public-safe troubleshooting:

- MSI installation failures.
- Updates stuck around 76 percent.
- PassMan DC Agent Service connection issues.
- Browser extension pairing issues.
- HTTPS certificate warnings.
- Partial audit-chain states.
- License read-only state.
- External share package failures.

## Security and Support Boundaries

Do not upload private keys, signing certificates, database files, environment files, AD bind credentials, agent tokens, license issuer material, customer data, logs or screenshots containing secrets to this repository.

Installers, ZIP packages, PowerShell scripts and signed manifests belong in GitHub Releases, not in the git tree.

Useful policies:

- [Security policy](SECURITY.md)
- [Support policy](SUPPORT.md)
- [Release notes](RELEASES.md)

## Update Verification

PassMan-managed updates verify:

- Signed update manifest.
- SHA-256 checksums.
- Release asset metadata.
- MSI signer thumbprint.

PassMan does not require a global CA chain for its own update trust when the signed manifest pins the local release signer. CA-backed or trusted signing is still recommended for Windows reputation and broad OS-level trust.

## Repository Validation

Run before publishing public documentation changes:

```powershell
npm run validate
```

The validation checks local links, TR/EN doc parity, required visual assets, stale latest-version wording and forbidden secret-like patterns.
