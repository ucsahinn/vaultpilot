# Secure Notes Screen

The topbar `?` opens this page from the Secure notes screen. Use it for sensitive operational text that does not fit a password, API key, certificate or file record.

## Work Here

- Keep notes short, structured and owned.
- Prefer fields and tags over long unstructured text when the item needs future review.
- Move credentials into typed records instead of hiding them inside notes.

## Screen States

| State | Operator response |
| --- | --- |
| Draft note | Remove accidental credentials before saving general procedure text. |
| Review due | Confirm the note still has an owner and current purpose. |
| Too broad | Split unrelated procedures into separate records for safer access control. |

## Before You Act

- Decide whether the content belongs in a note or should be a typed secret record.
- Add enough labels and ownership metadata for future review without exposing the protected text.
- Move runbooks without sensitive values into docs; keep only protected operational details in the vault.

## Safe Evidence

- Safe to share: note category, owner/review state, label shape and redacted validation concern.
- Keep private: note titles with customer context, note contents, internal hostnames, credentials, recovery details and customer-specific wording.
- Move procedure text that is safe for public reuse into docs; keep protected operational details inside the vault.

## Operator Notes

Secure notes are encrypted, but public support evidence must still redact note titles, contents, internal hostnames and customer-specific language.

## Related

- [Security and trust model](security-and-trust-model.md)
- [Support evidence pack](support-evidence-pack.md)
- [Public issue redaction KB](../../kb/en/public-issue-redaction.md)
