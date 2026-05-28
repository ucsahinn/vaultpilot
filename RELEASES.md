# PassMan Release Notes

## PassMan 1.5.1

Release page: https://github.com/ucsahinn/passman-releases/releases/tag/v1.5.1

### Main Application 1.5.1

- Active Directory provider selection now renders synced OU, group, and user objects as a searchable tree instead of a capped flat list.
- Login scope and credential import selections are separated with clear checkbox states, branch-level credential selection, and count chips for large domains.
- Empty, waiting, and no-match states on the AD provider surface clarify whether the blocker is first sync, search filtering, or missing users.

### DC Agent Service 1.0.10

- Fixed service wrapper install failures caused by overwriting `PassManDCAgentService.exe` while an existing `PassManDCAgent` service was still running.
- The installer now stops and removes an existing service before replacing the script, config, or wrapper binary.
- The wrapper is compiled in a temporary directory and copied into place only after successful compilation.
- Compiler output is written to `C:\ProgramData\PassMan\ad-agent\passman-dc-agent-install.log`.
- Added `-RepairService`, `-Status`, `-TailLog`, and `-RequirePassManOnline`.
- Agent and service logs redact agent ids, tokens, passwords, and secret-like values before writing to disk.

### Chromium Extension 3.1.8

- Active-site match badge counts remain available for recognized login pages.
- Autofill and save/update login prompts remain part of the extension package.
- Browser notifications avoid plaintext usernames, passwords, or secret values.

### Offline Share Decrypter 1.2.0

- Offline `.pmshare` decryption remains local-only in the browser.
- File-backed share packages are supported.
- Distinct error states remain available for invalid JSON, wrong passphrase, tampered metadata, expired packages, and exhausted usage limits.

## PassMan 1.5.0

- Consolidated the enterprise vault console UX pass.
- Added dynamic theme tokens across shell, cards, charts, CTAs, focus states, and gradient surfaces.
- Added selected-record sharing including files.
- Added 15-minute browser-process RAM fast unlock.
- Cleaned up component version visibility so the main MSI and browser extension remain the actionable update cards.

## Older History

Earlier `1.0.x` through `1.4.x` releases covered the self-hosted MSI baseline, offline licensing, selected-secret sharing, browser extension management, update manifests, file vault work, RBAC, audit hardening, and enterprise UI polish.
