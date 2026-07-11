# Secure Notes Screen

The top-bar `?` button opens this guide from **Secure Notes**. Use this record type for protected operational text that does not belong in a password, API key, certificate, or file record—for example, private recovery steps or environment-specific maintenance instructions.

You need access to an unlocked vault to read notes. Creating, editing, duplicating, or deleting a note also requires write access to that vault and a license mode that permits changes.

## Find Your Way Around

- **Search current screen** does not index the note body or the optional hidden field. It searches visible metadata such as title, owner or team, system or reference, URL, host, domain, category, tags, source, and risk.
- Type counters narrow the list. **Cards** and **Table** change presentation only; they do not alter any record.
- Each row provides reveal and copy controls plus a menu for **Create a copy**, **Edit secret**, and **Delete secret**.
- In **Bulk actions**, **Download Excel template** is available without write access. **Import from Excel** requires a writable vault and shows a preview with conflict choices before it creates records.
- After you select records, **Export selected**, **Run security check**, and **Add to audit report** can remain available in read-only use. **Assign category**, **Assign tags**, **Archive selected**, **Disable / revoke**, **Append note**, **Edit selected**, and **Remove with confirmation** require vault write access. **Bulk share** carries the selection to Sharing, where the role and vault checks for package creation still apply.

## Common Tasks

### Create a secure note

1. Select **New secure note** on the Secure Notes screen. It opens the secure-note form directly; there is no record-type choice in this flow.
2. Give the record a short title that describes its purpose without disclosing protected details.
3. Add only the private operational text that belongs in the vault. Put reusable, non-sensitive procedures in your documentation system instead.
4. Add categories or tags that will help with review, verify the destination vault, and save. The row menu then offers **Create a copy**, **Edit secret**, and **Delete secret**.

Expected result: the note appears in the list and its body remains hidden until the vault is unlocked and you deliberately reveal it. If saving is blocked, check the vault role and license state without pasting the note into an error report.

### Locate and read a note safely

1. Narrow the list with search and smart filters, remembering that search never inspects the note body.
2. Confirm the title and last-updated time before revealing anything.
3. **Reveal secret** first opens the **Reveal secret value?** confirmation. After **Reveal temporarily**, the value becomes visible and VaultPilot writes a `VIEW` audit event. Use **Hide secret** as soon as you finish.
4. **Copy secret value** copies the note body, or the optional hidden field when the body is empty, and writes a `COPY` audit event on the successful path.

VaultPilot makes a best-effort attempt to clear the copied value after 30 seconds. It can do so only when the clipboard still contains that exact value and the browser permits clipboard reads and writes. It cannot erase operating-system clipboard history, cloud clipboard synchronization, or a value already pasted into another application. Do not treat the timer as proof that every copy has disappeared.

### Update or remove a note

Use **Edit secret** to change the body or classification. Before deleting a note, confirm that another operator or procedure does not still depend on it. The confirmation dialog is the final safe point to cancel the removal.

## Screen States

| State | Operator response |
| --- | --- |
| No records | Clear any filters. If the vault is genuinely empty, create the first note from **New record**. |
| No matches | Remove the search term or active smart filters; no-match does not mean the records were deleted. |
| Read-only | Reading remains available, but create, edit, duplicate, and delete actions are disabled. Check the license and vault role. |
| Access denied | Request access to the correct vault instead of copying the information into another vault to bypass ownership. |
| Save error | Keep the form open and check its required fields. Do not include the protected text in diagnostics. |
| Loading | Wait for the list to settle before selecting records or starting a bulk action. |

## Before You Act

- Decide whether the information belongs in a more specific record type.
- Verify the destination vault, the responsible owner, and the retention purpose.
- Make sure the title and tags identify the note without revealing customer or system details.
- For bulk work, review both the selected count and the current filter set.

## Safe Evidence

- **Safe to share:** the screen name, approximate time, record type, a redacted category or tag pattern, and the visible error code.
- **Keep private:** note titles and bodies, hidden fields, internal system names, recovery details, user or customer information, and copied text.

Reproduce content-sensitive problems with a synthetic note whenever possible. If the real body must be inspected, use a private support channel rather than a public issue.

## Related

- [Security and trust model](security-and-trust-model.md)
- [Support evidence pack](support-evidence-pack.md)
- [Redacting a public issue](../../kb/en/public-issue-redaction.md)
