# Security Policy

## Supported Release

Only the latest verified public VaultPilot/PassMan release is supported for new installations and updates. The prepared major release is **VaultPilot Enterprise Vault Console 2.0.0**, but as of June 30, 2026, the latest verified GitHub Release is still **PassMan Enterprise Vault Console 1.8.21**. Do not treat `2.0.0` assets as public proof until the release gate publishes and verifies the final MSI, manifest, signatures and hashes.

## Reporting Security Issues

Report security issues privately to the VaultPilot maintainer or licensed support channel. Do not open public issues that include secrets, exploit payloads, customer data, logs with sensitive values, screenshots containing secret records, agent tokens, license private keys, certificates, or database files.

## Public Repository Boundaries

This repository may contain public documentation and public release notes. Customer delivery files belong as GitHub Release assets, not committed files in the git tree. It must not contain:

- Private source code.
- Signing private keys or certificate packages.
- License issuer private keys.
- Update manifest private keys.
- Databases, backups, or logs.
- Real AD bind credentials, agent IDs, agent tokens, customer URLs, or license codes.
- Screenshots showing secret values.

## Verification Model

VaultPilot-managed updates verify a signed manifest, asset SHA-256 hashes, release metadata, and MSI signer thumbprints. A local release signer can be accepted by VaultPilot when the signed manifest pins that signer. CA-backed or trusted signing is still recommended for Windows reputation.

Use [release asset verification](docs/en/release-asset-verification.md) before manual installation, mirror, or internal redistribution. Use the [security and trust model](docs/en/security-and-trust-model.md) to understand which boundaries VaultPilot enforces and which controls remain operator-owned.
