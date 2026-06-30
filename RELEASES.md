# VaultPilot / PassMan Release Notes

Latest prepared release note: **VaultPilot 2.0.0**.

Latest published GitHub Release verified in this workspace: **PassMan 1.8.21**.

VaultPilot is the canonical product name for new work. PassMan remains the compatibility name for older installed services, data paths, environment variables, cookies, headers, update aliases, extension protocol names, and release artifacts that existing customers may still depend on.

## Release label guide

| Label | Color intent | Use in release notes |
| --- | --- | --- |
| Major | Blue | Product identity, broad workflow, or compatibility-significant change. |
| Minor | Amber | Operator-facing capability, UI, component, or workflow improvement. |
| Patch | Slate | Bug fix, packaging correction, layout fix, or maintenance change. |
| Security | Green | Zero-knowledge, validation, signing, pairing, diagnostics, or secret-handling boundary. |
| Compatibility | Gold | Legacy alias, migration, rollback, or old-client behavior intentionally kept. |
| Removed | Red | A visible action or old path intentionally removed from the daily flow. |

## VaultPilot 2.0.0

Release date: 2026-06-28

Type: major product transition with compatible upgrade/rollback contracts.

Audience: Windows server operators, browser extension users, support operators, and teams upgrading from PassMan-branded installs.

Publication status: this release note is ready as the local/public-doc source for a GitHub Release body. Do not treat `v2.0.0` as published until the GitHub Release, final assets, manifest, signatures, and SHA-256 evidence are verified.

### Highlights

- VaultPilot becomes the primary product identity across the console, first-run and unlock screens, logo areas, package descriptions, docs, diagnostics copy, and operator-facing release language.
- Overview becomes an operator cockpit instead of a short mechanical changelog card. It groups security posture, recommendations, breach status, server readiness, operational state, record distribution, quota/update signals, access trend, maintenance, and recent activity into clickable widgets.
- Sign-in security now focuses on master password change, 2FA setup, 2FA binding revoke, and Owner-visible active session review.
- Server System becomes a professional settings surface for log rotation, log retention, audit retention, safe diagnostics, public host, port, HTTPS certificate state, restart guidance, and non-destructive maintenance boundaries.
- License and license-generator language now map capacity, trial/licensed mode, write state, expiry/renewal risk, and unavailable capabilities to real modules such as extension, auto update, RBAC, integrations, and sharing.
- Extension, offline share decrypter, and DC agent packages adopt VaultPilot naming while keeping compatibility aliases for existing installations.
- Same-version MSI repair is corrected so runtime helper files and installer support folders are still present when the service install custom action needs them.

### Action required

- Normal MSI upgrade should preserve the existing vault, SQLite data, extension pairing, server API behavior, and update trust model.
- Take a server backup before production update.
- After upgrade, verify the Windows service, data directory, Update Center state, extension pairing, active session view, audit retention setting, license state, and Server System diagnostics.
- If rollback is required, use the previous signed release package and the retained PassMan compatibility aliases. Do not manually edit ProgramData folders as a rollback method.

### Console 2.0.0

#### Major

- VaultPilot replaces PassMan as the primary product name in the visible console and release language.
- This is a broad product identity move, not a breaking vault migration. Encryption, storage, pairing, manifest verification, and API compatibility remain compatible with existing PassMan installations.

#### Minor

- Overview widgets now expose security posture, prioritized recommendations, breach-check state, server readiness, operations, category composition, quota/update state, access trend, maintenance, and activity in one scan-friendly timeline.
- Widget move arrows appear only in edit mode, keeping daily operator use cleaner while preserving customization.
- Sign-in security stays focused on master password change, 2FA setup, visible 2FA binding state, revoke flow for lost phones, and active server sessions.
- Server System gathers log rotation, log retention, audit retention, diagnostics, host, port, HTTPS certificate, restart guidance, and non-destructive maintenance guidance in one place.
- License screens explain capacity, expiry, trial/licensed state, read-only behavior, renewal risk, and module availability in operator language.
- The login screen keeps the existing visual background while using quieter VaultPilot treatment and more readable foreground text.

#### Patch

- Same-version MSI repair no longer removes runtime helper files before the repair path needs them.
- Overview and Server System layouts use stricter wrapping and grid rules so long real-world labels do not collide.
- Browser-console backup import/export controls are removed from the daily UI. Backup and restore remain a server-admin workflow through VaultPilot Backup Tool.

#### Security

- Zero-knowledge boundaries are unchanged: vault keys, master-derived keys, plaintext secrets, API keys, private keys, and master passwords are not persisted or logged.
- Server API payload validation, RBAC checks, CSRF header expectations, extension pairing, and signed update manifest verification remain active.
- Legacy fast-unlock remnants are cleaned through a delete-only path. Current unlock behavior keeps sensitive material out of localStorage, sessionStorage, cookies, logs, and server persistence.
- Browser extension decrypted vault snapshots stay in runtime memory only; background-worker restart or suspension locks the extension again.
- Additional hardening covers integration API organization scope, database singleton URL alignment, Authorization-header log redaction, active-session listing, and TOTP management.
- Diagnostics remain redacted and non-destructive. The console does not clear logs, caches, browser history, databases, update jobs, or customer data.

