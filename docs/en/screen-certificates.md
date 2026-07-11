# Certificates Screen

The topbar `?` opens this guide for the Certificates screen. This workspace manages certificate, certificate-package, and private-key records in the selected vault. It does not install or replace the VaultPilot server?s HTTPS certificate; the live public certificate is managed through the separate flow in **Server settings**.

Auditors cannot access secret records or vault keys. Owner, Admin, and User accounts can use only vaults assigned to them. A **Viewer** in the selected vault can read records, temporarily reveal or copy secret material, and download an original file when one exists. Vault **Editors** and **Managers** can create, duplicate, edit, and delete records while the license remains writable.

## Work Here

- Use **Search certificates** across title, owner/service, endpoint, category, tags, issuer, Subject/CN, and serial number.
- Combine the **Renewal**, **Expired**, **No date**, and **Revoked** quick filters with smart filters such as validity window, certificate authority, and organization. A quick-filter chip appears only when its matching record count is greater than zero.
- Switch between card and table layouts, and use Refresh to query the selected vault again.
- When you have write access, choose **New certificate** to open the editor; use **Import certificate file** there or paste certificate/private-key material.
- Use row actions to reveal secret material, download the original file, or open the menu for certificate details, copy secret value, duplicate, edit, and delete.

## How to Read the Screen

A list row shows the title and last-updated time. Imported records may also show file name, format, size, remaining validity, Subject/CN, issuer, and a short SHA-256 prefix. These values identify the record after the vault is unlocked; they are metadata, not the certificate body, private key, or package contents.

**View certificate details** opens a side panel with context such as source, risk, record state, account/service, target, category, owner, tags, and last update. It does not expose secret material or the original file, and opening it alone does not write a `VIEW` audit event.

After confirmation, the eye button first displays the material in the browser session and then attempts to write a `VIEW` event. **Copy secret value** first places the entire secret field on the clipboard and then attempts to write a `COPY` event. **Download certificate file** is enabled only when a downloadable original exists; it first downloads the file and then attempts to write an `EXPORT` event. If the server rejects the audit request, it cannot undo a completed local reveal, copy, or download; the UI may report an error and the operator must reconcile the result with the audit log. Hiding masks the value again.

### Metadata and secret-material boundary

Title, owner/service, endpoint, note, expiry date, Subject/CN, and certificate-authority classification are record context visible after the vault is unlocked. They are also stored inside the encrypted record payload, but viewing them does not require a separate reveal confirmation.

The **Certificate or private key** field is the required secret value and remains masked by default. Importing a file puts both its original bytes and prepared material inside the encrypted record payload. This screen has no separate PFX/P12 passphrase field. Do not put a package passphrase in title, owner/service, endpoint, or note; use a separate password record when it must be retained.

Certificate-authority cards show the provider name, signal description, and access-mode label. Selecting one replaces any recognized CA tag, sets category to `Certificate`, defaults an empty source to `manual`, and adds both the `certificate` tag and the selected authority tag. Selecting DigiCert, GoDaddy, GlobalSign, Let?s Encrypt, Microsoft CA, or Self-signed does not connect to an external service or start issuance, renewal, rekey, or revocation.

## Recommended Workflows

### Create a record from a certificate file

1. Unlock an assigned vault where you have write access and choose **New certificate**.
2. Enter the required title, then add owner/service and endpoint as record context.
3. Use **Import certificate file** to select PEM, CRT, CER, DER, P7B/P7C, PFX/P12, PKCS12, P8/P8E/PK8, or KEY. The file limit is 10 MB.
4. Review file name, format, size, import time, SHA-256, and any detected validity or Subject values.
5. Correct **Expiry date** and **Subject / CN** when needed, then choose the certificate-authority classification.
6. Confirm that the secret field contains the intended material and save the record.

For text files, Subject, issuer, serial number, and expiry can be extracted only from recognizable lines. Binary packages may not populate these fields automatically. Missing metadata does not by itself prove that a package is invalid; verify its source privately.

