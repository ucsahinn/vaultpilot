# Backups and Restore

VaultPilot backups contain encrypted payloads, wrapped keys, audit metadata, and an integrity manifest. They do not contain plaintext secrets or master passwords.

## Recommended Workflow

1. Export a backup before updates.
2. Store the backup outside the VaultPilot server disk.
3. Restrict access; backup metadata is sensitive.
4. Test restore in a controlled environment.

## VaultPilot Backup Tool

Run backup collection on the Windows server as Administrator. The packaged executable is currently `PassManBackupTool.exe`, but the tool identifies itself as VaultPilot Backup Tool for the 2.0 line.

Record the output path and keep the archive private. It can contain encrypted vault data, configuration, and certificate material. Do not attach the archive to public issues, public support threads, or this repository.

Restore and import remain an administrator/support procedure. Do not document or run a public restore command until the exact supported restore path is release-verified.

For uninstall, data retention, rollback and purge boundaries, use [Uninstall, data retention and rollback](uninstall-rollback-data-retention.md). Normal uninstall should preserve the data directory unless an explicit private purge approval exists.

## Integrity

Import verifies the SHA-256 integrity manifest and item counts. If the values do not match, stop the import.
