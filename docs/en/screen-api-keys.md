# API Keys Screen

The topbar `?` opens this context-specific guide while the API Keys workspace is active. Use this screen to find, review, and?when your access permits?update service keys, access tokens, and similar machine-to-machine secrets in the active vault. Marking a VaultPilot record revoked does not revoke the real key at its provider.

## Access, Vault Role, and License

- Owner, Admin, and User system roles can use the API key workspace when they have readable access to a vault. Auditors cannot enter secret workspaces.
- The active vault must be unlocked and its key available in the browser session before records can be decrypted.
- Listing, revealing, and copying require readable vault access. Creating, duplicating, editing, deleting, and write-producing bulk actions require **Editor** or **Manager** on the active vault and a license that is not read-only.
- A system role does not grant vault access by itself. Verify the active vault and your role on that vault before acting.

## Work Here

- Create encrypted records with a title, client/owner/service account, provider-console URL, API key or token value, and a scope or rotation note.
- Narrow the visible record set with search, quick filters, and smart filters.
- Copy the secret or reveal it after confirmation; open the provider console when a valid HTTP/HTTPS address exists.
- Duplicate, edit, delete, prepare for Sharing, or include records in controlled bulk actions.

## Search, Filters, and View

Text search covers title, client or owner, URL, host, domain, category, source, risk, and tags. It does not search inside the secret key value.

Based on available data, quick filters show up to seven options drawn from **All**, **Critical**, **Warning**, **Imported**, and common product, category, or tag values. When several conditions are selected through **Add smart filter**, a record must match all of them. **All** restores type, risk, and smart filters to their defaults, but you may still need to clear the search text separately.

**Cards** uses wider record cards; **Table** uses a dense column layout. **Refresh** reruns the record query. Records are returned with the most recently updated first.

### Selection scope

- A previously checked record can remain selected in page memory after a filter hides it.
- **Select visible records** replaces the selection with the records currently visible. When every visible row is selected, **Clear selection** empties the entire selection.
- The count at the top reflects visible selections, while some bulk handlers use hidden selected IDs too. After changing filters, explicitly clear and rebuild the intended selection.

## Record Row Actions

The primary actions are **Copy secret value** and, when a valid HTTP/HTTPS address exists, **Open console**. **More actions** contains:

- **Reveal / hide secret**
- **Copy URL**
- **Create a copy**
- **Edit secret**
- **Delete secret**

**Open console** opens only a validated HTTP/HTTPS address and attempts to write a `VIEW` event. It does not sign in to the provider, validate the key, or query its effective scope.

## Reveal, Copy, and Audit

**Reveal secret** first requires a sensitive-value confirmation. The value then appears on the card and a `VIEW` event is attempted. Reveal does not close on a short fixed timer. It can remain visible until you hide it, reveal another record, lock the vault, or the 15-minute inactivity lock runs.

After the key or URL is written to the clipboard, VaultPilot attempts a `COPY` event. The clipboard-clear timer waits 30 seconds and writes an empty value only when the clipboard still contains the same content. Browser shutdown, clipboard permissions, the operating system, or a clipboard manager can prevent clearing. Do not treat the timer as an access-revocation guarantee.

Clipboard writing and reveal happen before the audit request. If the audit write fails, the value may still be on screen or on the clipboard. Missing audit evidence does not prove that the value was never exposed.

## New Record and Editing

The **New API key** editor provides required title and secret-value fields, plus optional client/owner/service account, console URL, and scope or rotation note. The draft value exists as plaintext in the browser while it is being edited. Control screen sharing and shoulder-surfing risk.

On save, the browser encrypts the record with the active vault key. A new record emits `CREATE`; an update emits `EDIT`. **Edit** changes only the VaultPilot record. It does not change the provider-side token value, scope, expiry, or client settings.

### Value generator and expiry metadata

The editor?s generator runs in the browser, defaults to 24 characters, and supports 12?64. Lowercase is always in the alphabet; uppercase, digit, and symbol toggles expand it. The result only fills the form. It does not issue, validate, rotate, or revoke a provider key; create the real key through the provider?s approved flow first.

The manual editor has no separate expiry field. An `expiresAt` value imported through the `API Keys` Excel sheet becomes encrypted record metadata; it does not schedule rotation or revocation and does not prove provider-side expiry. Import sets source to `imported`, status to `ACTIVE`, and risk once at import: `expired` only when the date is already past, otherwise `unknown`. Do not treat that classification as continuously advancing expiry monitoring.

