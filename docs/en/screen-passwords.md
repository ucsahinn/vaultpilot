# Passwords Screen

The topbar `?` opens this context-specific guide while Passwords is active. This screen is for finding and reviewing password records in the active vault, and editing them when your access permits it. Generate, copy, and ?prepare autofill? actions here do not change the account in the target system by themselves.

## Access, Vault Role, and License

- Owner, Admin, and User system roles can use the password workspace when they have readable access to a vault. Auditors cannot enter secret workspaces.
- The active vault must be unlocked and its key available in the browser session before records can be decrypted.
- Reading requires readable vault access. Creating, duplicating, editing, deleting, and write-oriented bulk actions require **Editor** or **Manager** on the active vault and a license that is not read-only.
- A read-only license does not block listing, revealing, copying, or local breach checks, but vault-changing actions are disabled.
- A system role does not grant vault access by itself. Verify the active vault and your role on that vault before acting.

## Work Here

- Create or re-encrypt records containing a title, username or email, sign-in URL, password, and note.
- Narrow the visible set with search, quick filters, and combinable smart filters.
- Copy passwords, usernames, and URLs through separate actions in card or table view.
- Run an optional HIBP Pwned Passwords exposure check.
- Prepare selected records for Sharing or for bulk editing, reports, export, and deletion.

## Search, Filters, and View

Text search covers title, username, URL, host, domain, owner, category, source, risk, and tags. It does not search inside the password value.

Based on available data, the quick-filter band shows up to seven options drawn from **All**, **Exposed**, **Unchecked**, **Warning**, and the most common product, service, or category values. **Add smart filter** can offer username or owner, product or service, category, tag, and breach-status values. A record must match every active smart filter.

Selecting a filter chip removes only that filter; **Clear** removes all smart filters. The **All** quick filter restores the default type, risk, and smart-filter state, but you may still need to clear the search text separately.

**Cards** uses wider record cards; **Table** uses a denser layout with column headings. **Refresh** reruns the record query. Records are returned with the most recently updated first.

### Selection scope

- Individually checked records can remain selected after a filter hides them.
- **Select visible records** replaces the selection with the currently visible records; it does not preserve an older hidden selection. When all visible records are selected, **Clear selection** empties the whole selection.
- The selected count at the top counts only visible selections, while some bulk handlers use every selected ID still held in page memory. After changing filters, explicitly clear and rebuild the selection.

## Record Row Actions

The primary password-row actions are **Copy secret value** and, when a valid HTTP/HTTPS address exists, **Open site**. The secondary menu contains:

- **Prepare autofill**
- **Breach check**
- **Copy username**
- **Reveal / hide secret**
- **Copy URL**
- **Create a copy**, **Edit secret**, and **Delete secret**

**Open site** opens only a validated HTTP/HTTPS address and attempts to write a `VIEW` event. It does not sign in or fill fields on the page.

## Reveal, Copy, and Audit

**Reveal secret** first requires a warning confirmation. The value then appears in the browser card and a `VIEW` event is written. Reveal does not close on a short fixed timer. It can remain visible until you hide it, reveal another record, lock the vault, or the 15-minute inactivity lock runs.

Password, username, URL, and fill-package copies are written to the operating-system clipboard, followed by a `COPY` event. The clipboard-clear timer is 30 seconds and writes an empty value only if the clipboard still contains the same content. Browser shutdown, clipboard permissions, the operating system, or a clipboard manager can prevent clearing. Do not treat the timer as an access-revocation guarantee.

Clipboard writing and reveal happen before the audit request. If the later audit write fails, the value may still be on screen or on the clipboard. Missing audit evidence does not prove that the sensitive value was never exposed.

### ?Prepare autofill? boundary

On this screen, **Prepare autofill** copies the username and password as one tab-separated string and writes a `COPY` event. The operator pastes it into the target page's username field. This does not remotely run the browser extension and does not guarantee that fields were found, filled, or accepted. The VaultPilot Browser Vault Extension page-fill flow is a separate trust boundary.

## HIBP Breach Check

**Breach check** on a record or in the editor calculates the password's SHA-1 digest in the browser. Only the first five digest characters are sent to `api.pwnedpasswords.com/range`; the full password and full digest are not sent. Returned suffixes are compared locally, and the request uses the padding header.

The result shows **Exposed** or **Not found**, the observed count, and the check time. **Not found** does not prove that a password is strong, unique, or safe. For **Exposed**, change the real password in the owning system first, then update the vault record.

A single-record check does not write its own server audit event. Bulk **Run security check** attempts a `VIEW` event for each record successfully checked.

Without storing the password, results are kept by record ID with status, count, and time in this browser profile's `localStorage`. Another browser or cleared storage shows a different result set. A cached result may not represent a password changed elsewhere or in another session; rerun the check before relying on it.

## New Record and Editor

The **New password** editor provides required title and password fields, plus optional username or email, sign-in URL, and note. The password draft is displayed as plaintext in a text area while editing; control screen sharing and shoulder-surfing risk.

