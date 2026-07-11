# Server Settings Screen

The topbar `?` opens this guide while a system Server settings tab is active. On **Sign-in security**, the same button opens the separate personal-security guide.

Use Server settings to define the public HTTPS address, configure the SMTP delivery channel, import recovery or migration data, queue a controlled service restart, and back up, clear, or restore selected operational history. This screen does not provide controls for changing log rotation, log retention, or audit-retention values.

## Access and Authority

- Owner, Admin, and Auditor roles can read the three system tabs. A User is directed to personal **Sign-in security** instead.
- Only an Owner can save Access or SMTP settings, upload a certificate, send an SMTP test, import a server backup, restart the service, or run and restore maintenance backups.
- A read-only license does not disable these Owner-only server routes. It does block migration into a vault because that flow requires an unlocked writable vault and **Editor** or **Manager** access.
- Admin and Auditor views are observational. Disabled controls do not grant a way around the server-side Owner check.

## Access & HTTPS

**Public address or domain** and **Public port** describe the address users should open. The server normalizes the host and always constructs an HTTPS URL. There is no HTTP/HTTPS toggle on this screen.

Choose one certificate source:

- **Automatic certificate** keeps the managed-server certificate source.
- **Enterprise certificate** accepts a `.pfx` or `.p12` file up to 2 MiB. Saving uploads it into the server-managed certificate directory and records the managed path in settings.

The upload control does not ask for a certificate password and does not prove the issuer, trust chain, expiry, private-key presence, hostname match, or runtime handshake. Validate the package outside public channels and verify the resulting HTTPS endpoint after restart.

Changing the public address, port, or enterprise certificate can interrupt browser access after restart. Keep the current working URL and an approved console or server recovery route available before saving.

## SMTP

**SMTP enabled** exposes account name, host, port, sender email, TLS/STARTTLS, authentication, username, and password-or-token fields. **SMTP disabled** pauses email delivery while in-app notifications and audit logging continue; saved SMTP details remain unless authentication is explicitly turned off and the form is saved.

Important boundaries:

- SMTP host is a hostname only. Do not enter a URL, credentials, a port, a path, or query data in that field.
- When authentication is enabled, TLS/STARTTLS, a username, and either a new or already-saved password/token are required.
- A blank password field preserves an already configured credential. The UI never reads the saved secret back.
- Recipients and event rules are managed on **Notifications**, not on this tab. Enabling SMTP requires at least one recipient and one notification event.
- **Send test** uses the values currently visible on the screen before they are saved. It requires a test recipient and does not persist the draft.
- A successful test writes a `SERVER_MAINTENANCE` event with operation `SMTP_TEST_EMAIL_SEND`. The password or token is not included in audit metadata.

## Shared Save and Reset Behavior

Access and SMTP look like separate tabs, but they share one form and one draft:

- **Save settings** submits the public address, certificate selection, SMTP configuration, and the already-loaded hidden log-policy values together.
- An incomplete enabled SMTP configuration can therefore block a save started from **Access & HTTPS**. An invalid public host or port can block a save started from **SMTP**.
- **Reset form** discards the unsaved draft across both tabs and reloads the last settings returned by the server. It is not a server rollback.
- The Operations tab runs its own actions and has no Save or Reset footer.
- Save success means the settings file was written. The UI instructs the operator to restart before relying on new values.

If an enterprise certificate was selected, its upload happens before the settings save. A later validation, persistence, or audit failure can leave the uploaded file on the server even when the overall action reports an error. Re-read Server settings and inspect the certificate audit event before trying again.

## Maintenance & Logs

This tab shows the current database path, database-protection status, and service log path. These are diagnostic values, not editable fields. The current UI does not expose log-size, log-package, log-retention, or audit-retention controls.

### Import server backup

**Import server backup** accepts a VaultPilot Backup Tool ZIP archive or encrypted JSON export. It is a whole-profile recovery operation, not a merge:

- The Owner confirms the operation before upload.
- Integrity and authenticity information is checked. A legacy or foreign backup requires a separate downgrade confirmation.
- The existing organization, users, vaults, encrypted records, file chunks, and audit history are replaced inside one database transaction.
- Imported 2FA bindings are cleared. After import, all persistent sessions are closed and the operator must unlock with the master password from the backup profile.
- The restored profile receives an `IMPORT` audit event describing counts and whether authenticity was downgraded.

There is no browser-console button here to create or export a full server backup. Create that recovery artifact with VaultPilot Backup Tool.

### Import & migration

**Choose export file** reads supported exports in the browser and opens a preview on the Passwords screen. Bitwarden CSV/JSON, LastPass CSV, KeePass XML/CSV, 1Password CSV, and Chrome/Edge CSV are represented. A `.1pux` archive is not imported; use the 1Password CSV export. **VaultPilot template** downloads the product template.

Preview is not persistence. The final import requires an unlocked active vault, a writable license, and Editor or Manager access. Rows are then created or updated sequentially according to the chosen conflict rule, so a later row can fail after earlier rows were committed. Reconcile the result counts and record-level audit events before retrying.

### Restart server service

**Restart** is enabled only for an Owner with no unsaved Server settings draft. After warning confirmation, the app queues a restart of `VaultPilotServer` or the legacy `PassManServer` service. It does not wait for a completed health check. The console may disconnect briefly, and only saved settings are eligible to take effect.

The queue action writes `SERVER_RESTART` with operation `SERVER_RESTART_QUEUE`. Verify the service, effective HTTPS URL, and a fresh sign-in after connectivity returns.

### Maintenance records

The only cleanup mode exposed is **Back up & clear**. It works on one category at a time:

