# Uninstall, Data Retention and Rollback

Use this guide when an operator needs to remove VaultPilot from a Windows host, preserve server data, or roll back after a failed upgrade. It is intentionally conservative: removal should not destroy encrypted vault data unless the operator has a separate, reviewed purge plan.

## Safety Boundary

| Area | Default |
| --- | --- |
| Service removal | Allowed through MSI maintenance or the packaged uninstall helper. |
| Data directory | Preserve by default. Do not delete `C:\ProgramData\VaultPilot` or legacy `C:\ProgramData\PassMan` during normal uninstall. |
| Backups | Export and verify before any uninstall, rollback or destructive support step. |
| Purge | Treat as destructive and require explicit operator approval outside this public doc. |
| Evidence | Share only redacted service state, version, logs and error text. Never share databases, backups, PFX/P12 packages, private keys or master passwords. |

## Before Uninstall Or Rollback

1. Record the installed version, service name, public host and public HTTPS port.
2. Export an encrypted backup and store it outside the server disk.
3. Confirm the backup imports in a clean validation profile or staging host.
4. Record whether the data path is `C:\ProgramData\VaultPilot` or a legacy `C:\ProgramData\PassMan` compatibility path.
5. Download the target signed MSI or rollback package only from GitHub Releases.
6. Verify the package name, signer, SHA-256 and manifest before running it.

## Normal Uninstall With Data Preserved

1. Open Windows Apps and Features or run the same MSI in maintenance mode.
2. Choose Remove only when a verified backup exists.
3. Let MSI maintenance remove the Windows service, firewall rule and installed server files.
4. Preserve the data directory unless a separate purge has been approved.
5. Confirm the service is gone:

```powershell
sc.exe query VaultPilotServer
```

The query may report that the service does not exist. That is expected after uninstall. Do not attach raw logs if they can contain private host names or support context.

## Rollback Path

Rollback is a controlled recovery action, not a normal update flow.

1. Stop broad user access to the server.
2. Preserve the current data directory and export a fresh backup if the UI is still reachable.
3. Download the previous signed MSI from GitHub Releases.
4. Verify the previous MSI and its manifest evidence.
5. Run the previous MSI as Administrator.
6. Confirm the service starts and the browser opens `https://<SERVER_HOST>:1903` or the configured public HTTPS port.
7. Validate owner unlock, license state, audit visibility, extension pairing and Update Center state before reopening access.

If rollback fails, stop and collect a redacted support evidence pack. Do not manually edit the SQLite database or key material.

## Data Purge Boundary

Public docs do not provide a copy-paste purge command. Deleting the data directory can permanently remove encrypted vault payloads, wrapped keys, audit metadata, license state, server settings and certificate material. A purge decision should be made in a private operational change record with backup proof and explicit approval.

## Restore Drill

Test restore separately from uninstall:

1. Use a clean validation host or profile.
2. Import the encrypted backup.
3. Confirm item counts, integrity manifest, owner unlock and audit visibility.
4. Record only redacted proof that the restore worked.

Related:

- [Backups and restore](backups-and-restore.md)
- [Windows Server installation](install-windows-server.md)
- [Release asset verification](release-asset-verification.md)
- [Support evidence pack](support-evidence-pack.md)
