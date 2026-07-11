# Users Screen

The topbar `?` opens this page from the Users screen. Use it to review local and Active Directory-backed users, global roles, account and 2FA state, and each user's vault-grant count.

Only **Owner** and **Admin** can open this screen. Auditor and User cannot list users. When the license is read-only, the list and details remain available, but actions that change a user are blocked.

## Work Here

- Create a local user and assign a temporary master password and initial role.
- Edit a username or display name.
- Assign Admin, Auditor, or User to a non-Owner user.
- Disable a user, reactivate them when capacity allows, or permanently delete an already-disabled user.
- From the founding Owner only, set a temporary password or reset 2FA for another non-Owner user.

This screen does not create another Owner. Normal creation and role changes offer only **Admin**, **Auditor**, and **User**.

## Read the List and Details

Users are listed in creation order. Each row shows role and source badges, display name/username, vault-grant count, a shortened public-key fingerprint, 2FA state, and `ACTIVE`/`DISABLED` state.

**View detail** presents the same facts in a drawer. It does not show sessions, a per-user audit timeline, creation time, Active Directory DN, or the full public key.

Source badges mean:

- **Local:** a `LOCAL` user created in VaultPilot.
- **Synced:** a `DIRECTORY` user; the provider appears when it can be resolved.
- **Active Directory:** a `CREDENTIAL` user linked to an encrypted AD credential record.

The UI may heuristically label a `LOCAL` user as **Synced** when their username or display name matches a selected directory object. The badge alone is not authoritative proof of the stored login source.

An `ACTIVE` user can sign in and counts toward active license capacity. A `DISABLED` user cannot sign in and does not consume active capacity; the record has not been deleted. Skeleton rows appear while loading and an empty state appears when no users are returned.

## Create a Local User

1. Open **Create new user**.
2. Enter a unique username of at least two characters.
3. Optionally enter a display name.
4. Select Admin, Auditor, or User.
5. Enter the same temporary master password in both fields; it must be at least 14 characters.
6. Select **Create user**.

Creation requires Owner or Admin, a writable license, and available active-user capacity. If capacity is full, upgrade the license or disable an account that should no longer sign in.

The browser derives the auth verifier, user key pair, and personal-vault key material from the temporary master password; plaintext password is not sent to the server. The server creates an `ACTIVE`, `LOCAL` user, creates a personal vault, and grants the user Manager access to it.

Never put the temporary password in an audit note, support ticket, or screenshot. Deliver it through a trusted separate channel.

## Edit Identity and Roles

Owner and Admin can edit the username and display name of active users. An Owner username is immutable, and an Admin cannot edit an Owner record. An Owner may edit their own display name.

| Role | Console scope |
| --- | --- |
| Admin | Manages users and vaults, but cannot manage the license. |
| Auditor | Views audit and system status without access to secret values or vault keys. |
| User | Uses assigned vaults according to the Manager, Editor, or Viewer role held in each vault. |

A user cannot change their own global role, and the Owner role is immutable. The UI disables editing and role selection for disabled users; reactivate the user before making console-managed changes.

Do not confuse the global role with a vault role. The count on the row does not show the permission level held in each vault.

## Active Directory Sign-in Access

AD sign-in access is not granted from a Users row. Use **Allow VaultPilot sign-in** or **Remove from VaultPilot sign-in** on the related Active Directory record.

This flow is Owner-only and requires a writable license. A directory source needs provider and DN details; a credential source needs its source secret. A newly managed user is created as User; an existing Admin or Auditor role may be preserved.

VaultPilot does not perform an LDAP bind on every sign-in. Enabling access derives a local VaultPilot verifier and key material from the current encrypted AD credential password. A password changed later outside VaultPilot is not synchronized automatically. Selecting an OU or user does not automatically provision an account.

Refreshing managed sign-in material is rejected when the existing managed user has shared-vault access. Removing sign-in access sets the user to `DISABLED` and revokes sessions.

Changing the user state and saving the directory provider selection are separate requests. The first can succeed while the second fails. After an error, reload and verify the Users list and AD selection separately.

## Set Password and Reset 2FA

These actions are available only to the founding Owner. New installations use `VpAdm`; the legacy founding username `administrator` remains recognized for compatibility. Neither action can target the current account or any Owner account.

### Set a temporary password

- The password must be at least 14 characters and match its confirmation.
- The auth verifier and user key pair are replaced.
- The 2FA binding is reset and open sessions are revoked.
- `USER_PASSWORD_SET` is written; the plaintext password is not written to audit.

> **Stop condition:** Do not treat this action as lossless vault recovery or routine password rotation. The implementation generates a new personal-vault key and can re-wrap only matching shared-vault grants that the founding Owner can currently unlock. Existing personal-vault ciphertext or shared grants that were not re-wrapped can become unreadable. Stop unless the content and vault-access inventory has been verified.

