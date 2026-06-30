# Security And Trust Model

This public page explains the security model at an operator level without exposing private implementation or source code.

## Trust Boundaries

| Boundary | What crosses it | Operator rule |
| --- | --- | --- |
| Browser to VaultPilot server | Authenticated API requests and encrypted vault material. | Use HTTPS for production access and keep browser sessions locked when unattended. |
| VaultPilot server to SQLite | Encrypted secret payloads and operational metadata. | Do not copy or publish the database; rely on encrypted backup workflows. |
| Update Center to GitHub Releases | Signed manifest and release assets. | Trust only assets whose manifest signature, hash, size and signer metadata verify. |
| Browser extension to server | Pairing code, wrapped vault keys and encrypted snapshots. | Pair only approved devices and revoke stale devices. |
| DC Agent to server | Directory metadata and agent heartbeat. | Keep AD bind password local to the agent setup flow; never send it to public support. |
| External sharing | Encrypted selected-record package and passphrase-protected open flow. | Share only selected records and communicate passphrases out of band. |

## What VaultPilot Protects

- Password records, credentials, API keys, secure notes, certificates and file-backed secrets.
- Vault unlock material while the browser session is active.
- Share packages through expiry, max-open controls and encrypted package metadata.
- Update packages through manifest signature, hash, size and MSI signer metadata.
- Audit evidence through visible event history and chain state.

## What Operators Must Protect

- Master passwords and authenticator devices.
- License private or issuer-side material.
- Update signing private keys.
- Certificate private keys and PFX/P12 files.
- Databases, backups and logs that may contain sensitive metadata.
- AD bind credentials and agent tokens.
- Real screenshots showing records, users, internal hostnames or customer data.

## Update Trust Chain

1. Operator downloads or checks `vaultpilot-update.json`.
2. VaultPilot verifies the manifest signature.
3. VaultPilot verifies release URLs stay on allowed GitHub release hosts.
4. VaultPilot compares MSI SHA-256 and file size.
5. VaultPilot validates the MSI signer thumbprint from the manifest.
6. Only then should the MSI update be treated as trusted for the VaultPilot-managed update path.

CA-backed or trusted-signing certificates remain recommended for Windows reputation. VaultPilot-managed update trust can still accept a local signer when the signed manifest pins that signer thumbprint.

## Public Evidence Rule

If a support case needs evidence, send only:

- Version numbers.
- Redacted service state.
- Redacted error messages.
- Manifest version, hash, size and signer status.
- Screenshots with all real records, URLs and users removed.

Never send plaintext secrets, master passwords, license private material, AD bind passwords, databases, backups, private keys or PFX/P12 files.

Related:

- [Release asset verification](release-asset-verification.md)
- [Audit and security posture](audit-and-security-posture.md)
- [Support evidence pack](support-evidence-pack.md)
