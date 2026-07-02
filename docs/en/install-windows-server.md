# Windows Server Installation

This runbook covers a normal VaultPilot Server installation or in-place upgrade on Windows. Use it before opening the server to other users.

## Requirements

| Requirement | Notes |
| --- | --- |
| Windows Server or approved Windows host | Use a controlled host with stable storage and backup policy. |
| Administrator rights | Required for the MSI, service registration and firewall rule. |
| Inbound TCP access | Default port is `1903`; change only if your network policy requires it. |
| Backup decision | Export or preserve the existing data directory before production upgrades. |
| Release assets | Use the MSI and update manifest from GitHub Releases, not files copied from chat or support threads. |

## Install

1. Download `VaultPilot-2.0.0-x64.msi` from GitHub Release `v2.0.0`.
2. Verify the filename, source, checksum and signer before running it. Use [release asset verification](release-asset-verification.md) when you need the full checklist.
3. Run the MSI as Administrator.
4. The installer prepares the standalone server, bundled Node runtime, Prisma/SQLite runtime files, Windows service, firewall rule, data directory and log directory.
5. Open VaultPilot from the server first:

```text
https://127.0.0.1:1903
```

Then validate remote access:

```text
https://<SERVER_HOST>:1903
```

First-run profile creation and vault unlock require browser Web Crypto. The installed server exposes the public browser entry over HTTPS on port `1903` by default, using a managed self-signed certificate until a trusted PFX/P12 is configured. Plain HTTP is only for internal upstream or local development paths and should not be documented as the operator entry point.

## Installed Surfaces

| Surface | Value |
| --- | --- |
| Windows service | `VaultPilotServer`; legacy `PassManServer` may appear only as an upgrade alias |
| Display name | `VaultPilot Server` |
| Data directory | `C:\ProgramData\VaultPilot`; legacy `C:\ProgramData\PassMan` remains an upgrade alias |
| Log directory | `C:\ProgramData\VaultPilot\logs`; legacy PassMan log paths remain upgrade aliases |
| Default port | `1903` |
| Browser entry | `https://<SERVER_HOST>:1903` with managed self-signed HTTPS until a trusted certificate is configured |

## Post-Install Validation

Run these checks before creating broad access:

```powershell
sc.exe query VaultPilotServer
```

```text
https://127.0.0.1:1903/api/profile
```

Expected result:

- The service is installed and running.
- The local API responds.
- The remote URL opens from an approved workstation.
- The firewall rule allows only the intended network path.
- No installer error remains in the VaultPilot log folder; upgraded hosts may also have legacy PassMan log evidence.

## First Login Path

After service validation:

1. Create the owner profile.
2. Unlock the vault with the master password.
3. Apply the license.
4. Configure public host and HTTPS.
5. Enable 2FA before adding additional users.

## Upgrade Notes

- Export a backup before production upgrades.
- Let the MSI update the server and support components together.
- The offline decrypter and DC agent script are refreshed by the MSI and also documented in release notes.
- Do not manually replace files under the installed server directory unless support explicitly asks for that diagnostic step.

## Upgrade From PassMan-Branded Installs

Before upgrading, export a server backup and record the current service name, data directory, port, and running version. Run the VaultPilot 2.0 MSI as Administrator. Do not manually rename `C:\ProgramData\PassMan` or existing service entries.

After upgrade, verify `VaultPilotServer`, the data directory, Update Center, extension pairing, license state, audit retention, and Server System diagnostics. Legacy PassMan aliases may remain only for compatibility and rollback.

## Public Evidence For Support

Safe to share after redaction:

- MSI filename.
- VaultPilot server version.
- Windows service status.
- Redacted installer log excerpt.
- Browser URL shape, with real host replaced by `<SERVER_HOST>`.

Do not share databases, backups, PFX/P12 files, private keys, master passwords, secret values or real internal hostnames.
