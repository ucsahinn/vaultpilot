# Chrome Web Store Review Or Privacy Mismatch

Use this when the Chrome Web Store update is blocked, the privacy practices page no longer matches the extension, or a reviewer asks for clearer permission, data-use, screenshot, or remote-code evidence.

## First Checks

1. Confirm the submitted extension ID is `hjkbedlaieikhkoplgpiohlaakgebobi`.
2. Confirm the submitted package version matches the release notes and [Chrome Web Store listing guide](../../docs/en/chrome-web-store-listing.md).
3. Compare Developer Dashboard privacy practices with [PRIVACY.md](../../PRIVACY.md). The current disclosure categories should be personally identifiable information, authentication information, and web history.
4. Inspect the packaged `manifest.json` for permissions and host permissions.
5. Search the packaged extension for remote executable code patterns before upload.
6. Confirm all screenshots use synthetic data and match the submitted VaultPilot release UI.

If the reviewer asks for package evidence, run the Package Audit Commands in the [Chrome Web Store listing guide](../../docs/en/chrome-web-store-listing.md#package-audit-commands) and keep the output with the redacted submission notes.

## Common Review Causes

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Privacy practices mismatch | Dashboard categories, privacy policy, and extension behavior do not describe the same data handling. | Align all three before resubmission. |
| Permission justification rejected | A permission is broader than the described feature set, or the feature is not visible to the user. | Remove unused permissions or document the user-facing feature that needs the permission. |
| Remote hosted code concern | Packaged extension contains executable JavaScript or WASM loaded from outside extension files. | Bundle executable code inside the extension package; keep API responses as data only. |
| Screenshot rejected or unsafe | Screenshot contains real hostnames, users, secret titles, logs, tokens, or support context. | Replace with sanitized VaultPilot screenshots using synthetic data. |
| Store text sounds stale | The listing still presents PassMan as the current product or the ZIP as the normal install path. | Use the publisher dashboard handoff in the listing guide, keep VaultPilot as the product name, and keep Chrome Web Store as the normal install/update channel. |

## Safe Evidence

Provide only:

- Extension ID and version.
- Redacted rejection reason or review message.
- Permission list from packaged `manifest.json`.
- Screenshot filenames and sanitized preview status.
- Whether [PRIVACY.md](../../PRIVACY.md) and Developer Dashboard categories match.

Do not publish:

- Developer account screenshots with private account data.
- Real customer URLs, usernames, vault record names, tokens, logs, databases, backups, certificates, or support tickets.

## Escalation

If the review issue is about product behavior, fix the extension package before store resubmission. If it is only about public wording, update [Chrome Web Store listing and privacy](../../docs/en/chrome-web-store-listing.md), [PRIVACY.md](../../PRIVACY.md), [browser extension docs](../../docs/en/browser-extension.md), and release notes together.

## Related

- [Chrome Web Store listing and privacy](../../docs/en/chrome-web-store-listing.md)
- [Browser extension](../../docs/en/browser-extension.md)
- [Public external surface drift](../../docs/en/public-external-surface-drift.md)
- [Public screenshot standards](../../docs/en/public-screenshot-standards.md)