On save, the browser encrypts the record with the active vault key. A new record emits `CREATE`; an update emits `EDIT`. **Edit** moves the existing record into the New record screen. **Save** changes only the encrypted vault record, not the account in the target system.

### Password generator

The generator defaults to 24 characters. The UI offers a 12-64 character range and toggles for uppercase letters, digits, and symbols; lowercase is always included. Generation uses `crypto.getRandomValues` in the browser. Enabled classes expand the possible alphabet, but the result is not guaranteed to contain at least one character from every enabled class.

**Short**, **Ready**, and **Strong** classify length only: below 16, 16-23, and at least 24 characters. They do not verify the target system's policy, uniqueness, or breach status.

**Generate new password** on an exposed card uses the current generator settings and opens the editor with the new value. It is not written to the vault until you choose **Save**, and it never changes the target-system password automatically.

## Duplicate, Delete, Bulk Actions, and Sharing

**Create a copy** creates a new record in the same vault and adds ?copy? to its title. It does not create another account in the external system. Write access is required, and the new record leaves a `CREATE` event.

**Delete secret** requires a second confirmation for an irreversible operation and emits `DELETE` when successful. It removes only the VaultPilot record; it does not disable the target account or change its password.

The bulk menu includes Excel template/download and import, export, category or tag assignment, archive, disable, security check, audit report, share, append note, edit the first selected record, and confirmed delete.

- Category, tag, archive, disable, note, edit, import, and delete require write access.
- **Disable / revoke** changes the encrypted password-record metadata to `DISABLED`; it does not disable the target account.
- **Export selected** writes the complete decrypted records and passwords to a plaintext JSON file after a dangerous-action confirmation. Audit events are attempted afterward on a best-effort basis.
- **Add to audit report** writes record metadata, not password values, to a CSV file.
- Bulk edits and deletes process records sequentially. A failure partway through does not roll back earlier successes. Refresh and reconcile records with audit evidence before retrying.
- **Bulk share** moves selected IDs to the method step of Sharing; it does not send a package yet. Actual delivery remains subject to the Sharing feature, Manager role, writable license, and the selected delivery method's rules.

## Screen States

| State | Operator response |
| --- | --- |
| Loading records | Wait for the four skeleton rows to disappear. If needed, verify the session and use **Refresh**. |
| No records in the vault | Verify the active vault and lock state. If you have write access, start with **New password**. |
| No matching records | Clear the search text, quick filter, and smart-filter chips separately. |
| Empty list when records are expected | There is no dedicated query-error card. Check the session, server connection, active vault, and network request. |
| Read-only | Reveal and copy may remain available, but create, duplicate, edit, delete, and write-producing bulk actions are disabled. |
| Clipboard error | The value may already have been written to the clipboard. Clear it manually and check the `COPY` audit trail. |
| Reveal audit could not be written | The value may remain visible. Hide it immediately or lock the vault, then reconcile the audit trail separately. |
| Breach check unavailable | Check the network, browser policy, or HIBP access. Do not treat the result as clean. |
| Breach detected | Change the actual password in the target system, then update the vault record and check it again. |
| Bulk operation stopped partway through | Do not retry blindly. Compare the visible and hidden selection, vault state, and audit events first. |

## Before You Act

- Confirm that the active vault, record title, username, and URL belong to the same account.
- Close screen sharing and clipboard managers before reveal, copy, or plaintext export.
- If filters changed, clear hidden bulk selections and rebuild the intended scope.
- Plan to change the password in the target system first, then update the VaultPilot record.
- On Sharing, recheck the recipient, expiry, use limit, and delivery boundary before creating a package.

## Safe Evidence

- Safe to share: screen name, generic card or table view, approximate time range, record count, broad filter type, a breach state that cannot be tied to an account, generic error class, and whether the role and license are writable.
- Keep private: passwords, username-and-URL pairs, record titles, notes, vault names or IDs, exact timestamps, account-linked HIBP counts, selected record IDs, clipboard contents, plaintext JSON exports, and screenshots showing a value.
- If a password or fill package reaches a public channel, do not rely on timed clipboard clearing. Change the password in the target system, then update the vault record.

## When to Stop

Stop if the active vault is unclear, the record and target URL do not match, hidden bulk selection is possible, clipboard or screen recording is outside your control, the audit trail conflicts with the action, the breach result may be stale, a bulk operation stopped partway through, or only the vault record would change before the target system. Reconcile the scope and last safe step in a private channel before retrying.

## Operator Notes

VaultPilot stores the password record encrypted, but an unlocked browser temporarily reconstructs plaintext for reveal, edit, HIBP checks, export, and clipboard actions. The screen, clipboard, and downloaded plaintext file are separate trust boundaries. Do not report **Disable**, **New password**, or **Prepare autofill** as proof that the account changed in the target system.

## Related

- [Security and trust model](security-and-trust-model.md)
- [Sharing screen](screen-sharing.md)
- [Browser extension screen](screen-browser-extension.md)
- [Audit Log screen](screen-audit-log.md)
- [Safe support evidence](support-evidence-pack.md)
- [Operator runbook](operator-runbook.md)
