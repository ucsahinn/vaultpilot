# Update Center

VaultPilot Update Center manages the main Windows MSI package. The browser extension is installed and updated through Chrome Web Store, while Offline Share Decrypter and VaultPilot DC Agent Service are tracked as component release notes and refreshed by the MSI or their documented release assets.

![VaultPilot Update Center](../../assets/screenshots/update-center-vaultpilot-2.png)

This sanitized UI capture uses synthetic data and shows the server update lane, manifest-led MSI asset, component notes, and manual repair package separation. The visible filename, package size, manifest URL and SHA-256-like values are documentation fixtures; use the release asset verification page for published asset names, sizes and hashes.

## Secure Update Model

VaultPilot verifies:

- Signed update manifest.
- Package URL and filename.
- SHA-256 checksum.
- MSI Authenticode signer thumbprint.
- File size and release metadata.

A global CA chain is not required for VaultPilot-managed update trust when the signed manifest pins the local release signer thumbprint. CA-backed or trusted-signing certificates remain recommended for Windows SmartScreen reputation and broad OS-level trust.

## Normal Update Flow

1. Export a backup.
2. Open Update Center.
3. Check for updates.
4. Review version, notes, signer and checksum.
5. Start the update.
6. VaultPilot downloads and verifies the MSI on the server.
7. The quiet Windows Installer flow runs.
8. The VaultPilot service restarts.
9. Reopen the console and confirm version and health.

## Release Assets

The current 2.0.0 GitHub Release asset set is:

- `VaultPilot-2.0.0-x64.msi`
- `vaultpilot-update.json`
- Chrome Web Store extension listing: `https://chromewebstore.google.com/detail/vaultpilot-browser-vault/hjkbedlaieikhkoplgpiohlaakgebobi`
- `vaultpilot-browser-vault-extension.zip` release archive and development fallback only

Older Chrome Web Store URLs may redirect from a historical store slug; validate the published extension ID `hjkbedlaieikhkoplgpiohlaakgebobi`.
- `vaultpilot-extension-update.json`
- `vaultpilot-share-decrypter.zip`
- `vaultpilot-share-decrypter.json`
- `vaultpilot-dc-agent.ps1`
- `vaultpilot-dc-agent.json`

For manual verification, use [release asset verification](release-asset-verification.md) before installing or forwarding assets internally. Compare asset names, sizes and SHA-256 values against GitHub Release `v2.0.0`, not against unpublished build output.

## Component Notes

Update Center should not create a browser extension installer flow; Chrome Web Store owns extension install and update distribution. It should also avoid separate installer flows for the DC agent and decrypter. Their version notes remain visible, but the MSI refreshes the support files shipped by the server package. Operators can still download the latest release asset when they need manual installation or recovery.

## Troubleshooting

| Symptom | First check |
| --- | --- |
| Update stops around 76 percent | MSI signature and Windows Installer event log. |
| Checksum mismatch | Delete the downloaded MSI and retry from the release asset. |
| Service does not restart | Query `VaultPilotServer` and review installer logs. On upgraded hosts, also check legacy PassMan service aliases. |
| Version did not change | Confirm the MSI completed, then restart the service. |
