# Sign-In Security Screen

The topbar `?` opens this guide for **Server settings > Sign-in security**. This tab manages the unlocked personal profile's master-password change, TOTP-based 2FA binding, and?when the role is Owner?active server sessions. VaultPilot sign-in uses username, master password, and an authenticator code when 2FA is enabled. There is no email link, emailed password reset, external IdP/SSO, or recovery-code flow here.

## Access, Role, and Server-Settings Context

Sign-in security is not gated by a separate license feature, and every system role can see the tab. Owner, Admin, and Auditor see the other Server settings tabs as well; only User receives the reduced tab set containing **Sign-in security**. Separately, any non-Owner attempt to enter License or Integrations routes to this personal-security tab.

The self password and self 2FA APIs accept Owner, Admin, and User; Auditor can see the forms but the server rejects those mutations. The database mutation requires a writable license, so read-only licensing blocks profile changes even though the controls are not disabled in advance. Active-session listing and revocation are Owner-only.

This is personal-profile context. Owner does not reset another user's password or 2FA binding here. The founding Owner's tools for eligible non-Owner users live on Users and have separate role, target, confirmation, and read-only boundaries.

## Work Here

- Verify the current master password, then enter and confirm a new master password of at least 14 characters.
- When 2FA is off, generate a TOTP secret and QR code, then enable the binding with the first six-digit authenticator code.
- When 2FA is active, check whether both the master-key-encrypted copy and server verification material are ready.
- If a phone is lost or an app is changed while the profile remains unlocked, revoke the current binding after confirmation and start setup again.
- As Owner, review active sessions by user, role, last seen, expiry, and current-session state; revoke a non-current session.
- Use the topbar **Lock vault and sign out** action to lock this browser profile manually.

There is no lock-timeout setting, failed-sign-in lockout policy, or trusted-device list on this tab. Automatic lock is fixed at 15 minutes and cannot be changed here.

## Change Master Password

**Change master password** affects only the current unlocked user's profile. The current password is required; the new value must contain at least 14 characters and match confirmation. The route accepts at most six password-change requests per ten minutes.

The browser derives keys from the current and new passwords, re-encrypts the profile private key, and, when present, re-encrypts the master-key-protected TOTP copy. The server verifies the current verifier and stores the new verifier and encrypted material. Plaintext master passwords are not stored in the server profile.

A successful change writes a `PASSWORD_CHANGE` audit event and revokes the same user's other persistent server sessions while preserving the current request session. The success message says the profile keys were re-wrapped. This is not another user's temporary-password assignment, a profile reset, or forgotten-password recovery.

## 2FA States and Setup

### 2FA off / Setup pending

**Start 2FA setup** generates a new TOTP secret in the browser. **Regenerate QR** replaces that not-yet-saved setup secret; the old QR is not an enabled binding. The setup card shows a QR code, formatted manual key, and six-digit code field.

A skeleton appears while QR rendering runs. If QR generation fails, an error appears and the manual key can remain available. Both QR and manual key are highly sensitive. Add the account to the authenticator, enter the current six-digit code, then choose **Enable 2FA**. The code is checked in the browser and again on the server with time tolerance; the route accepts at most 12 2FA update requests per ten minutes.

On success, one TOTP copy is encrypted with the master-derived key for re-encryption/recovery and another with the server key for sign-in verification. Other persistent sessions are revoked, and `TWO_FACTOR_ENABLE` is written. The next ordinary unlock requires an app code.

### 2FA active / Ready or Check

An **Active** binding shows **Code required on unlock**. When both `serverTotpReady` and the master-key-encrypted TOTP copy are present, the state is **Ready / Dual-encrypted binding**. If either side is missing, the state is **Check / Binding check pending**; do not treat it as healthy.

An older profile with 2FA enabled but missing server verification material is rejected at unlock. Recovery guidance points to an administrator backup or profile reset; it offers no email, recovery code, or TOTP bypass.