Use this safe sequence for a key rotation:

1. Create a new least-privilege key at the provider.
2. Move consuming systems to the new value in a controlled maintenance window and verify their operation.
3. Revoke the old key at the provider.
4. Update the VaultPilot record and operation note, then reconcile the audit trail.

VaultPilot does not connect to the provider and perform those steps automatically.

## Duplicate, Delete, and Bulk Actions

**Create a copy** creates a new encrypted record in the same vault; it does not create a new key at the provider. **Delete secret** removes the VaultPilot record irreversibly after a second confirmation; the provider-side key can continue to work.

The bulk menu includes Excel template/import, plaintext export, category and tag assignment, archive, disable/revoke, security check, audit report, share, append note, edit first selected, and confirmed delete.

- **Disable / revoke** changes encrypted metadata for selected API key records to `REVOKED`, sets source to `revoked`, and risk to `warning`. It sends no revocation request to the provider.
- **Export selected** writes complete decrypted records and key values to a plaintext JSON file. The downloaded file is a separate sensitive copy and is not deleted automatically.
- **Add to audit report** writes record metadata rather than secret values to CSV.
- Bulk updates and deletes process records sequentially. A mid-run failure does not roll back earlier successes. Refresh and reconcile the actual scope and audit events before retrying.
- **Bulk share** moves the selection to Sharing?s method step; it has not sent a package and selection grants no permission. An internal-recipient bundle requires Owner/Admin, **Manager** on the active vault, and a writable license. An external package requires **Manager** on the active vault and a writable license.
- **Run security check** can apply the HIBP password-check mechanism to a secret value. It does not prove that an API key is valid, least-privileged, or unexposed at its provider.

## Screen States

| State | Operator response |
| --- | --- |
| Loading records | Wait for skeleton rows to disappear. If needed, verify the session and active vault, then use **Refresh**. |
| No records | Verify the correct vault and lock state. If you have write access, start with **New API key**. |
| No matching records | Clear search text, the quick filter, and smart-filter chips separately. |
| Read-only | Reveal and copy may remain available, but record-changing actions are disabled. |
| `REVOKED` | This is VaultPilot metadata only. Verify the actual revocation state in the provider console. |
| Clipboard or audit error | The value may already be exposed. Clear the clipboard manually, hide the value, and reconcile the event separately. |
| Bulk action stopped partway through | Do not retry blindly. Compare hidden selection, changed records, and the provider?s real state. |

## Before You Act

- Identify the key owner, consuming applications, environment, scope, and maintenance window.
- Verify the active vault and selected records. If filters changed, clear and rebuild the selection.
- Close screen sharing and clipboard managers before reveal, copy, or export.
- Do not mark VaultPilot metadata revoked without provider-side revoke/rotate authority and a rollback plan.
- On Sharing, recheck the recipient, expiry, use limit, and delivery channel.

## Safe Evidence

- Safe to share: screen name, approximate time range, generic provider type, record count, redacted error class, broad rotation state, and whether the role and license permit writes.
- Keep private: API key or token values, full client IDs, title-and-URL pairs, detailed scope, vault names or IDs, exact timestamps, selected records, clipboard contents, plaintext exports, and screenshots showing a value.
- If a value reaches a public channel, clearing the clipboard is not enough. Revoke it at the provider, create a replacement, update consumers, and only then reconcile the vault record.

## When to Stop

Stop if the active vault, key owner, or consuming system is unclear; provider-side revoke/rotate authority is missing; hidden bulk selection is possible; clipboard or screen recording is outside your control; the audit trail conflicts with the action; a bulk operation stopped partway through; or changing only the VaultPilot record could be mistaken for completing the external rotation. Reconcile the last safe step in a private channel before retrying.

## Operator Notes

VaultPilot stores API key records encrypted at rest, but an unlocked browser temporarily reconstructs plaintext for reveal, edit, copy, and export. The screen, clipboard, and downloaded JSON file are separate trust boundaries. Do not report `REVOKED`, `ARCHIVED`, or deletion in VaultPilot as evidence of the provider-side key state.

## Related

- [Security and trust model](security-and-trust-model.md)
- [Sharing screen](screen-sharing.md)
- [Audit Log screen](screen-audit-log.md)
- [Public API reference](public-api-reference.md)
- [Integration API clients](api-clients.md)
- [API client access KB](../../kb/en/api-client-401.md)
- [Safe support evidence](support-evidence-pack.md)
