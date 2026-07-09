# First Run, Owner and License

## First Owner Profile

The first profile becomes the VaultPilot owner account. This account manages users, license, security, and system settings.

Recommendations:

- Use a unique and long master password.
- Enable 2FA after the first unlock.
- Keep at least two owner accounts for continuity.
- Export an initial backup after setup.

## License

VaultPilot uses offline license verification. The server verifies the license code with a public verification key; private signing material is never installed on customer servers.

The License screen shows:

- Plan and customer information.
- User capacity.
- Remaining days.
- Signature verification status.
- Plan capabilities.

## Trial and Read-only

When trial or license time expires, read and backup-export access can remain available while writes, user creation, sharing, extension pairing, and update install actions are restricted.

## Recovery Pointers

Do not remove the last owner account. If a license expires or a replacement license fails verification, keep owner access available, export a backup if the UI permits it, and use the license read-only recovery path before changing capacity or users.

## Related

- [License lifecycle](license-lifecycle.md)
- [Sign-in security screen](screen-sign-in-security.md)
- [License screen](screen-license.md)
- [License read-only KB](../../kb/en/license-read-only.md)
- [Support evidence pack](support-evidence-pack.md)
