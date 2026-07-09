# External share package fails to open

Use this when the offline share decrypter rejects a package, reports a passphrase problem, refuses metadata, or opens but does not reveal the expected records. External share packages are designed for limited, offline access; diagnose package integrity and recipient handling before recreating a share.

## Triage

1. Open [Sharing](../../docs/en/screen-sharing.md) and confirm the package was created from the intended records only.
2. Confirm the package JSON was not edited, reformatted by chat software, renamed into another format or pasted into a document.
3. Confirm the passphrase came from the one-time display and was transferred through a different channel than the package.
4. Check expiry, maximum opens and whether the package was already consumed.
5. Confirm the recipient browser supports Web Crypto and is not blocking local file execution.
6. If the recipient still cannot open it, revoke the old share and create a new package with a narrower record set.

## Error Types

| Error | Likely cause | Operator action |
| --- | --- | --- |
| Wrong passphrase | Transcription, whitespace or wrong recipient message | Re-send the passphrase privately; do not put it beside the package. |
| Tampered metadata | Package content changed after export | Revoke and recreate the package from VaultPilot. |
| Expired package | Time window passed | Create a new package with a justified expiry window. |
| Exhausted usage count | Maximum opens reached | Check recipient handling before issuing a replacement. |
| Unsupported version | Old decrypter or future package format | Use the decrypter linked from the same release context as the package. |

## Safe Evidence

- Package creation time, expiry and max-open policy.
- Decrypter error category and browser family.
- Whether the package was transferred as an attached `.json` file.
- Share id placeholder such as `<SHARE_ID>`, not package contents.
- Confirmation that the passphrase was not sent in the same channel.

## Do Not Send

Do not send package JSON, passphrases, recipient identities, record names, screenshots of decrypted content or private links to public support channels.

Related: [Sharing screen](../../docs/en/screen-sharing.md), [Sharing and offline decrypter](../../docs/en/sharing-and-offline-decrypter.md), [Support evidence pack](../../docs/en/support-evidence-pack.md), [Public issue redaction](public-issue-redaction.md).