### Reset the 2FA binding

The current authenticator binding is removed, `TWO_FACTOR_DISABLE` is written, and open sessions are revoked. After the next successful sign-in, the user can enroll a new device. No action is performed when there is no active 2FA binding.

## Disable, Reactivate, and Permanently Delete

### Disable a user

Owner or Admin can disable another active, non-Owner user, but not themselves. State changes to `DISABLED`, sessions are revoked, active license usage decreases, and `USER_DISABLE` is written. The UI does not allow any Owner to be disabled.

### Reactivate a user

**Reactivate** appears only for a disabled user. It requires a writable license and free active-user capacity. Success changes the user to `ACTIVE` and writes `USER_UPDATE`.

### Permanently delete a user

Only an already-disabled user who is neither the current account nor an Owner can be deleted. The action cannot be undone.

> **Stop condition:** Do not delete until ownership is transferred for the personal vault, shared-vault grants, and user-linked operational records. Database relationships can also remove authored audit rows, extension devices, API clients, directory providers/actions, discovery records, file chunks, and sent or received share bundles linked to that user.

A `USER_DELETE` event is created immediately before deletion. Its metadata records target identity and role, personal-vault count, and a count/last-hash summary of the audit rows that will be removed with the user. This does not retain the user's complete historical audit trail.

## Audit and Operation Boundaries

| Action | Audit event |
| --- | --- |
| Create user | `USER_CREATE` |
| Edit identity | `USER_UPDATE` |
| Change role | `USER_ROLE_UPDATE` |
| Disable / remove AD sign-in | `USER_DISABLE` |
| Reactivate / refresh managed access | `USER_UPDATE` |
| Founding Owner sets password | `USER_PASSWORD_SET` |
| Reset 2FA | `TWO_FACTOR_DISABLE` |
| Permanently delete | `USER_DELETE` |

Not every event links to the affected user with the same detail. Many create, identity/role update, disable, reactivate, and password events omit a dedicated target-user ID. Review actor, time, action, and any available target or metadata together.

The user mutation, audit append, and session revocation are not one atomic operation. A late audit or session-cleanup failure can appear after the user changed. After an error, reload the list and verify account, session, license, and Audit state before retrying. Do not repeat a destructive action blindly.

## Screen States

| State | Operator response |
| --- | --- |
| Loading | Do not begin an action until skeleton rows clear. |
| Empty list | Verify the server profile and session; a missing founding Owner is not normal. |
| Read-only license | Review only; do not start an action that changes a user. |
| Capacity full | Do not create or reactivate; free capacity or upgrade the license. |
| Unexpected source badge | Verify stored login source and AD selection separately. |
| Error after mutation | Reload and verify user, license, session, and audit state. |
| Password recovery | Stop when content and key-access inventory is missing. |
| Permanent deletion | Stop until ownership transfer and dependency inventory are complete. |

## Before You Act

- Confirm the correct server profile and user row.
- Review global role and vault role separately.
- For an AD user, check the AD record and VaultPilot account state separately.
- Confirm a password/2FA target is neither the current account nor an Owner.
- Transfer active work and integration ownership before disabling access.
- Before deletion, inventory vault, sharing, API-client, directory/discovery, and audit dependencies.
- Check active-user capacity before creation or reactivation.
- Read the username in the confirmation dialog one final time.

## Safe Evidence

- Safe to share: role category, `ACTIVE`/`DISABLED`, a 2FA enabled/disabled summary, and a redacted vault-grant count.
- Use the audit event type, timestamp, and a shortened integrity hash.
- For license evidence, show only active-user total and limit.
- Keep private: real usernames, display names, email/UPN, DN, public keys, personal-vault names, and screenshots of the user list.
- Never include a temporary master password, TOTP secret, authenticator QR/recovery data, or vault key.
- For private support screenshots, redact usernames and key fingerprints and never capture populated password fields.

## Operator Notes

- The screen does not show last sign-in or last activity. Do not report those fields as if reviewed here.
- **Set password** does not change an external-provider password and is not automatic rotation.
- AD sign-in access is not live LDAP authentication, and selected AD objects are not automatically provisioned.
- Disabling preserves the record; permanent deletion is irreversible and has broad linked-record effects.
- The user change and audit/session cleanup do not share one atomic boundary.
- This screen has no control for creating another Owner or transferring the Owner role.

## Related

- [First run, owner and license](first-run-owner-license.md)
- [Security and trust model](security-and-trust-model.md)
- [Audit log screen](screen-audit-log.md)
- [Active Directory records screen](screen-active-directory-records.md)
- [Sharing screen](screen-sharing.md)
- [License screen](screen-license.md)
