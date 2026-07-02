# Backups and Restore

VaultPilot backups contain encrypted payloads, wrapped keys, audit metadata, and an integrity manifest. They do not contain plaintext secrets or master passwords.

## Recommended Workflow

1. Export a backup before updates.
2. Store the backup outside the VaultPilot server disk.
3. Restrict access; backup metadata is sensitive.
4. Test restore in a controlled environment.

## VaultPilot Backup Tool

Run backup collection on the Windows server as Administrator. The primary packaged executable is `VaultPilotBackupTool.exe`; `PassManBackupTool.exe` remains only as a legacy upgrade/support alias.

Record the output path and keep the archive private. It can contain encrypted vault data, configuration, and certificate material. Do not attach the archive to public issues, public support threads, or this repository.

The current console can import either a VaultPilot Backup Tool ZIP archive or an encrypted JSON export from the server-backup import panel. Import rebuilds the server profile from the backup and closes active sessions, so run it only as an administrator recovery action after confirming the file source and backup purpose.

If the ZIP contains a Backup Tool database archive, VaultPilot requires the Backup Tool manifest before converting the server database into the encrypted local backup shape. Raw database files, WAL/SHM companions, customer backups and support archives still do not belong in this public repository or public issue text.

For uninstall, data retention, rollback and purge boundaries, use [Uninstall, data retention and rollback](uninstall-rollback-data-retention.md). Normal uninstall should preserve the data directory unless an explicit private purge approval exists.

## Integrity

Encrypted JSON import verifies the SHA-256 integrity manifest and item counts. ZIP archive handling rejects malformed archives, unsafe entry names and unsupported payloads before restore. If any value does not match or the source is unclear, stop the import and use a private support channel.