| Category | Scope |
| --- | --- |
| Audit log | Audit screen history, chain-check records, and dashboard audit history. |
| Discovery | Discovery jobs, findings, suppressions, and scan policies. |
| Executions | Execution history and finished background jobs; active executions and running jobs are retained. |

After warning confirmation, VaultPilot writes a durable JSON backup under the server's `maintenance-backups` directory, records its count and SHA-256 digest, and then clears that category. Vault secrets, source files, service log files, and the other maintenance categories are not part of this cleanup.

The archive table shows file name, category, creation time, record count, size, digest, and **Restore**. Restore replaces only the selected category with its backup state. Live records created after that backup can change or be lost; other categories remain unchanged. Both cleanup and restore write `SERVER_MAINTENANCE` evidence with operation, category, counts, backup file name, and digest.

## Sign-in Security Context

**Sign-in security** is a personal-security panel embedded in the Server settings shell, but it is not part of the shared server-settings form. It manages the current user's master password and 2FA binding. Only an Owner additionally sees the active-session table and can revoke non-current sessions.

While this tab is active, the topbar `?` intentionally opens [Sign-in security](screen-sign-in-security.md), not this page.

## Audit and Partial-Completion Boundary

These routes perform the operational side effect before all follow-up evidence has necessarily been written. An error response does not always mean that nothing happened:

- A certificate file can be stored before the settings save completes.
- Settings can be written before their audit event is appended.
- A test email can be delivered before its audit event is appended.
- A service restart can be queued before its audit event is appended.
- A maintenance backup and category clear or restore can finish before the final maintenance event is appended.
- A profile import can replace the database before session cleanup completes.
- A migration import can commit some rows before another row fails.

After an ambiguous error, do not immediately repeat the action. Refresh the relevant screen, check the effective state, review the audit and operation logs, and reconcile any durable backup entry first.

## Screen States

| State | Operator response |
| --- | --- |
| Waiting for server API | Wait for diagnostics to load. If it persists, verify the current session and server reachability. |
| Current | The loaded draft matches the saved settings returned by the server. This is not proof that an external HTTPS or SMTP endpoint works. |
| Unsaved change | Save or reset before leaving the task. Remember that the draft spans Access and SMTP. |
| Restart after save / Restart required | Preserve a working recovery route, save first, then use the Operations restart action in an approved window. |
| SMTP disabled | Email is paused; in-app notifications and audit logging continue. |
| Password saved / No password | A credential is present or absent on the server. The saved value is never displayed. |
| Test sending | Wait for the result and confirm the destination mailbox before sending another test. |
| Owner role required | Continue read-only review or transfer the change to an Owner. |
| Reading maintenance archive | Wait for the durable server-side archive list. Do not infer that no backup exists yet. |
| No maintenance backup | Run **Back up & clear** only if clearing the selected category is actually intended. |
| Category maintenance running | Do not start another maintenance category or restart the service. |
| Importing backup | Keep the browser and server available; do not refresh, restart, or upload the file again. |
| Action returned an error | Verify whether the side effect already occurred before retrying. |

## Before You Act

- Confirm the active role, license state, tab, and exact intended scope.
- For Access changes, record the current working URL and arrange server-console access before restart.
- Validate an enterprise certificate's origin, hostname coverage, expiry, private key, and recovery copy outside the browser console.
- For SMTP, confirm the sender, test recipient, recipient list, event rules, and whether the blank password field should preserve the saved credential.
- Use VaultPilot Backup Tool to create a full recovery backup before whole-profile import or other high-impact server work.
- Before maintenance cleanup, name the category, capture its visible count, and confirm that the automatic maintenance backup?not a full profile backup?is the intended recovery scope.
- Before restore, compare the backup category, creation time, record count, and digest, and identify newer records that can be replaced.
- Before migration, unlock the intended vault, clear unrelated selections, choose the conflict rule, and review every invalid or duplicate row.

## Safe Evidence

- Safe to share: the tab name, general state, broad time window, redacted host such as `<SERVER_HOST>`, public port, certificate source and file extension, SMTP enabled/TLS/auth flags, recipient and event counts, maintenance category, and aggregate success/failure counts.
- Keep private: exact internal hostnames or IP addresses, database and log paths, PFX/P12 contents, certificate passwords or private keys, SMTP username/password/token, sender and recipient addresses, session IDs, backup ZIP/JSON files, migration exports, record names, raw logs, and copied audit metadata containing customer context.
- Share exact backup file names or full digests only through the approved private support channel when they are needed for reconciliation.

## When to Stop

Stop if the current working URL is not recorded, server-console recovery is unavailable, certificate ownership or private-key coverage is unclear, SMTP would send to an unapproved recipient, the active vault or conflict rule is uncertain, a backup category or timestamp does not match the intended restore, the maintenance archive cannot be read, newer category records have not been assessed, or any previous attempt returned an ambiguous error. Reconcile the last durable state before continuing.

## Operator Notes

Do not describe Save as an immediate runtime change, Restart as a completed health check, SMTP test failure as proof that no message was delivered, maintenance backup as a full vault backup, migration preview as a completed import, or category restore as a whole-server rollback. Never publish certificate packages, credentials, recovery archives, local paths, or raw logs.

## Related

- [Server System](server-system.md)
- [Public host and HTTPS](public-host-https-certificate.md)
- [Sign-in security](screen-sign-in-security.md)
- [Notifications screen](screen-notifications.md)
- [Audit Log screen](screen-audit-log.md)
- [Safe support evidence](support-evidence-pack.md)
- [Server settings restart and maintenance KB](../../kb/en/server-settings-restart-maintenance.md)
- [Backup import fails](../../kb/en/backup-import-fails.md)