### Revoke binding and reset boundary

After confirmation, **Revoke binding** removes the current profile's authenticator binding, revokes its other persistent sessions, and writes `TWO_FACTOR_DISABLE`. The current session remains open. The user can then set up a new device; no existing secret is revealed and no recovery code is generated.

Self-service revoke is unavailable when the user is locked out without the authenticator device because the profile and server session must already be open. On Users, the founding Owner can reset only another non-Owner user's 2FA. That administrative action cannot target self or an Owner account.

## Active Sessions

**Active sessions** loads only for Owner and refreshes about every 15 seconds while the security tab is active. **Refresh** performs an immediate query. The list includes non-expired sessions for active users in the Owner's organization; expired rows are removed during the query.

Summary counts show total active, **current**, and **revocable**. Each row contains an 18-character public session ID, user/display name, role, last-seen time, expiry, state, and action. It does not show IP address, browser name, or device fingerprint, so this table alone cannot identify a physical device conclusively.

The current row is marked **Current** and its **Revoke** button is disabled. **Revoke** on another row sends the revocation immediately without a second confirmation dialog. Success removes the session, refreshes session and audit data, and writes `SESSION_REVOKE`. Do not include session IDs or usernames in public evidence.

Three skeleton rows appear while sessions load. There is no dedicated query-error branch; if a request fails with no retained data, the panel can fall through to **No active sessions are available**. Do not use that empty state as proof of zero sessions until Refresh, connectivity, and Owner session are verified.

## Manual Lock, Automatic Lock, and Fast Unlock

Topbar **Lock vault and sign out** clears revealed/copied state, the generated share package, unlock TOTP input, temporary 2FA setup secret/QR/code, fast-unlock state, and query cache; it removes unlocked keys from the app store and calls server logout on a best-effort basis. It does not explicitly clear the share passphrase, selected share IDs, or share-package metadata (`sharePackageMeta`); the UI locks, but this React state can remain in memory.

The vault automatically locks after 15 minutes without browser activity. Pointer, keyboard, wheel, focus, and visibility events refresh the timer. At timeout, revealed/copied state, share package/passphrase and selected share IDs, fast-unlock state, server session, query cache, and unlocked keys are cleared. Unlike manual lock, the auto-lock callback does not explicitly clear share-package metadata (`sharePackageMeta`) or the unlock and temporary TOTP setup state; the lock screen hides them, but do not rely on auto-lock as the cleanup step after exposing sensitive share metadata, a QR code, or a manual key.

If you abandon an exposed sharing or TOTP workflow, do not rely on either lock path alone; perform a full page reload.

After ordinary unlock, a 15-minute fast-unlock snapshot can be held in SharedWorker/Service Worker runtime memory, with a restore token in browser history state. Legacy IndexedDB fast-unlock remnants are delete-only. This lane does not persist the master password or master-derived key in normal browser storage. Manual or automatic lock clears the fast-unlock snapshot.

## Password, Profile Reset, and Recovery Boundaries

- **Change master password** re-wraps the current user's profile material; it does not delete profile data.
- **Users > Set password** is a separate action for the founding Owner against another non-Owner user. It revokes the target's sessions, resets target 2FA, and re-wraps the personal-vault key to a new temporary password.
- **Reset server profile** is not a Sign-in security control. A separate destructive Owner route requires an authenticated Owner session and the exact `DELETE_LOCAL_PROFILE` phrase; it deletes organization, users, vaults, secrets, sharing/integration/directory data, audit data, and every server session. It is not a lightweight forgotten-password reset.
- The lock-screen recovery message first asks the operator to check master password, Caps Lock, and TOTP, then directs persistent server/profile failures to a VaultPilot Backup Tool restore. Support does not know and should not request the master password, TOTP secret, or session cookie.

The current browser flow has no email password reset, recovery code, SMS, IdP redirect, or support-side authentication bypass.

## Recommended Workflows

### Set up the first 2FA binding

