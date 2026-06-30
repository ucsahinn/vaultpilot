# Release Asset Verification

Use this page before installing or publishing a VaultPilot public release asset internally. The goal is to verify that the MSI and support packages match the signed manifest and the exact GitHub Release being evaluated.

## Release State

As of June 30, 2026, the latest verified published GitHub Release is still `v1.8.21`.

The table below is the prepared VaultPilot 2.0.0 asset set and must not be treated as public proof until the `v2.0.0` GitHub Release, final assets, manifest, signatures and hashes are published and verified.

## Prepared 2.0.0 Asset Set

| Component | Version | Asset |
| --- | ---: | --- |
| VaultPilot Enterprise Vault Console | 2.0.0 | `VaultPilot-2.0.0-x64.msi` after publication |
| Chromium Browser Extension | 1.3.1 | Chrome Web Store listing; `vaultpilot-browser-vault-extension.zip` release archive |
| Offline Share Decrypter | 1.2.0 | `vaultpilot-share-decrypter.zip` |
| VaultPilot DC Agent Service | 1.2.10 | `vaultpilot-dc-agent.ps1` after publication |
| Update manifest | 2.0.0 channel metadata | `vaultpilot-update.json` after publication |

## Public Asset Set

The public GitHub Release should contain exactly the customer-safe delivery assets:

- `VaultPilot-2.0.0-x64.msi`
- `vaultpilot-update.json`
- `vaultpilot-browser-vault-extension.zip`
- `vaultpilot-share-decrypter.zip`
- `vaultpilot-dc-agent.ps1`

The Chrome Web Store listing is the primary customer install and update channel for the browser extension. The extension ZIP is retained only as a release archive, lab validation package, local development package or emergency fallback artifact.

The git tree should not contain MSI, ZIP, EXE, PFX, P12, DB, SQLite, backup or signing-key files.

## 2.0.0 Asset Metadata Status

Final 2.0.0 size and SHA-256 values are intentionally not written here yet. They must come from the fresh release gate after `npm run build:windows`, manifest issue/verify, MSI verification, and publication evidence.

As of June 30, 2026, the latest verified GitHub Release is still `v1.8.21`; do not reuse old `1.8.22` asset sizes or hashes as 2.0.0 proof.

## Verification Steps

1. Open the `v2.0.0` GitHub Release only after publication. Until it exists, use this page as a pre-publication checklist only.
2. Confirm the release tag is `v2.0.0` and the release is not draft or prerelease unless your internal policy explicitly allows it.
3. Download `vaultpilot-update.json` from that release.
4. Confirm the manifest lists server version `2.0.0`.
5. Confirm the MSI filename is `VaultPilot-2.0.0-x64.msi`.
6. Confirm each asset URL uses the approved public GitHub Release host.
7. Confirm the downloaded MSI file size and SHA-256 match the manifest.
8. Confirm the MSI Authenticode signer metadata matches the manifest signer thumbprint.
9. Confirm extension release archive, decrypter and DC Agent package hashes match the manifest before internal redistribution; browser users should install and update the extension from Chrome Web Store.

## What To Record Internally

| Evidence | Safe to record publicly? |
| --- | --- |
| Release tag, file names, sizes and hashes | Yes. |
| MSI signer subject and thumbprint | Yes. |
| Manifest signature value | Yes. |
| Local install path, private hostnames and user names | Redact first. |
| License code, signing private key, PFX/P12 or database | Never. |

## If Verification Fails

Do not install or redistribute the package. Collect the release tag, asset name, expected hash, observed hash, file size and signer status, then use a private support channel.

Related:

- [Update Center](update-center.md)
- [Uninstall, data retention and rollback](uninstall-rollback-data-retention.md)
- [Security and trust model](security-and-trust-model.md)
- [Support evidence pack](support-evidence-pack.md)
