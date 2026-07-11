# Files Screen

The topbar `?` opens this guide from the **Files** screen. This screen manages `FILE` records in the active vault; it is not a general document archive, network share, or cloud-storage client.

## Access and License Boundary

The Files screen is available to non-Auditor system roles only for assigned vaults that are unlocked in the browser session. The **Viewer**, **Editor**, and **Manager** vault roles can list and download file records. The Auditor system role has no secret-record or vault-key access.

Creating a new file, replacing a file, creating a copy, editing record details, or deleting requires a writable license and the **Editor** or **Manager** role on the active vault. The Viewer role and a read-only license block these writes but do not block downloading an existing file. Files has no separate license module. **Bulk share** opens a different workflow where the **Sharing** license capability and the Sharing screen's narrower role checks also apply.

## Work Here

- Use **Search files** to search file records in the active vault.
- Use **Add smart filter** to combine imported, warning, category, tag, or product matches.
- Return to the **All** quick filter, choose **Cards** or **Table**, and use **Refresh** to reload the vault list.
- If you have write access, use **New file** to create an encrypted file record.
- Review the file name, size, chunk count, shortened SHA-256 hash, and last-updated time on a row.
- Use **Download file** to decrypt the chunks in the browser and download the file.
- Use **VirusTotal hash lookup** to search only the file hash on VirusTotal.
- Open **More actions** to **Create a copy**, **Edit secret**, or **Delete secret**.
- Select rows and use **Bulk actions** for operations that apply to file records.

## File Size, Chunks, and Encryption Boundary

A selected file cannot exceed 1 GB. The server also limits the encrypted file chunks written by the current user to 1 GB per user and vault. A file smaller than 1 GB can therefore still be rejected when available space is insufficient. Files does not display the exact remaining amount; the server enforces the limit while chunks are written.

VaultPilot processes a file as up to 512 chunks of 2 MB each. SHA-256 is calculated in the browser during save, and every chunk is encrypted in the browser with the active vault key. The server stores encrypted chunks, chunk order, and size data required for quota enforcement. It does not move the contents into a separate cloud object store or retain a plaintext server-side file.

The chunk count and size shown on a row are record metadata. The shortened SHA-256 value helps identify a file; it does not make confidential file contents safe to disclose.

## Create a New File

1. Confirm that the intended writable vault is active.
2. Choose **New file**.
3. Enter the required **Title**.
4. Optionally complete **Owner or recipient**, **Related system or ticket**, and **File note**.
5. Choose one file with **Select file**. The screen shows its name, size, and calculated chunk count; if Title is empty, the file name becomes the title.
6. Choose **Save encrypted record**. Progress first covers the record payload, then encryption and upload of the file chunks.
7. When the operation completes, verify the file name, size, chunk count, and SHA-256 value in Files.

A file selection is required for a new record. A file over 1 GB is cleared from the form. Saving also fails when the vault is locked, the role cannot write, the license is read-only, or the user/vault quota is full.

## Edit, Replace, Copy, and Delete

**Edit secret** opens the current title, owner, related-system, and note details. Replacing the attachment is optional. If you choose a new file under **Replace file**, VaultPilot re-encrypts the record metadata, clears the old chunks, and uploads the new file in 2 MB chunks. Do not leave the page while save is in progress.

**Create a copy** is not a clipboard action. VaultPilot decrypts the source chunks in the browser with the active vault key, re-encrypts them for a new record, and creates a separate file record in the same vault. A copy is not created when source chunks are incomplete; VaultPilot attempts to clean up an incomplete new copy record.

**Delete secret** permanently removes the file record and its encrypted chunks from the server vault after confirmation. It cannot be undone. Bulk delete also requires confirmation; if a batch partly fails, refresh and reassess the records that remain.

## Download, Reveal, Copy, and Audit Behavior

File rows do not offer **Reveal secret** or **Copy secret value**. File contents are not exposed in the row or placed on the clipboard. **Download file** requests the encrypted chunks in order, verifies the expected count, decrypts them in the browser with the active vault key, and hands the reconstructed file to the browser download flow. The vault must be unlocked.

The server writes an `EXPORT` Audit event when it successfully returns the file-chunk list, before the UI verifies the expected count, decrypts the chunks, or starts the browser download. An `EXPORT` event can therefore exist when chunks are incomplete, browser decryption or download later fails, or **Create a copy** stops after its source-chunk preflight. Share preparation also lists source chunks, so it can write the same event even when package creation later fails.

**VirusTotal hash lookup** does not upload the file; it opens `https://www.virustotal.com/gui/file/{sha256}` in a new tab and attempts to write a `VIEW` Audit event. This sends the SHA-256 hash to a third-party service; do not use it when organizational policy forbids that disclosure.

A new file record normally produces two Audit events: `IMPORT` for record creation and `EDIT` when the existing chunk set is cleared before upload. Replacing a file can produce one `EDIT` for the record update and a second `EDIT` for clearing the old chunks. Deletion is recorded as `DELETE`. During copy, listing source chunks writes `EXPORT`, while writing the new record and chunks produces `IMPORT` and `EDIT`. Copying a file name or visible metadata through operating-system selection does not create a separate VaultPilot Audit event.

## Sharing and Bulk Actions

In a writable vault, **Select visible records** selects only file records in the current search and filter. When all visible records are selected, the button becomes **Clear selection** and clears them. For a Viewer or in read-only mode, file records are excluded from the bulk-visible selection set, so this button is disabled; row checkboxes remain visible and files can still be selected individually. Clear those selections by unchecking each row.

The file-screen bulk menu can include:

- **Export selected** writes record payloads to JSON after a sensitive-action confirmation and creates an `EXPORT` event for each record. For a file record, this contains title, notes, and file metadata; it does not contain the encrypted chunks or replace **Download file**.
- **Assign category**, **Assign tags**, **Archive selected**, **Disable / revoke**, **Append note**, **Edit selected**, and **Remove with confirmation** require a writable vault.
- **Add to audit report** writes only generic record fields to CSV: title, type, source, status, risk, owner, category, tags, updated time, and directory fields that are empty for file records. It does not include file name, size, chunk count, SHA-256, or file content.
- **Run security check** is not an antivirus or malware scan for files. File records have no copyable secret value, so this action does not scan binary file content.
- **Import from Excel** is the generic record-template workflow, not a multi-file binary uploader. Use **New file** to create an encrypted attachment.
- **Bulk share** carries the selected records into **Sharing**. No package is sent until recipient, expiry, and use limits are confirmed there.

Internal sharing requires the **Manager** role on the active vault, user-management permission, and a writable license. In an internal bundle, selected files cannot total more than 1 GB or 512 chunks. An external share package requires the **Manager** vault role and a writable license; it has no separate aggregate chunk-count cap, but the package still has the 1 GB total limit and each source file remains subject to the 1 GB/512-chunk file limit. In both methods, file chunks are opened in the browser and re-encrypted with the share key; this does not make the original vault record public.

## Recommended Workflows

### Add a new encrypted file

1. Confirm the intended vault and the Editor or Manager role.
2. Check the file size, owner, and retention reason. Files does not show the exact remaining amount, so leave headroom under the 1 GB per-user/vault limit.
3. Prepare the record with **New file** and wait for save progress to finish.
4. Verify name, size, chunk count, and SHA-256 in the list.
5. Confirm the normal `IMPORT` record-creation event and chunk-clear `EDIT` event in Audit.

### Download a file safely

1. Match the file name, size, and shortened SHA-256 to the expected record.
2. Choose **Download file**.
3. If no incomplete-chunk warning appears, move the download to an approved location.
4. When required, compare a local SHA-256 value and confirm the `EXPORT` Audit event. This proves that chunks were listed, not that the browser download completed.

### Replace a file

1. Open the intended record with **Edit secret**.
2. Choose **Replace file** and check the new name, size, and chunk count.
3. Save the encrypted update without closing the tab during progress.
4. Verify the new chunks with a download test and the two possible `EDIT` events in Audit.

## Screen States

| State | Operator response |
| --- | --- |
| Files loading | Wait for the skeleton rows before creating, downloading, or running bulk actions. |
| No records in this vault | If you can write, choose **New file** and confirm the file belongs in this vault. |
| No search or filter matches | Change the query, clear active smart filters, or return to **All**. |
| Viewer / read-only | Download remains available; create, replace, copy, edit, delete, and share creation are blocked. **Select visible records** is disabled, but row checkboxes can be used individually. |
| No file selected | On a new record, choose one file with **Select file** before saving. |
| 1 GB limit or quota exceeded | Reduce file size or per-user/vault usage. Files does not show the exact remaining amount; the server enforces the limit. |
| Encrypting and uploading chunks | Do not refresh the page or close the tab until progress completes. |
| File chunks incomplete | Refresh the vault; if it persists, edit the record and replace the file. Do not copy or share the incomplete record. |
| File download failed | Check that the vault is unlocked, the role has access, and chunks are complete, then refresh once. |
| No records selected for bulk action | Select at least one visible file record first. |
| Share is preparing file attachments | Do not download, copy, or send the package before all chunks are ready. |

## Before You Act

- Confirm the correct server profile, vault, and file record.
- For create or replace, verify the active vault role is Editor or Manager and the license is writable.
- Confirm file ownership, retention and destruction expectations, related ticket, and file name.
- Check that the file is no larger than 1 GB. Because exact remaining space is not displayed, leave headroom under the user/vault limit and let the server make the final enforcement decision.
- Apply data-classification and retention policy before storing logs, database dumps, private keys, certificate bundles, or screenshots.
- Confirm that the download target, sharing recipient, and third-party hash lookup such as VirusTotal are allowed by policy.
- Before replacement or deletion, confirm that any required approved recovery copy exists.

## Safe Evidence

- Safe to share: screen state, general error class, rounded size band, chunk count, role/license mode, and operation time with no confidential context.
- Keep private: file contents, full file name, full SHA-256 hash, record ID, owner or recipient, internal system or ticket URL, vault name, notes, customer context, and local download path.
- When sending `IMPORT`, `EDIT`, `EXPORT`, `VIEW`, or `DELETE` evidence, redact the user, target ID, correlated timestamps, and integrity hashes as required.
- Never upload raw logs, database dumps, private keys, signing material, installers, release archives, or unredacted screenshots to a public support channel.
- If a hash was sent to a third-party lookup, record that fact in the evidence package; do not imply the file itself was uploaded.

## When to Stop and Escalate

Stop if the expected file name, size, or SHA-256 changes; chunks remain incomplete; encryption/upload progress never completes; a deleted record returns; per-user/vault usage is unexpectedly full; an expected Audit event is absent; or the wrong file was downloaded, copied, or added to a share. Open a private support case with no file content and include the screen state, redacted record ID, general size, chunk count, last safe step, time, and error text.

## Operator Notes

Files does not automatically classify content, scan it for malware, or delete it when a retention period expires. **VirusTotal hash lookup** is only an external hash query. The operator remains responsible for data ownership, retention policy, a safe download destination, and permanent deletion when required.

## Related

- [New record screen](screen-new-item.md)
- [Sharing screen](screen-sharing.md)
- [Audit Log screen](screen-audit-log.md)
- [Backups and restore](backups-and-restore.md)
- [Public repository boundary](public-repository-boundary.md)
- [Support evidence pack](support-evidence-pack.md)