### Add material manually or update a record

Without choosing a file, enter a title and paste PEM, certificate body, or private-key material into the required secret field. Expiry date and Subject/CN can be entered manually. A manual record has no downloadable original; if download is required, open **Edit** and re-import the authorized source file.

For renewal review, check **Renewal**, **Expired**, and **No date** first, then add a validity-window or certificate-authority filter when needed. Complete renewal through the certificate authority or organizational process. When the new file is ready, update the existing record through **Edit**; the classification card does not renew anything.

### Reveal, copy, or download material

Reveal only when needed and after stopping screen sharing. The 30-second clipboard cleanup is best effort: VaultPilot can read and clear the clipboard only when permissions allow, and only if the same copied value is still present. A permission failure or a different intervening value prevents cleanup; it does not retract the earlier copy. A disabled download button means the record may contain manually entered material or a legacy package without a downloadable original. Re-import the authorized source file; do not assume the screen can convert packages or unlock a package passphrase.

## Screen States

| State | Operator response |
| --- | --- |
| Loading | Wait for skeleton rows before interpreting results. |
| No records | If you have write access, create the first record; otherwise confirm the vault and role. |
| No matches | Clear search and active smart filters. |
| Valid | Still verify remaining term, endpoint, and renewal owner. |
| Renewal window | Put records with 30 days or less into the organization?s renewal process. |
| Expired | Do not distribute the material; verify source state and its replacement. |
| No date | Complete expiry from an authoritative source; do not treat missing as unlimited validity. |
| Revoked / disabled | Do not use the record as an active certificate; reconcile it with the source system. |
| Reading certificate | Wait for import to finish before saving or choosing another file. |
| Too large / unreadable | Confirm the 10 MB limit and a supported format; do not upload the file publicly. |
| Download disabled | No downloadable original is stored; re-import from the authorized source if needed. |
| Write disabled | Check vault role and license read-only state. |

## Before You Act

- Confirm the selected vault and that your vault role permits the intended operation.
- Confirm the license is not read-only before writing a record.
- Decide whether the task targets a vault record or the live server HTTPS certificate.
- Verify file source, expected SHA-256, Subject/CN, issuer, and expiry through a trusted channel.
- Account for `VIEW`, `COPY`, and `EXPORT` audit events requested by reveal, copy, and download respectively.
- Confirm that bulk category, tag, archive, disable/revoke, note, edit, and delete actions require Editor or Manager vault access.

## Safe Evidence

- **Safe to share:** certificate state class, broad validity window, file format and size, certificate-authority class, and a short SHA-256 prefix.
- **Keep private:** certificate or private-key material, original PEM/KEY/PFX/P12 package, package passphrase, full serial number and fingerprint, internal system name, complete Subject/issuer values, customer endpoint, and unmasked record screenshots.
- Mask title, owner/service, URL, Subject/CN, issuer, and full SHA-256 in screenshots sent to support.
- If a private key or package passphrase is exposed, stop copying or repackaging it and start the organization?s incident-response and certificate-authority process privately.

## When to Stop and Escalate

Stop when the file?s SHA-256 differs from the expected value, Subject/issuer or expiry differs from the source record, the original file cannot be traced to an authorized source, secret material was shown to the wrong person, or a vault record is being mistaken for the live server certificate. Open a private support case with record ID, broad format and size, short SHA-256 prefix, redacted error, and attempted steps?never the secret material.

## Operator Notes

A vault certificate record is not a deployment tool or certificate-authority client. Importing a file does not change the VaultPilot server?s HTTPS binding; the live public certificate is managed only through **Server settings**. Renewal, certificate-authority, and deployment notes are operational context, not automatic actions.

## Related

- [Certificate dashboard screen](screen-certificate-dashboard.md)
- [Server settings screen](screen-server-settings.md)
- [Public address and HTTPS](public-host-https-certificate.md)
