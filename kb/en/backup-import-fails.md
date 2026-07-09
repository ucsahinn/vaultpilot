# Backup Import Fails Or Closes Sessions

Use this when a VaultPilot backup import fails, returns an archive error, rejects an oversized upload, or succeeds but active sessions are closed.

## First Checks

| Check | Healthy result |
| --- | --- |
| Operator role | Import is started by an Owner. |
| File source | The file is an approved VaultPilot Backup Tool ZIP archive or encrypted JSON export. |
| Upload size | JSON and multipart ZIP uploads are no more than `512,000,000` bytes. |
| Multipart upload | The browser sends `Content-Length`; retry through the UI if the request lacks it. |
| Archive shape | ZIP archive has at most `64` entries and no more than `512,000,000` uncompressed bytes total. |

## What The Errors Usually Mean

| Error | Meaning | Operator action |
| --- | --- | --- |
| `PAYLOAD_TOO_LARGE` | The upload exceeds the route limit. | Confirm the file source and size; do not split or edit the archive manually. |
| `CONTENT_LENGTH_REQUIRED` | Multipart upload did not include `Content-Length`. | Retry through the VaultPilot UI or an approved browser path. |
| `BACKUP_ARCHIVE_INVALID` | Archive content is malformed, unsafe, empty, has too many entries, or exceeds ZIP processing limits. | Stop and verify the backup was produced by the approved tool. |
| `BACKUP_ARCHIVE_UNSUPPORTED` | No supported VaultPilot backup payload was found in the archive. | Use the correct backup export or Backup Tool archive. |

## Successful Import Side Effect

A successful import rebuilds the server profile from the backup and closes all active sessions. Users must sign in again through the canonical VaultPilot URL after the import completes.

## Safe Evidence

Send privately after redaction:

- VaultPilot version.
- Backup file type: ZIP archive or encrypted JSON export.
- File size rounded to the nearest MB.
- Exact non-secret error code from the UI or log.
- Whether the import reached profile rebuild and session close.
- Timestamp and server role context.

Do not send backup archives, encrypted JSON exports, raw database files, WAL/SHM files, certificate packages, private keys, master passwords, logs with secrets, or screenshots showing real vault records.

Related:

- [Backups and restore](../../docs/en/backups-and-restore.md)
- [Support evidence pack](../../docs/en/support-evidence-pack.md)
- [Public repository boundary](../../docs/en/public-repository-boundary.md)
