# Files Screen

The topbar `?` opens this page from the Files screen. Use it only for approved encrypted attachments that have a clear owner and retention reason.

## Work Here

- Confirm the file belongs in the vault before uploading.
- Prefer small, reviewable support or recovery artifacts over broad archives.
- Name files with purpose and owner, not with secret values.

## Screen States

| State | Operator response |
| --- | --- |
| Empty | Add files only when the owner and retention reason are clear. |
| Large file | Confirm it belongs in VaultPilot rather than an approved document store. |
| Upload blocked | Check role, license and file policy before retrying. |

## Before You Act

- Confirm the file is needed in the vault and cannot be represented as a smaller typed record.
- Check file name, owner, review date and retention expectation before upload.
- Reject logs, dumps and screenshots that contain secrets unless they have been sanitized through an approved path.

## Safe Evidence

- Safe to share: file category, size band, owner/review state, retention reason and redacted validation error.
- Keep private: file contents, filenames with customer context, database dumps, logs, installers, release archives, private keys and raw screenshots.
- Move any file that contains secrets or customer evidence into private support review before discussing it publicly.

## Operator Notes

Do not store database dumps, raw logs, installers, release archives, private keys or unredacted screenshots unless an approved internal process explicitly requires it.

## Related

- [Backups and restore](backups-and-restore.md)
- [Public repository boundary](public-repository-boundary.md)
- [Support evidence pack](support-evidence-pack.md)
