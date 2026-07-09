# New Item Screen

The topbar `?` opens this page from the New item screen. Use it when deciding which record type to create and how much metadata to add.

## Work Here

- Choose the narrowest record type: password, API key, credential, certificate, secure note or file.
- Put searchable ownership and system context in metadata fields; keep the secret value only in the encrypted value field.
- Add tags only when they help future review or rotation.

## Screen States

| State | Operator response |
| --- | --- |
| Draft | Finish ownership, vault and type decisions before adding secret values. |
| Validation error | Fix labels and required metadata without copying secret fields into support text. |
| Save blocked | Check license, role and vault access before retrying. |

## Before You Act

- Choose the item type first; changing type later can hide fields that need review.
- Confirm the target vault and owner before entering any sensitive value.
- Use placeholders in examples and never paste production secrets into public notes.

## Safe Evidence

- Safe to share: intended item type, target vault category, owner role, validation code and placeholder field names.
- Keep private: secret values, usernames paired with passwords, API keys, certificate material, file contents and copied form screenshots.
- Use placeholders for examples and rotate any real value that was pasted into public evidence.

## Operator Notes

Do not paste test secrets into public examples. Use placeholders such as `<SERVICE_NAME>`, `<ACCOUNT_NAME>` and `<REDACTED_SECRET>`.

## Related

- [Passwords screen](screen-passwords.md)
- [API keys screen](screen-api-keys.md)
- [Files screen](screen-files.md)