#### Compatibility

- New installs prefer `VaultPilotServer`, `VaultPilot Server`, `C:\ProgramData\VaultPilot`, `VAULTPILOT_*`, `vaultpilot-update.json`, and VaultPilot package names.
- Existing installs may still rely on `PassManServer`, `PassMan Server`, `C:\ProgramData\PassMan`, `PASSMAN_*`, `passman_session`, `x-passman-request`, `passman-update.json`, and legacy package names.
- Extension protocol names, cookies, headers, environment variables, update aliases, and MSI aliases remain available for old clients and rollback paths.

### Browser Vault Extension 1.3.1

- Changed: popup, content panel, README text, package output names, and store/enterprise deployment language now use VaultPilot Browser Vault Extension identity.
- Changed: Chrome Web Store remains the primary install and update channel. ZIP output is retained only for archive, local development, and emergency fallback.
- Security: decrypted vault snapshots are held only in extension runtime memory. If Chromium suspends or restarts the background worker, the extension locks again.
- Compatibility: legacy extension origin and environment aliases remain accepted for managed Chrome installs, enterprise policy distribution, and ZIP fallback flows.

### Offline Share Decrypter 1.2.0

- Changed: downloadable archive names, screen headings, and external-sharing copy now use VaultPilot terminology.
- Security: package opening happens in the browser. Passphrases, plaintext content, and file payloads are not sent to the server or written to durable browser storage.
- Compatibility: legacy PassMan external-share package type values remain accepted for previously generated files.

### VaultPilot DC Agent Service 1.2.10

- Changed: downloadable agent script, service-name copy, status output, and operator commands now use VaultPilot DC Agent Service language.
- Security: the agent collects OU, group, and user metadata only. It does not collect AD passwords, hashes, Kerberos tickets, vault keys, or plaintext secrets.
- Fixed: repair and token validation work with the new VaultPilot id/token wording while still carrying legacy PassMan agent configuration forward.
- Compatibility: older installed agents can be repaired without creating a second provider.

### Expected release assets

Final asset names and hashes must come from the release gate. The expected component set is:

- `VaultPilot-2.0.0-x64.msi` plus legacy MSI aliases only when the public release lane still needs them.
- `vaultpilot-update.json` plus the legacy `passman-update.json` alias.
- `vaultpilot-browser-vault-extension.zip` plus the legacy Chromium extension ZIP alias.
- `vaultpilot-share-decrypter.zip` plus the legacy share-decrypter ZIP alias.
- `vaultpilot-dc-agent.ps1` plus the legacy AD-agent script alias.

### Verification before publishing

- `npm run lint`
- `npm run test`
- `npm run build:windows`
- `npm run update:manifest:issue -- --version 2.0.0 --tag v2.0.0`
- `npm run update:manifest:verify -- --manifest public\downloads\vaultpilot-update.json`
- `npm run update:manifest:verify-assets -- --manifest public\downloads\vaultpilot-update.json --manifest public\downloads\passman-update.json`
- `npm run ui:smoke`
- `npm run msi:verify`
- `npm run msi:sandbox-package -- -AllowUnsignedDevMsi`
- `npm run msi:evidence`
- `npm audit --audit-level=high`
- Secret scan the source and public-doc surfaces before pushing or publishing.

## PassMan 1.8.21

Release date: 2026-06-09

Type: hotfix patch.

GitHub Release: https://github.com/ucsahinn/vaultpilot/releases/tag/v1.8.21

### Highlights

- Reduces SQLite lock contention during high-frequency directory-agent polling and audit traffic.
- Reduces unnecessary heartbeat writes when the directory agent has already checked in recently.
- Avoids rewriting unchanged large Active Directory full-sync snapshot fields.
- Makes installer and restart-helper logging best-effort so a local log permission issue does not interrupt the helper path.

### Fixed

- SQLite now starts with WAL mode, normal synchronous mode, foreign-key enforcement, and a 15-second busy timeout.
- Directory-agent polling keeps `last_seen_at` stable inside the one-minute heartbeat window when no command is leased.
- Unchanged full-sync payloads no longer rewrite large snapshot fields.

### Security and compatibility

- Vault, sharing, extension, update, and DC agent command contracts remain unchanged.
- Helper log writes stay support-friendly without logging secret values or failing the update path because a local evidence file is locked.

### Published assets

- `PassMan-1.8.21-x64.msi`
- `passman-update.json`
- `passman-chromium-extension.zip`
- `passman-share-decrypter.zip`
- `passman-ad-agent.ps1`

## PassMan 1.8.20

Release date: 2026-06-06

Type: browser extension channel patch.

