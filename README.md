# PassMan Releases

Public release artifacts, signed update manifests, and customer-facing download metadata for PassMan Enterprise Vault Console.

This repository intentionally contains distribution assets only. The PassMan product source code, build system, signing workflow, and internal development history remain in the private `ucsahinn/passman` repository.

## Current Release

Latest stable release: **PassMan 1.5.1**

- Release page: https://github.com/ucsahinn/passman-releases/releases/tag/v1.5.1
- Latest release redirect: https://github.com/ucsahinn/passman-releases/releases/latest
- Signed update manifest: https://github.com/ucsahinn/passman-releases/releases/latest/download/passman-update.json

PassMan verifies the signed update manifest, pinned SHA-256 checksums, and package metadata before exposing update packages in the application.

## Component Versions

| Component | Version | Distribution |
| --- | ---: | --- |
| PassMan Enterprise Vault Console | 1.5.1 | Windows MSI |
| Chromium browser extension | 3.1.8 | ZIP package and extension metadata |
| Offline Share Decrypter | 1.2.0 | ZIP package and metadata |
| PassMan DC Agent Service | 1.0.10 | PowerShell service installer and metadata |

The Update Center exposes the main MSI and browser extension as actionable update cards. The Offline Share Decrypter and PassMan DC Agent Service are MSI-refreshed support components and remain visible in release notes and package metadata.

## Release Assets

| Asset | Purpose |
| --- | --- |
| `PassMan-1.5.1-x64.msi` | Self-hosted PassMan server installer for Windows. |
| `passman-update.json` | Signed update manifest for the main application and support components. |
| `passman-chromium-extension.zip` | Chromium extension fallback or managed rollout package. |
| `passman-extension-update.json` | Browser extension package metadata. |
| `passman-share-decrypter.zip` | Offline external-share decrypter package. |
| `passman-share-decrypter.json` | Offline decrypter package metadata. |
| `passman-ad-agent.ps1` | PassMan DC Agent Service installer/repair/status script. |
| `passman-ad-agent.json` | DC Agent package metadata. |

## DC Agent Service

The current DC Agent Service release is `1.0.10`.

The agent script installs the Windows service as `PassManDCAgent` with display name `PassMan DC Agent Service`. It supports:

- `-InstallService` for first service installation.
- `-RepairService` to rebuild and restart the service using the existing protected local config.
- `-Status` to print redacted service, config, and log status.
- `-TailLog` to watch agent logs from a terminal while the service keeps running.

The AD bind password is collected locally on the DC-side machine. It is not sent to PassMan and is not written to release metadata.

## Release Notes

See [RELEASES.md](./RELEASES.md) for the current release summary and component history.

## Licensing

These release artifacts are distributed for licensed PassMan users. This repository is not an open source source-code repository.

## Security

Do not upload private keys, signing certificates, database files, environment files, AD bind credentials, agent tokens, or customer data to this repository. Installers and package archives belong in GitHub Releases, not in the source tree.
