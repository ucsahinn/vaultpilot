# Extension pairing remains pending

Use this when the Chromium extension is installed but the VaultPilot panel stays on pending, does not show the device, or pairs once and then stops syncing. Pairing is account, origin and browser-profile specific; diagnose those three boundaries before recreating packages.

## Triage

1. Open [Browser Extension](../../docs/en/screen-browser-extension.md) in VaultPilot and keep the page visible while retrying.
2. Confirm the extension server origin exactly matches the VaultPilot host, port and scheme shown to operators.
3. Start a new pairing code if the old code expired or if the extension was opened in another browser profile.
4. Confirm the extension username matches the signed-in VaultPilot account.
5. Unlock at least one vault in the VaultPilot web UI before expecting secret sync.
6. Approve the new device from the VaultPilot Browser Extension screen, then revoke stale or duplicated devices.

## What To Check

| Boundary | Symptom | Action |
| --- | --- | --- |
| Origin | Code accepted but server stays pending | Match `https://<SERVER_HOST>:<PORT>` exactly, including scheme and port. |
| Browser profile | Pairing works in one profile but not another | Pair each profile separately or use the intended managed profile only. |
| Account | Device appears under a different user | Sign out of the extension, sign in as the intended VaultPilot user and restart pairing. |
| Vault unlock | Device is approved but no records sync | Unlock the intended vault and verify assigned access. |
| Device list | Multiple rows for the same profile | Revoke stale devices, pair once, and record the new device label. |

## Safe Evidence

- Extension version and browser family.
- Redacted VaultPilot origin such as `<VAULTPILOT_URL>`.
- Pairing state: new, pending, approved, revoked or expired.
- Device label and timestamp with user names redacted when public.
- Console error category only; do not paste tokens or wrapped pairing material.

## Security Notes

The extension stores PIN-wrapped pairing material in the Chromium profile. Plaintext secret values, master passwords, pairing secrets and API client secrets must not be stored in persistent browser storage, screenshots or public issues.

Related: [Browser Extension screen](../../docs/en/screen-browser-extension.md), [Browser extension guide](../../docs/en/browser-extension.md), [Chrome Web Store review KB](chrome-web-store-review.md), [Public issue redaction](public-issue-redaction.md).