GitHub Release: https://github.com/ucsahinn/vaultpilot/releases/tag/v1.8.20

### Highlights

- Chrome Web Store becomes the primary browser extension install and update channel.
- The old manual ZIP install call-to-action is removed from the normal customer flow.
- Update Center explains the Web Store channel instead of treating the local ZIP as the standard browser install path.
- Extension About view exposes installed version and Web Store update checks.

### Action required

- Operators should use the Chrome Web Store listing and supported extension ID for normal customer deployment.
- Keep the ZIP only for archive, local development, and emergency fallback scenarios.

### Security and compatibility

- Vault, pairing, MSI runtime, zero-knowledge storage, autofill, save/update, and update trust contracts remain unchanged.
- Extension ZIP remains available as a release archive, not as the recommended customer channel.

## PassMan 1.8.0

Release date: 2026-06-20 in the local product timeline.

Type: minor milestone.

### Highlights

- Update Center, enterprise console layout, credential operations, and MSI maintenance fixes are consolidated into one customer-facing milestone.
- Update Center shows download, verification, service restart, and console reload as one progress flow.
- Credential operations now include bulk actions, import preview, export, category/tag assignment, and audit reporting.
- MSI maintenance and legacy installer-helper compatibility are kept visible instead of hidden in proof-only patch notes.

### Security

- Signed manifest verification, SHA-256 checks, service health confirmation, and browser reconnect behavior remain part of the main update lane.
- Credential import and audit flows avoid writing secret values to logs or evidence files.

## PassMan 1.7.0

Release date: 2026-06-01.

Type: enterprise console and MSI maintenance release.

GitHub Release: https://github.com/ucsahinn/vaultpilot/releases/tag/v1.7.0

### Highlights

- Same-version manual MSI runs keep the Windows Installer maintenance path so Repair and Remove are available.
- Newer MSI packages show an explicit upgrade screen when an older PassMan installation is detected.
- Enterprise console polish adds clearer shell hierarchy, real density controls, token-led surfaces, and a cleaner Update Center.
- Credential bulk operations add template download, Excel import preview, selected export, category/tag assignment, archive, revoke/disable, security check, audit report, and guarded deletion.
- AD-synced credentials expose source, domain, DN/path, account, status, risk, owner, tags, last seen, and last synced metadata while keeping sensitive values masked.

### Installer and update

- Upgrade sequencing avoids the route where a built-in WiX welcome/license flow can skip the detected-upgrade screen.
- `RemoveExistingProducts` and runtime preparation are sequenced so PassMan stops its own service before Windows Installer decides a reboot is required.
- Manual and silent MSI flows suppress unnecessary restart prompts while still allowing PassMan to restart its own service.

### Security

- Import preview validates rows before persistence and reports created, updated, skipped, and failed rows without logging secret values.
- Runtime log directories are readable for support while vault data stays restricted to SYSTEM and Administrators.

## PassMan 1.5.4

Release date: 2026-05-28.

Type: maintenance hardening and update-observability release.

### Highlights

- MSI update reliability, service repair, TOTP hardening, CSP handling, and 15-minute RAM fast-unlock behavior are consolidated.
- Windows Installer sequencing, stale update-job reconciliation, quiet MSI status visibility, rollback handling, and support-safe detail are improved.
- Redacted logs and local signer thumbprint checks are kept inside the release evidence model.

### Security

- CSP nonce boundaries are preserved.
- TOTP behavior is hardened.
- Redacted diagnostics prevent support evidence from carrying plaintext secrets, tokens, or master-derived key material.

## PassMan 1.3.0

Release date: 2026-04-18.

Type: secure sharing milestone.

### Highlights

- Selected records, file chunks, and external share packages become one guarded sharing model.
- Password, credential, API key, secure note, certificate, and file records can be included in controlled share packages.
- Internal bundles stay encrypted on the server for approved recipients.
- External packages open offline with a passphrase and the local decrypter.

### Security

- Share package metadata hash, expiry, usage limits, and policy information are visible for audit.
- External plaintext is not stored by the server as part of the recipient flow.

## PassMan 1.0.3

Release date: 2026-02-10.

Type: self-hosted Windows server foundation.

### Highlights

- The standalone Next server, bundled Node runtime, Windows service, firewall rule, and data/log directories are wired into the MSI lane.
- Offline Ed25519 license verification and signed update manifest handling are established.
- The browser-access model is anchored on a Windows server installation reached by users through the server IP and product port.

### Security

- The self-hosted foundation keeps secrets local to the server runtime.
- The public/private release boundary is established so public release assets can be distributed without exposing private signing material or source internals.

## Older public history

Earlier 1.0.x through 1.4.x builds established the self-hosted MSI baseline, offline licensing, selected-secret sharing, browser extension management, update manifests, file vault work, RBAC, audit hardening, and enterprise UI polish. Public downloads for retired builds should not be used for new deployments; use the latest published GitHub Release or the latest verified VaultPilot release once it is published.