1. Confirm the profile is unlocked, the server session is verified, and the license is writable.
2. Choose **Start 2FA setup**.
3. Scan the QR in the authenticator or enter the manual key directly; do not take a screenshot.
4. Enter the current six-digit code and choose **Enable 2FA**.
5. Confirm **Active** and **Ready / Dual-encrypted binding**.
6. Perform a controlled lock and verify unlock with username, master password, and a fresh TOTP code.

### Revoke a suspicious old session

1. As Owner, refresh **Active sessions**.
2. Compare user, role, last seen, and expiry; remember that device/IP evidence is absent.
3. Select the approved non-**Current** row.
4. Remember that **Revoke** acts without a second confirmation, then press it once.
5. Confirm the list changed and `SESSION_REVOKE` audit evidence exists.

## Screen States

| State | Operator response |
| --- | --- |
| 2FA off / Setup pending | Create a binding and keep QR/manual key private. |
| QR generating | Wait for the skeleton; do not regenerate repeatedly. |
| QR generation failed | Use the manual key when present, or restart setup when it is absent. |
| Authenticator code invalid | Check six digits, device time, and account; never bypass verification. |
| 2FA active / Ready | Dual-encrypted material exists; perform a controlled unlock test. |
| 2FA active / Check | Do not treat missing binding material as healthy; verify private backup/recovery before locking. |
| Changing password | Do not submit again; wait for success or error. |
| Current password invalid | Check profile/password and Caps Lock; do not rush into profile reset. |
| Sessions loading | Wait for three skeleton rows. |
| No active sessions are available | Because there is no query-error card, verify connectivity and Owner role, then refresh. |
| Session revoke failed | Confirm it is not Current, role is Owner, and the server is reachable. |
| Vault auto-locked | Unlock with master password and TOTP when required; assume fast unlock was cleared. |
| Server session unverified | Fast unlock can remain in memory for 15 minutes while connection retries. |
| Legacy 2FA profile | Do not bypass missing server material; use administrator backup or approved profile recovery. |

## Before You Act

- Separate an action against your profile, another user, and the entire server profile.
- Confirm role and writable-license status; Auditor can see forms but cannot mutate the profile.
- Disable screen sharing/recording while QR or manual TOTP key is visible.
- Plan for other persistent sessions to be revoked after master-password or 2FA changes.
- Remember session Revoke has no second confirmation and the current session cannot be revoked from the table.
- Verify approved backup and re-entry path before revoking 2FA or resetting a profile.

## Safe Evidence

- Safe to share: system-role class, 2FA **off/active/ready/check** state, total and revocable session counts, approximate last-seen/expiry window, general error category, and broad time range.
- Keep private: username/display name, master password and derived verifier, TOTP secret, QR code, six-digit code, encrypted TOTP/private-key material, session ID/token/cookie, profile-reset ID, backup file, and exact timestamp.
- The session table does not contain device fingerprint or IP; do not invent those fields in evidence.
- Do not merely blur a manual TOTP key in a screenshot. Mask it completely and verify that no copy retains it.

## When to Stop and Escalate

Stop making security changes when 2FA is enabled but remains **Check**, server verification material is missing, the profile private key cannot be opened after password change, other sessions remain active after a change, the session list shows an unexpected user, or automatic lock does not clear expected sensitive state. Open a private support case with role class, general state, broad time window, error code, and last safe step?without secret values.

## Operator Notes

Sign-in security is not an identity-provider or email-account management screen. Master password, TOTP, and session management operate within the VaultPilot server profile and browser-memory boundaries. Never publish recovery material, TOTP secret, master password, auth hash, cookie, or one-time code.

## Related

- [First run, owner and license](first-run-owner-license.md)
- [Users screen](screen-users.md)
- [Server settings screen](screen-server-settings.md)
- [Session 401 after login KB](../../kb/en/session-401-after-login.md)
- [Security and trust model](security-and-trust-model.md)
