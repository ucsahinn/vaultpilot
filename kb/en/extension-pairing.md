# Extension pairing remains pending

Use this when the Chromium extension is installed but the VaultPilot panel does not approve or sync the device.

## Checks

1. Confirm the extension server origin matches the VaultPilot host and scheme.
2. Start pairing again if the code expired.
3. Confirm the username in the extension matches the VaultPilot account.
4. Unlock at least one vault in the VaultPilot web UI.
5. Approve the device from the VaultPilot Browser Extension screen.
6. Revoke stale or duplicated devices before retrying.

## Security notes

The extension stores PIN-wrapped pairing material in the Chromium profile. Plaintext secret values must not be stored in persistent browser storage.
