# Release Asset Verification

Use this page before installing or publishing a VaultPilot public release asset internally. The goal is to verify that the MSI and support packages match the signed manifest and the exact GitHub Release being evaluated.

## Release State

The current verified public release is GitHub Release [`v3.0.2`](https://github.com/ucsahinn/vaultpilot/releases/tag/v3.0.2), published on July 23, 2026.

Treat the GitHub Release asset metadata as the public source of truth. Unpublished build output, copied files, support attachments and chat uploads are not release evidence.

## VaultPilot 3.0.2 Components

| Component | Version | Asset |
| --- | ---: | --- |
| VaultPilot Enterprise Vault Console | 3.0.2 | `VaultPilot-3.0.2-x64.msi` |
| Chromium Browser Extension | Chrome Web Store 1.3.3; v3.0.2 archive 1.3.3 | Chrome Web Store listing; no ZIP in the default update manifest |
| Offline Share Decrypter | 1.2.1 | `vaultpilot-share-decrypter.zip` |
| VaultPilot DC Agent Service | 1.2.22 | `vaultpilot-dc-agent.ps1` |
| Update manifest | 3.0.2 channel metadata | `vaultpilot-update.json` |

## VaultPilot 3.0.2 Release Evidence

This matrix records the independently checked public `v3.0.2` asset set used for customer downloads.

| Component | Version | Delivery |
| --- | ---: | --- |
| VaultPilot Enterprise Vault Console | 3.0.2 | Versioned Windows MSI and signed update manifest |
| Chromium Browser Extension | 1.3.3 | Chrome Web Store version; no extension ZIP in this release |
| Offline Share Decrypter | 1.2.1 | Versioned release archive and signed component manifest |
| VaultPilot DC Agent Service | 1.2.22 | Versioned PowerShell asset and signed component manifest |
| VaultPilot Backup Tool | 1.0.3 | Bundled server support component; not a separate GitHub Release asset |
| VaultPilot Log Collector | 1.0.3 | Bundled server support component; not a separate GitHub Release asset |

## Public Asset Set

The public GitHub Release contains these customer-safe delivery assets. This table records the locally verified publication set issued on July 23, 2026:

| Asset | Size | SHA-256 |
| --- | ---: | --- |
| `VaultPilot-3.0.2-x64.msi` | 65,441,792 | `33f43c95379b53122c92674ad6bef973ad29f6a29a44dd761d2ebd263a6e249e` |
| `vaultpilot-update.json` | 1,374 | `25dba9059350152c37d687b7061a5ad254f70fc57aef4814a473e8a9a6842397` |
| `vaultpilot-share-decrypter.zip` | 51,566 | `e72cef76a1a8389339ea75469e6467b908cd51cd7e8f6381fcb61910eb9af756` |
| `vaultpilot-share-decrypter.json` | 218 | `5d4af2cd0be93f7d553a37def1446d71962c9d0f5a8403038455197659ba7da8` |
| `vaultpilot-dc-agent.ps1` | 234,224 | `1db27b19a7417b00da5102cebc39e85529ea07f0b957e76d63c7fed4b9e8f8a8` |
| `vaultpilot-dc-agent.json` | 213 | `ebaaeed49bf1be99df8f3607addea5adc60cc9c339204c69dd16b37a23362ea3` |
| `VpUninstallTool-3.0.2-x64.msi` | 69,632 | `bca790aa016ed4627fcf7cdba49768dde27d6fb6b8c3740f407cc26ed131558e` |

The Chrome Web Store listing is the primary customer install and update channel for the browser extension and can advance independently from a GitHub Release. The live store reports `1.3.3`; the default `v3.0.2` update manifest does not publish an extension ZIP.

The MSI is signed with the manifest-pinned VaultPilot development signer and has no RFC3161 timestamp. VaultPilot-managed updates still verify the signed manifest, exact SHA-256 and signer thumbprint, but Windows trust and SmartScreen reputation remain environment-dependent. Commit-bound final artifact, standalone payload, and managed-component evidence passed for the published MSI hash. Fresh local Health, elevated Repair/Health, and physical Windows Sandbox Install/Health evidence were not rerun for this exact hotfix MSI.

Legacy compatibility files can remain inside installed migration and rollback paths, but new public releases contain VaultPilot-named customer assets only.

The git tree should not contain MSI, ZIP, EXE, PFX, P12, DB, SQLite, backup or signing-key files.

## Verification Steps

1. Open GitHub Release [`v3.0.2`](https://github.com/ucsahinn/vaultpilot/releases/tag/v3.0.2).
2. Confirm the release tag is `v3.0.2` and the release is not draft or prerelease unless your internal policy explicitly allows it.
3. Download `vaultpilot-update.json` from that release.
4. Confirm the manifest lists server version `3.0.2`.
5. Confirm the MSI filename is `VaultPilot-3.0.2-x64.msi`.
6. Confirm each asset URL uses the approved public GitHub Release host.
7. Confirm each downloaded file size and SHA-256 matches the table above and the manifest where the component is listed.
8. Confirm the MSI Authenticode signer metadata matches the manifest signer thumbprint.
9. Confirm extension release archive, decrypter and DC Agent package hashes before internal redistribution; browser users should install and update the extension from Chrome Web Store.

## Windows Verification Commands

Run these commands from a temporary folder that contains the downloaded release files. Keep the output with internal release evidence; redact local paths or hostnames before sharing publicly.

```powershell
gh release view v3.0.2 --repo ucsahinn/vaultpilot --json tagName,name,isDraft,isPrerelease,publishedAt,assets,url

Get-ChildItem -File |
  Where-Object { $_.Name -like 'VaultPilot-3.0.2-x64.msi' -or $_.Name -like 'vaultpilot-*' -or $_.Name -like 'VpUninstallTool-*' } |
  Select-Object Name,Length

Get-FileHash .\VaultPilot-3.0.2-x64.msi -Algorithm SHA256
Get-FileHash .\vaultpilot-* -Algorithm SHA256

Get-AuthenticodeSignature .\VaultPilot-3.0.2-x64.msi |
  Format-List Status,StatusMessage,SignerCertificate
```

If `gh release view` shows a different tag, draft/prerelease state, asset count, size, digest or URL, stop and update this page and the public external-surface drift register before continuing.

## What To Record Internally

| Evidence | Safe to record publicly? |
| --- | --- |
| Release tag, file names, sizes and hashes | Yes. |
| MSI signer subject and thumbprint | Yes. |
| Manifest signature value | Yes. |
| Local install path, private hostnames and user names | Redact first. |
| License code, signing private key, PFX/P12 or database | Never. |

## If Verification Fails

Do not install or redistribute the package. Collect the release tag, asset name, expected hash, observed hash, file size and signer status, then use the licensed support channel from your purchase or onboarding materials.

Related:

- [Update Center](update-center.md)
- [Uninstall, data retention and rollback](uninstall-rollback-data-retention.md)
- [Security and trust model](security-and-trust-model.md)
- [Support evidence pack](support-evidence-pack.md)
